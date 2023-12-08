# 0. 简介

本文件主要整理了自己安装Ubuntu所遇见的问题，及参考的Blog

**Key Words**: DELL, ALIENWARE, M17, RTX, Nvidia, Ubuntu 20.04/14.04


# 1. 安装参考教程 
 
>游戏本中安装Ubuntu很不友好，尤其是DELL笔记本。建议大家安装双系统

1. DELL笔记本双系统安装，系统配置额外需要做[修改](https://www.dell.com/support/article/zh-cn/sln308010/ubuntu-win10%E5%8F%8C%E7%B3%BB%E7%BB%9F%E5%AE%89%E8%A3%85%E6%95%99%E7%A8%8B?lang=zh)


2. 从U盘安装，可以参考官方[教程](https://ubuntu.com/tutorials/create-a-usb-stick-on-windows#1-overview)

3. 分区视频教程[参考](https://www.bilibili.com/video/BV1Nx411i7qb?from=search&seid=10889423622965857203)

4. 安装Ubuntus时候会出现[黑屏](https://askubuntu.com/questions/1284693/install-ubuntu20-04-in-dellalienware-m17-2020?noredirect=1#comment2179916_1284693)。
百度一下如何修改 [nomodset](https://blog.csdn.net/new_delete_/article/details/81544438?utm_medium=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.channel_param&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.channel_param) 即可

5. 对于Ubunt 20.04 系统，显卡驱动可以在软件更新中安装即可，对于低版本或者想从Nvidia网站上安装显卡驱动，可以参考[博客](https://blog.csdn.net/wf19930209/article/details/95237824)，记住一定要提前在Nvidia官网下载正确的显卡驱动，然后再跟着教程安装

# 2. 低版本 Ubuntu 常见问题

 在游戏本中安装Ubunt 14.04，往往没有以太网和Wi-Fi网卡驱动。我的解决方法是

- 安装完成后，先去网上买一个外接USB Wi-Fi 网卡，解决上网问题
- 然后，阅读[博客](https://askubuntu.com/questions/1253630/alienware-m17-r3-ubuntu-16-04-network-drivers)
- 如果你以太网网卡型号也是 Killer E3000 2.5 Gigabit Ethemet Controller, 下载[驱动](https://github.com/TallGuy74/r8125)解决以太网上网问题。安装步骤可以参考此[博客](https://blog.csdn.net/u014221090/article/details/82702840)

# 3. Ubuntu 安装后常见的问题

1. 双系统来回切换会造成系统显示时间不正确，参考[博客](https://zhuanlan.zhihu.com/p/27921873)

显示硬件时间(一般是正确的)

""sudo hwclock --show""

设置操作系统时间的软件时间与硬件时间同步

""sudo hwclock -s""


# 4. 卸载Ubuntu
参考[博客](https://zhuanlan.zhihu.com/p/134293931)



