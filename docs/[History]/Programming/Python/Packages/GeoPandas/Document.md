
[GeoPandas 1.0.1 — GeoPandas 1.0.1+0.g747d66e.dirty 文档](https://geopandas.org/en/stable/index.html)

[pyogrio - bulk-oriented spatial vector file I/O using GDAL/OGR — pyogrio 0.10.0+5.gfc555f0.dirty documentation](https://pyogrio.readthedocs.io/en/latest/index.html) | 读取geojson

[Shapely — Shapely 2.0.6 documentation](https://shapely.readthedocs.io/en/stable/index.html) | 操作几何图形

```shell
conda install gdal geopandas pyogrio -y -c conda-forge

gdalinfo --version
set GDAL_INCLUDE_PATH=%CONDA_PREFIX%\Library\include
set GDAL_LIBRARY_PATH=%CONDA_PREFIX%\Library\lib
set GDAL_VERSION=3.9.3
```

