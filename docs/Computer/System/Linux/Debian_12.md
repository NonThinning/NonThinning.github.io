
[Installing Client GPUs — Intel® software for general purpose GPU capabilities documentation](https://dgpu-docs.intel.com/driver/client/overview.html)

- `Debian 12`参考`Ubuntu 22.04LTS`安装方法

## GNOME

[AppIndicator and KStatusNotifierItem Support - GNOME Shell Extensions](https://extensions.gnome.org/extension/615/appindicator-support/)

- 状态栏图标，方便例如FDM或CV等应用使用

## Download

FDM：[Free Download Manager - 從網路下載任何東西](https://www.freedownloadmanager.org/zh/)

qBittorrent Enhanced: [c0re100/qBittorrent-Enhanced-Edition: [Unofficial] qBittorrent Enhanced, based on qBittorrent](https://github.com/c0re100/qBittorrent-Enhanced-Edition)

## Terminal

- 终端出现`（END）`，输入`q`退出并进行下一步
- 搜索包含特定字段的包，例如安装前缀为`libxcb`的包：`sudo apt search libxcb*`
- 拔出移动设备前，查看是否有大量数据写入未完成`cat /proc/meminfo|grep -i Dirty`
- 提示缺少特定文件时，可使用类似`cp ~/lib/R/modules/lapack.so ~/lib/R/modules/libRlapack.so`的语句将已有的其他地方的文件复制到所需位置，或使用符号链接或称软链接`ln -s`

## Office

[winunix/wps-office-fonts: TTF Fonts to WPS Office](https://github.com/winunix/wps-office-fonts/tree/master)

- 可将`Windows`中字体复制并安装，相当一部分其他来源的文档依赖这些字体

## VMware

[Build host vmware kernel modules - VI-Toolkit](https://wiki.vi-toolkit.com/index.php/Build_host_vmware_kernel_modules) | `sudo apt-get install linux-headers-$(uname -r)`

## Software

[Flatpak—the future of application distribution](https://flatpak.org/setup/Debian)

## More

[git鉴权失败问题 以及每次clone 都要输入用户名密码问题_git clone 鉴权失败-CSDN博客](https://blog.csdn.net/qq_45495460/article/details/125077989)