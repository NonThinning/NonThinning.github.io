
## Preparation

```bash
conda install r-base=4.0.5 r-devtools r-raster r-terra r-dismo r-sf r-classInt r-units r-stars r-gstat r-rgdal r-XML r-codetools r-reshape r-Hmisc r-ROCR r-randomForest r-pbkrtest r-quantreg r-lme4 r-car r-brglm r-qvcalc r-BradleyTerry2 r-R.utils r-gdalUtils r-rjson r-RCurl r-spatstat r-mda r-psych r-nortest r-fossil r-AICcmodavg r-SDMTools r-xgboost r-ranger r-snowfall r-h2o r-hexbin r-Cubist r-randomForestSRC r-ggRandomForests r-doParallel r-gam r-glmnet r-SuperLearner r-intamap r-fasterize r-aqp=1.42 r-geoR
```

```r
devtools::install_version("sftime", version="0.2-0")
devtools::install_version("plotKML", version="0.8-3")
devtools::install_version("soiltexture", version="1.5.1")
devtools::install_version("quantregForest", version="1.3-7")
devtools::install_version("maxlike", version="0.1-10")
devtools::install_github("h2oai/h2o-3/h2o-r/ensemble/h2oEnsemble-package")
remotes::install_github("cran/GSIF#1") # 可能导致部分错误,临时解决方法
```

```bash
conda install jupyterlab jupyter-lsp r-languageserver jupyterlab-language-pack-zh-CN
```

```r
devtools::install_github('IRkernel/IRkernel')
IRkernel::installspec()
```
