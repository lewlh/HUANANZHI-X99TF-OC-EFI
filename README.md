# HUANANZHI-X99-TF-OC-EFI

## 电脑配置

+ CPU: Intel E5-2666-v3
  + [cpubenchmark](https://www.cpubenchmark.net/cpu.php?cpu=Intel+Xeon+E5-2666+v3+%40+2.90GHz&id=2471)
  + [techpowerup](https://www.techpowerup.com/cpu-specs/xeon-e5-2666-v3.c2876)
+ 主板：[华南金牌-X99-TF](http://www.huananzhi.com/more.php?lm=10&id=306)
  + BIOS: [X99-TFV3.0JX22-09-16.rar](http://www.huananzhi.com/attach/Drive/X99-TFDrive/X99-TFV3.0JX22-09-16.rar)
+ 独显：[XFX GTS RX 580 XXX 8 GB](https://www.techpowerup.com/gpu-specs/xfx-gts-rx-580-xxx-8-gb.b4480)
+ 内存：SAMSUNG DDR3 ECC REG 1866HZ 32GB*3;
+ 存储：[Intel 660p QLC 1TB NVMe](https://www.techpowerup.com/ssd-specs/intel-660p-1-tb.d436)
+ WIFI及蓝牙：BCM943602CS
+ SASRaid: [浪潮2308 6G直通卡IT模式](https://item.taobao.com/item.htm?_u=n8646pve6e7&id=772642815737&pisk=gJ971SqXLep4opUDq4nVl1-I1YWQdeMZpkspjHezvTBROJKy5MyFTbjQdZttqalnZeOXJEfPyw5FdMTNo3yEq3oIdHKOy9RPzML2REVyzp7euvtM5_yyvprkiF-TULllLJ6lK93Z7Akaq3Xhp70uXD4uMMs-LuedJTXY7aZr6AkwqnZP2c-xQLkC4nsg9JLdwseAbZIRJJI-csINv9eR98FYkZjdp9IdySIAxM4L28LLkrICbJILp_eYkMIGpgLdy-nfxHqLOGF5x3iVYBzivJzC5ZwLpKsx-w-Sg8S6EgZG53_jWN9VVFb92ZwLpaSQiVxpJ2wFBCYXd1BEd-XyfIBAVIiLMaC6wCBJdVaJD1Ow6s9nI8x5saBfmpu0ewOv9L5lKz35cLt6dBsrbR764NPQc12CcNojcWVnrLTiBTLV-t5RmgmrcmaAt_IccimjcWchwijo5mibPvf..&skuId=5391221020198&spm=a1z09.2.0.0.661b2e8dAESMVA)
+ 系统版本：Ventura 13.7.2 (22H313)

## OpenCore

### MacOS 系统

我已经将 OpenCore 更新到 1.0.3 最新版本，当然也想第一时间尝试安装最新的 Sequoia 15.1.1 系统，但是失败了，Sonoma 14.7.2 也是一样卡在安装的过程中，我没有找到解决的办法，最后只能安装 Ventura 13.7.2 系统了。

```bash
                    'c.          lewlh@lewlhdeMac-Pro.local
                 ,xNMM.          ------------------------------------
               .OMMMMo           OS: macOS 13.7.2 22H313 x86_64
               OMMM0,            Host: Hackintosh (SMBIOS: MacPro7,1)
     .;loddo:' loolloddol;.      Kernel: 22.6.0
   cKMMMMMMMMMMNWMMMMMMMMMM0:    Uptime: 2 mins
 .KMMMMMMMMMMMMMMMMMMMMMMMWd.    Packages: 25 (brew)
 XMMMMMMMMMMMMMMMMMMMMMMMX.      Shell: zsh 5.9
;MMMMMMMMMMMMMMMMMMMMMMMM:       Resolution: 3008x1692@2x
:MMMMMMMMMMMMMMMMMMMMMMMM:       DE: Aqua
.MMMMMMMMMMMMMMMMMMMMMMMMX.      WM: Quartz Compositor
 kMMMMMMMMMMMMMMMMMMMMMMMMWd.    WM Theme: Blue (Dark)
 .XMMMMMMMMMMMMMMMMMMMMMMMMMMk   Terminal: iTerm2
  .XMMMMMMMMMMMMMMMMMMMMMMMMK.   Terminal Font: 0xProtoNFM-Regular 12
    kMMMMMMMMMMMMMMMMMMMMMMd     CPU: Intel Xeon E5-2666 v3 (20) @ 2.90GHz
     ;KMMMMMMMWXXWMMMMMMMk.      GPU: AMD Radeon RX 580
       .cooc,.    .,coo:.        Memory: 9383MiB / 98313MiB

```

### 关于内存

Mac Pro7,1 需要自定义内存，博主使用 DDR3 ECC 1866Hz 内存，三根总容量为 96 GB，如你需要修改内存的参数，请参考一下文档：

+ [修复MacPro7,1内存错误](https://sumingyd.github.io/OpenCore-Post-Install/universal/memory.html)
+ [PlatformInfo: Memory 属性](https://oc.skk.moe/10-platform-info.html#10-4-Memory-%E5%B1%9E%E6%80%A7)

### 关于 XFX 显卡 UEFI 启动问题

博主一开始买的是GIGABYTE Radeon™ RX 580 GAMING 8G 的N手矿卡，用了一个月就坏了，幸亏淘宝店家给换了同参数的显卡 XFX GTS RX 580 XXX 8 GB，在 win11 下面运行正常，在安装黑苹果的时候才发现这货有问题。在 OpenCore 安装指南中，明确指出 XFX(讯景) 显卡 vBios 存在问题，导致关闭 CSM 下，显卡无法正常使用。后来查阅了互联网的资料，找到了通过升级、刷新 GOP 的方式解决这个问题的方法，最后验证可以顺利安装 MacOS 系统。

+ [XFX RX580+爱国家Z97在纯UEFI环境启动时黑屏问题一例的解决方法](https://www.bilibili.com/opus/769990819214000227)
+ [GOP_Updater工具下载链接](https://e1.pcloud.link/publink/show?code=kZUzB8ZLrwnBMPHdzh9ibVNRd8uU01GcX77#returl=https%3A//e1.pcloud.link/publink/show%3Fcode%3DkZUzB8ZLrwnBMPHdzh9ibVNRd8uU01GcX77&page=login)

### 关于WIFI以及蓝牙

一开始我是按照 [OpenCore安装指南->收集文件->Kexts->WiFi 和 蓝牙](https://sumingyd.github.io/OpenCore-Install-Guide/ktext.html#wifi-%E5%92%8C-%E8%93%9D%E7%89%99)配置相关驱动，wifi 使用正常，但是蓝牙总是会莫名奇妙地成功连接之后过一会儿就自动断开。结果的过程中我以为是USB没有映射的问题，使用[USB 修复](https://sumingyd.github.io/OpenCore-Post-Install/usb/#%E4%B8%BA%E4%BB%80%E4%B9%88%E4%BD%A0%E8%A6%81usb%E6%98%A0%E5%B0%84)重新映射了USB，但是蓝牙的问题依然出现。后来查看外文的资料，有个回答说这个型号的蓝牙，实际是免驱的，所以我就把相关的 kexts 删掉后，果然就没有这个问题了，WIFI、蓝牙、隔空投送都使用正常，真的是非常意外！

### 声卡问题

之前参考的 EFI 作者提到：

> 另外我仍继续用DSDT-HUANANZHI.aml来解决声卡驱动，没太多时间去折腾，反正也不用WIN，用WIN也是直接用PD，所以不存在双系统引导WIN时卡ACPI问题。有需的伙伴自取，哈哈。

我继续使用声音其实并没有什么问题，所以就没有把 DSDT-HUANANZHI 删掉。如果你要修改，可以参考一下文档：

+ [ALC892](https://github.com/acidanthera/AppleALC/blob/master/Resources/ALC892/Info.plist)
+ [修复AppleALC的音频](https://sumingyd.github.io/OpenCore-Post-Install/universal/audio.html)

## BIOS 设置

+ ACPI Settings>ACPI Sleep State=S3(开启S3睡眠支持，需要的童学可以开启）
+ CSM Configuration>CSM Support=Disabled(首先要把设置 Boot Option Filter=UEFI Only, Video = UEFI,这里改完重启重新进BIOS才能改上一步）
+ NCT5532D Super I0 Configuration>Restone AC Power Loss=Powen On(这个是开启来电自启功能）

## Issues

目前遗留的问题有两个：

+ SASMegaRAID.kext 无法驱动浪潮2308 6G直通卡IT模式, SAS 硬盘无法识别。在系统信息里面找不到这个 Raid 卡的信息，但是在 Hackintool 中能看到 Raid 卡的信息。
+ ~~[Issue1](https://github.com/lewlh/HUANANZHI-X99TF-OC-EFI/issues/1): 系统进入休眠状态后，无法重新唤醒，需要强行关机后，才能重新正常启动。~~

## ChangeLogs

+ 20250118
  + 删除`SSDT-CPUM.aml`解决系统进入休眠状态后，无法重新唤醒的问题 [Issue1](https://github.com/lewlh/HUANANZHI-X99TF-OC-EFI/issues/1);
+ 20250110
  + 升级 OpenCore 0.9.1 -> 1.0.3;
    + WhateverGreen.kext 使用官方版本;
  + 由于 BCM943602CS 免驱，因此移除了 bcm 相关 kext 驱动;

## Reference

+ [Hackintool](https://github.com/benbaker76/Hackintool)
+ [OCAuxiliaryTools](https://github.com/ic005k/OCAuxiliaryTools)
+ [国光的黑苹果安装教程](https://apple.sqlsec.com/)
+ [OpenCore的安装指南](https://sumingyd.github.io/OpenCore-Install-Guide/)
+ [OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/prerequisites.html)
+ [OpenCore 简体中文参考手册](https://oc.skk.moe/)
+ [Driver for LSI MegaRAID SAS family](https://www.insanelymac.com/forum/topic/285197-driver-for-lsi-megaraid-sas-family/)
+ [osx-goodies](https://github.com/dukzcry/osx-goodies)
+ [10.15.5黑苹果上SAS氦气硬盘手记（附控制卡驱动)](https://post.smzdm.com/p/ag87gxk3/)
+ [黑苹果系统(MacOS)之网卡篇](https://juejin.cn/post/7324980656994484258)
+ ![华南金牌主板诊断卡代码](/sources/华南金牌主板诊断卡代码.jpg)
+ ![华南金牌主板诊断吗问题汇总](/sources/华南金牌主板诊断吗问题汇总.png)
