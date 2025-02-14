
[Debian 中文社区](https://debiancn.org/)

## SWAP

[How to Fix Debian Slow Boot After Partition Resize or “No Matching Swap Device is Available” Error – The Linux Notes](https://thelinuxnotes.com/index.php/how-to-fix-debian-slow-boot-after-partition-resize-or-no-matching-swap-device-is-available-error/)

- 扩展SWAP分区后需修改Initramfs配置

## Fonts

[Nerd Fonts - Iconic font aggregator, glyphs/icons collection, & fonts patcher](https://www.nerdfonts.com/font-downloads)

[JetBrains Mono: A free and open source typeface for developers | JetBrains: Developer Tools for Professionals and Teams](https://www.jetbrains.com/lp/mono/)

## Intel

[Installing Client GPUs — Intel® software for general purpose GPU capabilities documentation](https://dgpu-docs.intel.com/driver/client/overview.html)

- `Debian 12`参考`Ubuntu 22.04LTS`安装方法

[tiagovignatti/intel-gpu-tools: upstream is at http://cgit.freedesktop.org/xorg/app/intel-gpu-tools/](https://github.com/tiagovignatti/intel-gpu-tools) | GPU监测

## GNOME

[AppIndicator and KStatusNotifierItem Support - GNOME Shell Extensions](https://extensions.gnome.org/extension/615/appindicator-support/)

- 状态栏图标，方便例如FDM或CV等应用使用

[Customize IBus - GNOME Shell Extensions](https://extensions.gnome.org/extension/4112/customize-ibus/)

- 对iBus输入法的字体字号和背景等进行设置

[Clipboard Indicator - GNOME Shell Extensions](https://extensions.gnome.org/extension/779/clipboard-indicator/)

[system-monitor-next - GNOME Shell Extensions](https://extensions.gnome.org/extension/3010/system-monitor-next/)

[Vitals - GNOME Shell Extensions](https://extensions.gnome.org/extension/1460/vitals/)

- [corecoding/Vitals: A glimpse into your computer's temperature, voltage, fan speed, memory usage and CPU load.](https://github.com/corecoding/Vitals)

[Lunar Calendar 农历 - GNOME Shell Extensions](https://extensions.gnome.org/extension/675/lunar-calendar/)

[mjakeman/extension-manager: A utility for browsing and installing GNOME Shell Extensions.](https://github.com/mjakeman/extension-manager)

[Battery Health Charging](https://maniacx.github.io/Battery-Health-Charging/)

- [frederik-h/acer-wmi-battery：用于 Acer WMI 电池健康控制接口的 linux 内核驱动程序](https://github.com/frederik-h/acer-wmi-battery)

## Eumlator

⭐ [Waydroid | Android in a Linux container](https://waydro.id/) 

- Document: [Waydroid | Waydroid](https://docs.waydro.id/)
- Old: [anbox/anbox: Anbox is a container-based approach to boot a full Android system on a regular GNU/Linux system](https://github.com/anbox/anbox)
- Old: [OSBoxes - Virtual Machines for VirtualBox & VMware](https://www.osboxes.org/)
- 在缩小窗口后，移动窗口：点击`Alt+F7`，出现十字箭头，此时可更改窗口位置
- [casualsnek/waydroid_script: Python Script to add OpenGapps, Magisk, libhoudini translation library and libndk translation library to waydroid !](https://github.com/casualsnek/waydroid_script) | 当前存在部分错误 2024-01-12
- [spyoungtech/pyclip: Cross-platform Clipboard module for Python with binary support.](https://github.com/spyoungtech/pyclip) | 可选依赖项，无法用pipx处理

```bash
waydroid prop set persist.waydroid.width 480
waydroid prop set persist.waydroid.height 800
waydroid session stop
waydroid session start

```

## IME

[RIME | 中州韻輸入法引擎](https://rime.im/)

- [rime/plum: 東風破 /plum/: Rime configuration manager and input schema repository](https://github.com/rime/plum)
- [yanhuacuo/rimetool: 中州韵助手（重构版）](https://github.com/yanhuacuo/rimetool) | 有对应的词库，但目前尚存在Bug
- [Mark24Code/rime-auto-deploy: Rime输入法安装脚本，让一切更轻松。Make using Rime easy.](https://github.com/Mark24Code/rime-auto-deploy) | 当前方案
- [iDvel/rime-ice: Rime 配置：雾凇拼音 | 长期维护的简体词库](https://github.com/iDvel/rime-ice) | [Rime 配置：雾凇拼音 - Dvel's Blog](https://dvel.me/posts/rime-ice/)
- [fkxxyz/rime-cloverpinyin: 🍀️四叶草拼音输入方案，做最好用的基于rime开源的简体拼音输入方案！](https://github.com/fkxxyz/rime-cloverpinyin)
- [amzxyz/RIME-LMDG: LMDG - Language, Model, Dictionary, Grammar](https://github.com/amzxyz/RIME-LMDG)

## Download

FDM：[Free Download Manager - 從網路下載任何東西](https://www.freedownloadmanager.org/zh/)

qBittorrent Enhanced: [c0re100/qBittorrent-Enhanced-Edition: [Unofficial] qBittorrent Enhanced, based on qBittorrent](https://github.com/c0re100/qBittorrent-Enhanced-Edition)

## Terminal

- 终端出现`（END）`，输入`q`退出并进行下一步
- 搜索包含特定字段的包，例如安装前缀为`libxcb`的包：`sudo apt search libxcb*`
- 拔出移动设备前，查看是否有大量数据写入未完成`cat /proc/meminfo|grep -i Dirty`
- 提示缺少特定文件时，可使用类似`cp ~/lib/R/modules/lapack.so ~/lib/R/modules/libRlapack.so`的语句将已有的其他地方的文件复制到所需位置，或使用符号链接或称软链接`ln -s`

bash补全: [scop/bash-completion](https://github.com/scop/bash-completion/)

代替系统pip: [pipx](https://pipx.pypa.io/stable/)

intel gpu占用: `sudo apt install intel-gpu-tools`; 查看: `sudo intel_gpu_top`

安装oh-my-bash后恢复conda: `~/miniforge3/bin/conda init bash`

字体,使用apt安装: [GNU Unifont Glyphs](https://www.unifoundry.com/unifont/index.html)

## Grub

```bash
sudo nano /etc/default/grub
# 修改为 GRUB_TIMEOUT=0
# 修改为 GRUB_CMDLINE_LINUX_DEFAULT="quiet splash systemd.show_status=0 loglevel=0"
sudo update-grub
sudo apt install plymouth plymouth-themes
sudo plymouth-set-default-theme -R tribar
reboot
```

- `sudo apt install grub-customizer`
- `sudo apt-get install timeshift`

## Office

[winunix/wps-office-fonts: TTF Fonts to WPS Office](https://github.com/winunix/wps-office-fonts/tree/master)

- 可将`Windows`中字体复制并安装，相当一部分其他来源的文档依赖这些字体

## Password

[KeePass Password Safe](https://keepass.info/index.html) | Windows

- [KeePassXC Password Manager](https://keepassxc.org/) | Linux
- [KeePassDX](https://www.keepassdx.com/) | Android

## VMware

[Build host vmware kernel modules - VI-Toolkit](https://wiki.vi-toolkit.com/index.php/Build_host_vmware_kernel_modules) | `sudo apt-get install linux-headers-$(uname -r)`

## Package

[Repology](https://repology.org/)

[Flatpak—the future of application distribution](https://flatpak.org/setup/Debian)

- Ryujinx [Flathub - Apps for Linux](https://flathub.org/apps/io.github.ryubing.Ryujinx) | Mamory Limited, 安装deb版本可自动处理
- [Install Warehouse on Linux | Flathub](https://flathub.org/apps/io.github.flattool.Warehouse) | 管理Flatpak安装
- [prateekmedia/appimagepool: A simple, modern AppImageHub Client, powered by flutter.](https://github.com/prateekmedia/appimagepool/) | AppImage 下载和快捷方式管理

- [Linux捣鼓记录：安装flatpak软件仓库，更换国内镜像 - lwlnice - 博客园](https://www.cnblogs.com/lwlnice/p/18263967)

[Download | Nix & NixOS](https://nixos.org/download/#nix-install-linux)

- [NixOS & Flakes Book | Home Page](https://nixos-and-flakes.thiscute.world/)

## Tool

[calcurse: a text-based calendar and scheduling application](https://www.calcurse.org/) | Cli

[解决OBS在Linux下无法录屏_linux obs-CSDN博客](https://blog.csdn.net/izwmain/article/details/132865106) | 使用deb安装，flatpak存在权限问题

- [Debian 12 + KDE 屏幕共享失败问题解决 - Libitum - 博客园](https://www.cnblogs.com/libitum/p/18151341)

[CoolerControl / CoolerControl · GitLab](https://gitlab.com/coolercontrol/coolercontrol) | 风扇管理，笔记本不适用

[Mission Center](https://missioncenter.io/) | 任务中心、任务管理器

[Thunderbird](https://www.thunderbird.net/zh-CN/) | 邮件客户端

[Run Windows in a Bottle](https://usebottles.com/) | Wine 相关

[git鉴权失败问题 以及每次clone 都要输入用户名密码问题_git clone 鉴权失败-CSDN博客](https://blog.csdn.net/qq_45495460/article/details/125077989)

## Double System

[debian升级后Grub菜单中找不到Windows项（转） - 汉学 - 博客园](https://www.cnblogs.com/c2soft/articles/17804633.html)

- HP笔记本，使用DG可修改BIOS EIF启动顺序，并在Debian中启用`GRUB_DISABLE_OS_PROBER=false`
- Acer笔记本，使用DG修改失败，使用Easy UEFI修改成功，其他同上 [轻松管理EFI/UEFI启动项 & 管理EFI系统分区 & 修复EFI系统启动问题！- EasyUEFI](https://www.easyuefi.com/index-cn.html)

## Driver

[在 Debian 12 上安装 Nvidia 显卡驱动程序 | 晚花行乐](https://www.lfhacks.com/tech/debian-nvidia-driver/)