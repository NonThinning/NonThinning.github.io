
## Use Data: GLC-FCS30D

[GLC_FCS30D Global 30-meter Land Cover Change Dataset (1985-2022) - awesome-gee-community-catalog](https://gee-community-catalog.org/projects/glc_fcs/)

```Python
import ee
import geemap
geemap.ee_initialize()
FCS30D = ee.ImageCollection("projects/sat-io/open-datasets/GLC-FCS30D/annual")
image = FCS30D.mosaic(); image
map = geemap.Map()

def recodeClasses(image):
    classes = [10, 11, 12, 20, 51, 52, 61, 62, 
               71, 72, 81, 82, 91, 92, 120, 121, 
               122, 130, 140, 150, 152, 153, 181, 
               182, 183, 184, 185, 186, 187, 190, 
               200, 201, 202, 210, 220, 0]
    reclassed = image.remap(classes, ee.List.sequence(1, len(classes)))
    return reclassed

palette = [
  "#ffff64", "#ffff64", "#ffff00", "#aaf0f0", "#4c7300", "#006400", "#a8c800", "#00a000", 
  "#005000", "#003c00", "#286400", "#285000", "#a0b432", "#788200", "#966400", "#964b00", 
  "#966400", "#ffb432", "#ffdcd2", "#ffebaf", "#ffd278", "#ffebaf", "#00a884", "#73ffdf", 
  "#9ebb3b", "#828282", "#f57ab6", "#66cdab", "#444f89", "#c31400", "#fff5d7", "#dcdcdc", 
  "#fff5d7", "#0046c8", "#ffffff", "#ffffff"
]
vis_params = {"min": 1, "max": 36, "palette": palette}

def addLayer(image, name):
    map.addLayer(image, vis_params ,name)

for i in range(1,23):
    year = 1999 + i
    layerName = "GLC FCS " + str(year)
    band = image.select("b" + str(i))
    addLayer(recodeClasses(band), layerName)

map
```

## Download Data: GLC-FCS30D

```shell
conda install -c conda-forge geedim -y
```

```Python
import ee
import geemap

geemap.ee_initialize()
# 直接读取geojson
edge_ee = geemap.geojson_to_ee(r"C:\Users\Qiao\Documents\FireEdge.geojson")
# FeatureCollection转Feature 此时是线
edge = ee.Feature(edge_ee.toList(edge_ee.size()).get(0))
# 将LinearRing转换为坐标，再转换为多边形
edge_face = ee.Geometry.Polygon(edge_ee.geometry().coordinates())
map = geemap.Map()
map.addLayer(edge_face, {}, "edge")
map
# 读取数据集
FCS30D = ee.ImageCollection("projects/sat-io/open-datasets/GLC-FCS30D/annual")
image = FCS30D.mosaic(); image
image_2022 = (
    image.select("b23")
    .clip(edge_face).unmask()
)

# 数据集样式文件
def recodeClasses(image):
    classes = [10, 11, 12, 20, 51, 52, 61, 62, 
               71, 72, 81, 82, 91, 92, 120, 121, 
               122, 130, 140, 150, 152, 153, 181, 
               182, 183, 184, 185, 186, 187, 190, 
               200, 201, 202, 210, 220, 0]
    reclassed = image.remap(classes, ee.List.sequence(1, len(classes)))
    return reclassed
palette = [
  "#ffff64", "#ffff64", "#ffff00", "#aaf0f0", "#4c7300", "#006400", "#a8c800", "#00a000", 
  "#005000", "#003c00", "#286400", "#285000", "#a0b432", "#788200", "#966400", "#964b00", 
  "#966400", "#ffb432", "#ffdcd2", "#ffebaf", "#ffd278", "#ffebaf", "#00a884", "#73ffdf", 
  "#9ebb3b", "#828282", "#f57ab6", "#66cdab", "#444f89", "#c31400", "#fff5d7", "#dcdcdc", 
  "#fff5d7", "#0046c8", "#ffffff", "#ffffff"
]
vis_params = {"min": 1, "max": 36, "palette": palette}

map.addLayer(recodeClasses(image_2022), vis_params ,"image_2022"); map

geemap.download_ee_image(
    image_2022, 
    filename="GLC-FCS30D-2022-ROI.tif", 
    scale=30, 
    region=edge_face,
    crs='EPSG:4326',
    max_tile_dim = 512
)
```

## Download Data：Copernicus DEM GLO-30 

```shell
! conda install shapely -c conda-forge -y
```

```python
import ee
import geemap
geemap.ee_initialize()

dataset = ee.ImageCollection('COPERNICUS/DEM/GLO30')
elevation = dataset.select('DEM')
elevationVis = {
  "min": 0.0,
  "max": 1000.0,
  "palette": ['0000ff','00ffff','ffff00','ff0000','ffffff'],
}

map = geemap.Map()
map.setCenter(120, 52, 4)
map.addLayer(elevation, elevationVis, 'DEM'); map

import geopandas as gpd
gdf = gpd.read_file(r"C:\Users\Qiao\Documents\FireEdge.geojson")
gdf.crs # 查看坐标系
# 提取第一个几何对象
edge = gdf.geometry.iloc[0]; edge

from shapely.geometry import MultiLineString, LineString, Polygon
from shapely.ops import linemerge
edge.geom_type # 图形类型
edge.is_ring # 图形是否闭合，闭合的LineString可转换为多边形
merged = Polygon(linemerge(edge)); merged # 转换为多边形
merged = gpd.GeoDataFrame(geometry=[merged], crs="EPSG:4326") # 转换为GeoDataFrame

edge_ee = geemap.gdf_to_ee(merged)

map = geemap.Map()
map.addLayer(edge_ee, {}, "Edge"); map

image_ROI = (
    elevation.mosaic()
    .clip(edge_ee)
)
map.addLayer(image_ROI, elevationVis, "image_ROI"); map

geemap.download_ee_image(
    image_ROI, 
    filename="Copernicus DEM GLO-30-ROI.tif", 
    scale=30, 
    region=edge_ee.geometry(),
    crs='EPSG:4326',
    max_tile_dim = 512
)
```

## Download Data：ERA5-Land Monthly Aggregated - ECMWF Climate Reanalysis

5 years mean()

```python
import ee
import geemap
geemap.ee_initialize()

dataset = (
    ee.ImageCollection("ECMWF/ERA5_LAND/MONTHLY_AGGR")
    .filterDate("2019-01-01", "2023-12-31")
    .select("temperature_2m")
)
dataset

tem_mean = dataset.mean()
visualization = {
  "bands": ['temperature_2m'],
  "min": 250,
  "max": 320,
  "palette": [
    '000080', '0000d9', '4000ff', '8000ff', '0080ff', '00ffff',
    '00ff80', '80ff00', 'daff00', 'ffff00', 'fff500', 'ffda00',
    'ffb000', 'ffa400', 'ff4f00', 'ff2500', 'ff0a00', 'ff00ff',
  ]
}
map = geemap.Map()
map.addLayer(tem_mean, visualization, "temperature_2m"); map

edge_ee = geemap.geojson_to_ee(r"C:\Users\Qiao\Documents\FireEdge.geojson")
edge_face = ee.Geometry.Polygon(edge_ee.geometry().coordinates())

image_ERA5Land = (
    tem_mean.clip(edge_face)
)
map.addLayer(image_ERA5Land, visualization, "temperature_2m"); map

geemap.download_ee_image(
    image_ERA5Land, 
    filename="ERA5-Land-Tem2m-ROI.tif", 
    scale=30, 
    region=edge_face,
    crs='EPSG:4326',
    max_tile_dim = 512
)
```