
## Info

[rOpenSci - open tools for open science](https://ropensci.org/)

## Packages

[Framework for Easy Statistical Modeling, Visualization, and Reporting • easystats](https://easystats.github.io/easystats/) | 简单统计

[Univariate and Multivariate Spatial Modeling of Species Abundance • spAbundance](https://www.jeffdoser.com/files/spabundance-web/) | 物种模型

> [spAbundance: An R package for single‐species and multi‐species spatially explicit abundance models - Doser - 2024 - Methods in Ecology and Evolution - Wiley Online Library](https://besjournals.onlinelibrary.wiley.com/doi/full/10.1111/2041-210X.14332)

[Global Surface Summary of the Day (GSOD) Weather Data Client • GSODR](https://ropensci.github.io/GSODR/index.html) | 气温相关，查询气象站点

已停用，代码可参考 [ropensci/rnoaa: R interface to many NOAA data APIs](https://github.com/ropensci/rnoaa) | NOAA数据

[Interface to Download Meteorological (and Hydrological) Datasets • climate](https://bczernecki.github.io/climate/) | 气象水文数据集下载

[metno/esd: An R-package designed for climate and weather data analysis, empirical-statistical downscaling, and visualisation.](https://github.com/metno/esd) | 气候数据分析R包

[Tools for Descriptive Statistics • DescTools](https://andrisignorell.github.io/DescTools/) | 描述性统计分析

[daijiang/rtrees: rtrees: an R package to assemble phylogenetic trees from mega-trees](https://github.com/daijiang/rtrees) | 为动物和植物生成系统发育树

> [Deriving Phylogenies from Synthesis Trees • rtrees](https://daijiang.github.io/rtrees/)

[Interpretable Machine Learning • iml](https://giuseppec.github.io/iml/) | 可解释机器学习

[VGAM](https://www.stat.auckland.ac.nz/~yee/VGAM/) | 广义线性和加性模型

[CRAN: Package mgcv](https://cran.r-project.org/web/packages/mgcv/index.html) | 广义加法（混合）模型

[Visualisations for Generalized Additive Models • mgcViz](https://mfasiolo.github.io/mgcViz/index.html) | 广义加性模型可视化

[An R package for working with generalized additive models • gratia](https://gavinsimpson.github.io/gratia/index.html) | 广义加性模型可视化

[Tidy Model Visualisation for Generalised Additive Models • tidymv](https://stefanocoretta.github.io/tidymv/index.html) | 广义加性模型可视化

[vegan: an R package for community ecologists • vegan](https://vegandevs.github.io/vegan/index.html) | 群落和植被生态学家的排序方法、多样性分析和其他功能。

> [RPubs - vegan PCA: Principal Components Analysis with vegans rda function](https://rpubs.com/brouwern/veganpca)

[Multiverse: Create multiverse analysis in R • multiverse](https://mucollective.github.io/multiverse/)

> [multiverse: Multiplexing Alternative Data Analyses in R Notebooks | Proceedings of the 2023 CHI Conference on Human Factors in Computing Systems](https://dl.acm.org/doi/10.1145/3544548.3580726)

## Configuration

```shell
conda create -n renv -c conda-forge
conda install r-base r-essentials -c conda-forge
```

------

- 在conda中使用`R 4.0`和`jupyter lab`

```shell
conda create -y -n renv4
conda install -c conda-forge r-essentials r-base
```

- 在conda中使用`openblas`

[在Miniconda中安装openblas版本的numpy(附AMD测试) - 知乎](https://zhuanlan.zhihu.com/p/437405027)

```shell
conda install "libblas=*=*openblas" -c conda-forge
```
