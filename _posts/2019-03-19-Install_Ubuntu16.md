---
layout: post
title: Windows安装Ubuntu双系统
category: 环境配置
tags: 
  - linux
---







最近比较频繁的装了几次双系统，所以将收集到的攻略整理了一下，以备查用



## 启动盘制作

准备好一个空的U盘，格式化，然后参考Ubuntu[官网教程](https://tutorials.ubuntu.com/tutorial/tutorial-create-a-usb-stick-on-windows?_ga=2.245776452.1382908312.1543959324-2097928590.1543959324#0)就可以顺利制作启动盘了

## 双系统安装指南
双系统安装其实很简单，一般步骤为:  
Windows磁盘分区（如果事先装有Ubuntu需要先卸载掉）-> 关闭快速启动 -> 重启进入BIOS进行设置（一般的点电脑在启动时按住 `F2` 即可进入，需要关掉 Fast Boot） -> 进入Ubuntu安装 -> 磁盘分区 -> 安装成功  

卸载原有Ubuntu流程；
备份 Ubuntu 所需文件。在 Windows 10 下用管理员帐号，运行 cmd.exe，输入bootsect /nt60 c: /mbr修复主引导记录（覆盖掉 grub)；重新启动。打开磁盘管理，删除ubuntu分区，重新分区，或将 Windows 的分区进行扩展。

[卸载EFI分区](https://blog.csdn.net/mtllyb/article/details/78635757)：

- 利用管理员权限打开 cmd
- 输入 diskpart
- `list disk` 查看瓷盘信息
- 若 ubuntu 装在磁盘1，则选择磁盘1，`select disk 1`
- 查看磁盘1下所有分区，`list partition`
- 选择 EFI 所在分区（例如为分区4），`select partition 4`
- 删除分区，`delete partition override`
- 在磁盘管理中选择 `扩展卷` 将分区合并



最容易问题的地方在于磁盘分区，网上大多数的攻略是让我们设置 /boot 来作为系统引导，但这是在Legacy驱动下的教程，现在大多数电脑都换成了UEFI启动模式，如果按照网上大多数的攻略来安装Ubuntu，重启后会进入 Grub rescues 的错误而且很那修复(我尝试了很久还是放弃了)，所以在分区的时候不需要分 /boot，而是需要分出一块efi system partition。[具体攻略参考如下](https://www.bbsmax.com/A/q4zVeMjdKr/)



## 相关软件安装

装好Ubuntu之后，只是讲好了房子的骨架，在使他成为日常好用的系统之前，还需要装上大量的软件包和三方库

### 常用软件：  
**Chrome:** [安装地址](https://www.google.com/chrome/)  
**搜狗拼音:** [安装地址](https://pinyin.sogou.com/linux/?r=pinyin) [安装步骤](https://blog.csdn.net/ljheee/article/details/52966456) （键盘输入法系统由默认的iBus设置为fcitx)  
**VS Code:** [安装地址](https://code.visualstudio.com/)  
**Anaconda:** [安装地址](https://www.anaconda.com/download/#linux) [配置Jupyter路径](https://blog.csdn.net/Sukie_csdn/article/details/79766968)   
**Remarkable:** [安装指南](http://biexiaoyu1994.com/2018/12/remarkable-tutorial/)
**Typora** [安装地址](https://www.typora.io/)




### 常用三方库：  

**OpenCV 3**  
[安装地址](https://opencv.org/releases.html) [安装指南](https://docs.opencv.org/3.4.4/d7/d9f/tutorial_linux_install.html)  
```cpp
sudo apt-get install build-essential # compiler
sudo apt-get install cmake git libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev # required
sudo apt-get install python-dev python-numpy libtbb2 libtbb-dev libjpeg-dev libpng-dev libtiff-dev libjasper-dev libdc1394-22-dev # optinal
```
Eigen
```cpp
sudo apt install libeigen3-dev
```

Ceres  
[安装指南](http://ceres-solver.org/installation.html)

```
# CMake
sudo apt-get install cmake
# google-glog + gflags
sudo apt-get install libgoogle-glog-dev
# BLAS & LAPACK
sudo apt-get install libatlas-base-dev
# Eigen3
sudo apt-get install libeigen3-dev
# SuiteSparse and CXSparse (optional)
# - If you want to build Ceres as a *static* library (the default)
#   you can use the SuiteSparse package in the main Ubuntu package
#   repository:
sudo apt-get install libsuitesparse-dev
# - However, if you want to build Ceres as a *shared* library, you must
#   add the following PPA:
sudo add-apt-repository ppa:bzindovic/suitesparse-bugfix-1319687
sudo apt-get update
sudo apt-get install libsuitesparse-dev 
```
g2o  
[g2o github地址](https://github.com/RainerKuemmerle/g2o)




OpenMVG+OpenMVS [安装指南](http://biexiaoyu1994.com/2018/12/openmvg-openmvs/)