
## 使用土钻采样时估算土壤容重$\ g/cm^{3}$

```python
# 计算土钻取样容积
import math
# 已知：土钻内径=5cm；豁口弦长=3cm；土柱长度=5cm
diameter = 5; chordLength = 3; length = 5
OD = math.sqrt(math.pow((diameter / 2), 2) - math.pow((chordLength / 2), 2))
AOB = 2 * math.asin((chordLength / 2) / (diameter / 2)) # AOB夹角的弧度
sectorArea = AOB / (2 * math.pi) * math.pi * math.pow((diameter / 2), 2)
triangleArea = (1 / 2) * math.pow((diameter / 2), 2) * math.sin(AOB)
archArea = math.pi * math.pow((diameter / 2), 2) - (sectorArea - triangleArea)
soilColumnVolume = archArea * length
print("archArea: ", f"{archArea:.4f}")
print("soilColumnVolume: ", f"{soilColumnVolume:.4f}")
# archArea:  18.6131
# soilColumnVolume:  93.0654
```

以下公式根据`NY/T 1121.3—2006`、`NY/T 1121.4—2006`、`LY/T 1215—1999`修改
- 土壤自然含水量不适用于有机土(SOM > 200g/kg)的土壤
- $SWC,g/kg=\frac{m_{1}-m_{2}}{m_{2}-m_{0}} \times 1000$，其中1000为单位转换系数，如不使用则单位为$g/g$，如使用100则单位为$\%$；$m_{0}$为烘干空铝盒重，$m_{1}$为烘干前铝盒试样总重，$m_{2}$为烘干后铝盒试样总重，单位均为$g$；此公式对应标准中“水分（干基）”
- 不考虑砾石影响的容重：$BD,g/cm^{3}=\frac{(m_{3}-m_{4}) / (\frac{m_{1}-m_{2}}{m_{2}-m_{0}}+1)}{V}$，即将环刀中湿土的质量转换为对应的烘干土质量，再除以环刀体积，此处环刀体积使用土钻样品体积`soilColumnVolume`取代；$m_{3}$为环刀湿土总重，$m_{4}$为环刀质量，单位均为$g$，实际使用时环刀质量用样品保存容器（例如封口袋）质量代替
- 考虑砾石影响的容重：$BD,g/cm^{3}=\frac{(m_{3}-m_{4}-m_{5}) / (\frac{m_{1}-m_{2}}{m_{2}-m_{0}}+1)}{V-V_{5}}$，其中$m_{5}$为砾石质量，$V_{5}$为砾石体积

- 砾石含量通常指砾石体积含量，如使用以上方法取样：$V_{5}/soilColumnVolume$

## 土壤有机碳测定值的处理

以下公式根据`HJ 695-2014`、`HJ 613-2011`修改
- 因上机测定时使用质量为风干土壤质量，故在原数值$TC,g/kg$基础上转换：$TC_{re},g/kg=TC/(\frac{m_{2}-m_{0}}{m_{1}-m_{0}})$，$m_{0}$为容器质量，$m_{1}$为带盖容器及风干土壤总重，$m_{2}$为带盖容器及烘干土壤总重
- 测量值过低可能的原因是仪器$\%$和$g/kg$单位转换过程中的错误，需乘10倍转换

- 根据土壤有机碳密度的计算公式，按照0-5cm，5-15cm取样计算的土壤有机碳密度无法在土层间比较

## 平行测定样品平均数处理原则，使用Excel `AVERAGE`函数

1. 完整的测量为至少$a,b,c$三个测量
2. 除测量$a$外，存在二个平行样品：$avg = (a+b+c)/3$
3. 除测量$a$外，存在一个平行样品：$avg = (a+b)/2$
4. 除测量$a$外，没有平行样品：$avg = a$
5. 缺少测量，如无法补充测量则空置

