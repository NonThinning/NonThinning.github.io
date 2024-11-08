---
date: 2024-07-02
---

[《结构方程模型》低价购书_王济川 著_教材教辅考试_孔网](https://item.kongfz.com/book/30678327.html) | [结构方程模型 (豆瓣)](https://book.douban.com/subject/6432843/)

###### 24/07/02

[Composite Variables](https://jslefche.github.io/sem_book/) 学习记录

2 全局估计

2.1 方差`variance`和协方差`covariance`

方差：在一组数据中的扩展程度；捕捉每个点与所有点平均值的偏差；对于变量`variance`x和响应`response`y;方差越大，数据在平均值附近的分布越广

协方差：衡量两个变量`variance`之间相关性的指标，如果x的变化倾向于跟随y的变化，则两个变量被认为是共同变化的 `cov(x, y)`

方差和协方差取决于单位的大小，如果x的单位远大于y，则协方差将很大；变量间单位差异较大将使变量集之间（协）方差的解释和比较产生误导，通过将变量标准化为平均值0、方差为1的Z变换实现`Z-transformation`

在协方差计算中，用标准化的值替换x和y的值，得到皮尔逊乘积矩相关性`Pearson product moment correlation`r，相关性以平均值的标准差为单位，无论原始变量的大小都可以进行公平的比较 `cor(x, y)`；与x和y的协方差除以标准偏差的乘积相同

2.2 回归系数`Regression Coefficients`

SEM建模的推理核心是回归（路径）系数；回归系数量化了一个变量对另一个变量的依赖性（多为线性）；如何从相关系数中导出路径系数`path coefficients`；

回归（路径）系数`regression (path) coefficient`和相关系数`correlation coefficient`之间的重要区别：

简单线性回归，响应变量y，预测`predictor`变量（因子）x，两个变量之间的关联用于生成预测`predictor`(响应变量的估计值)$\hat y = bx + a$；其中b是回归系数，a是截距，此时的b意味着线性关系 

x、y之间的回归系数可通过方程关系与相关系数`correlation coefficient`相关，如果变量进行Z变换，则回归系数=相关系数

关键点：当变量Z变换后，回归系数=相关系数；对于多元回归（x1，x2不止一个预测因子），值为偏相关系数`partial correlation coefficients`；比例关系`scaled to mean = 0 and variance = 1`称为标准化系数`standardized coefficients`

未标准化的系数存在原始的度量单位，但可通过方程与方差相关；

方差、协方差、相关性的概念为非标准化和标准化回归系数的计算提供信息

路径系数`path coefficients`的8条规则

2.2.1 规则1：外生变量之间未指明的关系只是它们的双变量相关性

外生变量`exogenous variables`：只有路径（没有箭头进入）的变量，两个外生变量之间不存在有向路径，它们之间的关系可以用简单相关性来表示，但并非总是用双箭头表示；箭头指向的变量称为内生变量`endogenous variable`，内生变量也可以有指向它的箭头，但必须被预测而不仅仅是预测因子

`x1 <-> == cor(x1, x2)`

2.2.2 规则2：当两个变量通过一条路径连接时，该路径的系数就是回归系数

`x1 -> y1 -> y2`, 构建一个简单的路径图，在这种情况下，`x1 -> y1`的路径系数是回归系数$γ_{y1,x1}$,`y1 -> y2`的路径系数是回归系数$β_{y2,y1}$，如果数据是标准化的，回归系数=两者间相关性；γ表示的外生和内生联系之间的区别，β表示的两个内生变量之间的关系

2.2.3 规则3：复合路径`compound path`（包括多个链路`multiple links`的路径）的强度是个体系数的乘积

SEM的优势是能量化间接或级联联系，通过简单相乘实现；x1对y2的影响是路径x1−>y1和y1−>y2的系数的乘积，但不等于x1和y2之间的相关性，意味着x1和y2之间的关系不能完全用通过y1的间接路径来解释，需要额外的信息解决，以x1−>y2之间缺失的链接的形式出现

y1和y2之间的关系现在有两个来源，一是它们的直接联系，二是x1通过y1对y2的间接影响；需要计算每个变量对其他变量的独立影响，以“偏”回归系数的形式出现

2.2.4 规则4：当变量由多个途径连接时，每个途径都是“偏”回归系数

偏回归系数说明了多个变量对响应变量的联合影响，一个预测器`predictor`的系数控制模型中其他预测器的影响；此时y2收到两个变量x1、y1的影响；需要去除x1和y1之间的共同方差，以导出它们与y2的关联

计算x1的部分效应：结果是x1对y2的部分影响；偏回归系数实现了统计控制（而不是实验控制），x1的部分效应解释了y1的统计贡献，因此部分效应`partial effects`应在难以或不可能应用实验控制的情况下有用。

在多个预测因子的情况下，回归过程产生偏系数；在去除了y1对y2的影响后，计算x1对y2的影响

提出了残差，第二个方程在y2中仍具有与x1或y1中的变化无关的方差，该模型不能完全预测y2，残差（无法解释的）方差`residual (unexplained) variance`概念与第五条规则相关。

2.2.5 规则5：内生变量的误差与未测量变量产生的无法解释的相关性或方差有关

$R^{2}$统计量，y2中解释的变异与总变异的比率，无法解释的（或残差）方差为1-$R^{2}$，该值包含了导致y2和其他变量之间的相关性偏离1的其他未知源；如果x1是控制y2的唯一变量，它们的相关性将为1，它们的预测误差将为0，因为已经考虑了影响y2的所有因素

在路径图`path diagram`中，误差方差表示为$ζ$，箭头指向内生变量，代表$ζ$效应的路径系数通常表示为误差相关性，与其他（标准化）系数的表示一致

2.2.6 规则6：两个内生变量之间的未分析（残差）相关性是它们的偏相关性

假设移除`y1->y2`路径，变为`y1<- x1 ->y2`，这两个变量均为内生，它们的关系可量化但需要消除x1对两个变量的影响

条件独立性的概念在局部估计的实现中至关重要

推导出了与直接、间接、和误差方差或相关性的所有量，我们就有了计算总效应所需的所有信息

2.2.7 规则7：一个变量对另一个变量的总影响是其直接和间接影响的总和

x1对y2的总影响包括由y1介导的直接影响和间接影响

2.2.8 规则8：总效应（包括无向路径`undirected paths`）等于总相关性

要点：标准化系数反映（部分）相关性；一个变量对另一个变量的间接影响是通过乘以各个路径系数的总和；二元相关性是总效应加上任何无向路径的总和

对协方差cov和相关性cor的理解对于理解SEM的全局估计方法至关重要

2.3 基于方差的结构方程建模

SEM的经典方法是基于方差和协方差的思想；对于>2个的变量，可以构造一个方差-协方差矩阵，其中对角线是每个变量的方差、离对角线是每对之间的协方差

三个变量x1、y1、y2的方差-协方差矩阵，称之为观测到的全局方差协方差矩阵`observed global variance-covariance matrix`

基于协方差的SEM机制是再现全局方差-协方差矩阵，`Σ=Σ(Φ)`其中∑是观测方差-协方差矩阵，∑（Φ）是用Φ表示的模型估计协方差矩阵，Φ是模型估计参数（即系数）的矩阵

这个方程表明，观测到的协变量可以用统计参数来理解，统计参数可以用来预测相同的协变量，可认为基于协方差的SEM是一种多元回归方法

问题：我们如何得出∑（Φ），或者更相关地说，我们如何估计导致估计方差-协方差矩阵的模型参数Φ的矩阵？最常见的工具是最大似然估计，它迭代地搜索参数空间并不断细化参数值的估计，从而使观测到的方差-协方差矩阵和期望的方差-方差矩阵之间的差异最小化。最大似然估计量具有一些可取的性质，主要是它们对变量的尺度不变，并基于一些假设提供无偏估计。

样本量的概念很好：随着模型变得越来越复杂，它们需要更多的数据来拟合。模型的“可识别性”和样本量的问题将在下一节中讨论。

2.4 模型识别`Model Identifiability`

拥有足够的能力来检验你的假设是对你的数据做出稳健、无偏见的推断的关键。这一要求与SEM特别相关，SEM通常同时评估多个假设，因此需要比其他方法更多的数据。

如果我们能够唯一地估计模型的每个参数，那么模型就被“识别”了。这不仅包括在参数估计的矩阵中，还包括它们的误差。换句话说，我们至少需要与“未知”信息一样多的“已知”信息才能拟合模型。

我们现在有更多的已知信息，而不是未知信息，因为我们已经基于前两个方程得出了a和b的解。在这种情况下，我们称方程组为过度识别`overidentified`，因为我们拥有的信息超过了为未知变量得出唯一解所需的信息。这是理想的状态，因为这些额外的信息可以用来提供额外的见解

您可能也听说过被称为饱和的模型。这样一种模式将被确定；不饱和模型`unsaturated`将被过度识别`overidentified`，而过饱和模型`oversaturated`将不被充分识别`underidentified`。

t规则

模型识别是确定模型是否能提供唯一解决方案的第一步：样本量会限制模型拟合，无法为$F_{ML}$函数提供足够的复制，从而无法获得路径系数的稳定估计集；经验法则：复制水平`the level of replication`应至少是估计系数数量的5倍，在之前的路径模型中，估计了两种关系，至少需要n = 10 拟合该模型

可识别性`Identifiability`和复制`replication`(<mark>备注：此处应意为重复</mark>)不仅是提供实际解决方法的关键，也是评估模型适用性的额外信息的关键

2.5 适合度度量`Goodness-of-fit Measures`

基于协方差的SEM的目的是再现全局观测方差-协方差矩阵，但假设的关系可能实际上不匹配，需评估模型估计`model-estimated`的方差-协方差矩阵与观测`observed`方差-协方差矩阵的匹配程度

误差方差或相关性评估作为反映测量的变量未捕捉到的外部变化源，高误差方差将导致变量之间关系估计不准确，导致观测和模型隐含的方差-协方差矩阵不一致

χ2统计量；χ2差异检验简单地说就是两个模型之间χ2值的差异，自由度是两个模型间自由度的差异。然后可以将得到的统计数据与χ2表进行比较，得出显著性值。同样，此测试适用于嵌套模型。对于非嵌套模型，其他统计数据允许进行模型比较，包括AIC和BIC。AIC或BIC得分≥2通常被认为表示模型之间的显著差异，较小的值表示两个模型之间的等效性。χ2检验往往受到样本量的影响，较大的样本更可能由于较小的绝对偏差而产生较差的拟合

基于协方差的SEM有几个其他拟合指数试图纠正这个问题：
近似均方根误差（RMSEA）：该统计数据根据样本量对模型进行惩罚。“可接受”值通常小于0.10，“良好”值则小于0.08。
比较拟合指数（CFI）：该统计数据考虑了与“零”模型的偏差。在大多数情况下，null估计所有方差，但将协变量设置为0。大于0.9的值被认为是好的。
标准化均方根残差（SRMR）：观察到的相关性和预测的相关性之间的标准化差异。小于0.08的值被认为是好的。

了解模型的哪些部分未能通过模型隐含方差-协方差矩阵进行再现。这可以通过两种方式实现：
模型残差的检验相关性：残差相关性大（观察到的和预期的差异）的参数可能表明信息缺失或联系。
修正指数，或者如果模型中包含缺失路径，则χ2的预期下降。修改索引的高值将表明应该包括丢失的路径。（我们在局部估计一章中介绍的定向分离测试提供了类似的见解，并通过分段SEM`piecewiseSEM`自动返回。）

SEM是一种在很大程度上依赖于知情模型规范的技术`a technique that relies heavily on informed model specification.`。在中添加数据建议但用户未预期的路径，只是为了实现适当的拟合，这在其他应用中可能是合适的，但忽略了SEM背后的基本原理，即关系基于先验知识和直觉`a priori knowledge and intuition`。

```r
# R 4.3.3 
x <- c(1, 2, 3, 4)
y <- c(2, 3, 4, 5)
# 计算方差
# variance in x 
sum((x - mean(x))^2)/(length(x) - 1) == var(x)
# variance in y
sum((y - mean(y))^2)/(length(y) - 1) == var(y)
# 计算协方差，方差和协方差大小取决于单位
sum((x - mean(x)) * (y - mean(y)))/(length(x) - 1) == cov(x, y)
cov(x, y)
# increase units of x
x1 <- x * 1000
cov(x1, y)
# Z变换，将变量标准化为均值为 0，方差为 1
zx <- (x - mean(x)) / sd(x)
zy <- (y - mean(y)) / sd(y)
# can also be obtained using the function `?scale`
# 计算相关性r
sum(zx * zy)/(length(zx) - 1) == cor(x, y)
# 结果一致，但是输出为[1] FALSE
(cov(x, y) / (sd(x) * sd(y))) == cor(x, y)

set.seed(111)
data <- data.frame(y1 = runif(100))
data$x1 <- data$y1 + runif(100)
unstd.model <- lm(y1 ~ x1, data)
# 非标准化系数
# get unstandardized coefficient
summary(unstd.model)$coefficients[2, 1]
# now using covariance
(cov(data$y1, data$x1) / var(data$x))
# repeat with scaled data
std.model <- lm(y1 ~ x1, as.data.frame(apply(data, 2, scale)))
# get standardized coefficient
summary(std.model)$coefficients[2, 1]
# now using correlation
cor(data$y1, data$x1)
data$y2 <- data$y1 + runif(100)
(pathx1_y1 <- summary(lm(y1 ~ x1, as.data.frame(apply(data, 2, scale))))$coefficients[2, 1])
cor(data$y1, data$x1)
(pathy1_y2 <- summary(lm(y2 ~ y1, as.data.frame(apply(data, 2, scale))))$coefficients[2, 1])
cor(data$y2, data$y1)
pathx1_y1 * pathy1_y2
cor(data$y2, data$x1)
(partialx1 <- (cor(data$x1, data$y2) - (cor(data$x1, data$y1) * cor(data$y1, data$y2))) / (1 - cor(data$x1, data$y1)^2))
((cor(data$x1, data$y2) - (cor(data$x1, data$y1) * cor(data$y1, data$y2))) / (1 - cor(data$x1, data$y1)^2))* (sd(data$y2)/sd(data$x1))
summary(lm(y2 ~ x1 + y1, data))$coefficients[2, 1]
(partialy1 <- (cor(data$y2, data$y1) - (cor(data$y2, data$x1) * cor(data$y1, data$x1))) / (1 - cor(data$x1, data$y1)^2))
summary(lm(y2 ~ x1 + y1, as.data.frame(apply(data, 2, scale))))$coefficients[2:3, 1]
partialx1; partialy1
residsx1 <- residuals(lm(x1 ~ y1, as.data.frame(apply(data, 2, scale))))
summary(lm(scale(data$y2) ~ residsx1))$coefficients[2, 1]
partialx1
1 - summary(lm(y2 ~ y1 + x1, as.data.frame(apply(data, 2, scale))))$r.squared
1 - sqrt(summary(lm(y1 ~ x1, as.data.frame(apply(data, 2, scale))))$r.squared)
1 - cor(data$y1, data$x1)
(errory1y2 <- (cor(data$y1, data$y2) - (cor(data$x1, data$y1) * cor(data$x1, data$y2))) / sqrt((1 - cor(data$x1, data$y1)^2) * (1 - cor(data$x1, data$y2)^2)))
(cor(
  resid(lm(y1 ~ x1, as.data.frame(apply(data, 2, scale)))),
  resid(lm(y2 ~ x1, as.data.frame(apply(data, 2, scale))))
))
errory1y2
cor(data$y1, data$x1) * cor(data$y2, data$x1)
(totalx1 <- partialx1 + cor(data$y1, data$x1) * partialy1)
totalx1 == cor(data$y2, data$x1)
(totaly1y2 <- cor(data$y1, data$x1) * cor(data$y2, data$x1) + errory1y2 * sqrt(1 - summary(lm(y1 ~ x1, data))$r.squared) * sqrt(1 - summary(lm(y2 ~ x1, data))$r.squared))
totaly1y2 == cor(data$y1, data$y2)
cov(data)
```

2.6 使用lavan进行模型拟合

以加利福尼亚州野火干扰对植物多样性影响的研究

```r
# R 4.4.0
library(lavaan)
library(piecewiseSEM)

data(keeley)

# 首先考虑火灾严重程度和林分年龄的关系
# age→firesev 既是线性回归，也是简单的SEM
# lavaan中，公式作为字符串传递

keeley_formula1 <- 'firesev ~ age'
class(keeley_formula1)
keeley_sem1 <- sem(keeley_formula1, data = keeley)
summary(keeley_sem1)

# 输出解读
# 似然优化方法；参数数量（2）；模型总样本量（90）；估计量、拟合统计量
# 自由度为0；关系β=0.06；P<0.001
# 内生变量的估计误差`estimated error variance`

keeley_mod <- lm(firesev ~ age, data = keeley)
summary(keeley_mod)$coefficients

# 得到β=0.05967903；同时得到截距
# 强制lavaan包返回截距
summary(sem(keeley_formula1, keeley, meanstructure = T))
# 简单线性回归的斜率，也得到β=0.05967903
cov(keeley[, c("firesev", "age")])[2, 1]/var(keeley$age)

# 标准化系数等于相关性
cor(keeley$firesev, keeley$age)
coefs(keeley_mod) # piecewiseSEM；计算标准化系数；此处等于二元相关性
standardizedsolution(keeley_sem1) # 使用lavaan返回标准化系数；
# 缺点是不会返回原始系数和解释信息

summary(keeley_sem1, standardize = T) # 通过传参的方式显示
summary(keeley_sem1, standardize = T, rsq = T) # 误差方差为1-`R-Square`;此处为R-Square

# 稍微复杂的SEM `age->firesev->cover`
# 两个方程，放在单独的行上，代表两个内生变量
# 在这里，我们检验了植物总覆盖率是火灾严重程度的函数的假设，
# 而火灾严重程度又取决于植物在特定地块中的年龄（已用线性回归进行研究）
# 。此测试称为完全调解。换句话说，年龄的影响完全由火灾严重程度介导。

keeley_formula2 <- '
firesev ~ age
cover ~ firesev
'
keeley_sem2 <- sem(keeley_formula2, data = keeley)
summary(keeley_sem2, standardize = T, rsq = T)
# 自由度为1
# P 值的大小并不反映拟合度的增加，
# 只是增加了对观测值和模型估计协方差没有差异

fitMeasures(keeley_sem2) # 获取其他拟合统计信息

# 计算间接影响；规则3，沿复合路径的间接效应是各个路径系数的乘积
# Std.all 0.454*(-0.437) = -0.198 indirect
keeley_formula2.1 <- '
firesev ~ B1 * age
cover ~ B2 * firesev

indirect := B1 * B2
'
keeley_sem2.1 <- sem(keeley_formula2.1, keeley)
summary(keeley_sem2.1, standardize = T)
# -0.198 indirect

# age->firesev->cover
# age->cover

# 部分中介，或者年龄的影响部分由火灾严重程度介导
# 年龄和覆盖率之间仍然存在直接影响。

keeley_formula3 <- '
firesev ~ age
cover ~ firesev + age
'
keeley_sem3 <- sem(keeley_formula3, data = keeley)
summary(keeley_sem3, standardize = T)
# 模型以及饱和，没有剩余的自由度测试模型拟合
# 但可用χ2 test确定此模型是否比部分中介模型更受支持
# cover ~ age 0.067 年龄对覆盖率的影响不显著

anova(keeley_sem2, keeley_sem3)

# P=0.06939 模型有显著差异；也可用AIC、BIC比较

# 植物覆盖率并不直接受到林分年龄的影响，
# 而是年龄的影响完全通过烧伤的严重程度来介导。
```

3 局部估计

3.1 全局与局部估计

上一章，使用SEM估计变量网络之间的关系，基于重现单个方差-协方差矩阵的尝试，这种方法称为全局估计`global estimation`,方差-协方差矩阵一次捕获模型中所有变量之间的关系；该方法对数据进行了许多假设，多变量正态，重复数足够多，可以生成无偏的参数估计，多数生态数据违背了这些假设

基于方差-协方差的方法已考虑非正态性，但基于图论的分段SEM`piecewise SEM`或局部估计是一种替代方法，在此方法中每个内生（响应）变量的关系都是单独估计的

全局估计假设线性关系，拟合SEM的输出与线性模型的输出一致；局部估计为每个响应拟合一个线性模型，然后将推断串在一起，而不是试图估计所有关系；局部估计更像拼图而不是把图像绘制在一块画布

局部估计具有灵活性，与每个响应相关的假设可以单独评估和处理，而不是将每个变量视为来自同一数据生成过程

例如：广义线性模型可以适用于非高斯数据，例如计数（如丰度）、比例（如存活率）、或二元结果（如存在-不存在）。混合效应或分层模型可以适用于嵌套或遵循某些预定义结构的数据；类似地可以将非独立性（如空间、时间、系统发育）纳入模型结构中，提供更稳健的参数估计`more robust parameter estimates`；此外只需要足够多的数据就可以拟合和估计每个单独的回归

分段方法不能免除统计相关的所有假设，数据仍需满足单个模型的假设，如线性回归假设方差恒定且误差独立，但此时可以用对应模型的工具（如残差直方图、Q-Q图）

分段方法的拟合优度度量和全局估计不同，有使用基于有向无环图的测试方法`a new test based on directed acyclic graphs (or DAGs)`；DAG是假设因果关系的图示，即路径图，DAG假设递归关系，或者不存在反馈循环或双向关系。因此，局部估计不适合这种方法，必须采用全局方法（对这种模型结构有一些附加条件）；对数似然方法 ???

3.2 定向分离测试`Tests of directed separation`

在全局估计中，通过χ2统计量对观测方差协方差矩阵与估计方差协方差矩阵进行比较，询问模型隐含的关系是否与数据中存在的关系有很大偏差。如果不是，那么假设模型拟合良好，我们可以继续使用它进行推理。

结构方程建模需要仔细说明假设的结构。在识别不足的模型（即已知信息少于待估计参数的模型）的情况下，这意味着可能存在但未包括的关系缺失。路径可能被排除在外，因为没有先验的理由或机制来怀疑因果关系。回想一下，修正指数`modification indices`可以用来测试包含这些缺失路径的χ2统计量的变化（即模型拟合程度）。

定向分离的测试`The tests of directed separation`通过实际拟合缺失的关系来更直接地评估这一假设，以测试路径系数是否与零显著不同，以及我们是否有理由排除它们。这个问题实际上隐含在χ2统计中：与观察到的相关性的显著偏差表明，我们的模型中缺少了可能使我们的估计更符合我们的观察结果的信息。

如果两个变量在统计上是独立的，则它们的联合影响是d分离`d-separated`的。

因此，我们的第一条有向分离规则是：基集中独立性声明的总数不能从基集中其他声明的组合中导出。

我们的d-sep检验的第二条规则是：条件变量只由与正在评估其独立性的两个变量直接相关的变量组成。

3.3 评估模型拟合度的对数似然法

当不满足最大似然的条件时，例如距离矩阵上的回归时，不能使用该方法，因此在这些情况下，只能进行有向分离测试。然而，基于对数似然的｛^2｝是一个非常有用的补充，由于其灵活性和与传统方法的相似性，它很可能会成为未来默认的拟合优度度量。

3.4 使用分段SEM进行模型拟合

拟合分段结构方程模型就像单独拟合每个回归一样简单：如果你能在R中拟合lm，那么你就已经拟合了SEM！

```r
library(piecewiseSEM)
data(keeley) # 加利福尼亚州野火扰动植物多样性
# 相对于lavaan，分段对每个模型进行编码将赋予更大的灵活性，
# 例如拟合广义线性方程、混合效应模型
# age -> firesev -> cover
keeley_psem <- psem(
  lm(cover ~ firesev, data = keeley),
  lm(firesev ~ age, data = keeley),
  data = keeley)
keeley_psem # 检查

# 导出基集
basisSet(keeley_psem)
# 有一个单独的独立性声明，表示age和cover间缺失路径

dSep(keeley_psem, .progressBar = FALSE)
# 0.07503437 
# 输出与评估独立性声明时的输出相同
# d-sep 检验获得P值 计算Fisher C统计量
summary(lm(cover ~ firesev + age, data = keeley))$coefficients[3, ]
(C <- -2 * log(summary(lm(cover ~ firesev + age, data = keeley))$coefficients[3, 4]))
1-pchisq(C, 2) # 0.07503437 
fisherC(keeley_psem) # 计算Fisher C 和 P值

# 对数似然的χ2统计量；创建饱和模型
keeley_psem2 <- psem(
  lm(cover ~ firesev + age, data = keeley),
  lm(firesev ~ age, data = keeley),
  data = keeley
)

# 使用每个SEM的logLik函数来获得两个子模型的对数似然性
# 取它们的差，并构建χ2统计量
LL_1 <- logLik(lm(cover ~ firesev, data = keeley)) - logLik(lm(cover ~ firesev + age, data = keeley))
LL_2 <- logLik(lm(firesev ~ age, data = keeley)) - logLik(lm(firesev ~ age, data = keeley))
(ChiSq <- -2*sum(as.numeric(LL_1), as.numeric(LL_2)))

DF <- 1 # 饱和模型中估计的一个附加参数
1 - pchisq(ChiSq, DF)
# 因此，我们也无法拒绝基于从该测试中获得的P值的模型。
# 使用原始（不饱和）模型上的函数LLchisq，可以更容易地获得相同的输出
LLchisq(keeley_psem) # 得到Chisq和P

# 对于假设多元正态性的模型，
# ｛^2｝统计量和P值实际上与lavan获得的相同：
library(lavaan)
keeley_formula <- '
firesev ~ age
cover ~ firesev
'
keeley_sem <- sem(keeley_formula, data = keeley)
fit <- lavInspect(keeley_sem, "fit")
fit["chisq"]; fit["pvalue"]

# 还可获得该模型的AIC分数。默认值基于对数似然χ2
AIC(keeley_psem) # 364.696
# 为了获得基于Fisher C统计量和d-sep检验的AIC值，可添加以下参数
AIC(keeley_psem, AIC.type = "dsep") # 17.18
# 一个完全饱和或刚刚确定的模型将产生0的C统计量。
# 基于上面的希普利方程，AIC分数降低到2K，或者可能性自由度的两倍。
# 这与基于实际可能性的替代公式形成了对比。
# 因此，在希望比较完全饱和的模型的情况下，我们建议使用默认的基于χ2的值。

# 可以使用SEM对象上的摘要函数同时执行以上所有操作
summary(keeley_psem, .progressBar = FALSE)
# 输出应该与其他摘要调用（如summary.lm）的输出非常相似。
# 报道了拟合优度的d-sep检验、χ2检验、Fisher C检验和AIC检验。

# 此外，还会返回模型系数。与lavan不同，标准化估算是默认提供的。
# 与lavan不同的是，默认情况下也会返回单个型号的R2值。
# 这两组统计数据都是推理的关键，因此我们决定将它们与传递给摘要的任何进一步的参数一起提供。

# We can compare the piecewiseSEM output to the lavaan output:】
library(lavaan)
sem1 <- '
firesev ~ age
cover ~ firesev
'
keeley_sem1 <- sem(sem1, keeley)
summary(keeley_sem1, standardize = T, rsq = T)
# 同样，因为我们正在做出与全局估计相同的假设（即，多元正态性），
# 所以所有的输出都是相同的（或基于舍入和优化差异几乎相同）。
# 当然，如果我们结合不同的分布和更复杂的模型结构，我们可能会期望这两种方法之间有更大的差异

```

3.5 广义混合效应模型`Generalized Mixed Effects Models`的推广

关于树木生存的例子，对20个地点的单株树木进行随访，测量出芽时间、第一次出芽前的累计天数、生长率、存活率；这些数据具有多个层次的层次结构，站点之间、站点内个体之间，站点中个体内年份之间；生存率为二元变量

假设以以下方式相关`lat -> DD -> Date -> Growth -> Survival`

```r
data(shipley)
shipley_model <- '
DD ~ lat
Date ~ DD
Growth ~ Date
Live ~ Growth
'
shipley_sem <- sem(shipley_model, shipley)
summary(shipley_sem, standardize = T, rsq = T)
# 拟合优度是可以估计的，但该模型的拟合较差（P<0.001）
# 与其篡改修改索引并试图重新调整模型结构，
# 不如让我们使用分段方法分析同一路径图，
# 并识别数据的层次结构和非正态性。
# 为此，我们将使用两个常见的混合效果模型包lme4和nlme

library(nlme)
library(lme4)
shipley_psem <- psem(
  
  lme(DD ~ lat, random = ~ 1 | site / tree, na.action = na.omit,
      data = shipley),
  
  lme(Date ~ DD, random = ~ 1 | site / tree, na.action = na.omit,
      data = shipley),
  
  lme(Growth ~ Date, random = ~ 1 | site / tree, na.action = na.omit,
      data = shipley),
  
  glmer(Live ~ Growth + (1 | site) + (1 | tree),
        family = binomial(link = "logit"), data = shipley)
  
)
summary(shipley_psem, .progressBar = FALSE)
# 基于Fisher’s C的直接明显差异是，该模型不再是差拟合：我们有12个自由度，对应于6个独立性声明，
# 所有这些声明都P>0.05。因此，模型范围内的P=0.484，因此我们拒绝数据不支持假设的模型结构
# 虽然参数估计的方向保持不变，但它们的幅度变化很大
# 模型R2 s也都更高，仅针对固定效应（边际），尤其是针对固定和随机效应（条件）
# 因此，通过解决数据的非独立性，我们已经集中支持假设的模型结构，更准确的参数估计，以及比使用lavan更高比例的解释方差。
# 然而，请注意，该模型没有报告χ2统计数据，并发出了收敛警告。
# 当饱和SEM中的一个或多个子模型无法收敛时，可能会产生无效的似然估计，导致χ2<0的情况。
# 由于这是不允许的，函数返回χ2统计量和相关P值的NA。
# 潜在的解决方案包括调整模型优化器以确保收敛的解决方案，或者依赖Fisher的C。

```

3.6 非线性模型`Non-linear Models`的扩展

上面提到的更新的基于对数似然的拟合优度过程的好处之一是，它可以扩展到真正的非线性模型，例如应用最大似然估计的广义加性模型（GAM）

```r
set.seed(100)
n <- 100
x1 <- rchisq(n, 7)
mu2 <- 10*x1/(5 + x1)
x2 <- rnorm(n, mu2, 1)
x2[x2 <= 0] <- 0.1
x3 <- rpois(n, lambda = (0.5*x2))
x4 <- rpois(n, lambda = (0.5*x2))
p.x5 <- exp(-0.5*x3 + 0.5*x4)/(1 + exp(-0.5*x3 + 0.5*x4))
x5 <- rbinom(n, size = 1, prob = p.x5)
dat2 <- data.frame(x1 = x1, x2 = x2, x3 = x3, x4 = x4, x5 = x5)
# 存在线性和非线性变量的混合，包括泊松分布和二项式分布。

# x1 -> x2 
# x2 -> x3  x2 -> x4
# x3 -> x5  x4 -> x5

# 首先拟合一个假设多元正态的严格线性SEM
shipley_psem2 <- psem(
  lm(x2 ~ x1, data = dat2),
  lm(x3 ~ x2, data = dat2),
  lm(x4 ~ x2, data = dat2),
  lm(x5 ~ x3 + x4, data = dat2)
)

LLchisq(shipley_psem2)
# 尽管生成的数据本质上是非正态和非线性的，但该模型实际上很适合P值为0.529的数据
# 尽管如此，我们知道我们可以做得更好，既可以包括非高斯分布，也可以通过应用广义加性模型，
# 该模型不是将响应建模为预测因子的线性函数，而是通过允许出现非线性关系的平滑函数。
# 让我们使用GLM和GAM的组合来重新拟合模型

library(mgcv)
shipley_psem3 <- psem(
  gam(x2 ~ s(x1), data = dat2, family = gaussian),
  glm(x3 ~ x2, data = dat2, family = poisson),
  gam(x4 ~ x2, data = dat2, family = poisson),
  glm(x5 ~ x3 + x4, data = dat2, family = binomial)
)

LLchisq(shipley_psem3)
# 该模型也具有足够的拟合性，P值为0.647。
# 让我们计算两者的AIC得分（基于对数似然），并进行比较
AIC(shipley_psem2, shipley_psem3)
# 第二种SEM——更好地解决了数据的基本形式——比直线SEM有更高的支持率，
# ΔAIC=49.45。因此，我们会选择第二个模型
summary(shipley_psem3)

# 请注意，输出不会报告平滑变量的估计值或标准误差。这是因为，如前所述，这些不是线性系数，而是平滑函数，并且没有一个值与例如x1如何随x2变化有关。
# 因此，使用GAM无法计算直接和间接影响，这可能会使其在目标是比较模型内各种途径的强度时不太理想。

# 可以在模型之间进行比较并验证DAG的拓扑结构，这在许多情况下足以检验假设。
# 那些试图理解x1如何与x2非线性变化的人，除了路径图之外，还必须提供这种关系的额外预测图。

```

3.7 一个特例：图论失败的地方

在大多数情况下，独立性声明的方向无关紧要，因为尽管系数不同，但它们的P值相同。因此，测试y|x或x|y并不重要，因为声明将产生相同的显著性测试。除非中间内生变量是非正态分布的。

`x1 -> y1 x1 -> y2`
`y1 -> y3 y2 -> y3`

在本SEM中，有两个独立性声明

$y3 | x1 (y1, y2)$ 和 $y2 | y1 (x1)$

```r


set.seed(87)
glmdat <- data.frame(x1 = runif(50), y1 = rpois(50, 10), y2 = rpois(50, 50), y3 = runif(50))
# LM
summary(lm(y1 ~ y2 + x1, glmdat))$coefficients[2, 4]
summary(lm(y2 ~ y1 + x1, glmdat))$coefficients[2, 4]
summary(glm(y1 ~ y2 + x1, "poisson", glmdat))$coefficients[2, 4] 
summary(glm(y2 ~ y1 + x1, "poisson", glmdat))$coefficients[2, 4]

logLik(glm(y1 ~ y2 + x1, "poisson", glmdat))
logLik(glm(y2 ~ y1 + x1, "poisson", glmdat))
# piecewiseSEM通过向用户提供三个选项来解决此问题

# 我们可以指定测试的方向性，例如，如果对y 1和y 2进行测试而不是相反更有生物学意义（例如：丰度驱动物种丰富度，而不是相反）；
# 或者我们可以从基集中删除该路径，而是使用%～%将其指定为相关错误。这完全避开了这个问题，但假设这两个变量都是由某个底层过程生成的可能没有意义；
# 或者我们可以同时进行这两种测试，并在对数似然中选择最保守（即最低）的P值或最大差值。

glmsem <- psem(
  glm(y1 ~ x1, "poisson", glmdat),
  glm(y2 ~ x1, "poisson", glmdat),
  lm(y3 ~ y1 + y2, glmdat)
)

summary(glmsem) # 如果SEM中确定了上述情况，这些选项将通过摘要返回
summary(glmsem, direction = c("y1 <- y2"), .progressBar = F)$dTable
# 在选项1中，可以使用direction=c（）作为要汇总的附加参数来指定方向性。

summary(update(glmsem, y1 %~~% y2), .progressBar = F)
# 在选项2中，可以更新SEM，通过将其指定为相关错误来删除该测试。

summary(glmsem, conserve = T, .progressBar = F)$dTable
# 最后，可以通过指定conserve=T作为附加参数来调用选项3
# 用户应警惕此类情况，并确保指定的路径和独立声明都具有生物学意义。
# 在d-sep测试的基本假设可能会对拟合优度统计产生偏差的情况下，分段SEM应自动提醒用户并提出解决方案。

```

4 系数`Coefficients`

4.1 非标准化`Unstandardized`和标准化系数`Standardized Coefficients`

路径（或回归）系数是结构方程建模背后的推理引擎`the inferential engine`，进而是所有线性回归的推理引擎；将因变量y的变化与自变量x的变化联系起来以作为关联的衡量标准；在全局估计中，路径系数可以表示为（偏）相关性，无单位的关联度量，适合比较；还允许生成对x的新值的预测，以测试和外推

考虑两种回归系数：非标准化（原始）系数和标准化系数

非标准化系数为统计程序的标准返回值，反映了预测因子中每个单位变化的预期（线性）响应变化

在具有一个以上自变量（例如，x1、x2等）的模型中，系数反映了给定模型中其他变量的y的预期变化。这意味着一个特定变量的影响控制着其他变量的存在，通常是通过将它们保持在平均值不变。这就是为什么这些系数被称为偏回归系数，因为它们反映了任何特定变量的独立（或部分）贡献。

当应用对数变换时，变量之间的关系不再是线性的。这意味着我们必须稍微改变我们的解释。当对y进行对数变换时，系数β被解释为x的1个单位变化导致y的（e x p（β）−1）×100变化。

原始系数不同，标准化系数以等效单位表示，与原始测量无关。这些通常是以平均值的标准偏差为单位的（标度标准化）；标准化的目标是提高可比性。换言之，可以直接比较标准化系数的大小，以推断关系的相对强度。

在SEM中，通常建议同时报告非标准化系数和标准化系数，因为它们呈现出不同且相互排斥的信息。非标准化系数包含关于方差和均值的信息，因此对预测至关重要。沿着这些思路，它们也有助于在适用于相同变量但使用不同数据集的模型之间进行比较。由于最常见的标准化形式涉及按样本标准差缩放，因此来自不同来源（即不同数据集）的数据具有不同的样本方差，其标准化系数不能立即进行比较。

标准化效应有助于比较同一模型中与不同路径相关的相对变化幅度

从广义上讲，有必要进行标准化，以比较同一模型中不同路径集之间的间接或复合效应：例如，比较部分中介模型中的直接路径与间接路径。这是因为这些途径可以而且经常以非常不同的单位进行测量，它们的相对幅度可能只是反映了它们的测量单位，而不是任何更强或更弱的影响。

比较不同模型中同一组变量的间接或复合效应的强度需要非标准化系数。使用标准化系数在不同模型之间比较相同的路径需要证明样本方差没有显著差异

标准化系数和非标准化系数在结构方程建模中都有其位置。

4.2 尺度标准化`Scale Standardization`

lavaan和pilewiseSEM都返回标度标准化的系数。lavaan需要一组不同的函数或参数，而plicwiseSEM将默认使用函数coefs来完成。coefs还有一个好处，就是它可以在任何模型对象上调用，因此在结构方程建模之外也有应用。

```r
library(lavaan)
library(piecewiseSEM)

set.seed(6)

data <- data.frame(y = runif(100), x = runif(100))
xy_model <- lm(y ~ x, data = data)
# perform manual standardization
beta <- summary(xy_model)$coefficients[2, 1]
(beta_std <- beta * (sd(data$x)/sd(data$y)))
# now retrieve with piecewiseSEM
coefs(xy_model)$Std.Estimate
# and with lavaan
xy_formula <- 'y ~ x'
xy_sem <- sem(xy_formula, data)
standardizedsolution(xy_sem)$est.std[1]
```

4.3 范围标准化`Range Standardization`

请注意，全局估计章节中所示的（部分）相关性的分解不可能与相关范围相结合，因此，如果目标是计算间接或总影响，则不建议进行范围标准化。

```r
#by hand
(beta_rr <- beta * (max(data$x) - min(data$x))/(max(data$y) - min(data$y)))
coefs(xy_model, standardize = "range")$Std.Estimate
```

规模`Scale `和相关范围`Range`标准化仅适用于响应正态分布的情况。如果不是，我们必须做出一些假设才能获得标准化系数。

4.4 二项式响应模型`Binomial Response Models`

二项式反应是那些二元（0，1）的反应，如成功或失败，或存在与不存在。它们的独特之处在于，它们与预测器x没有线性关系。相反，它们最好使用S形曲线进行建模。为了演示，让我们生成一些数据，拟合二元模型，并绘制预测关系图：

```r
set.seed(44)
x <- rnorm(20)
x <- x[order(x)]
y <- c(rbinom(10, 1, 0.8), rbinom(10, 1, 0.2))
glm_model <- glm(y ~ x, data = data.frame(x = x, y = y), "binomial")
xpred <- seq(min(x), max(x), 0.01)
ypred <- predict(glm_model, list(x = xpred), type = "response")
plot(x, y)
lines(xpred, ypred)
```

这些数据不是线性的，因此对它们进行建模会忽略底层数据生成过程。相反，正如你所看到的，我们使用广义线性模型（GLM）将它们拟合为二项式分布。

GLM由三个部分组成：（1）随机分量，或基于其潜在分布的响应的预期值，（2）表示预测因子线性组合的系统分量，以及（3）链接函数，该函数通过变换将响应（随机分量）的预期值与预测因子的线性组合（系统分量）联系起来。基本上，链接函数采用固有的非线性，并试图将其线性化。这可以通过在链接尺度上绘制预测来显示：

```r
ypred_link <- predict(glm_model, list(x = xpred), type = "link")
plot(xpred, ypred_link)
```
对于二项式响应，有两种链接函数：logit和probit。我们现在将重点关注logit链接，因为它更常见。有了这个链接，系数以logits或对数比值比为单位，反映了观察到结果（1）的概率相对于不观察结果（0）的概率的对数。

问题是（对数）比值比本身在不同的模型中是不可比较的。此外，目前还不清楚它们是如何标准化的，因为系数是在链接（线性）尺度上报告的，而我们唯一能计算的方差是来自非线性尺度上的原始数据。因此，我们需要找到一些摇摆，以获得与系数相同的线性化尺度上的方差估计。

4.4.1 潜在理论方法`Latent Theoretic Approach`
4.4.2 观察实证法`Observation-Empirical Approach`

```r
# get beta from model
beta <- summary(glm_model)$coefficients[2, 1]
preds <- predict(glm_model, type = "link") # linear predictions
# latent theoretic
sd.ystar <- sqrt(var(preds) + (pi^2)/3) # for default logit-link
beta_lt <- beta * sd(x)/sd.ystar
# observation empirical
R2 <- cor(y, predict(glm_model, type = "response"))^2 # non-linear predictions
sd.yhat <- sqrt(var(preds)/R2)
beta_oe <- beta * sd(x)/sd.yhat
# obtain using `coefs`
coefs(glm_model, standardize.type = "latent.linear"); beta_lt
coefs(glm_model, standardize.type = "Menard.OE"); beta_oe

```

4.5 缩放到其他非正态分布

在很多方面，逻辑回归是标准化要求最高的情况，因为我们实际上是在建模一个潜在的（不可测量的）性质，其方差是未知的（但如上所述，可以估计）。对于其他分布，我们正在对实际值进行建模：这意味着只能使用观测经验方法，这大大简化了过程，因为我们不需要担心任何理论误差方差。让我们通过一个使用计数数据的泊松分布的例子来学习。
泊松模型的默认链接函数是对数链接，这意味着我们只是对响应的对数进行建模。因此，我们将假设拟合泊松分布的广义线性模型与拟合正态分布的对数变换响应的一般线性模型大致相同。这种近似等效性很快就会变得清晰起来。

```r
# 泊松分布数据示例
set.seed(100)
count_data <- data.frame(y = rpois(100, 10))
count_data$x <- count_data$y * runif(100, 0, 5)
# 用对数转换的响应来拟合LM
lm_model <- lm(log(y) ~ x, count_data)
coefs(lm_model)$Std.Estimate
# 简单线性回归的标准化系数实际上是两者之间的二元相关性
with(count_data, cor(x, log(y)))
# 让我们使用GLM将该模型重新拟合为具有默认日志链接的泊松分布
glm_model2 <- glm(y ~ x, family = poisson(link = "log"), count_data)
coef(glm_model2)[2]
# βx=0.012，这与线性模型有点不同。这是因为未标准化系数是在链路尺度上报告的。
R2 <- cor(count_data$y, predict(glm_model2, type = "response"))^2 # non-linear predictions
sd.yhat <- sqrt(var(predict(glm_model2, type = "link"))/R2)
coef(glm_model2)[2] * sd(count_data$x)/sd.yhat
```

5 类别变量`Categorical Variables`

虽然SEM最初只考虑连续变量（事实上，大多数应用程序仍然如此），但通常情况下——尤其是在生态学中——观察到的变量是离散的。例如：二进制（是/否、失败/成功等）、标称（站点1、站点2）或有序级别（小<中<大）。建模方面的最新进展允许直接或以更迂回的方式将分类变量纳入SEM。
有两种方式可以包括分类变量：作为外源（预测因子）或内源性（反应）。我们将首先处理外生分类变量的更简单的情况，因为它们不是一个计算问题，而是一个概念问题。

5.1 外源范畴变量导论`Introduction to Exogenous Categorical Variables`

预测y的线性回归具有以下标准形式$y = \alpha + \beta_{1}*x_{1} + \epsilon$；α是截距，β1是x对y的影响的斜率，ε是残差

当x连续时，截距α被积分为当x=0时y的值。对于分类因子，截距α有不同的解释。考虑具有k个级别的x值。由于x的水平是离散的，并且可能永远不会假设值为0，因此α是x的“参考”水平上y的平均值。回归系数βk是相对于参考水平的每个其他水平的影响。因此，对于k个水平，有k−1系数是用反映第k个水平的附加α项估计的。

另一种看待这一现象的方法是使用所谓的“伪”变量`‘dummy’ variables`。想象一下，每个级别都被分解为一个值为0或1的单独变量：一个级别为“a”和“b”的两级因子将变成两个级别分别为0和1的因子“a”或“b”。（在R中，这意味着将行转换为列。）

将这些伪变量的所有值设置为0来估计截距：这意味着完全不存在因子，这不是一种状态。另一种思考方式是，伪变量是线性相关的：如果“a=1”，那么根据定义，“b=0”作为响应变量不能同时占据这两种状态。因此，需要设置一个级别作为参考，这样就可以相对于没有“b”来解释“a”的影响，这也是为什么你不能恢复尽可能多的系数。这种行为给路径图的参数化带来了挑战：从x到y的路径没有一个系数，也没有足够的系数来为x的每个级别填充一个单独的箭头（因为必须有一个级别作为参考）。

有几个潜在的解决方案：

1.对于二进制变量，将值设置为0或1，并将模型设置为数字，这将产生一个单一的系数，表示当x从状态“0”变为另一状态“1”时y的预期变化。

2.对于序数变量，根据因子的顺序设置值，例如，small=1< medium=2 < large=3，然后将模型设置成数字，这也将产生单一的系数表示当你从最小值爬到中等值时x的预期变化，以此类推。

3.为每个级别创建虚拟变量：这在程序上与上面相同（将级别划分为状态为或/1的k-1个独立变量）。这里的关键是不要创建k个变量，以避免上面提出的关于级别之间依赖性的问题。这是lavan的默认行为。

这种方法对于大量的类别或级别变得令人望而却步，并且会大大增加模型的复杂性。此外，在有向分离测试中，每个级别都被视为自变量，因此在分段应用中会增加自由度。

1.对于与分类变量的可疑相互作用，需要进行多组分析。在这种情况下，相同的模型适用于每个级别的因子，具有潜在的不同系数。

2.使用ANOVA测试分类变量的影响，但不报告系数。这种方法将表明一个因素是否重要（即，水平是否与反应显著不同），但忽略了关于哪些水平以及变化的方向和幅度的重要信息。例如，显著的治疗效果是否意味着反应的增加或减少，增加或减少多少？因此，这种方法是有效的，但并不理想。

另一种方法利用了这一最后一点，包括测试和报告模型的估计或边际均值。 `the model-estimated or marginal means.`

5.2 作为边际均值的外生范畴变量`Exogenous Categorical Variables as Marginal Means`

所有模型都可以用于预测。在多元回归中，通常计算一个变量的预测值，同时将其他变量的值保持在其平均值。边际均值是这些预测的平均值。换句话说，它们是给定模型中其他协变量的一个预测器的预期平均值。

对于分类变量，边际均值特别有用，因为它们提供了每个因素的每个水平的估计均值。
考虑一个简单的例子，其中包含一个响应和两组“a”和“b”：

```r

set.seed(111)
dat <- data.frame(y = runif(100), group = letters[1:2])
model <- lm(y ~ group, dat)
summary(model)
# 注意，汇总输出给出了一个简单的系数，这是在没有组“a”的情况下组“b”对y的影响。
# 如上所述，截距只是群“a”中y的平均值：
summary(model)$coefficients[1, 1]
mean(subset(dat, group == "a")$y)
# 边际均值是组“a”和组“b”中y的预期平均值。
predict(model, data.frame(group = "a"))
predict(model, data.frame(group = "b"))
# 因为这是一个简单的线性回归，这些值只是数据的两个子集的平均值，
# 因为它们不控制任何其他协变量：
mean(subset(dat, group == "a")$y)
mean(subset(dat, group == "b")$y)
# 添加一个连续协变量
dat$x <- runif(100)
model <- update(model, . ~ . + x)
# 必须在将协变量x保持在其平均值的同时评估边际平均值
predict(model, data.frame(group = "a", x = mean(dat$x)))
mean(subset(dat, group == "a")$y)
# 这个值现在与数据子集的平均值不同，因为它再次控制了x对y的影响

# 随着因子水平的数量和协变量的数量，这个过程变得越来越复杂。
# emmeans包提供了一种计算边际均值的简单方法
library(emmeans)
emmeans(model, specs = "group") # where specs is the variable or list of variables whose means are to be estimated
# 组“a”的输出值与使用上述函数相同，但也返回组“b”的边际平均值，同时还控制预测x
predict(model, data.frame(group = "b", x = mean(dat$x)))

# 该函数继续提供较低和较高的置信区间，这提供了额外的信息水平，即每个平均值是否与零显著不同。
# 再加上对类别之间差异的方差分析检验，边际均值提供了其他方面缺乏的关键信息，
# 即响应值是否以及如何根据因素水平变化。
# emmeans包通过对每个因素水平的平均值之间的差异进行事后测试，提供了额外的功能
emmeans(model, list(pairwise ~ group))
# 第二个输出，它是组“a”和“b”的平均值之间的成对对比，以及相关的显著性测试
# 这些成对的Tukey测试提供了最终的信息水平，即每个水平的反应是否与其他水平有显著差异

# 分段SEM中的函数采用了两层方法，首先使用ANOVA计算分类变量的显著性，然后报告边际均值和事后检验
library(piecewiseSEM)
coefs(model)
# 在这个输出中，我们检索连续x的正常输出，包括标准化的效果大小。
# ANOVA的显著性检验报告在与群体效应相对应的行中，下面是分组因子每个水平的边际均值。请注意，方差分析效应或边际均值都没有标准化估计，
# 因为正如我们所确定的，这些都不是线性系数，因此不能像往常一样标准化。

# 该解决方案以模型估计的边际均值的形式提供了外生分类变量和响应之间的路径是否显著的度量，
# 以及每个水平的参数。
```

5.3 作为边际均值的外生范畴变量：一个实例`Exogenous Categorical Variables as Marginal Means: A Worked Example`

在这项研究中，作者对盐沼植物芦苇的不同微生物组如何驱动生态系统功能，并最终产生地上生物量感兴趣。在这种情况下，他们考虑了三个微生物群落：来自北美本土谱系、墨西哥湾沿岸谱系和引入谱系的微生物群落。每个群落类型中都有额外的基因型，因此必须应用随机效应来解释种内变异。

在这种情况下，变量“芦苇状态”对应于三种群落类型，不能使用单个系数来表示。因此，边际方法是阐明每种群落类型对近端和最终生态系统特性的影响的理想方法，同时测试这条路径的总体意义。

```r
bowen <- read.csv("bowen.csv")
bowen <- na.omit(bowen)
library(nlme)
bowen_sem <- psem(
  lme(observed_otus ~ status, random = ~1|Genotype, data = bowen, method = "ML"),
  lme(RNA.DNA ~ status + observed_otus, random = ~1|Genotype, data = bowen, method = "ML"), 
  lme(below.C ~ observed_otus + status, random = ~1|Genotype, data = bowen, method = "ML"), 
  lme(abovebiomass_g ~ RNA.DNA + observed_otus + belowCN + status, random = ~1|Genotype, data = bowen, method = "ML"),
  data = bowen
)
summary(bowen_sem, .progressBar = FALSE)
```

这种情况下，根据原始作者使用的Fisher’s C统计量（P=0.057），该模型似乎足够好地拟合数据。注意，基于似然的χ2统计实际上意味着较差的拟合（P=0.043）。在这种情况下，检查d-sep测试表明包含了从b elowCN到belowC的路径可能会提高贴合度。然而，我们正在应用一种原始作者无法使用的工具，因此我们将按照他们的做法进行，并假设其足够合适。

微生物群落类型（s t a t u s）和丰富度（o b s e r v e d o t u s。边际平均数的检查表明微生物活性（R N A。D N A）和地下碳（b e l o w。C）通常在具有本地微生物群落的芦苇中最高。然而，这些特性似乎都不会影响生物质的最终生产（a b o v e b i o m a s s g）。相反，这种特性似乎完全由植物微生物组类型（s t a t u s）控制：那些引入微生物群落的植物在控制微生物活性和土壤养分后，根据其边际平均值，具有显著更高的地上生物量。
因此，尽管有多级分类预测因子（s t a t u s），方差分析和边际均值计算的两步程序允许对该物种植物生物量的驱动因素有更机械的理解。

5.4 内生范畴变量`Endogenous Categorical Variables`

内生分类变量要棘手得多，而且目前还没有以分段SEM的方式实现。

在分段框架中的内生分类变量的情况下，实际上只有两种解决方案：

对于二进制变量，将值设置为0或1，并将模型设置为数字，这将产生单个系数。
对于有序变量，根据因子的顺序设置值，例如，small=1 < medium=2 < large=3，然后建模为数字，这将产生单个系数。

名义变量（即水平没有排序）可以使用多项式回归进行建模，尽管这种方法必须手动执行。另一种选择是使用因子水平来构建一个复合变量，这是后面一章的主题。lavaan以验证性因素分析的形式提供了一种稳健的替代方案；在分段SEM中，复合材料必须手工构建

6 多组分析`Multigroup Analysis`

6.1 多组分析导论

在生态学中，我们经常希望比较两个或更多组的结果。这些组可以反映实验处理、不同地点、不同性别或任何类型的组织。这种分析的最终目标是询问预测变量和反应变量之间的关系是否因组而异。

从历史上看，这样的目标将通过应用统计交互来实现。例如，杀虫剂对无脊椎动物生物量的影响是否随着杀虫剂的施用位置而变化？此模型可能如下所示：$biomass = pesticide \times location$

$pesticide \times location$之间的显著相互作用表明，施用杀虫剂对无脊椎动物生物量的影响确实因地点而异。当然，这将取决于作者利用他们对该系统的了解来推测为什么会这样。

如果相互作用在统计上不显著，作者会得出结论，杀虫剂的作用对位置是不变的。相反，作者可以概括农药的作用，这样无论在哪里使用，它都会产生相同程度的影响。

多组模型本质上是相同的原理，但不是专注于单个响应，而是将相互作用应用于整个结构方程模型。换言之，它询问是否不仅一个系数，而且所有系数在组之间是相同的还是不同的。从某种意义上说，它可以被认为是一种“全模型”的交互，事实上，这就是我们稍后使用分段方法处理它的方式。

当然，您可能会问：为什么不简单地将相同的模型结构应用于不同的数据子集呢？不幸的是，这将不允许您识别哪些路径会根据组而更改，哪些路径不会更改，这可能是关键的见解。相反，人们必须手动比较每对系数的幅度和标准误差，而不是通过正式的统计程序。

多组模型的应用在全局估计（即基于方差-协方差的SEM）和局部估计（即分段SEM）之间有所不同，但它们坚持相同的思想，即识别哪些路径在组间具有相同的效果，哪些路径因组而异。

6.2 基于全局估计的多组分析`Multigroup Analysis using Global Estimation`

使用全局估计的多组建模从两个模型的估计开始：一个模型允许所有参数在组之间不同，另一个模型将所有参数固定为从跨组的汇总数据分析中获得的参数。我们将第一个模型称为“自由”模型，因为所有参数都可以自由变化，而将第二个称为“受约束”模型，原因是每条路径，无论其组如何，都被约束到由整个数据集确定的单个值。

如果这两个模型没有显著差异，并且后者很好地拟合数据，那么可以假设路径系数没有按组变化，并且不需要多组方法。在这种情况下，将报告受约束模型的输出。

如果是，那么练习将转向理解哪些路径相同，哪些路径不同。这是通过依次约束每条路径的系数并重新拟合模型来实现的。

让我们用一个随机的例子来说明这个过程，使用三个变量——x、y和z——分为两组：“a”和“b”

在这个例子中，我们假设一个简单的中介模型：x−>y−>z，并且所有三个变量都在某种程度上相关，所以这个模型是有意义的。
我们可以使用lavaan来适应“自由”模型。关键是通过指定group=参数来允许系数发生变化：

```r
set.seed(111)
dat <- data.frame(x = runif(100), group = rep(letters[1:2], each = 50))
dat$y <- dat$x + runif(100)
dat$z <- dat$y + runif(100)
multigroup.model <- '
y ~ x
z ~ y
'
library(lavaan)
multigroup1 <- sem(multigroup.model, dat, group = "group") 
summary(multigroup1)

# 请注意，与典型的lavaan输出不同，打印输出现在是按组组织的，每组中的每条路径都有单独的系数。
# 由于该模型允许变化，因此组“a”中x−>y路径的系数与组“b”报告的系数不同。
# 接下来，我们通过指定额外的参数组来拟合约束模型。equal=c（“intercepts”，“regression”）。
# 此参数将每组中的截取和路径系数固定为相同。

multigroup1.constrained <- sem(multigroup.model, dat, group = "group", group.equal = c("intercepts", "regressions"))
summary(multigroup1.constrained)
# 这个输出与第一个略有不同：系数是按组报告的，但现在组之间是相同的（例如，组“a”中的γx=组“b”中的伽玛x）。
# 受约束的路径由路径旁边的括号指示（例如，路径1的（.p1.））。
# 基于χ2统计，约束模型和自由模型都很好地拟合了数据，我们可以使用卡方差分检验对两者进行正式比较：
anova(multigroup1, multigroup1.constrained)

# 显著的P值意味着自由模型和约束模型显著不同。换言之，有些路径会发生变化，而另一些路径可能不会。如果模型没有显著差异，
# 那么人们会得出结论，约束模型与自由模型等效，或者系数不会因组而异，在单个全局模型中分析汇集的数据是公平的。

# 然而，本例并非如此，我们现在可以经历引入和释放约束的过程，以尝试确定组之间的路径不同。
# 在这个简化的例子中，我们有两个选择：x−>y和y−>z。让我们先关注x−>y
# 我们可以通过修改模型公式并重新拟合模型来引入单个约束

multigroup.model2 <- '
y ~ c("b1", "b1") * x
z ~ y
'
multigroup2 <- sem(multigroup.model2, dat, group = "group")

# 字符串c（“b1”，“b1”）将路径命名为b1，并确保两组（因此两个条目）之间的系数相等。
# 如果我们像以前一样使用卡方差分检验：
anova(multigroup1, multigroup2)
# 这些模型仍然存在显著差异，这意味着x−>y之间的路径不应受到限制，而是应根据组的不同而不同。
# 使用第二条路径y−>z重复此练习：
multigroup.model3 <- '
y ~ x
z ~ c("b2", "b2") * y
'
multigroup3 <- sem(multigroup.model3, dat, group = "group")
anova(multigroup1, multigroup3)
# 在这种情况下，两个模型之间没有显著差异（P=0.23），
# 这意味着受约束模型和无约束模型的拟合没有差异，并且该约束是有效的。
```

如果我们在这三个备选方案中进行选择，我们将选择第三个模型，其中x−>y允许变化，y−>z在组之间受到约束。需要注意的是，该模型也很好地拟合了基于χ2统计的数据；如果不是，那么就像所有拟合不佳的路径模型（多组或其他）一样，从中提出并得出结论是不明智的。

这种放松和施加约束的练习可能是非常具有探索性的，并且可能会对更复杂的模型（即具有许多潜在约束/放松路径的模型）变得详尽无遗。用户应该避免约束和放松所有路径，然后选择最节省的模型。相反，选择限制哪些途径应该受到这样一个问题的激励：例如，我们可能期望一些影响是普遍的（例如，温度对代谢率的影响），而不是其他影响（例如，农药的影响可能因不同地点的施用历史而不同）。

至关重要的是，模型的自由度不会根据组的数量而变化，因为系数是根据具有相同维度的方差-协方差矩阵估计的。然而，样本量必须足够大，以便以最小的偏差估计每组中的所有参数。虽然这对所有结构方程模型都是正确的，但在根据不具有相同复制的不同子集（组）导出的协变量来估计参数的情况下尤其如此。

标准化系数也是一个挑战。由于各组之间的方差可能不相等（除非它们来自同一人群），因此必须在每组的基础上计算标准化系数，即使非标准化系数被限制在全局值内。SEM的两个软件包都会自动执行此操作，因此您可能会注意到，即使在受约束的路径中，标准化解决方案也可能会发生变化，而且往往会发生变化。

6.3 使用局部估计的多组分析

使用局部估计的多组分析的目标与全局估计的目标相同：确定单个全局模型是否足以描述数据，或者某些或所有路径是否因某些分组变量而异。不同之处在于执行：虽然lavaan是一个来回手动的放松和约束路径的过程，但分段SEM会测试约束，并自动为您的数据选择最佳输出。

好处是，规定约束条件的艰巨而有些繁琐的过程得到了处理；不利的一面是，目前不可能手动约束特定的路径。

局部估计过程中的第一步是实现模型范围的交互。换句话说，模型中的每个项都与分组变量相互作用。如果相互作用是显著的，那么路径可以自由地因组而异；如果不是，则路径采用来自全局数据集的估计。通过这种方式，分段多群过程分解为一系列经典的交互项：它是我们在本章开头讨论的模型范围内的交互

考虑一下我们之前使用lavaan安装的示例。在分段方法中，我们将首先对x×g r o u p之间的相互作用进行建模，以查看x对y的影响是否应因组而异：

```r
# 考虑一下我们之前使用lavaan安装的示例。在分段方法中，
# 我们将首先对x×g r o u p之间的相互作用进行建模，以查看x对y的影响是否应因组而异：
anova(lm(y ~ x * group, dat))
# 在这种情况下，x对y的影响取决于g r o u p（一个重要的相互作用项）。
# 然后，我们将估计数据的每个子集的x和y的影响，并分别报告系数=
# 接下来，我们按组评估y对z的影响：
anova(lm(z ~ y * group, dat))
# 在预测z时，y×g r o u p之间的第二个相互作用不显著，表明y对z的影响不取决于g r o u p。
# 然后，我们将使用整个数据集来估计y对z的影响，并报告所有组中的单个约束系数。

# 这种方法在分段SEM中的实现非常简单：首先，使用psem建立模型，
# 然后使用函数multigroup进行multigroup分析。
library(piecewiseSEM)
pmodel <- psem(
  lm(y ~ x, data = dat),
  lm(z ~ y, data = dat)
)
pmultigroup <- multigroup(pmodel, group = "group")
#### 此处疑似有错误 ####

standardizedSolution(multigroup3)
pmultigroup$group.coefs
```

7 潜在变量建模`Latent Variable Modeling`

潜在变量是未被观察到的变量，但其影响可以通过一个或多个指标变量进行总结。它们可用于捕获难以直接量化或测量的系统的复杂或概念属性。

8 复合变量`Composite Variables`

复合变量是除潜在变量之外的另一种方式，用于表示结构方程建模中的复杂多变量概念。两者之间最重要的区别在于，虽然潜在变量产生了不可观察概念的可测量表现形式，但复合变量来自测量变量的总组合影响。

在其他情况下，该属性可能来自变量的集体影响，但并非没有错误。例如，土壤条件的概念源于土壤的不同方面：土壤的 pH 值、水分、粒度等。然而，人们可能只测量其中的一部分，因此还有其他因素（养分含量等）可能有助于土壤条件的概念。在这种情况下，复合材料会有误差，因此被称为潜在复合材料。

与潜在变量相比，复合变量实际上非常容易估计：它只是其指标的总和，因此称为复合变量。

指标求和的方式取决于它们是否具有相同的权重（固定综合）或不同的权重（统计综合）。前者可能类似于物种相对丰度。后者是我们在这里重点关注的，因为它在生态学中具有最实际的应用。

###### 24/07/03

[R 笔记：复现 Nature 论文中的 SEM 结构方程模型](https://mp.weixin.qq.com/s?__biz=MzI3ODE3NDU4MA==&mid=2650639877&idx=1&sn=3b8ad9b3cea993da038efebdd22229af)

> [Decoupling of soil nutrient cycles as a function of aridity in global drylands | Nature](https://www.nature.com/articles/nature12670)
>
> [Integrative modelling reveals mechanisms linking productivity and plant species richness | Nature](https://www.nature.com/articles/nature16524)

###### 24/07/15

[Causal Inference in R](https://www.r-causal.org/)

###### 24/07/19

[Preface | R for Calculus](https://dtkaplan.github.io/RforCalculus/preface.html)

前言：

微积分的本质是对数学函数的处理。微积分`calculus`与计算`calculate`来自相同词根，微积分的大部分主题都涉及对函数的计算。

R是函数式计算机语言；R生态系统

`mosaicCalc`包

数学和统计计算与文字处理的本质区别：求解、整合、统计摘要——形成操作链，需要表达操作链的步骤；最终产品不是唯一重要的东西，数学和统计计算中最终产品是一系列计算的结果，链中的每个步骤都要记录在案并可重复，以检查、更新、验证

计算机语言比自然语言容易得多，学习它是为了表达复杂的想法，以系统的方式表达、使用计算机的力量、增加对数学和统计思想的理解。

1 表示`represent`数学函数`mathematical functions`

1.1 数字`numbers`、数量`quantities`、名称`names`

数量`quantities`, 是数字`numbers`和维度（单位）`dimension`的综合；例如美元和欧元或平方米和平方英尺

使用数量的名称提醒单位，例如`income_per_year`、`family_income_euros_per_year`

上标和下标的命名是不可避免的，但在计算机程序中，需使用字符串

1.2 R语言函数

函数，参数，默认值

```r
as_daily_income <- function(yearly_income, duration = 365) {
  yearly_income / duration
}
```

1.3 有文化地使用参数

```r
dose <- 100 # mg
duration <- 10 # days
time_constant <- 4 # days
dose * exp(- duration / time_constant)
```

更好的做法，定义一个函数

```r
drug_remaining <- function(dose, duration, time_constant) {
  dose * exp(- duration / time_constant)
}
drug_remaining(dose = 100, duration = 10, time_constant = 4)
```

1.4 关于

!!! info
    [Project MOSAIC](https://www.mosaic-web.org/)

    [ProjectMOSAIC/mosaic：Project MOSAIC](https://github.com/ProjectMOSAIC/mosaic?tab=readme-ov-file)

    [ProjectMOSAIC/mosaicCalc: Calculus in R](https://github.com/ProjectMOSAIC/mosaicCalc)

2 绘图功能

2.1 绘制数学函数

函数是从输入到输出的转换，用于表示数量之间的关系

2.2 绘制两个变量的函数

图形是分层构造的，例如

```r
Housing = read.csv("http://www.mosaic-web.org/go/datasets/Income-Housing.csv")
gf_point( 
  CrimeProblem ~ Income, data=Housing ) %>%
  slice_plot(
    40 - Income/2000 ~ Income, color = "red")
gf_point(
  CrimeProblem ~ Income, data = Housing) %>% 
  slice_plot(
    40 - Income / 2000 ~ Income, color = "blue") %>%
  gf_lims(
    x = range(0,100000), 
    y=range(0,50))
gf_point(
  CrimeProblem ~ Income, data=Housing) %>%
  gf_labs(x= "Income Bracket ($US per household)/year",
          y = "Fraction of Households",
          main = "Crime Problem") %>%
  gf_lims(x = range(0,100000), y = range(0,50))
```

2.3 两个变量的图形函数

等高线图

```r
contour_plot(
  sin(2*pi*t/10)*exp(-.2*x) ~ t & x, 
  domain(t = range(0,20), x = range(0,10)))
```

三维图

```r
interactive_plot(
  sin(2*pi*t/10)*exp(-.5*x) ~ t & x, 
  domain(t = 0:20, x = 0:10))
```

3 参数和函数

3.5 无参数函数：样条曲线和平滑器

数学模型试图捕捉现实世界中的模式，模型比世界本身更容易研究和操作

函数用于重现、捕获、建模 数据中出现的模式

平滑器和样条曲线是两种通用函数，可以捕获数据中的模式，但没有简单的代数形式；摆脱函数必须始终有公式的观点

样条线和线性连接

```r
g1 = spliner(Volume ~ Girth, data = Cherry)
g2 = connector(Volume ~ Girth, data = Cherry)
slice_plot(g1(x) ~ x, domain(x = 8:18)) %>%
  slice_plot(g2(x) ~ x, color ="red") %>%
  gf_point(Volume ~ Girth, data = Cherry) %>%
  gf_labs(x = "Girth (inches)")
```

平滑器

```r
g3 <- smoother(Volume ~ Girth, data = Cherry, span=1.5)
gf_point(Volume~Girth, data=Cherry) %>%
  slice_plot(g3(Girth) ~ Girth) %>%
  gf_labs(x = "Girth (inches)")

g4 <- smoother(Volume ~ Girth, data=Cherry, span=1.0)
gf_point(Volume~Girth, data = Cherry) %>%
  slice_plot(g4(Girth) ~ Girth) %>%
  gf_labs(x = "Girth (inches)", y = "Wood volume")
```

多变量平滑器

```
g5 <- smoother(Volume ~ Girth+Height, 
               data = Cherry, span = 1.0)
gf_point(Height ~ Girth, data = Cherry) %>%
  contour_plot(g5(Girth, Height) ~ Girth + Height) %>%
  gf_labs(x = "Girth (inches)", 
          y = "Height (ft)", 
          title = "Volume (ft^3)")
```

4 求解

5 使用线性组合进行建模

6 将函数拟合到数据 模型拟合`model fitting`

------



