
## Intel

[Installing Client GPUs — Intel® software for general purpose GPU capabilities documentation](https://dgpu-docs.intel.com/driver/client/overview.html)

- `Debian 12`参考`Ubuntu 22.04LTS`安装方法

## GNOME

[AppIndicator and KStatusNotifierItem Support - GNOME Shell Extensions](https://extensions.gnome.org/extension/615/appindicator-support/)

- 状态栏图标，方便例如FDM或CV等应用使用

[Customize IBus - GNOME Shell Extensions](https://extensions.gnome.org/extension/4112/customize-ibus/)

- 对iBus输入法的字体字号和背景等进行设置

## IME

[RIME | 中州韻輸入法引擎](https://rime.im/)

- [rime/plum: 東風破 /plum/: Rime configuration manager and input schema repository](https://github.com/rime/plum)
- [yanhuacuo/rimetool: 中州韵助手（重构版）](https://github.com/yanhuacuo/rimetool) | 有对应的词库，但目前尚存在Bug
- [Mark24Code/rime-auto-deploy: Rime输入法安装脚本，让一切更轻松。Make using Rime easy.](https://github.com/Mark24Code/rime-auto-deploy) | 当前方案
- [iDvel/rime-ice: Rime 配置：雾凇拼音 | 长期维护的简体词库](https://github.com/iDvel/rime-ice) | [Rime 配置：雾凇拼音 - Dvel's Blog](https://dvel.me/posts/rime-ice/)
- [fkxxyz/rime-cloverpinyin: 🍀️四叶草拼音输入方案，做最好用的基于rime开源的简体拼音输入方案！](https://github.com/fkxxyz/rime-cloverpinyin)

## Download

FDM：[Free Download Manager - 從網路下載任何東西](https://www.freedownloadmanager.org/zh/)

qBittorrent Enhanced: [c0re100/qBittorrent-Enhanced-Edition: [Unofficial] qBittorrent Enhanced, based on qBittorrent](https://github.com/c0re100/qBittorrent-Enhanced-Edition)

## Terminal

- 终端出现`（END）`，输入`q`退出并进行下一步
- 搜索包含特定字段的包，例如安装前缀为`libxcb`的包：`sudo apt search libxcb*`
- 拔出移动设备前，查看是否有大量数据写入未完成`cat /proc/meminfo|grep -i Dirty`
- 提示缺少特定文件时，可使用类似`cp ~/lib/R/modules/lapack.so ~/lib/R/modules/libRlapack.so`的语句将已有的其他地方的文件复制到所需位置，或使用符号链接或称软链接`ln -s`

bash补全: [scop/bash-completion](https://github.com/scop/bash-completion/)

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

## Office

[winunix/wps-office-fonts: TTF Fonts to WPS Office](https://github.com/winunix/wps-office-fonts/tree/master)

- 可将`Windows`中字体复制并安装，相当一部分其他来源的文档依赖这些字体

## VMware

[Build host vmware kernel modules - VI-Toolkit](https://wiki.vi-toolkit.com/index.php/Build_host_vmware_kernel_modules) | `sudo apt-get install linux-headers-$(uname -r)`

## Software

[Flatpak—the future of application distribution](https://flatpak.org/setup/Debian)

## More

[git鉴权失败问题 以及每次clone 都要输入用户名密码问题_git clone 鉴权失败-CSDN博客](https://blog.csdn.net/qq_45495460/article/details/125077989)