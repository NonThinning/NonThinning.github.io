---
data: 2024-04-27
---

```r
#### 参考链接 ####
# 主要参考
# https://www.jianshu.com/p/19935c44cbf7
# 补充
# https://github.com/psychbruce/drawMap
# https://malagis.com/gis-tutorial-how-to-download-checked-map.html
# https://xiangyun.rbind.io/2022/02/draw-china-maps/
# https://www.xzywisdili.com/blog/%E6%88%91%E5%9C%A8-r-%E9%87%8C%E7%94%BB%E5%9C%B0%E5%9B%BE%E4%B8%80/
# https://ytluck.github.io/data-mining/my-dataming-post-20.html

#### 民政部数据 ####
# 审图号：GS（2022）1873号

# https://mp.weixin.qq.com/s/qj1SRc6D8sgYJYaZzDux6Q
library(sf)
library(ggplot2)
# API前缀
API_pre <- "http://xzqh.mca.gov.cn/data/"
# 精确到县级
xian_quanguo <- sf::st_read(dsn = paste0(API_pre, "xian_quanguo.json"), 
                            stringsAsFactors=FALSE)

ggplot(xian_quanguo) + 
  geom_sf(aes(fill = QUHUADAIMA), show.legend = FALSE) + 
  coord_sf() + 
  scale_fill_manual(values = xian_quanguo$FillColor, 
                    labels = xian_quanguo$QUHUADAIMA)

# 精确到省级
China = st_read(dsn = paste0(API_pre, "quanguo.json"), 
                stringsAsFactors=FALSE) 
st_crs(China) = 4326

ggplot(China)+
  geom_sf()+
  labs(title="Ministry of Civil of PRC",x="Lon",y="Lat")

# 包含九段线，全国轮廓
China_Line = st_read(dsn = paste0(API_pre, "quanguo_Line.geojson"), 
                stringsAsFactors=FALSE) 
st_crs(China_Line) = 4326

ggplot(China_Line)+
  geom_sf()+
  labs(title="Ministry of Civil of PRC",x="Lon",y="Lat")

# 保存文件
library(geojsonsf)
geo_map = sf_geojson(China_Line,atomise = T)
write(geo_map,"China_Line.json")
geo_map = sf_geojson(China,atomise = T)
write(geo_map,"China.json")
geo_map = sf_geojson(xian_quanguo,atomise = T)
write(geo_map,"xian_quanguo.json")

#### 简数科技 ####
# https://data.jianshukeji.com/
# https://geojson.cn/

#### 阿里 ####
# https://l7.antv.antgroup.com/
# https://l7.antv.antgroup.com/custom/tools/map
# https://github.com/ruiduobao/shengshixian.com
# 实际来源 民政部数据

#### 其他1 ####
# https://rdrr.io/github/psychbruce/drawMap/man/drawChinaMap.html
# https://github.com/psychbruce/drawMap
install.packages("devtools")
devtools::install_github("psychbruce/drawMap")
library(drawMap)
drawChinaMap()

```

```r
# 天地图 2024年数据 审图号：GS（2024）0650号
# https://cloudcenter.tianditu.gov.cn/administrativeDivision
```