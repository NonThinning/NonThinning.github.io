
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
        SWC[0] = np.max(np.array([minSMDBareSWC, minSWCDF]))
                                            # 总结：根据环境因素调节含水量
      
    if(SWC[0]>SMD1bar):                     # 累计表层土壤水分亏缺 > 0.444 * SMDMaxAdj
        RM_Moist = 1.0
    else:
        RM_Moist = (RMFMin + (RMFMax - RMFMin) * (SMDMaxAdj - SWC[0]) / (SMDMaxAdj - SMD1bar) )   
    
    return RM_Moist
```
- 湿度，表层土壤水分亏缺(TSMD)率修正系数b，应用于积极生长的植被
- 在南半球，天气数据文件应在土壤湿润的7月开始，但在输出时显示1月

```python
# Calculates the plant retainment modifying factor (RMF_PC)
def RMF_PC (PC):        # PC 植被覆盖 无覆盖为0 农作物覆盖为1
     
    if (PC==0):
        RM_PC = 1.0
    else:
        RM_PC = 0.6

    return RM_PC
```
- 存在生长中的植物，土壤覆盖系数 Soil cover factor 会减缓分解

```python
# Calculates the decomposition and radiocarbon 计算分解和放射性碳
def decomp(timeFact, DPM,RPM,BIO,HUM, IOM, SOC, DPM_Rage, RPM_Rage, \
           BIO_Rage, HUM_Rage, Total_Rage, modernC, RateM, clay, C_Inp, FYM_Inp, DPM_RPM):

    zero = 0e-8                     # 使计算精确到小数点后8位
# rate constant are params so don't need to be passed
    DPM_k = 10.0                    # 值根据RothC现场试验的数据设定
    RPM_k = 0.3
    BIO_k = 0.66
    HUM_k = 0.02 
                                    # 每个隔室（碳池）的分解速率常数，以years^{-1}为单位
    conr = np.log(2.0) / 5568.0     # 14C的常规半衰期为5568年

    tstep = 1.0/timeFact    # monthly 1/12, or daily 1/365  
      
    exc = np.exp(-conr*tstep) 
      
 
# decomposition
    DPM1 = DPM[0] * np.exp(-RateM*DPM_k*tstep)
    RPM1 = RPM[0] * np.exp(-RateM*RPM_k*tstep)      
    BIO1 = BIO[0] * np.exp(-RateM*BIO_k*tstep)      
    HUM1 = HUM[0] * np.exp(-RateM*HUM_k*tstep) 

      
    DPM_d = DPM[0] - DPM1
    RPM_d = RPM[0] - RPM1      
    BIO_d = BIO[0] - BIO1
    HUM_d = HUM[0] - HUM1 
      
    
    x=1.67*(1.85+1.60*np.exp(-0.0786*clay)) # 根据土壤粘土含量计算形成的CO2/(BIO+HUM)
                                            # 比例因子1.67根据Roth土壤设置
# proportion C from each pool into CO2, BIO and HUM      
    DPM_co2 = DPM_d * (x / (x+1))
    DPM_BIO = DPM_d * (0.46 / (x+1))
    DPM_HUM = DPM_d * (0.54 / (x+1))
      
    RPM_co2 = RPM_d * (x / (x+1))
    RPM_BIO = RPM_d * (0.46 / (x+1))
    RPM_HUM = RPM_d * (0.54 / (x+1))    
      
    BIO_co2 = BIO_d * (x / (x+1))
    BIO_BIO = BIO_d* (0.46 / (x+1))
    BIO_HUM = BIO_d * (0.54 / (x+1))
      
    HUM_co2 = HUM_d * (x / (x+1))
    HUM_BIO = HUM_d * (0.46 / (x+1))
    HUM_HUM = HUM_d * (0.54 / (x+1))  
           
      
# update C pools  
    DPM[0] = DPM1
    RPM[0] = RPM1
    BIO[0] = BIO1 + DPM_BIO + RPM_BIO + BIO_BIO + HUM_BIO
    HUM[0] = HUM1 + DPM_HUM + RPM_HUM + BIO_HUM + HUM_HUM    
      
# split plant C to DPM and RPM 
    PI_C_DPM = DPM_RPM / (DPM_RPM + 1.0) * C_Inp
    PI_C_RPM =     1.0 / (DPM_RPM + 1.0) * C_Inp

# split FYM C to DPM, RPM and HUM 
    FYM_C_DPM = 0.49*FYM_Inp
    FYM_C_RPM = 0.49*FYM_Inp      
    FYM_C_HUM = 0.02*FYM_Inp   
      
# add Plant C and FYM_C to DPM, RPM and HUM   
    DPM[0] = DPM[0] + PI_C_DPM + FYM_C_DPM
    RPM[0] = RPM[0] + PI_C_RPM + FYM_C_RPM  
    HUM[0] = HUM[0] + FYM_C_HUM
      
# calc new ract of each pool      
    DPM_Ract = DPM1 *np.exp(-conr*DPM_Rage[0])
    RPM_Ract = RPM1 *np.exp(-conr*RPM_Rage[0]) 
      
    BIO_Ract = BIO1 *np.exp(-conr*BIO_Rage[0])
    DPM_BIO_Ract = DPM_BIO * np.exp(-conr*DPM_Rage[0])
    RPM_BIO_Ract = RPM_BIO * np.exp(-conr*RPM_Rage[0])
    BIO_BIO_Ract = BIO_BIO * np.exp(-conr*BIO_Rage[0])
    HUM_BIO_Ract = HUM_BIO * np.exp(-conr*HUM_Rage[0])
      
    HUM_Ract = HUM1 *np.exp(-conr*HUM_Rage[0])   
    DPM_HUM_Ract = DPM_HUM * np.exp(-conr*DPM_Rage[0])
    RPM_HUM_Ract = RPM_HUM * np.exp(-conr*RPM_Rage[0])
    BIO_HUM_Ract = BIO_HUM * np.exp(-conr*BIO_Rage[0])
    HUM_HUM_Ract = HUM_HUM * np.exp(-conr*HUM_Rage[0])
      
    IOM_Ract = IOM[0] *np.exp(-conr*IOM_Rage[0]) 
      
# assign new C from plant and FYM the correct age   
    PI_DPM_Ract = modernC * PI_C_DPM
    PI_RPM_Ract = modernC * PI_C_RPM
      
    FYM_DPM_Ract = modernC * FYM_C_DPM
    FYM_RPM_Ract = modernC * FYM_C_RPM
    FYM_HUM_Ract = modernC * FYM_C_HUM          
      
# update ract for each pool        
    DPM_Ract_new = FYM_DPM_Ract + PI_DPM_Ract + DPM_Ract*exc
    RPM_Ract_new = FYM_RPM_Ract + PI_RPM_Ract + RPM_Ract*exc    
    
    BIO_Ract_new = (BIO_Ract + DPM_BIO_Ract + RPM_BIO_Ract + 
                    BIO_BIO_Ract + HUM_BIO_Ract )*exc
      
    HUM_Ract_new = FYM_HUM_Ract + (HUM_Ract + DPM_HUM_Ract + 
                                   RPM_HUM_Ract + BIO_HUM_Ract + HUM_HUM_Ract )*exc  
      
      
    SOC[0] = DPM[0] + RPM[0] + BIO[0] + HUM[0] + IOM[0]     
      
    Total_Ract = DPM_Ract_new + RPM_Ract_new + BIO_Ract_new + HUM_Ract_new + IOM_Ract
      

# calculate rage of each pool.      
    if(DPM[0]<=zero): 
        DPM_Rage[0] = zero
    else:
        DPM_Rage[0] = ( np.log(DPM[0]/DPM_Ract_new) ) / conr

    
    if(RPM[0]<=zero):
        RPM_Rage[0] = zero
    else:
        RPM_Rage[0] = (np.log(RPM/RPM_Ract_new) ) / conr 
    
    if(BIO[0]<=zero):
        BIO_Rage[0] = zero
    else:
        BIO_Rage[0] = ( np.log(BIO/BIO_Ract_new) ) / conr
    
    
    if(HUM[0]<=zero):
        HUM_Rage[0] = zero
    else:
        HUM_Rage[0] = ( np.log(HUM/HUM_Ract_new) ) / conr
    
    
    if(SOC[0]<=zero):
        Total_Rage[0] = zero
    else:
        Total_Rage[0] = ( np.log(SOC[0]/Total_Ract) ) / conr    
    
    return
```