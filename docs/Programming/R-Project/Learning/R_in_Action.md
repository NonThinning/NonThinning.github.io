
## Cha.1

建议设置项

- `General -> Workspace`取消勾选Re...并设置Sa...为Never
- `Code -> Saving -> Ser... -> Default...`选择UTF-8
- `Appearance -> Editor theme:`选择Dracula
- `Packages -> Package Management`修改CRAN为国内镜像
- `Python`使用conda创建的虚拟环境

操作提醒

- `Tab`补全函数
- `Ctrl+Enter`逐行运行
- 运行时出现控制台出现`+`，输入语句不完全，可使用`Esc`退出或在控制台补全

```r
ls() # 列出对象
rm() # 移除对象
options() # 例如用于设置timeout
dir.create() # 创建文件夹（新目录）
library() # 显示库中包
.libPaths() # 显示库位置
```

```r
class() # "numeric" "character" "list"
mode() # class()和mode()在对tibble数据框使用时结果会有较大差异 数据框各列的模式mode()可以不同
typeof() # 数据类型 "double" "character"
str() # 提供信息
attributes() # str()和attributes()在对tibble数据框使用时结果会有较大差异
c() # vector 向量 "numeric" "character" "logical" ...
matrix() # matrix 矩阵，二维数组 "matrix"
array() # array n维数组
factor() # factor "factor" 用于分类变量（名义、顺序） 可根据实际值创建新的值标签
data.frame() # 数据帧（数据框） 2维表格，由多个列组成，每个列是一个向量 行表示观测值，列表示变量
list() # list 列表 "list"
```

```r
rownames() # 行名，通过row.names()设置
with()
cbind() # 按列合并对象
rbind() # 按行合并对象
na.omit() # 删除缺失值的行
```

```r
mean() # 均值、平均数
sd() # 标准差
cor() # 相关性
summary() # 统计概要
```

