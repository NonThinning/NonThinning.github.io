
## Document

### Developer

[PyQGIS Developer Cookbook — QGIS Documentation documentation](https://docs.qgis.org/3.34/en/docs/pyqgis_developer_cookbook/index.html)

[PyQGIS开发者手册](https://luolingchun.github.io/PyQGIS-Developer-Cookbook-cn/)

### User

[CUOSGwiki](https://dges.carleton.ca/CUOSGwiki/)

[QGIS Tutorials and Tips — QGIS Tutorials and Tips](https://www.qgistutorials.com/en/)

[Principles and Applications of GIS and RS - open educational resource — Principles of GIS and Remote Sensing 4.0.0 documentation](https://principles-and-applications-of-rs-and-gis.readthedocs.io/en/latest/index.html)

[QGIS及Open Geodata資源網@Sinica](https://gis.rchss.sinica.edu.tw/qgis/)

## Plugin

[About SWAT+ - SWAT+ Installation & Help (gitbook.io)](https://swatplus.gitbook.io/docs/)

> [ChrisWGeorge / QSWATPlus3 / Downloads — Bitbucket](https://bitbucket.org/ChrisWGeorge/qswatplus3/downloads/)

[WhiteboxTools for Processing — Alexander Bruy](https://bruy.me/plugins/whitebox-tools-for-processing/) | [Geospatial Software: WhiteboxTools Open Core - Whitebox Geospatial Inc](https://www.whiteboxgeo.com/geospatial-software/) | [WhiteboxTools for QGIS — QGIS Python Plugins Repository](https://plugins.qgis.org/plugins/wbt_for_qgis/)

[Conefor for Processing — Alexander Bruy](https://bruy.me/plugins/conefor-for-processing/) | [What is Conefor? | Conefor](http://www.conefor.org/)

> [Alexander Bruy](https://bruy.me/)

[KIOS-Research/ImportPhotos: This tool can be used to import Geo-Tagged photos (jpg or jpeg) as points to QGIS.](https://github.com/KIOS-Research/ImportPhotos)

> [mariosmsk.wordpress.com](https://mariosmsk.wordpress.com/)

[SLYR: the ESRI to QGIS Compatibility Suite – North Road (north-road.com)](https://north-road.com/slyr/)

------

[SAGA - System for Automated Geoscientific Analyses (sourceforge.io)](https://saga-gis.sourceforge.io/en/index.html)

[GRASS GIS 8.3.2dev Reference Manual - GRASS GIS Manual (osgeo.org)](https://grass.osgeo.org/grass83/manuals/index.html)

[Orfeo ToolBox – Orfeo ToolBox is not a black box](https://www.orfeo-toolbox.org/)

[SNAP – STEP (esa.int)](https://step.esa.int/main/toolboxes/snap/)

------

[QField - Efficient field work built for QGIS](https://qfield.org/)

## More

[Open Sans - Download & use Open Sans font](https://www.opensans.com/)

[Fsu0413's Original Qt builds](https://build-qt.fsu0413.me/index.html)

> [Qt 镜像使用帮助 — USTC Mirror Help 文档](https://mirrors.ustc.edu.cn/help/qtproject.html#id1)

### Tips

**QField**

- 创建矢量使用`.gpkg`格式；在QField 手机端导入的数据，会存入Imported Projects文件夹，导出时需注意，原导入文件位置中内容未改变，需导出该文件夹内容，可选`发送到`或`导出到文件夹`

**QSWAT+**

Main Steps→Delineate Watersh→Select DEM→Create streams→Create watershed

注意：DEM需事先重投影为对应区域的投影坐标系，如EPSG：4499

**QGIS**

- 矢量 - 空间索引 需将矢量文件保存为`.gpkg`而不是`.geojson`