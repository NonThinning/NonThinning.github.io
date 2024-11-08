+++
title = '链接剪藏：第〇〇三辑'
date = 2023-12-25T16:52:06+08:00
+++

使用`Hugo`和`Neocities`建立个人博客，使用`Scoop`安装组件。

[Hugo](https://gohugo.io/) | [Neocities](https://neocities.org/) | [Scoop](https://scoop.sh/)

1. 安装`Scoop`，以非管理员身份打开`PowerShell`并输入；通过`Scoop`安装`hugo`

```
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
Invoke-RestMethod -Uri https://get.scoop.sh | Invoke-Expression

scoop install main/git
scoop install main/hugo
scoop install main/ruby
scoop install main/msys2

ridk install
```

2. 安装`The Neocities CLI`，在上一步已安装依赖。

```
gem install neocities
neocities
```

3. 选定文件夹，此处以`D:\WebSite`为例，使用终端打开此目录，显示`PS D:\WebSite>`。以下建立了一个名为`thinning`的子文件夹，存放相关文件

```
hugo new site ./thinning
cd thinning
hugo new post/231221.md
cd themes
git clone https://github.com/spf13/hyde.git
cd ..
```

4. 在`D:\WebSite\thinning\content`文件夹，编辑`post/231221.md`文件；在`D:\WebSite\thinning\hugo.toml`内编辑，如下：

```
baseURL = 'https://nonthinning.neocities.org/'
languageCode = 'en-us'
title = 'Non Thinning Site'
theme = "hyde"

[params]
    description = "For programming, knowing how to learn is more important than knowing how to program. "
    copyright = "Copyleft (ɔ) 2024, NonThinning. "
```

5. 生成文件，上传至`neocities`；此处使用删除目录外内容的上传命令，初次登陆需输入<mark>用户名</mark>和密码

```
hugo
cd public
neocities push --prune .
```

<!--more-->

###### 读书

[书格 (shuge.org)](https://www.shuge.org/)

###### 学术

[PubScholar公益学术平台](https://pubscholar.cn/)

###### 资源

[异次元软件世界 - 软件改变生活！ (iplaysoft.com)](https://www.iplaysoft.com/)

###### 软件

[lstprjct/IDM-Activation-Script: IDM Activation & Trail Reset Script (github.com)](https://github.com/lstprjct/IDM-Activation-Script)

###### CSDN文章

[R语言根据研究区DEM数据进行子流域划分-CSDN博客](https://blog.csdn.net/2301_77925375/article/details/131389620)

###### 独立博客

[ZSYXY Meteorological workshop (yxy-biubiubiu.github.io)](https://yxy-biubiubiu.github.io/) | 气象相关

[伴夜 (aitimi.cn)](https://www.aitimi.cn/)

###### 网络安全

[丁爸网-首页 (dingba.top)](http://dingba.top/)

[美亚柏科官网 (300188.cn)](https://www.300188.cn/)

[FreeBuf网络安全行业门户](https://www.freebuf.com/)

[CN-SEC 中文网 | 聚合网络安全,存储安全技术文章,融合安全最新讯息](https://cn-sec.com/)

[中国人民公安大学出版社 (phcppsu.com.cn)](http://www.phcppsu.com.cn/)

###### 其他

[Google’s R Style Guide | styleguide](https://google.github.io/styleguide/Rguide.html)

[CPLOC: 编程语言开放社区理事会（Council of Programming Language Open Community，缩写“CPLOC”） (gitee.com)](https://gitee.com/ploc-org/CPLOC)

[CodeYell - 源码阅读交流平台](https://codeyell.com/)

[Abbreviations.com](https://www.abbreviations.com/) | 查询单词英文缩写

[卫星百科 - 灰机wiki (huijiwiki.com)](https://sat.huijiwiki.com/wiki/%E9%A6%96%E9%A1%B5)

------
