
## Info

[Extract Remote Sensing Vegetation Phenology • phenofit](https://phenofit.top/index.html)

[phenofit: An R package for extracting vegetation phenology from time series remote sensing - Kong - 2022 - Methods in Ecology and Evolution - Wiley Online Library](https://besjournals.onlinelibrary.wiley.com/doi/10.1111/2041-210X.13870)

> [Extract Remote Sensing Vegetation Phenology • phenofit2](https://eco-hydro.github.io/phenofit2/)
>
> [ggplot layers • gg.layers](https://rpkgs.github.io/gg.layers/)

[Photoperiod Explains the Asynchronization Between Vegetation Carbon Phenology and Vegetation Greenness Phenology - Kong - 2020 - Journal of Geophysical Research: Biogeosciences - Wiley Online Library](https://agupubs.onlinelibrary.wiley.com/doi/10.1029/2020JG005636)

[Welcome to the TIMESAT pages!](https://web.nateko.lu.se/timesat/timesat.asp)

[如何用MODIS数据在TIMESAT中提取物候参数-CSDN博客](https://blog.csdn.net/qq_40872284/article/details/121424632)

[teetor'n](https://nteetor.github.io/zeallot) | [R: Multiple assignment operators](https://search.r-project.org/CRAN/refmans/zeallot/html/operator.html)

> [未来的库可以使用R的zeallot库吗？ - r - SO中文参考 - www.soinside.com](https://www.soinside.com/question/GpR9GoePzgTLAsi72iFdzH)
>
> > [前缀、中缀、后缀表达式_前缀表示法-CSDN博客](https://blog.csdn.net/antineutrino/article/details/6763722)

------

[孔冬冬-教师个人主页 中国地质大学（武汉）教师个人主页系统](https://grzy.cug.edu.cn/kongdd)

> [2023CUG水文气象学课程](https://cug-hydro.github.io/class2023_CUG_HydroMet/)
>
> [CUG-hydro/class2023_CUG_HydroMet: 2023年CUG水文气象学课程](https://github.com/CUG-hydro/class2023_CUG_HydroMet)
>
> [孔sysu - 知乎](https://www.zhihu.com/people/kongdd)

## Example

[eco-hydro/phenofit: R package: A state-of-the-art Vegetation Phenology extraction package, phenofit](https://github.com/eco-hydro/phenofit)

[Extract Remote Sensing Vegetation Phenology • phenofit](https://phenofit.top/)

[eco-hydro/phenofit-scripts: phenofit examples in version 3.0](https://github.com/eco-hydro/phenofit-scripts)

以下代码仅在此基础上，修改`ImageCollection`为`COPERNICUS/S2_SR_HARMONIZED`，并修改`point`坐标。

`https://code.earthengine.google.com/c9d04866f70a19c4e1cf8588af7aedc5`

```javascript
var range = [122.20,53.38, 122.40,53.48];

var col = ee.ImageCollection('COPERNICUS/S2_SR_HARMONIZED')
  .filterDate('2013-01-01', '2023-12-31')
```

## 1

`https://github.com/eco-hydro/phenofit/blob/HEAD/vignettes/phenofit_CA-NS6.Rmd`

> 备注：每行的注释在上方

```r
# 物候
library(phenofit)
# 数据操作/处理
library(data.table)
# 时间数据处理转换
library(lubridate)
# 函数编程
library(purrr)
# 绘图
library(ggplot2)

ymax_min   <- 0.1
rymin_less <- 0.8
nptperyear <- 23
# wBisquare是phenofit包中定义的一个函数
wFUN       <- wBisquare

# 示例数据集，由两个数据框组成的列表
data('MOD13A1')
# 拆分为数据框，包含不同时间不同站点的植被指数等信息
df <- MOD13A1$dt 
# 拆分为数据框，包含各站点的坐标等信息
st <- MOD13A1$st

# 提示, df[,1]显示第一列（的部分行信息）
# :=为海象运算符，意为 variable_name := expression or value 此处用于添加列
# 该功能为data.table包引入
# ymd()、year()、yday()函数由lubridate包引入
# as.integer()将字符串转换为整数，此处用于计算在一年中的第几天并转换为整数
df[, `:=`(date = ymd(date), year = year(date), doy = as.integer(yday(date)))]
# 如果这一行缺少DayOfYear，则将doy的值给DayOfYear
df[is.na(DayOfYear), DayOfYear := doy]

# 为什么以300为界限(疑问？)
# 大于300的年份加1?
# 逐行进行计算，新增t，作为日期
# as.Date()由data.table包引入
# abs()取绝对值; sprintf()函数返回一个字符串，%d用于代替数字
# %nd 这里的"n"代指字符串的长度,如果够就用空格补齐,如果是0则用0补齐
# %m.nf 是用来处理浮点数的,m代表着字符宽度,n代表保留几位小数。
# "%Y-%j"将字符串格式化为年和一年的第几天，经过as.Date()函数后显示为2009-10-29的格式
df[abs(DayOfYear - doy) >= 300, t := as.Date(sprintf("%d-%03d", year+1, DayOfYear), "%Y-%j")] # last scene
df[abs(DayOfYear - doy) <  300, t := as.Date(sprintf("%d-%03d", year  , DayOfYear), "%Y-%j")]

# df[, .(site, t)] 筛选出其中名为site, t的两列
# 去除时间和站点同时重复的行 !duplicated
df <- df[!duplicated(df[, .(site, t)]), ]

# 新建了两列，qc_summary()函数的计算结果存入"QC_flag", "w"两列
df[, c("QC_flag", "w") := qc_summary(SummaryQA)]
# 选择了其中的6个变量，其中1e4为科学记数法形式
df <- df[, .(site, y = EVI/1e4, t, date, w, QC_flag)]

# Unique()函数 用于返回一个没有任何重复元素/行的向量、数据框或数组
sites        <- unique(df$site)
# 选择其中一个站点
sitename     <- sites[3]
# 根据站点筛选值
d            <- df[site == sitename] # get the first site data
sp           <- st[site == sitename]

# 区分南北半球
south      <- sp$lat < 0
print      <- FALSE # whether print progress
IsPlot     <- TRUE  # for brks

prefix_fig <- "phenofit"
# 格式化多变量为一个字符串，with()函数，意思是对sp变量内的变量进行操作
# 其中的ID 实际效果类似于sp$ID
titlestr   <- with(sp, sprintf('[%03d,%s] %s, lat = %5.2f, lon = %6.2f',
                               ID, site, IGBPname, lat, lon))
# 字符串操作，此处为了生成特定名称的文件名
file_pdf   <- sprintf('Figure/%s_[%03d]_%s.pdf', prefix_fig, sp$ID[1], sp$site[1])

# add_HeadTail 为phenofit中的函数
dnew  <- add_HeadTail(d, south, nptperyear = 23) # add additional one year in head and tail
# check_input 为phenofit中的函数
INPUT <- check_input(dnew$t, dnew$y, dnew$w, dnew$QC_flag,
                     nptperyear, south, 
                     maxgap = nptperyear/4, alpha = 0.02, wmin = 0.2)
# par()绘图的参数
par(mar = c(3, 2, 2, 1), mgp = c(3, 0.6, 0))
# init_lambda 为phenofit中的函数
lambda <- init_lambda(INPUT$y)
# season_mov 为phenofit中的函数
brks2 <- season_mov(INPUT, 
                    list(rFUN = "smooth_wWHIT", wFUN = wFUN, maxExtendMonth = 6, r_min = 0.1))
# 生成一个图，为phenofit中的函数
plot_season(INPUT, brks2)

fit  <- curvefits(INPUT, brks2,
                  options = list(
                    methods = c("AG", "Zhang", "Beck", "Elmore"), #,"klos",, 'Gu'
                    wFUN = wFUN,
                    nextend = 2, maxExtendMonth = 3, minExtendMonth = 1, minPercValid = 0.2
                  ))
l_param <- get_param(fit)
print(str(l_param, 1))

print(l_param$AG)
d_fit <- get_fitting(fit)

d_gof <- get_GOF(fit)
print(head(d_gof))
print(fit$`2002_1`$fFIT$AG$ws)

g <- plot_curvefits(d_fit, brks2, NULL, ylab = "NDVI", "Time",
                    theme = coord_cartesian(xlim = c(ymd("2000-04-01"), ymd("2017-07-31"))))

# grid包
# 此处生成一个图
grid::grid.newpage(); grid::grid.draw(g)# plot to check the curve fitting
l_pheno <- get_pheno(fit, IsPlot = F) #%>% map(~melt_list(., "meth"))

# 此处生成一个图
pheno <- get_pheno(fit[1:6], "Elmore", IsPlot = T)
head(l_pheno$doy$AG)
```

## 2

修改自 `https://github.com/eco-hydro/phenofit-scripts/blob/master/multiGS_Sentinel2_KongYing/phenofit-Sentinel2_KongYing.R`

待补充注释

```r
library(terra)
library(tidyverse)
library(sp)
library(phenofit) # install.packages("phenofit")

# remotes::install_github("rpkgs/sf2")
# remotes::install_github("kongdd/Ipaper")
  # install.packages("data.table")
  # install.packages("magrittr")

file_vi <- ".\\Data\\sentinel2_LYL_2_2019-2021_EVI2.tif"
file_qc <- ".\\Data\\sentinel2_LYL_2_2019-2021_SCL.tif"

read_rast <- function(file, dates = NULL) {
  r = rast(file)
  # guess date from band names
  # Note that might be failed to guess date
  if (is.null(dates)) {
    dates = names(r) %>% 
      gsub("_", "", .) %>% 
      substr(1, 8) %>% 
      as.Date("%Y%m%d")
  }
  # 如果日期不存在，根据名称猜测日期
  # 将日期变量和名称都改为日期
  terra::time(r) = dates
  names(r) = dates
  r
}



rast2mat <- function(r, backval = 0.1) {
  d_coord = sf2::rast_df(r[[1]])
  arr = sf2::rast_array(r)
  mat = Ipaper::array_3dTo2d(arr)
  
  range = ext(r) %>% as.vector() # [xmin, xmax, ymin, ymax]
  cellsize = res(r)
  grid <- sf2::make_grid(range, cellsize)
  x_mean = mat %>% rowMeans(na.rm = TRUE)
  I_grid = which(!(x_mean <= backval | is.na(x_mean)))
  d_coord = grid@coords %>% data.table::as.data.table() %>% magrittr::set_colnames(c("lon", "lat")) %>% cbind(I = 1:nrow(.), .)
  Ipaper::listk(mat, dates = terra::time(r), x_mean, 
                d_coord, I_grid, grid, r = r)
}

l = read_rast(file_vi) %>% rast2mat()
l_qc <- read_rast(file_qc) %>% rast2mat()

dates = l$dates

data <- Ipaper::listk(VI = l$mat, QC = l_qc$mat, dates, qcFUN = qc_sentinel2)

# install.packages("Cairo")
library(Cairo)
# 1为运行，0为跳过
if (0) {
  # explore raw file
  b = read_rast(file_vi)
  r = b[[6]]
  # file_raw = "sentinel2_kongying_raw.pdf"
  file_raw = "sentinel2_LYL_raw.pdf"
  Ipaper::write_fig({
    i = 1; terra::plot(b[[seq((i-1)*16+1, i*16)]])
    i = 2; terra::plot(b[[seq((i-1)*16+1, i*16)]])
    i = 3; terra::plot(b[[seq((i-1)*16+1, i*16)]])
    i = 4; terra::plot(b[[seq((i-1)*16+1, i*16)]])
    i = 5; terra::plot(b[[seq((i-1)*16+1, nlyr(b))]])
  }, file_raw, 10, 8, use.cairo_pdf = FALSE)
  # pdf_view(file_raw)
}

# 默认参数
opt_old <- get_options()

# 新设置的参数（问题：参数如何确定？）
opt <- list(
  nptperyear = 20,
  wFUN = wTSM, wmin = 0.2,
  verbose = FALSE,
  season = list(
    # rFUN = "smooth_wWHIT", smooth_wHANTS, smooth_wSG, lambda = 0.5,
    rFUN = "smooth_wHANTS", nf = 6, lambda = 10,
    maxExtendMonth = 12, r_min = 0.0, r_max = 0.1),
  # fine fitting parameters
  fitting = list(nextend = 1, minExtendMonth = 0, maxExtendMonth = 0.5,
                 methods = c("AG", "Zhang", "Beck", "Elmore", "Gu")[3], #,"klos",, 'Gu'
                 iters = 1,
                 minPercValid = 0)
)

set.seed(1)
inds = sample(1:nrow(data$VI), 100) %>% sort()
inds = 1:nrow(data$VI)
# inds = c(858, 878, 1017, 1129, 1222, 1328, 3101) # bads, 878 is the last error

par(mfrow = c(4, 1), mar = c(0, 3, 1.6, 1), mgp = c(1.2, 0.6, 0))
set_options(options = opt, season = list(rtrough_max = 0.7))

library(phenofit)
library(Ipaper) # remotes::install_github("rpkgs/Ipaper")
library(sf2) # remotes::install_github("rpkgs/sf.extra")
library(rcolors)
# library(lattice.layers)

library(grid)
library(ggplot2)
library(ggnewscale)
library(lubridate)
library(zeallot)
library(stringr)

library(dplyr)
library(job)
library(sp)
# library(sf)
# library(terra)

library(data.table)
library(dplyr)

library(magrittr)

get_input <- function(i, data, wmin = 0.2, wmid = 0.5) {
  d = data.table::data.table(VI = data$VI[i,], QC = data$QC[i, ])
  if (!is.null(data$DOY)) {
    # this is for MODIS DOY
    d %<>% mutate(t = getRealDate(data$dates, data$DOY[i, ]))
  }
  library(zeallot)
  c(d$QC_flag, d$w) %<-% data$qcFUN(d$QC, wmin = wmin, wmid = wmid)
  d
}

Ipaper::InitCluster(32, kill = FALSE)
res = foreach(i = inds %>% set_names(.,.), icount()) %dopar% {
  Ipaper::runningId(i, 1e2)
  d = get_input(i, data)
  # d$t = dates
  library(phenofit)
  input <- check_input(dates, d$VI, d$w, QC_flag = d$QC_flag,
                       nptperyear = get_options("nptperyear"),
                       maxgap = get_options("nptperyear") / 4, wmin = 0.2)
  tryCatch({
    # r = phenofit_point(d, dates)$pheno
    brks <- season_mov(input, years.run = NULL)
    rfit <- brks2rfit(brks) # used rough fitting directly
    r <- get_pheno(rfit)$doy
  }, error = function(e) {
    message(sprintf('%s', e$message))
  })
  
  # plot_season(input, brks, title = i, show.legend = F)
}
# dev_off()

save(res, file = "sentinel2_LYL_V2.rda")

load("sentinel2_LYL_V2.rda")

df = res %>% rm_empty() %>% melt_list("gridId") %>% cbind(meth = "rough", .) #%>% dplyr::select(-meth)
df[, gridId := as.integer(gridId)]
# df[, meth := as.factor(meth)]
inds_bad = df[grep("_4", flag)]$gridId %>% unique() %>% sort()

select_first_nGS <- function(df, nGS = 1) {
  ind_valid = rowMeans(df[, -(1:4)], na.rm = TRUE) %>% which.notna()
  df = df[ind_valid, ] %>% cbind(I = 1:nrow(.), .) # rm all NA records
  
  # inds_bad = df[, grep("_4", flag)]
  gs = as.numeric(substr(df$flag, 6, 6))
  inds_bad = gs %>% { which(. > nGS) }
  
  if (length(inds_bad) == 0) {
    return(df %>% select(-I, -TRS5.los))
  }
  info_bad = df[inds_bad, .N, .(gridId, meth, origin)] %>% select(-N)
  
  df_bad = merge(df, info_bad) %>%
    reorder_name(c("gridId", "meth", "origin", "flag"))
  df_good = df[-df_bad$I, ]
  
  df_mutiGS = dt_ddply(df_bad, .(gridId, meth, origin), function(d) {
    los = d$TRS5.eos - d$TRS5.sos
    n = length(los)
    if (n > nGS) {
      i_bad = which.min(los)
      # if the smallest GS in the head or tail
      if (i_bad %in% c(1, n)) {
        d = d[-i_bad, ]
      } else {
        # rm the GS with the largest ratio of unintersect period with the current year
        perc_bad_head = pmax(0 - d$TRS5.sos[1], 0) / d$TRS5.eos[1]
        perc_bad_tail = pmax(d$TRS5.eos[n] - 365, 0) / d$TRS5.eos[n]
        i_bad = ifelse(perc_bad_head >= perc_bad_tail, 1, n)
        d = d[-i_bad, ]
      }
      n = nrow(d)
      # if still > nGS, then only kept the l
      if (n > nGS) {
        ind = order(los, decreasing = TRUE)[1:nGS]
        d = d[ind, ]
      }
    }
    d %>% mutate(flag = sprintf("%s_%d", year(origin), 1:nrow(.)))
    # d
  })
  rbind(
    df_good %>% select(-I),
    df_mutiGS %>% select(-I)
  )
}

point2rast <- function(df, d_coord,
                       outdir = "OUTPUT", prefix = "phenofit", overwrite = TRUE)
{
  mkdir(outdir)
  sp2 <- as(df2sp(d_coord), "SpatialPixelsDataFrame")
  # flags <- unique(df$flag) %>% sort()
  d_grp = unique(df[, .(meth, flag)])[order(flag)]
  
  for (i in 1:nrow(d_grp)) {
    # if (i != 1) next()
    METH = d_grp$meth[i]
    FLAG = d_grp$flag[i]
    
    outfile <- glue("{outdir}/{prefix}_{METH}_{FLAG}.tif")
    mkdir(dirname(outfile))
    
    if (file.exists(outfile) && !overwrite) next()
    cat(outfile, "\n")
    
    d <- df[flag == FLAG & meth == METH, ]
    
    ind <- match(1:nrow(d_coord), d$gridId)
    data <- d[ind, -(1:4)]
    sp2@data <- data
    
    r <- raster::brick(sp2) %>% rast() %>% set_names(names(sp2))
    terra::writeRaster(r, outfile, overwrite = TRUE)
    # rgdal::setCPLConfigOption("GDAL_PAM_ENABLED", "FALSE")
    # file.remove(paste0(outfile, ".aux.xml")) # rm the .aux.xml file
  }
}

prj84 = sp::CRS("+proj=longlat +datum=WGS84 +no_defs")
df2sp <- function (d, formula = ~lon + lat, prj) {
  if (missing(prj))
    prj <- prj84
  coordinates(d) <- formula
  proj4string(d) <- prj
  return(d)
}

df2 = select_first_nGS(df, nGS = 1)
point2rast(df2, l$d_coord, outdir = "outdir",
           prefix = "Sentinel2_LYL_Pheno", overwrite = TRUE)


files = dir("outdir", "*.tif", full.names = TRUE)

test <- rast(files)

plot(test[[12:22]])
plot(test[[23:33]])
plot(test[[34:44]])
plot(test[[45:55]])
plot(test[[56:66]])
```



