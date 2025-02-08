
## Error 1

```shell
conda create -y -n renv363 r-base=3.6.3
conda activate renv363
conda install r-essentials=3.6
conda install r-devtools
```

install`https://cran.r-project.org/bin/windows/Rtools/Rtools35.exe`

```r
pkgbuild::check_build_tools(debug = TRUE)
devtools::install_version("GSIF", version = "0.5-5.1")
```

## 

```shell
scoop install versions/r41
scoop install versions/rtools40
```

