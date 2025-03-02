
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

## Calculate Landsat-5 dNBR

取值范围符合 [EFFIS - Fire Severity](https://forest-fire.emergency.copernicus.eu/about-effis/technical-background/fire-severity)

缺陷：未地形矫正、去云后未填充、图像直方图配准

```python
import ee
import geemap
geemap.ee_initialize()

scale = geemap.geojson_to_ee(r"C:\Users\Qiao\Documents\GEE\MoTa.geojson")

def addNBR(image):
    nbr = image.normalizedDifference(['SR_B4', 'SR_B5']).rename('NBR')
    return image.addBands(nbr)
def apply_scale_factors(image):
  optical_bands = image.select('SR_B.').multiply(0.0000275).add(-0.2)
  thermal_bands = image.select('ST_B6').multiply(0.00341802).add(149.0)
  return image.addBands(optical_bands, None, True).addBands(
      thermal_bands, None, True
  )
def Mask(image):
    qaMask = image.select('QA_PIXEL').bitwiseAnd(int('11111', 2)).eq(0)
    return image.updateMask(qaMask)

dataset = (
    ee.ImageCollection("LANDSAT/LT05/C02/T1_L2")
    .filterDate('1986-05-01', '1986-09-01')
    .filterBounds(scale)
    .filter(ee.Filter.lte('CLOUD_COVER', 25))
    .sort('CLOUD_COVER')
    .map(apply_scale_factors)
    .map(Mask)
    .map(addNBR)
)
postset = (
    ee.ImageCollection("LANDSAT/LT05/C02/T1_L2")
    .filterDate('1987-06-01', '1987-09-01')
    .filterBounds(scale)
    .filter(ee.Filter.lte('CLOUD_COVER', 25))
    .sort('CLOUD_COVER')
    .map(apply_scale_factors)
    .map(Mask)
    .map(addNBR)
)

dNBR = (dataset.select("NBR").mosaic().clip(scale)).subtract(postset.select("NBR").mosaic().clip(scale))

Vis = {
  "min": -1.0,
  "max": 1.0,
  "palette": ['0000ff','00ffff','ffff00','ff0000','ffffff'],
}

Map = geemap.Map()
Map.addLayer(dNBR, Vis, "dNBR")
Map

geemap.download_ee_image(
    dNBR, 
    filename="dNBR-ROI.tif", 
    scale=30, 
    region=scale.geometry(),
    crs='EPSG:4326',
    max_tile_dim = 512
)
```

## Calculate Histogram Matching

[一种快速修复Landsat影像条带色差的方法](https://www.gpxygpfx.com/article/2023/1000-0593-43-11-3483.html)

- [bqt2000204051.users.earthengine.app/javascript/landsat-5-modules.json](https://bqt2000204051.users.earthengine.app/javascript/landsat-5-modules.json)
- [GitHub - xingguangYan/Landsat-5-NDWI-image-restoration](https://github.com/xingguangYan/Landsat-5-NDWI-image-restoration)

```Python
import ee
import geemap
import numpy
geemap.ee_initialize()
MoTa = geemap.geojson_to_ee(r"C:\Users\Qiao\Documents\GEE_Data\MoTa_2022_1873.geojson")
Eumer = geemap.geojson_to_ee(r"C:\Users\Qiao\Documents\GEE_Data\Emuer_HyBAS.geojson")
centroid = ee.Geometry.Polygon(MoTa.first().geometry().coordinates().get(0)).centroid()
point = (
    float(numpy.array(centroid.coordinates().getInfo())[1]), 
    float(numpy.array(centroid.coordinates().getInfo())[0])
)
Map = geemap.Map(center=point, zoom=8)
Map.addLayer(MoTa.style(**{'color': 'ff0000', 'fillColor': '00000000'}), {}, 'MoTa')
Map.addLayer(Eumer.style(**{'color': 'BFD641', 'fillColor': '00000000'}), {}, 'Eumer');Map

# https://developers.google.com/earth-engine/datasets/catalog/LANDSAT_LT05_C02_T1_L2
def apply_scale_factors(image):
  optical_bands = image.select('SR_B.').multiply(0.0000275).add(-0.2)
  thermal_bands = image.select('ST_B6').multiply(0.00341802).add(149.0)
  return image.addBands(optical_bands, None, True).addBands(thermal_bands, None, True)

# https://developers.google.com/earth-engine/landsat_c1_to_c2
def Mask(image):
    qaMask = image.select('QA_PIXEL').bitwiseAnd(int('11111', 2)).eq(0)
    return image.updateMask(qaMask)

Vis = {
  "bands": ['SR_B3', 'SR_B2', 'SR_B1'],
  "min": 0.0,
  "max": 0.2,
}

dataset = (
    ee.ImageCollection("LANDSAT/LT05/C02/T1_L2")
    .filterDate('1987-06-01', '1987-09-01')
    .filterBounds(MoTa)
    .filter(ee.Filter.inList('system:index', 
                             ["LT05_121023_19870624", 
                              "LT05_122023_19870615", 
                              "LT05_123023_19870606"])) # 根据特定字段名称的列表筛选
    # .filter(ee.Filter.lte('CLOUD_COVER', 10)) # 根据云量筛选小于该云量的影像
    .sort('CLOUD_COVER')
    .map(apply_scale_factors)
    # .map(Mask) # 云遮罩
)
dataset

Map.addLayer(dataset, Vis, "dataset") # 显示集合
Map.addLayer(ee.Image(dataset.toList(dataset.size()).get(0)), Vis, "dataOnly");Map # 显示列表中第一幅

# 计算NBR测试
def addNBR(image):
    nbr = image.normalizedDifference(['SR_B4', 'SR_B5']).rename('NBR')
    return image.addBands(nbr)

VisNBR = {
  "min": -1.0,
  "max": 1.0,
  "palette": ['0000ff','00ffff','ffff00','ff0000','ffffff'],
}

Map.addLayer(addNBR(ee.Image(dataset.toList(dataset.size()).get(2))).select("NBR"), VisNBR, "data2") # 显示列表中第一幅
Map.addLayer(addNBR(ee.Image(dataset.toList(dataset.size()).get(1))).select("NBR"), VisNBR, "data1")
Map.addLayer(addNBR(ee.Image(dataset.toList(dataset.size()).get(0))).select("NBR"), VisNBR, "data0");Map # 显示列表中第一幅

# https://www.gpxygpfx.com/article/2023/1000-0593-43-11-3483.html
# https://bqt2000204051.users.earthengine.app/javascript/landsat-5-modules.json
# https://github.com/xingguangYan/Landsat-5-NDWI-image-restoration
# 参考影像区域，向内缓冲区，减少边界的影响
data_ref = ee.Image(dataset.toList(dataset.size()).get(0)).geometry().buffer(-1000)
Map.addLayer(data_ref, {}, "data_ref");Map

data_roi1 = (
    (ee.Image(dataset.toList(dataset.size()).get(1)).geometry())
             .difference((ee.Image(dataset.toList(dataset.size()).get(1)).geometry())
                         .intersection(ee.Image(dataset.toList(dataset.size()).get(0)).geometry()))
    .buffer(1000)
)
data_roi2 = (
    (ee.Image(dataset.toList(dataset.size()).get(2)).geometry())
             .difference((ee.Image(dataset.toList(dataset.size()).get(2)).geometry())
                         .intersection(ee.Image(dataset.toList(dataset.size()).get(0)).geometry()))
    .buffer(1000)
)
# 待修复区域1,2
Map.addLayer(data_roi1, {}, "data_roi1")
Map.addLayer(data_roi2, {}, "data_roi2");Map

# "blue", "green", "red", "nir", "swir1", "swir2", "nir"
reference = (
    addNBR(ee.Image(dataset.toList(dataset.size()).get(0)))
    .select(["SR_B1", "SR_B2", "SR_B3", "SR_B4", "SR_B5", "SR_B7", "NBR"])
    .clip(data_ref).clip(MoTa)
)
target1 = (
    addNBR(ee.Image(dataset.toList(dataset.size()).get(1)))
    .select(["SR_B1", "SR_B2", "SR_B3", "SR_B4", "SR_B5", "SR_B7", "NBR"])
    .clip(data_roi1).clip(MoTa)
)
target2 = (
    addNBR(ee.Image(dataset.toList(dataset.size()).get(2)))
    .select(["SR_B1", "SR_B2", "SR_B3", "SR_B4", "SR_B5", "SR_B7", "NBR"])
    .clip(data_roi2).clip(MoTa)
)

Map.addLayer(reference, Vis, "Testref")
Map.addLayer(target1, Vis, "Testtar1")
Map.addLayer(target2, Vis, "Testtar2"); Map

hisref = geemap.image_histogram(
    reference.select("NBR").multiply(100).toInt(), 
    reference.geometry(), scale = 30, return_df = False
)
histar1 = geemap.image_histogram(
    target1.select("NBR").multiply(100).toInt(), 
    target1.geometry(), scale = 30, return_df = False
)
histar1

# isinstance(reference, ee.Image) # 判断是否为ee.Image变量
def getHistData(image, band):
    # image = reference; band = "NBR"
    histogram = image.reduceRegion(
        reducer = ee.Reducer.histogram(maxBuckets = 2 ** 9), 
        geometry = image.geometry(), 
        scale = 100, 
        maxPixels = 1e13)
    dnList = ee.List(ee.Dictionary(histogram.get(band)).get("bucketMeans"))
    countsList = ee.List(ee.Dictionary(histogram.get(band)).get("histogram"))
    cumulativeCountsArray = ee.Array(countsList).accum(axis = 0)
    totalCount = cumulativeCountsArray.get([-1])
    cumulativeProbabilities = cumulativeCountsArray.divide(totalCount)
    array = ee.Array.cat(arrays = [dnList, cumulativeProbabilities], axis = 1)
    def list(list):
        return ee.Feature(None, {"dn":ee.List(list).get(0), "probability":ee.List(list).get(1)})
    fc = ee.FeatureCollection(array.toList().map(list))
    return fc

def equalize(referenceImage, targetImage, band):
    # referenceImage = reference; targetImage = target1; band = "NBR"
    referenceHistData = getHistData(referenceImage, band)
    targetHistData = getHistData(targetImage, band)
    probToDn = (
        ee.Classifier.smileRandomForest(100)
        .setOutputMode("REGRESSION")
        .train(features = referenceHistData, 
               classProperty = "dn", 
               inputProperties = ["probability"])
    )
    dnToProb = (
        ee.Classifier.smileRandomForest(100)
        .setOutputMode("REGRESSION")
        .train(features = targetHistData, 
               classProperty = "probability", 
               inputProperties = ["dn"])
    )
    targetImageProb = targetImage.select(band).rename('dn').classify(dnToProb, "probability")
    targetImageDn = targetImageProb.classify(probToDn, band)
    return targetImageDn

bandNames = ["SR_B1", "SR_B2", "SR_B3", "SR_B4", "SR_B5", "SR_B7", "NBR"]
def match(referenceImage, targetImage, bandNames):
    def banddef(band):
        return equalize(referenceImage, targetImage, band)
    matchedBands = [banddef(x) for x in bandNames] # 对js中map函数的改写
    return ee.Image.cat(matchedBands)

matched = match(reference, target2, bandNames); matched
matchedNBR = matched.select("NBR").toDouble(); matchedNBR
Map.addLayer(matchedNBR, VisNBR, "data2_hist");Map # 显示列表中第一幅
```

