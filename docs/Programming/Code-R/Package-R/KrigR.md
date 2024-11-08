---
date: 2024-06-25
---

经测试，win平台 r 4.3.3版本适合于此包安装

[Quick Guide | Erik Kusch](https://www.erikkusch.com/courses/krigr/quickstart/)

以下代码根据需求在此教程基础上部分修改，用于下载地表温度数据，参考[Bioclimatic Variables | Erik Kusch](https://www.erikkusch.com/courses/krigr/bioclim/)还可以下载降水数据

```r
# R version 4.3.3 
# devtools::install_github("https://github.com/cran/rgdal")
# library(rgdal)
# devtools::install_github("https://github.com/ErikKusch/KrigR")
library(KrigR)
Dir.Base <- getwd() # identifying the current directory
Dir.Data <- file.path(Dir.Base, "Data") # folder path for data
Dir.Covariates <- file.path(Dir.Base, "Covariates") # folder path for covariates
Dir.Exports <- file.path(Dir.Base, "Exports") # folder path for exports
## create directories, if they don't exist yet
Dirs <- sapply(
  c(Dir.Data, Dir.Covariates, Dir.Exports),
  function(x) if (!dir.exists(x)) dir.create(x)
)
source("FUN_Plotting.R")

Extent_ext <- extent(c(121.30, 126.10, 52.10, 53.50))
Extent_ext

API_User <- 略
API_Key <- "略"


QS_Raw <- download_ERA(
  Variable = "2m_temperature",
  DataSet = "era5-land",
  DateStart = "2023-01-01",
  DateStop = "2023-01-31",
  TResolution = "day",
  TStep = 1,
  Extent = Extent_ext,
  Dir = Dir.Data,
  FileName = "QS_Raw",
  API_User = API_User,
  API_Key = API_Key
)

Plot_Raw(QS_Raw, Dates = colnames(as.data.frame(QS_Raw, xy = TRUE))[c(-1, -2)])
QS_Raw

Covs_ls <- download_DEM(
  Train_ras = QS_Raw,
  Target_res = .02,
  Dir = Dir.Covariates,
  Keep_Temporary = TRUE
)
Plot_Covs(Covs_ls)
Covs_ls

QS_Krig <- krigR(
  Data = QS_Raw, # data we want to krig as a raster object
  Covariates_coarse = Covs_ls[[1]], # training covariate as a raster object
  Covariates_fine = Covs_ls[[2]], # target covariate as a raster object
  Keep_Temporary = FALSE, # we don't want to retain the individually kriged layers on our hard-drive
  nmax = 40, # degree of localisation
  Cores = 4, # we want to krig using three cores to speed this process up
  FileName = "QS_Krig.nc", # the file name for our full kriging output
  Dir = Dir.Exports # which directory to save our final input in
)
# Plot_Krigs(QS_Krig, Dates = colnames(Raw_df)[c(-1, -2)])
plot(QS_Raw[[1]])
plot(QS_Krig[-3]$Kriging_Output[[1]])
plot(QS_Raw[[1:16]])
plot(QS_Krig[-3]$Kriging_Output[[1:16]])
plot(QS_Raw[[17:31]])
plot(QS_Krig[-3]$Kriging_Output[[17:31]])
QS_Krig[-3]$Kriging_Output

writeRaster(QS_Krig[-3]$Kriging_Output, "test.tif", overwrite = TRUE)
```
