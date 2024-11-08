---
date: 2024-10-24
---

## Install

[Renegade Project | Renegade Project](https://renegade-project.tech/zh/home)

## Activation

[沧水的KMS服务 - Kms激活|Windows激活|Office激活|Windows下载|Office下载|搭建KMS服务器](https://kms.cangshui.net/) | [KMS 列表](https://www.coolhub.top/tech-articles/kms_list.html)

[zbezj/HEU_KMS_Activator](https://github.com/zbezj/HEU_KMS_Activator)

[Microsoft KMS Activation | vlmcsd](http://wind4.github.io/vlmcsd/) | [Wind4/vlmcsd: KMS Emulator in C (currently runs on Linux including Android, FreeBSD, Solaris, Minix, Mac OS, iOS, Windows with or without Cygwin)](https://github.com/Wind4/vlmcsd)
    
1. 运行`floppy`文件夹内虚拟机文件

> VMware 17 Keys [VMware Workstation Pro 17 full license keys. Collected and sorted out thousands of universal License Keys for all major versions of VMware Workstation Pro 17. x versions. · GitHub](https://gist.github.com/hegdepavankumar/e1c4c2d58d8698f69792d664d39bc402)
>
> `MC60H-DWHD5-H80U9-6V85M-8280D`

2. 记录 IPv4 address: `10.181.33.249`（根据实际IP修改此内容，只记录斜杠前面的数值）

3. 以管理员方式打开`PoweShell`

4. 输入 `slmgr -skms 10.181.33.249`

5. （更新激活时无需进行）输入 `slmgr -upk`

6. （更新激活时无需进行）输入 `slmgr -ipk NW6C2-QMPVW-D7KKK-3GKT6-VCFB2`（以Win10教育版GVLK为例）

7. 输入 `slmgr -ato`

8. 输入 `slmgr -dlv` 查看结果

9.  Office需要先清除许可证，后选择批量许可证，输入相同IP | [Office Tool Plus](https://otp.landian.vip/zh-cn/)

10. 可全程断网激活，如使用手机作为热点连接但不联网，此时也会出现需要的IP

11. 虚拟机仅有IPv6时，修改`虚拟机设置→网络适配器→NAT模式`

## Info

[HWiNFO - Free System Information, Monitoring and Diagnostics](https://www.hwinfo.com)

## Setting

[电脑常见问题汇总解答（病毒吧）](https://docs.qq.com/doc/DSU9mbmt5SHp2YmFS)

关闭 CompatTelRunner.exe

- 方法1：`taskschd.msc` → 任务计划程序库 → Microsoft → Windows → Application Experience → Microsoft Compatibility Appraiser → 禁用
- 方法2：`gpedit.msc` → 计算机配置 → 管理模板 → Windows组件 → 数据收集和预览版 → 允许遥测 → 策略设置 → 已禁用

关闭休眠

- 使用`powercfg -h off`关闭Windows休眠

仅登录Edge不登录系统

- `Windows管理工具→本地安全策略→本地策略→安全选项→账户：阻止Microsoft账户`，设置为第三个选项

命令行安装kaspersky

- `.\kav21.3.10.391abzh-Hans_26151.exe /pPRODUCTTYPE=kfa`
- KFA 激活码 `3SXCM-M9RJM-6985N-PWKP7` | `A23B5-44EXM-85MVF-KM2GQ`

## WSL

[旧版 WSL 的手动安装步骤 | Microsoft Learn](https://learn.microsoft.com/zh-cn/windows/wsl/install-manual)

[WSL 的基本命令 | Microsoft Learn](https://learn.microsoft.com/zh-cn/windows/wsl/basic-commands)

