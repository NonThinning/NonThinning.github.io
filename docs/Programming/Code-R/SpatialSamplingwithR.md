
###### 参考资料

```r
# https://dickbrus.github.io/SpatialSamplingwithR/
# https://opengeohub.github.io/spatial-sampling-ml/
```

###### R markdown 备忘

```r
# https://cosname.github.io/rmarkdown-guide/
# install.packages("rmarkdown")
# install.packages('tinytex')
# tinytex:::install_prebuilt("D:\\Software\\More\\R\\TinyTeX-v2023.04.zip")
# tinytex::tlmgr_repo('http://mirrors.tuna.tsinghua.edu.cn/CTAN/')
# install.packages('rticles')
```

###### SpatialSamplingwithR

导入该文档所需数据。

```r
remotes::install_github("DickBrus/sswr")
library(sswr)
```

###### A test: cLHS & RF

Sampling -> cLHS
Digital Soil Mapping -> Random Forest

```r
# DEM https://registry.opendata.aws/copernicus-dem/
# land cover https://esa-worldcover.org/en
# forest cover https://essd.copernicus.org/articles/16/1353/2024/essd-16-1353-2024-discussion.html
# soil organ carbon https://rdrr.io/cran/geodata/man/soil_grids.html

# TWI SAGA&QGIS
# watershed SWAT+&QGIS

# DSM R

# http://soils.issas.ac.cn/html/tr/2021/5/tr202010070432.htm

#### SAGA TWI ####

library(terra)
library(tidyverse)
library(RSAGA)

watershed <- vect("./data0909/watershed_line_epsg32651.geojson")

# 注意此处在重投影时采用了多线程和设置分辨率
dem <- rast("./data0909/Copernicus_DSM_10_N53_00_E122_00_DEM.tif") %>%
  project(., "EPSG:32651", threads = TRUE, res = 30) %>%
  crop(., watershed)
writeRaster(dem, "dem.sdat", overwrite=TRUE)

# SAGA的文件是一组格式不同名称相同的文件
rsaga.wetness.index(in.dem = "./dem",out.wetness.index = "./wi")

wi <- rast("wi.sdat")
plot(wi)
writeRaster(wi, "./use0909/wi_use.tif", overwrite=TRUE)

#### DEM Info ####
aspect <- rast("./data0909/Copernicus_DSM_10_N53_00_E122_00_DEM.tif") %>%
  project(., "EPSG:32651", threads = TRUE, res = 30) %>%
  terrain(., v = "aspect", unit = "radians") %>%
  crop(., watershed) %>%
  resample(., wi, method = "near", threads = TRUE)

slope <- rast("./data0909/Copernicus_DSM_10_N53_00_E122_00_DEM.tif") %>%
  project(., "EPSG:32651", threads = TRUE, res = 30) %>%
  terrain(., v = "slope", unit = "radians") %>%
  crop(., watershed) %>%
  resample(., wi, method = "near", threads = TRUE)

dem <- rast("./data0909/Copernicus_DSM_10_N53_00_E122_00_DEM.tif") %>%
  project(., "EPSG:32651", threads = TRUE, res = 30) %>%
  crop(., watershed) %>%
  resample(., wi, method = "near", threads = TRUE)

writeRaster(aspect, "./use0909/aspect_use.tif", overwrite=TRUE)
writeRaster(slope, "./use0909/slope_use.tif", overwrite=TRUE)
writeRaster(dem, "./use0909/dem_use.tif", overwrite=TRUE)

#### ForestCover ####

fc <- rast("./data0909/GLC_FCS30D_20002022_E120N55_Annual.tif") %>%
  .[[23]] %>% 
  project(., "EPSG:32651", threads = TRUE, res = 30, method = "near") %>%
  crop(., watershed) %>%
  resample(., wi, method = "near", threads = TRUE)
plot(fc, type = "class")
fc_use <- fc

lc <- rast("./data0909/ESA_WorldCover_10m_2020_v100_N51E120_Map.tif") %>%
  project(., "EPSG:32651", threads = TRUE, res = 30, method = "near") %>%
  crop(., watershed) %>%
  resample(., wi, method = "near", threads = TRUE)
plot(lc, type = "class")
lc_use <- lc

lc_use[lc_use != 10] <- NA
plot(lc_use, type = "class")

fc_mask <- mask(fc_use, lc_use, maskvalues = NA)
plot(fc_mask, type = "class")

fc_use[fc_use > 82] <- NA
fc_use[fc_use < 61] <- NA
fc_use[fc_use == 61] <- 6
fc_use[fc_use == 62] <- 6
fc_use[fc_use == 71] <- 7
fc_use[fc_use == 72] <- 7
fc_use[fc_use == 81] <- 8
fc_use[fc_use == 82] <- 8
plot(fc_use, type = "class")

writeRaster(fc_use, "./use0909/fc_use.tif", overwrite=TRUE)

#### Ready ####

# install.packages("remotes")
# remotes::install_github("DickBrus/sswr")
# sswr::grdAmazonia

fc_use <- rast("./use0909/fc_use.tif")
aspect_use <- rast("./use0909/aspect_use.tif")
slope_use <- rast("./use0909/slope_use.tif")
dem_use <- rast("./use0909/dem_use.tif")
wi_use <- rast("./use0909/wi_use.tif")
watershed <- vect("./data0909/watershed_line_epsg32651.geojson")

all <- c(fc_use, aspect_use, slope_use, dem_use, wi_use)
all <- all %>%
  mask(., fc_use, maskvalues = NA) %>%
  mask(., as.polygons(watershed))
plot(all)
all_table <- as.data.frame(all, xy = TRUE) %>% as_tibble() %>%
  mutate_at(.vars = 3, .funs=as.integer)
colnames(all_table)[3] <- "fc"
colnames(all_table)[6] <- "dem"
head(all_table)

#### cLHS ####
# https://dickbrus.github.io/SpatialSamplingwithR/cLHS.html

library(clhs)
covs <- c("fc", "aspect", "slope", "dem", "wi")
set.seed(314)
res <- clhs(
  all_table[, covs], 
  size = 100, 
  iter = 50000, 
  temp = 1, 
  tdecrease = 0.95,
  length.cycle = 10, 
  progress = FALSE, 
  simple = FALSE
  )
mysample_CLH <- all_table[res$index_samples, ]

ggplot(data = all_table) +
  geom_raster(mapping = aes(x = x / 1000, y = y / 1000, fill = fc)) +
  geom_point(data = mysample_CLH, mapping = aes(x = x / 1000, y = y / 1000), colour = "red", size = 2) +
  scale_x_continuous(name = "Easting (km)") +
  scale_y_continuous(name = "Northing (km)") +  
  scale_fill_viridis_c(name = "fc") +
  coord_fixed()

probs <- seq(from = 0, to = 1, length.out = nrow(mysample_CLH) + 1)
bounds <- apply(all_table[, covs], MARGIN = 2, FUN = function(x) quantile(x, probs = probs))
ggplot(data = all_table) +
  geom_point(mapping = aes(x = wi, y = dem), colour = "black", size = 1, alpha = 0.5) +
  geom_vline(xintercept = bounds[c(-1, -nrow(bounds)), 1], colour = "grey") +
  geom_hline(yintercept = bounds[c(-1, -nrow(bounds)), 3], colour = "grey") +
  geom_point(data = mysample_CLH, mapping = aes(x = wi, y = dem), colour = "red", size = 1) +
  scale_x_continuous(name = "wi") +
  scale_y_continuous(name = "dem")

probs <- seq(from = 0, to = 1, length.out = nrow(mysample_CLH) + 1)
bounds <- apply(all_table[, covs], MARGIN = 2,
                FUN = function(x) quantile(x, probs = probs))
mysample_CLH <- as.data.frame(mysample_CLH)
counts <- lapply(1:5, function(i)
  hist(mysample_CLH[, i + 2], bounds[, i], plot = FALSE)$counts)

countslf <- data.frame(counts = unlist(counts))
countslf$covariate <- rep(covs, each = 50)
countslf$stratum <- rep(1:50, times = 10)
ggplot(countslf) +
  geom_point(mapping = aes(x = stratum, y = counts), colour = "black", size = 1) +
  facet_wrap(~covariate) +
  scale_x_continuous(name = "Stratum") +
  scale_y_continuous(name = "Sample size", breaks = c(0, 1, 2))

trace <- res$obj
tail(trace, n = 1)

countslf <- data.frame(counts = unlist(counts))
O1 <- sum(abs(countslf$counts - 1))
rho <- cor(all_table[, covs])
r <- cor(mysample_CLH[, covs])
O3 <- sum(abs(rho - r))
print(O1 + O3)

#### TestDSM ####

# library(devtools)
# r.proxy::proxy()
# install_bitbucket("brendo1001/ithir/pkg")
# library(ithir)
# https://smartdigiag.com/DSM_book/pages/dsm_cont/sspfs/rf/

library(terra)
library(sf)
library(randomForest)

soc <- rast("./data0909/soc_0-5cm_mean_30s.tif") %>%
  crop(., ext(100, 150, 20, 60)) %>%
  project(., "EPSG:32651", threads = TRUE) %>%
  crop(., watershed) %>%
  resample(., wi_use, method = "cubic", threads = TRUE) %>%
  mask(., fc_use, maskvalues = NA) %>%
  mask(., as.polygons(watershed))
plot(soc)

head(mysample_CLH[1:2])

soc_point <- terra::extract(soc, mysample_CLH[1:2], xy = TRUE, ID = TRUE) %>%
  drop_na() %>%
  select(ID, x, y, `soc_0-5cm`)
colnames(soc_point)[4] <- "soc5"
soc_point$soc5 <- round(soc_point$soc5, 2)
soc_point$x2 <- soc_point$x
soc_point$y2 <- soc_point$y
head(soc_point)

soc_point_sf <- sf::st_as_sf(x = soc_point, coords = c("x", "y"))
plot(soc_point_sf)
soc_raster <- all
names(soc_raster)[1] <- "fc"
names(soc_raster)[4] <- "dem"
plot(soc_raster)

soc_DSMdata <- terra::extract(x = soc_raster, y = soc_point_sf, bind = T, method = "simple")
soc_DSMdata <- as.data.frame(soc_DSMdata)

# 去除缺失值
which(!complete.cases(soc_DSMdata))
soc_DSMdata <- soc_DSMdata[complete.cases(soc_DSMdata), ]
# 设置伪随机数
set.seed(123)
soc_training <- sample(nrow(soc_DSMdata), 0.7 * nrow(soc_DSMdata))

soc.RF.Exp <- randomForest(soc5 ~ fc + aspect + slope + dem + wi, 
                           data = soc_DSMdata[soc_training, ], 
                           importance = TRUE, 
                           ntree = 1000)
print(soc.RF.Exp)
varImpPlot(soc.RF.Exp)

RF.pred.C <- predict(soc.RF.Exp, newdata = soc_DSMdata[soc_training, ])
goof(observed = soc_DSMdata$soc5[soc_training], predicted = RF.pred.C)

RF.pred.V <- predict(soc.RF.Exp, newdata = soc_DSMdata[-soc_training, ])
goof(observed = soc_DSMdata$soc5[-soc_training], predicted = RF.pred.V)

map.RF.r1 <- terra::predict(object = soc_raster, model = soc.RF.Exp, filename = "soc5_rf.tif", datatype = "FLT4S", overwrite = TRUE)

plot(map.RF.r1, main = "Random Forest model predicted SOC (0-5cm)")
```

输出内容见文件`https://forestcollection.lanzout.com/iMcsR1s782sf`;链接为蓝奏云外链

###### A test: KM & FKM & FCM

```r
#### Ready ####
library(tidyverse)
library(terra)

fc_use <- rast("./use0909/fc_use.tif")
aspect_use <- rast("./use0909/aspect_use.tif")
slope_use <- rast("./use0909/slope_use.tif")
dem_use <- rast("./use0909/dem_use.tif")
wi_use <- rast("./use0909/wi_use.tif")
watershed <- vect("./data0909/watershed_line_epsg32651.geojson")

all <- c(fc_use, aspect_use, slope_use, dem_use, wi_use)
all <- all %>%
  mask(., fc_use, maskvalues = NA) %>%
  mask(., as.polygons(watershed))
plot(all)
all_table <- as.data.frame(all, xy = TRUE) %>% as_tibble() %>%
  mutate_at(.vars = 3, .funs=as.integer)
colnames(all_table)[3] <- "fc"
colnames(all_table)[6] <- "dem"
head(all_table)

#### KM ####

# remotes::install_github("DickBrus/sswr")
# library(sswr) # 仅测试

library(sp)
library(fields)
library(ggplot2)

summary(all_table)
cor(all_table[,c(3,4,5,6,7)])

#Set number of sampling locations to be selected

n<-20

#Compute clusters

set.seed(314)
myClusters <- kmeans(scale(all_table[,c(3,4,5,6,7)]), centers=n, iter.max=100,nstart=10)
all_table$clusters <- myClusters$cluster

#Select locations closest to the centers of the clusters

rdist.out <- rdist(x1=myClusters$centers,x2=scale(all_table[,c(3,4,5,6,7)]))
ids.mindist <- apply(rdist.out,MARGIN=1,which.min)
mySample <- all_table[ids.mindist,]

#Plot clusters and sampling points

ggplot(all_table) +
  geom_tile(mapping = aes(x = x, y = y, fill = factor(clusters))) +
  scale_fill_discrete(name = "cluster") +
  geom_point(data=mySample,mapping=aes(x=x,y=y),size=2) +
  scale_x_continuous(name = "") +
  scale_y_continuous(name = "") +
  coord_fixed() +
  theme(legend.position="none")

ggplot(all_table) +
  geom_point(mapping=aes(y=dem,x=wi,colour=factor(clusters))) +
  geom_point(data=mySample,mapping=aes(y=dem,x=wi),size=2) +
  scale_y_continuous(name = "DEM") +
  scale_x_continuous(name = "WI") +
  theme(legend.position="none")

#### FKM ####
# https://search.r-project.org/CRAN/refmans/fclust/html/FKM.html
library(fclust)

myClustersFKM <- FKM(scale(all_table[,c(3,4,5,6,7)]), k = 20, seed = 314)
all_table$clusters <- myClustersFKM$clus[,1]
rdist.out <- rdist(x1=myClustersFKM$H,x2=scale(all_table[,c(3,4,5,6,7)]))
ids.mindist <- apply(rdist.out,MARGIN=1,which.min)
mySample <- all_table[ids.mindist,]

ggplot(all_table) +
  geom_tile(mapping = aes(x = x, y = y, fill = factor(clusters))) +
  scale_fill_discrete(name = "cluster") +
  geom_point(data=mySample,mapping=aes(x=x,y=y),size=2) +
  scale_x_continuous(name = "") +
  scale_y_continuous(name = "") +
  coord_fixed() +
  theme(legend.position="none")

ggplot(all_table) +
  geom_point(mapping=aes(y=dem,x=wi,colour=factor(clusters))) +
  geom_point(data=mySample,mapping=aes(y=dem,x=wi),size=2) +
  scale_y_continuous(name = "DEM") +
  scale_x_continuous(name = "WI") +
  theme(legend.position="none")

# 理解：和Kmean相同，都有clusters和 聚类与变量的相关矩阵

#### FCM ####
# https://www.rdocumentation.org/packages/ppclust/versions/1.1.0.1/topics/fcm
# https://ieeexplore.ieee.org/document/9985227
library(ppclust)

# Load dataset 
x <- all_table[,c(3,4,5,6,7)]

# Initialize the prototype matrix using K-means++ algorithm
v <- inaparc::kmpp(x, k=3)$v

# Initialize the memberships degrees matrix 
u <- inaparc::imembrand(nrow(x), k=3)$u

# Run FCM with the initial prototypes and memberships
fcm.res <- fcm(x, centers=v, memberships=u, m=2)

# Show the fuzzy membership degrees for the top 5 objects
head(fcm.res$u, 5)

all_table$clusters <- fcm.res$cluster

#Select locations closest to the centers of the clusters

# 此处注意使用scale()函数进行归一化处理
# https://www.jianshu.com/p/115d07af3029

rdist.out <- rdist(x1=scale(fcm.res$v),x2=scale(all_table[,c(3,4,5,6,7)]))
ids.mindist <- apply(rdist.out,MARGIN=1,which.min)
mySample <- all_table[ids.mindist,]

#Plot clusters and sampling points

ggplot(all_table) +
  geom_tile(mapping = aes(x = x, y = y, fill = factor(clusters))) +
  scale_fill_discrete(name = "cluster") +
  geom_point(data=mySample,mapping=aes(x=x,y=y),size=2) +
  scale_x_continuous(name = "") +
  scale_y_continuous(name = "") +
  coord_fixed() +
  theme(legend.position="none")

ggplot(all_table) +
  geom_point(mapping=aes(y=dem,x=wi,colour=factor(clusters))) +
  geom_point(data=mySample,mapping=aes(y=dem,x=wi),size=2) +
  scale_y_continuous(name = "DEM") +
  scale_x_continuous(name = "WI") +
  theme(legend.position="none")

```

输出内容见文件`https://forestcollection.lanzout.com/iWJ1l1s88n7g`;链接为蓝奏云外链