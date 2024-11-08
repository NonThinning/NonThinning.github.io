---
date: 2024-11-08
---

[fortls](https://fortls.fortran-lang.org/index.html)

[Fortran Package Manager — Fortran Package Manager](https://fpm.fortran-lang.org/index.html)

[Fortran 编程语言 — Fortran Programming Language](https://fortran-lang.org/zh_CN/)

[Fortran Wiki](https://fortranwiki.org/fortran/show/HomePage)

[Modern Fortran - Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=fortran-lang.linter-gfortran)

[fortran-lang/stdlib: Fortran Standard Library](https://github.com/fortran-lang/stdlib)

## Configuration

```shell
conda create -y -n gfort
conda install m2w64-toolchain -c msys2
gfortran --version
```

```fortran
program hello
    integer :: i
    i = 0
    i = i + 1
    i = i + 1
    print *, 'Hello, World!'
    print *, 'Hi again'
  end program hello
```

```shell
gfortran -g "C:\Users\Qiao\Desktop\test.f95" -o "C:\Users\Qiao\Desktop\test.exe"
```

------

- MSYS2 Fortran

[msys2 | 镜像站使用帮助 | 清华大学开源软件镜像站 | Tsinghua Open Source Mirror](https://mirrors.tuna.tsinghua.edu.cn/help/msys2/)

[Terminals - MSYS2](https://www.msys2.org/docs/terminals/)

[Pending Package Updates - MSYS2 Packages](https://packages.msys2.org/queue)

```shell
msys2 -ucrt64
msys2 -defterm -here -no-start -msys
msys2 -defterm -here -no-start -ucrt64
```

```bash
cd /home/Qiao
cd /c/Users/Qiao/Documents/MSYS2
```

```bash
pacman -Suy
pacman -S mingw-w64-ucrt-x86_64-toolchain
pacman -S mingw-w64-ucrt-x86_64-gcc-fortran
gfortran --version
```

```shell
msys2 -defterm -here -no-start -mingw64
```

```bash
pacman -S git mingw-w64-x86_64-gcc-fortran mingw-w64-x86_64-fpm
pacman -S mingw-w64-x86_64-fortran-stdlib
pacman -S mingw-w64-x86_64-toolchain
pacman -S python-pip
```

```bash
# WSL 安装 SageMath；mamba安装可能会出现sage.all错误
conda create -y -n sage sage -c conda-forge
```

- 配置 Modern Fortran

```shell
# 在conda base环境下
pip install fortls fprettify
```

Fortran › Linter: Compiler Path
`C:\Users\Qiao\scoop\apps\msys2\current\mingw64\bin\gfortran.exe`

Fortran › Formatting: Formatter
`fprettify`

Fortran › Formatting: Path
`C:\Users\Qiao\miniforge3\Scripts\fprettify.exe`

Fortran › Fortls: Path
`C:\Users\Qiao\miniforge3\Scripts\fortls.exe`

------

[用 VS Code + MSYS 搞定 Windows 上的 Fortran 开发](https://stblog.penclub.club/posts/Fortran/)

[Welcome to Python.org](https://www.python.org/)

```shell
scoop install msys2
```

[将MSYS2 MinGW集成到Windows终端_msys2 win7-CSDN博客](https://blog.csdn.net/witton/article/details/131052515)

```shell
# msys2 terminal 配置
%USERPROFILE%\scoop\apps\msys2\current\msys2_shell.cmd -defterm -no-start -use-full-path -here -mingw64

%USERPROFILE%

%USERPROFILE%\scoop\apps\msys2\current\mingw64.ico
```

[MSYS2 - USTC Mirror Help](https://mirrors.ustc.edu.cn/help/msys2.html)

```bash
sed -i "s#mirror.msys2.org/#mirrors.ustc.edu.cn/msys2/#g" /etc/pacman.d/mirrorlist*
pacman -Sy
pacman -S mingw-w64-x86_64-gcc-fortran
pacman -S mingw-w64-x86_64-gdb
```

添加环境变量`%USERPROFILE%\scoop\apps\msys2\current\mingw64\bin`

```shell
gfortran --version
```

[Get Started - fortls](https://fortls.fortran-lang.org/quickstart.html)

配置fortls和fprettify的path

["Had trouble installing fortls, please install manually" . How to install manually without pip? - Help / Visual Studio Code - Fortran Discourse](https://fortran-lang.discourse.group/t/had-trouble-installing-fortls-please-install-manually-how-to-install-manually-without-pip/6721/9)

> ` "fortran.fortls.path": "<your prefix root>/Scripts/fortls.exe"
`

```
# 在conda base环境安装
C:\Users\Qiao\miniforge3\Scripts\fprettify.exe
C:\Users\Qiao\miniforge3\Scripts\fortls.exe
```

[MSYS2 + VSCode 在 windows 上搭建 C/C++ 开发环境 | Keep](https://wjdready.github.io/2023/09/25/auto/40/MSYS2_VSCode_C_Cpp%E7%8E%AF%E5%A2%83%E6%90%AD%E5%BB%BA/) | 设置 C_Cpp 编译器路径

[Visual Studio Code 中的 C++ 和 MinGW-w64 入门](https://code.visualstudio.com/docs/cpp/config-mingw)

最终配置文件参照[用 VS Code + MSYS 搞定 Windows 上的 Fortran 开发](https://stblog.penclub.club/posts/Fortran/)

------

