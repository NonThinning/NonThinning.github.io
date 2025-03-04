
陈泮勤 地球系统碳循环 读书摘要

约定：`>`标识摘录，`-`标识要点，`!!!`标识基于原文的拓展联想

!!! 
    研究地球系统的最终目标是管理和重构（地球与类地行星系统）的物质循环、能量流动，以符合人类活动的基本需要；`Spacewar & System Administration`

P7
- 地球系统：物理气候系统、生物地球化学
- 生物地球化学：碳、氮等元素在地球子系统中进行物质转换，及对生物（圈）的影响；包括陆地生态系统等

P8
- 物理气候系统：温度、降水
- 生物地球化学：CO2、NOx

P11
- 气候决定生物群落，通过气候参数模拟陆表潜在植被分布，根据植被平均碳密度估计
- Holdridge life zones：[A new approach to ecological zoning of the Earth in a changing climate](https://doi.org/10.1038/s41893-024-01419-2)
- BIOME：[jedokaplan/BIOME4](https://github.com/jedokaplan/BIOME4)
- MAPSS：[MAPSS Model Desciption](https://www2.cgd.ucar.edu/vemap/abstracts/MAPSS.html) | [MAPSS](https://daac.ornl.gov/MODELS/guides/MAPSS_guide.html) | *Map
- **Extra**
- [bpbond/Biome-BGC](https://github.com/bpbond/Biome-BGC) | [Biome-BGCMuSo](https://nimbus.elte.hu/bbgc/index.html)
- [Biome: evolution of a crucial ecological and biogeographical concept](https://nph.onlinelibrary.wiley.com/doi/10.1111/nph.15609)
- [World Maps of Köppen-Geiger climate classification](http://koeppen-geiger.vu-wien.ac.at/koeppen.htm)

P12
- 影响土壤碳库的因素：土壤物理性质（粘粒、酸度、空隙）、进入土壤的植物残体（植被类型）、气候条件（影响植物残体的分解速率）

P19
- 植物光合作用，总初级生产力GPP
- 植物呼吸消耗部分有机物，释放CO2，剩余部分为净初级生产力NPP
- 陆地植被生物量碳库，异养呼吸释放CO2，剩余生物量、凋落物和土壤的碳积累为生态系统净生产力NEP
- 人类与自然干扰（火灾、采伐）导致碳排放，剩余碳为生物群区净生产力NBP

P24
- 森林对碳的吸收主要由于森林年龄结构变化

P37
- 森林forest
- 造林afforestration：至少50年没有森林的土地上进行植树
- 再造林reforestation：1990年以来没有森林的土地上进行植树
- 伐林deforestation

P61
- 大气CH4的自然来源：热带湿地、草地、温带至北方森林

P77
- 土地利用：土地由自然生态系统转换为人工生态系统（社会经济属性）
- 土地覆被：自然和人工地表覆盖（自然属性）
- 土地覆被：转变（conversion）和渐变（modification）

P78
- 农田向自然草地、森林、湿地的转化有助于增加碳储量

P80
- 土壤碳库以土壤呼吸的形式释放碳：生物学过程（植物根呼吸、土壤微生物呼吸、土壤动物呼吸）、含碳物质的化学氧化过程
- 森林生态系统碳库：植被、凋落物、土壤

!!!
    植被遥感

P82
- 生物地球化学循环：气相型（温室效应导致的气候变暖等过程的中间环节）、沉积型
- 生物地球化学模型：[DNDC](https://www.dndc.sr.unh.edu/)、[Century](https://www.nrel.colostate.edu/projects/century/)、[Terrestrial Ecosystem Model](https://github.com/MBL-TEM/TEM6.0.6) | [MBL Terrestrial Ecosystem Model](https://www.mbl.edu/research/research-centers/ecosystems-center/ecosystem-modeling/terrestrial-ecosystem-model-tem)
- 陆地生态系统碳循环模型：遥感驱动的陆地碳循环模型、生物地球化学模型、全球植被动态模型

P130
- 森林冠层和与大气CO2交换量依赖于微气象法
- 微气象法可代表较大的空间范围，静态箱法可提供植物生长温室气体排放的详细情况，并提供建立模式和验证模式必须的观测数据
- 静态箱-气相色谱法：气温、地表温度、土壤温度

P147
- 陆地生态系统碳循环模型应用遥感数据作为模型参数或驱动变量：CENTURY、[bpbond/Biome-BGC](https://github.com/bpbond/Biome-BGC)、TEM、MAPSS、[CASA](https://github.com/TreeYu123/PyCASA)、[BEPS](https://github.com/JChen-UToronto/BEPS_hourly_site)、[InTEC](http://faculty.geog.utoronto.ca/Chen/Chen's%20homepage/res_intec.htm)
- 植被指数、叶面积指数、光合有效辐射分量

P164
- 遥感用于提供植被分类和LAI变量
- 生物地球化学模型：[AVIM](http://www.tea.ac.cn/kxyj/msfz/lmmsavim/201405/t20140526_236214.html)、[Biome-BGC](https://www.umt.edu/numerical-terradynamic-simulation-group/project/biome-bgc.php)、CENTURY、TEM
- 生物地理过程模型：[BIOME2](https://www2.cgd.ucar.edu/vemap/abstracts/BIOME2.html)、[DOLY](https://www2.cgd.ucar.edu/vemap/abstracts/DOLY.html)、MAPSS

P166
- [SVAT](https://github.com/tjc181/simsphere)模型将卫星观测和通量塔观测的碳通量变量相联系

P168
- 尺度转换：将样地尺度的生态系统参数与遥感获得的较大尺度生态系统参数间建立关系

P169
- 通过输入数据的统一化，对特定值的输出结果进行比较
- 气候变化引起的植被分布和面积的变化可能大于生物地球化学循环变化的影响
- 地面观测的土壤呼吸量是土壤异养呼吸量与植物根呼吸量之和

P171
- 生物地球化学模型：以气候和土壤作为输入因子，模拟生物地球化学循环
- 生物地理过程模型：基于气候和植被的分布预测不同环境条件下植被类型的变化

P186
- 总初级生产力GPP
- 净初级生产力NPP = GPP - 植物自养呼吸RA
- 净生态系统生产力NEP = NPP - 异养呼吸RH
- 净生物群落生产力NBP = NEP - 人为活动或自然灾害碳损失Ld

P205
- 2/3存储于土壤有机质（包括相应的泥炭沉积层）中

P210






