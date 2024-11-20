# HUANANZHI-X99TF-OC-9.1-EFI

配置：

+ 主板：[华南X99TF](http://www.huananzhi.com/more.php?lm=10&id=306)
  + BIOS 更新到官网版本 [22-09-16](http://www.huananzhi.com/attach/Drive/X99-TFDrive/X99-TFV3.0JX22-09-16.rar)
+ 独显：[GIGABYTE Radeon™ RX 580 GAMING 8G](https://www.gigabyte.com/tw/Graphics-Card/GV-RX580GAMING-8GD-rev-10-11-12#kf)
+ 内存：SAMSUNG DDR3 ECC 1866HZ  32G*2
+ CPU：[Intel Xeon E5-2666 v3](https://www.cpubenchmark.net/cpu.php?cpu=Intel+Xeon+E5-2666+v3+%40+2.90GHz&id=2471)
+ 存储：Intel P660 1TB PCI-E 3.0x4
+ WIFI及蓝牙：[BCM 943602CS](https://item.taobao.com/item.htm?_u=k8646pv53d9&id=569121658326&pisk=fmrnr8s-EfOXF_8iINoCzk-yP9QtRpi747K-w0hP7fl1FeLdd4kzE7q8J8l-q7VuZX3PODEus-wRduBIYgDzM5m8pXh8sTVLF3CCPDKyZWwVOJhRducrsWPoP9G-abV8UyBODieQd0izZsIADJoDo3enL0lebTk-UbkPCySzu0iPM_Y942smVS_Fy4ke7AlsEY8E47oZbYHq4v8EUOcZExTyT7PzQOD-KbkyY4oNbxkS4eky8cuZexLeaXuy7OD-_H-aRIlr4qZN9z0r66lGPlMn-bx-_30Tbn3EgsGwq3cnp2YLLfxy4l4trQpIiGAZ68ybzVqk11n7BrVuz5Wy4b4ZnSmUS1-n4Dk0ODrF6Bmojxg0rWC64XU0Q50YXCKxbkV3YVmV4oTwuFNWVAW8bUTS8AMiM2tAHLCg-CjCIOA3C2ksHIBGIU9K8AMi-OXMtruECxCf.&spm=a1z09.2.0.0.1c612e8dZMUQlQ&skuId=4369136840865)
+ 系统版本：Sequoia 15.1

## BIOS设置

ACPI Settings>ACPI Sleep State=S3(开启S3睡眠支持，需要的童学可以开启）

CSM Configuration>CSM Support=Disabled(首先要把Boot Option Filter=UEFI Only，这里改完重启重新进BIOS才能改上一步）

NCT5532D Super I0 Configuration>Restone AC Power Loss=Powen On(这个是开启来电自启功能）

## OpenCore 设置

OC版本更新为9.1。机型有Mac Pro7,1，Mac Pro7,1的已自定义内存，能启用显示ECC，我是128G内存，内存比我大的（然后，比我小的可直接食用），可自行在Platformlnfo>Memory修改，Size（即容量）按你实际减少，总容量加起来为你实际的容量即可，Speed（即频率）按实际的填写，SeriaNumber、PartNumber、DeviceLocato这些可以随便填，也可以按你实际内存型号信息等填写，如是DDR4的，需将DataWidth改成64，Type改成26，非ECC内存的请把ErrorCorrection改成1或2（非ECC的建议改2）。我的自己修改一些装*参数，实际上没图的频率那么高，哈哈。

如不懂的怎么自定义的，请移至https://bbs.pcbeta.com/viewthread-1872987-5-1.html  此大神教程。或是在Kernel里添加SystemProfilerMemoryFixup.kext。

这次WhateverGreen.kext仍是用1.5.7，不过这次的WEG版本是是LEE大神魔改的，更高的版本我就没去测试了，此EFI里有加了5000、6000系列独显的注释，同时也有单独针对6600或6600xt部分品牌卡出现显示输出口异常问题：如只有一个DP口有输出，或亮屏速度太慢等问题简单、半解决方法。

另外我仍继续用DSDT-HUANANZHI.aml来解决声卡驱动，没太多时间去折腾，反正也不用WIN，用WIN也是直接用PD，所以不存在双系统引导WIN时卡ACPI问题。有需的伙伴自取，哈哈。
