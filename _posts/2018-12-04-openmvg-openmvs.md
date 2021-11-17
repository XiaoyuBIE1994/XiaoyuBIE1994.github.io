---
layout: post
title: Ubuntu16.04安装OpenMVG+OpenMVS踩坑记录
category: 环境配置
tags: 
  - openmvg
  - openmvs
---
___

因为最近的项目需求，需要把Slam的定位和三维重建的结果结合在一起，所以照着网上的教程装了一遍OpenMVG和OpenMVS。本文记录了大致编译的流程，主要参考了

#### 简介

通常意义上，三维重建的管线分为四个部分：
> Structure from Motion(SFM)
> Multi View Stereo(MVS)
> Surface Generation(SG)
> Texure Mapping(MP)

其中，OpenMVG可以完成第一步SFM，得到的是稀疏的3D model，而OpenMVS可以完成后三步，其中MVS可以得到稠密的model，SG对点云进行三角化（mesh/triangulation），最后由MP进行纹理渲染

#### 项目地址
[OpenMVG](https://github.com/openMVG/openMVG) | [OpenMVS](https://github.com/cdcseacave/openMVS)

#### OpenMVG

OpenMVG的安装非常简单，可以直接参考 [官方文档](https://github.com/openMVG/openMVG/blob/master/BUILD.md)。需要注意的地方是如果想把OpenMVG装成第三方库，那么在安装的时候需要把OpenMVG装在自己的路径下

#### OpenMVS

到了OpenMVS，事情就变得比较复杂了，可能由于作者太忙，按照[官方文档](https://github.com/cdcseacave/openMVS/wiki/Building)是没法装成功的，至少在我拉代码的时候是没办法的，下面有几项需要注意：
> VCG

对于VCG库，作者的做法是使用了`main_path= "pwd" `然后在编译的时候加上`-DVCG_ROOT="$main_path/vcglib"`，但有时候使用`pwd`取得的当前位置并不是VCG库的安装位置，所以最好的做法是使用ccmake或者cmake-gui把VCG的路径改为自己的安装路径

> OpenCV

对于目前版本的MVS，对于OpenCV4并不支持，会有一些宏定义的冲突，所以需要使用OpenCV2或者OpenCV3进行编译

> Boost

改好上面两项后，进入了最为坑爹的地方，程序编译时会在百分十70多的时候挂掉，报出一个关于Boost的Error: undefined reference，在这里，官方手册里面说Boost版本至少为1.56，其实并不正确，在[这篇博客](https://leohope.com/%E8%A7%A3%E9%97%AE%E9%A2%98/2018/08/03/openmvg-openmvs/) 中，发现至少需要Boost 1.63，而Ubuntu16.04的默认版本是1.58，所以需要参考[这里](https://askubuntu.com/questions/859333/how-to-install-libboost-version1-59-or-newer-on-ubuntu16-04)去下载更新的Boost库，但不要安装上面的建议装在`/usr/local`，而是装在`/opt`，不然以后编译其他程序的时候很容易让cmake找到local里面的Boost版本而不是自带的1.58

> Cmake

当装好新的Boost之后，本来以后一切OK，结果发现连MakeFile都无法正确生成了，原因是Ubuntu16.04自带的Cmake版本是3.5.2，但编译Boost 1.63需要3.7及以上版本的Cmake，所以可以按照[这里](https://askubuntu.com/questions/355565/how-do-i-install-the-latest-version-of-cmake-from-the-command-line)最高赞的方法，先移除自带的Cmake，然后安装新的Cmake版本，如果需要安装`cmake-gui`，可以使用`./bootstrap --qt-gui`。至此，OpenMVS终于能够成功编译，至少在我的电脑上是可以了 o(╯□╰)o

