
[QGIS](https://qgis.org/en/site/)

## Book

[Books & News from Locate Press | Geospatial Open Source E-Books](https://locatepress.com/)

## Map

[World Imagery Wayback](https://livingatlas.arcgis.com/wayback/)

> QGIS可用 WMTS 服务
> https://wayback.maptiles.arcgis.com/arcgis/rest/services/World_Imagery/MapSTrver/WMTS/1.0.0/WMTSCapabilities.xml

## Dev

[PyQGIS Developer Cookbook — QGIS Documentation documentation](https://docs.qgis.org/3.34/en/docs/pyqgis_developer_cookbook/index.html)

[Fsu0413's Original Qt builds](https://build-qt.fsu0413.me/index.html)

[Qt 镜像使用帮助 — USTC Mirror Help 文档](https://mirrors.ustc.edu.cn/help/qtproject.html#id1)

## User

[Open Sans - Download & use Open Sans font](https://www.opensans.com/)

[CUOSGwiki](https://dges.carleton.ca/CUOSGwiki/)

[QGIS Tutorials and Tips](https://www.qgistutorials.com/en/)

[Principles and Applications of GIS and RS](https://principles-and-applications-of-rs-and-gis.readthedocs.io/en/latest/index.html)

## Plugin

QSWAT+: [SWAT+](https://swatplus.gitbook.io/docs/) | [ChrisWGeorge / QSWATPlus3](https://bitbucket.org/ChrisWGeorge/qswatplus3/downloads/)

WhiteboxTools: [WhiteboxTools Open Core](https://www.whiteboxgeo.com/geospatial-software/) | [WhiteboxTools for Processing — Alexander Bruy](https://bruy.me/plugins/whitebox-tools-for-processing/) | [WhiteboxTools for QGIS](https://plugins.qgis.org/plugins/wbt_for_qgis/) | [WhiteboxTools User Manual](https://www.whiteboxgeo.com/manual/wbt_book/intro.html)

Conefor: [Conefor for Processing — Alexander Bruy](https://bruy.me/plugins/conefor-for-processing/) | [What is Conefor? | Conefor](http://www.conefor.org/sourcecodes.html)

SLYR: [SLYR: the ESRI to QGIS Compatibility Suite – North Road (north-road.com)](https://north-road.com/slyr/)

ImportPhoto: [KIOS-Research/ImportPhotos: This tool can be used to import Geo-Tagged photos (jpg or jpeg) as points to QGIS.](https://github.com/KIOS-Research/ImportPhotos)

QField: [QField Sync](https://plugins.qgis.org/plugins/qfieldsync/) | [QField - Efficient field work built for QGIS](https://qfield.org/) | Mobile

TianDiTu: [TianDiTu Tools](https://plugins.qgis.org/plugins/tianditu-tools/)

Project Packager: [Project Packager](https://plugins.qgis.org/plugins/ProjectPackager/) 

------

[GRASS GIS 8.3.2dev Reference Manual - GRASS GIS Manual (osgeo.org)](https://grass.osgeo.org/grass83/manuals/index.html)

[SAGA - System for Automated Geoscientific Analyses (sourceforge.io)](https://saga-gis.sourceforge.io/en/index.html)

[Orfeo ToolBox – Orfeo ToolBox is not a black box](https://www.orfeo-toolbox.org/)

## Blog

[QGIS及Open Geodata資源網@Sinica](https://gis.rchss.sinica.edu.tw/qgis/)

## Tips

**QField**

- 创建矢量使用`.gpkg`格式；在QField 手机端导入的数据，会存入Imported Projects文件夹，导出时需注意，原导入文件位置中内容未改变，需导出该文件夹内容，可选`发送到`或`导出到文件夹`

**QSWAT+**

- Main Steps→Delineate Watersh→Select DEM→Create streams→Create watershed

- DEM需事先重投影为对应区域的投影坐标系，如EPSG：4499

**QGIS**

- 矢量 - 空间索引 需将矢量文件保存为`.gpkg`而不是`.geojson`