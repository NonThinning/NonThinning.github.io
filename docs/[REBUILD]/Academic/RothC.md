
[Rothamsted Carbon Model (RothC): Understanding Soil Carbon Dynamics](https://www.rothamsted.ac.uk/rothamsted-carbon-model-rothc)

- [Rothamsted-Models/RothC_Py: RothC code in Python language](https://github.com/Rothamsted-Models/RothC_Py)

# INFO

- 模型适用于耕地、草地、林地的表层土壤有机碳周转；在底土、冻土带、北方森林土壤谨慎使用；排水不良土壤完全不适用。

## 运行模型的数据要求

1. 月降雨量(mm)
2. 月蒸发量(mm)：使用开放式蒸发皿测量，用于计算表层土壤水分亏缺(TSMD)，使用其他数据时需转换为等效的开放式蒸发皿数据
3. 月平均温度(°C)：使用空气温度，因月气温足以代表表层土壤(0-20cm)月平均土壤温度
4. 土壤粘土含量(%)：计算表土可容纳的植物可用水，影响有机物的分解方式
5. 输入植物材料可分解性的估计(DPM/RPM)：DPM易分解植物材料、RPM抗性植物材料
6. 土壤覆盖：特定月份的土壤裸露还是植被覆盖；休耕土壤的分解速度快于耕作土壤
7. 植物残体月输入量($t\ C\ ha^{-1}$)：每月放入土壤的碳量，包含作物生长过程中根系释放的碳；因此输入通常未知，从已知的土壤、站点和天气数据中逆向生成输入
8. ~~农场肥料(FYM, $t\ C\ ha^{-1}$)：可选参数，与植物残体处理方式存在差异~~
9. 取样土层深度

## 模型结构和参数

- DPM：易分解(Decomposable)植物材料
- RPM：抗性(Resistant)植物材料
- BIO：微生物生物量
- HUM：腐殖化(Humified)有机物
- IOM：惰性(Inert)有机物

- DPM/RPM：农作物和改良草地1.44；未改良的草原、稀树草原和灌丛0.67；落叶、热带林地0.25；所有植物材料仅通过这两部分一次
- DPM和RPM分解形成CO2、BIO、HUM；CO2/(BIO+HUM)由土壤的粘土含量决定；BIO和HUM进一步分解为更多CO2、BIO、HUM
- 如果活性隔室含有$Y\ (t\ C\ ha^{-1})$，月底降至$Y\ e^{-abckt}\ (t\ C\ ha^{-1})$；其中a为温度的速率修正系数、b为湿度的速率修正因素、c是土壤覆盖率修正系数、k为该隔室的分解速率常数、t为1/12，用于转换年分解速率k；特定月份分解的隔室材料量为$Y(1-e^{-abckt})\ (t\ C\ ha^{-1})$
- 每个隔室的分解速率常数k：DPM 10；RPM 0.3；BIO 0.66；HUM 0.02；数值根据Roth长期田间试验调整

## 代码(Python)

```shell
conda create -n RothC python=3.9.7 pandas numpy -c conda-forge -y
conda install jupyterlab jupyterlab-lsp python-lsp-server jupyterlab-language-pack-zh-CN -c conda-forge -y
```

```python
import pandas as pd
import numpy as np
```

```python
def RMF_Tmp (TEMP):
         
    if(TEMP<-5.0):
        RM_TMP=0.0
    else:
        RM_TMP=47.91/(np.exp(106.06/(TEMP+18.27))+1.0)
   
    return RM_TMP
```
- 温度的速度修正系数a，其中`TEMP`为月平均气温，月平均气温在-5以下时温度的速度修正系数为0

```python
def RMF_Moist (RAIN, PEVAP, clay, depth, PC, SWC):
        
    RMFMax = 1.0
    RMFMin = 0.2

    SMDMax=-(20+1.3*clay-0.01*(clay*clay))  # 此公式应用于0-23cm表土土层
    SMDMaxAdj = SMDMax * depth / 23.0       # 扩展到其他厚度的表土土层
    SMD1bar = 0.444 * SMDMaxAdj
    SMDBare = 0.556 * SMDMaxAdj             # 相当于TSMD / 1.8, 以减少裸露土壤的蒸发值; 裸露土壤蒸发BareSMD
      
    DF = RAIN - 0.75 * PEVAP                # RAIN降雨量, PEVAP月蒸发量，开放式蒸发皿蒸发量*0.75=潜在蒸发量

    
    minSWCDF=np.min (np.array([0.0, SWC[0]+DF]))
    minSMDBareSWC=np.min (np.array([SMDBare, SWC[0]]))
      
    if(PC==1):                              # PC 植被覆盖 无覆盖为0 农作物覆盖为1
        SWC[0] = np.max(np.array([SMDMaxAdj, minSWCDF]))        # SWC (mm per soil depth) 土壤水分亏缺
    else:
        SWC[0] = np.max(np.array([minSMDBareSWC, minSWCDF]))    # ?
       
      
    if(SWC[0]>SMD1bar):                     # 累计表层土壤水分亏缺 > 0.444 * SMDMaxAdj
        RM_Moist = 1.0
    else:
        RM_Moist = (RMFMin + (RMFMax - RMFMin) * (SMDMaxAdj - SWC[0]) / (SMDMaxAdj - SMD1bar) )   
    
    return RM_Moist
```
- 湿度，表层土壤水分亏缺(TSMD)率修正系数b，应用于积极生长的植被
- 在南半球，天气数据文件应在土壤湿润的7月开始，但在输出时显示1月

```python
def RMF_PC (PC):
     
    if (PC==0):
        RM_PC = 1.0
    else:
        RM_PC = 0.6

    return RM_PC
```