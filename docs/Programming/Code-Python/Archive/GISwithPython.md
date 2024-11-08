---
date: 2024-03-02
---

[Geoprocessing with Python [Book]](https://www.oreilly.com/library/view/geoprocessing-with-python/9781617292149/)

[Python 与开源GIS ——数据处理、空间分析与地图制图](https://book.sciencereading.cn/shop/book/Booksimple/show.do?id=B97098511F4AF9084E053020B0A0AA3EE000)

> [Python与开源GIS：数据处理、空间分析与地图制图 — Python与开源GIS 文档](https://www.osgeo.cn/pygis/index.html)

[R](https://mirrors.tuna.tsinghua.edu.cn/CRAN/bin/windows/base/) | [Rtools](https://mirrors.tuna.tsinghua.edu.cn/CRAN/bin/windows/Rtools/) | [RStudio](https://posit.co/downloads/)

[conda-forge/miniforge: A conda-forge distribution.](https://github.com/conda-forge/miniforge)

[Welcome to Mamba’s documentation! — documentation](https://mamba.readthedocs.io/en/latest/index.html)

- 安装Miniforge时，安装选项选择前三个，便于在RStudio GUI中设置Conda

```r
>>> quit
# 在RStudio中退出Python终端
> reticulate::repl_python()
# 在RStudio中从r终端到python终端切换
```

- Miniforge设置Tuna镜像

[anaconda | 镜像站使用帮助 | 清华大学开源软件镜像站 | Tsinghua Open Source Mirror](https://mirrors.tuna.tsinghua.edu.cn/help/anaconda/)

```shell
conda config --set show_channel_urls yes
# 生成.condarc文件
```

- 使用Miniforge安装所需软件包

```shell
conda create -y -n pygis python=3.12
# 创建名为pygis的conda环境，并安装python3.12
conda activate pygis 
# 切换到虚拟环境
conda install numpy scipy
conda install matplotlib scikit-learn
conda install gdal pyproj
# 安装书中对应软件包
python
pip install folium spectral
# 部分软件包需pip安装
conda activate base
conda create -y -n spyderide spyder
# 创建名为spyderide的conda环境，并安装spyder
# 使用RStudio输出图像时无法调整
conda env list
# 查看当前运行的环境和全部环境
```

- 配置CUDA、CUDnn和PyTorch

添加nvidia源镜像`https://mirrors.sustech.edu.cn/anaconda-extra/cloud/`，来源：[SUSTech Open Source Mirrors](https://mirrors.sustech.edu.cn/)

[windows系统下如何确认CUDA和CUDNN都安装成功了_windows 确定是否安装了cuda-CSDN博客](https://blog.csdn.net/qq_35768355/article/details/132985948)

```shell
nvidia-smi
# 检查显卡驱动和CUDA支持版本
conda create -y -n pytorch cuda=12.1 -c nvidia
nvcc -V
# 切换环境后，检查CUDA是否安装
conda install cudnn
conda install pytorch torchvision torchaudio pytorch-cuda=12.1 -c pytorch -c nvidia
# 完成后进入Python中检查是否安装成功
```

- WSL2，Ubuntu安装Conda

[旧版 WSL 的手动安装步骤 | Microsoft Learn](https://learn.microsoft.com/zh-cn/windows/wsl/install-manual)

[GNU nano 2：Linux上的DOS格式或Mac格式 - 码农俱乐部 - Golang中国 - Go语言中文社区](https://mlog.club/article/4193140)

> `Ctrl+O`然后`Enter`确认保持文件，`Ctrl+X`退出

```shell
wsl --list -v
wsl --shutdown
wsl --update
# 关闭虚拟机后，更新到最新的WSL
ubuntu2004 config --default-user root
# 设置默认用户为根用户
sudo apt update
# 更新软件包信息
sudo apt upgrade
# 更新软件包
wget -c https://mirrors.tuna.tsinghua.edu.cn/anaconda/miniconda/Miniconda3-latest-Linux-x86_64.sh
# 下载Miniconda
bash Miniconda3-latest-Linux-x86_64.sh
# 点击Enter，之后点击Page Down键翻页
yes
# 同意许可证，然后点击Enter
source ~/.bashrc
# 显示(base)即安装成功
cat ~/.condarc
# 查看镜像
sudo nano ~/.condarc
# 修改镜像源
```

- geemap(Python) 和 rgee(R) 安装

[geemap](https://geemap.org/) | 该链接安装部分内容较旧，不宜参考

[1. Introducing GEE and Geemap — Geospatial Data Science with Earth Engine and Geemap](https://book.geemap.org/chapters/01_introduction.html#installing-with-conda) | 经测试可用

```shell
conda create -n gee python
conda activate gee
conda install -c conda-forge geemap
conda install -c conda-forge mamba
mamba install -c conda-forge pygis

jupyter lab
# 进入web页面，也可在RStudio中运行
```

```Python
import os
os.environ['HTTP_PROXY'] = 'http://127.0.0.1:10809'
os.environ['HTTPS_PROXY'] = 'http://127.0.0.1:10809'
# 设置代理，如果rgee运行失败也需再次运行
import ee
ee.Authenticate()
# 此时要求输入验证代码
ee.Initialize(project='ee-furuyakotoko-240104')
# 需填入对应的项目名
# 如果显示错误，多重复几次，概率为网络延迟问题

import geemap

Map = geemap.Map()
Map
```

```r
install.packages("r.proxy")
r.proxy::proxy()
# 在R中设置代理，初次使用需输入address:port

# &gt; r.proxy::proxy()
# This maybe the first time proxy4you be load.
# Please complete below configrations:)
# Default setting can be accessed by Enter with nothing
# [socks5 proxy] {Default as 127.0.0.1:7890} (address:port): 127.0.0.1:10808
# [https proxy] {Default as 127.0.0.1:7890} (address:port): 127.0.0.1:10809
# [http proxy] {Default as 127.0.0.1:7890} (address:port): 127.0.0.1:10809

# r.proxy::noproxy()

library(rgee)
ee_Initialize()
db &lt;- 'CGIAR/SRTM90_V4'
image &lt;- ee$Image(db)
image$bandNames()$getInfo()
# 运行后显示一行语句即说明可正常运行
```

- PIE-Engine Python

[PIE-Engine 遥感与地理信息云服务平台](https://engine.piesat.cn/engine-studio/code-development)

- GwP书中相关Python文件的安装

```
pip install ospybook-latest.zip --user
```

- 安装jupyter notebook

在Conda中的jupyter版本不支持所用的Python 3.12.2，使用pip安装

```shell
pip install jupyterlab
pip install notebook

jupyter notebook
# 启动jupyter notebook
```

- 安装Basemap

Conda 默认频道的Basemap对应的Python版本较低，建议单独安装

```shell
conda create -y -n pybasemap basemap
```

测试是否安装成功，此方法安装后未出现[在Anaconda中Basemap安装教程_anaconda安装basemap库-CSDN博客](https://blog.csdn.net/weixin_54822781/article/details/121415432) 中的部分问题

```python
import matplotlib.pyplot as plt
from mpl_toolkits.basemap import Basemap
plt.figure(figsize=(10, 6))
m = Basemap()
m.drawcoastlines()
plt.show()
```

- 安装rasterio

[GitHub - rasterio/rasterio: Rasterio reads and writes geospatial raster datasets](https://github.com/rasterio/rasterio)