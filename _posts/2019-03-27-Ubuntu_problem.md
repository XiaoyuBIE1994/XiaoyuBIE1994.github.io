---
layout: post
title: Ubuntu16.04常见操作及问题汇总
category: 环境配置
tags: 
  - linux
---



在Ubuntu上搬砖的时候,总是会遇到各种神奇的问题,当然还是自己太菜,只能一一记录下来,使用的版本为Ubuntu 16.04

## 1. 常见操作

#### 1.1 查看相关信息



```shell
# Ubuntu版本
lsb_release -a
# 磁盘空间大小
df -h
# 显存大小(仅针对Nvida)
nvidia-smi
# 查看CPU信息
cat /proc/cpuinfo # 详细
cat /proc/cpuinfo | grep name | cut -f2 -d: | uniq -c # 简要
# 查看电脑运行状态(需下载htop)
htop
```



#### 1.2 查看内存信息



```
$ free
```



|                   | total | used | free | share | buffers | cached |
| ----------------- | ----- | ---- | ---- | ----- | ------- | ------ |
| Mem:              |       |      |      |       |         |        |
| -/+ buffers/cache |       |      |      |       |         |        |
| Swap              |       |      |      |       |         |        |



- Mem 行显示了从系统角度看来内存使用的情况  
- total是系统可用的内存大小, 数量上等于系统物理内存减去内核保留的内存  
- buffers和cached是系统用做缓冲的内存. buffers与某个块设备关联, 包含了文件系统元数据, 并且跟踪了块的变化. cache只包含了文件本身  
- -/+ buffers/cache行则从用户角度显示内存信息, 可用内存从数量上等于mem行used列值减去buffers和cached内存的大小  
- 因为buffers和cached是操作系统为加快系统运行而设置的, 当用户需要时, 可以只接为用户使用  
  top 和 vmstat 也显示了系统内存的信息.



#### 1.3  修改系统默认路径

```shell
gvim .bashrc
PATH=$(getconf PATH) # 将路径恢复为默认路径
export PATH=$PATH:my/own/path # 添加自己需要的路径
source .bashrc # 更新bash
```

这样做的好处是每次都提前将路径恢复到默认路径,然后再添加自己所需要的路径,否则PATH中可能会含有历史遗留路径



#### 1.4 查看库文件版本



```shell
# 查找第三方库的文件信息(如 opencv, eigen3)
pkg-config --modversion package_name
# 通过dpkg来查看已安装的包
dpkg -l 'package_name'
# 搜寻目录/lib和/usr/lib以及动态库配置文件/etc/ld.so.conf内所列的目录下，搜索出可共享的动态链接库
ldconfig -p | grep <name of package> 
# 查看gcc版本
gcc -v
# 查看cmake版本
cmake --version
# 查看Boost版本
dpkg -s libboost-dev | grep 'Version'
dpkg -S /usr/include/boost/version.hpp

```



## 2. Ubuntu系统常见问题



#### 2.1 双系统中无法进入 Bios setup，但可以进入win10

在win10中进入settings/update & security/recovery/advanced start up - restart pc

然后选择troubleshoot -> advanced -> UEFI firmware settings -> restart

就可以进入BIOS setup了



#### 2.2 启动 Ubuntu 发现 Secure Boot Violation

进入 Bios setup, Security -> Secure Boot Menu -> Secure Boot Control -> Disabled

然后 Boot -> Fast Boot -> Disabled, Boot -> Launch CSM -> Enabled

最后 Save & Exit -> Save Changes and Exit 

完成~



#### 2.3 Ubuntu 进入后出现 Minimal BASH-like line editing，报 grub 错误

有可能能是磁盘选区的时候出现的问题

在启动界面进入Bios Setup，再按esc退出，就可以进入了

修复办法 ：进入终端，输入


```shell
sudo update-grub2
sudo apt-get install grub2
sudo reboot
```

完了后可能出现我发进入Bios setup 和 Secure Boot Violation 错误，修复方法参考上面两条



#### 2.4 Ubuntu 升级Python后打不开终端

Ubuntu默认的python版本为2.7.6，终端也是使用Python打开的，所以如果升级了Python就会出现终端打不开的情况，解决办法如下：

- 打开Xterm, 输入 gnome-terminal，进入虚拟终端
- 输入 sudo apt-get install --reinstall python-minimal



#### 2.5 Ubuntu 中发生U 盘无法挂载

显示 command line .... "exfat"

解决办法：在 Ubuntu 14.04中，输入：

```shell
sudo apt-get install exfat-fuse exfat-utils
```



#### 2.6 Ubuntu 中无法打开 Chrome

在终端输入 google-chrome 后显示NSS版本过低

解决办法 : 升级相应的NSS版本 :

```shell
sudo apt-get install libnss3
```



#### 2.7 Ubuntu 忘记 root 密码

- 重启电脑
- 开机会进入Grub引导界面,选择 ++Advanced option for Ubuntu++
- 选择带有 ++Recavery mode++ 的菜单,按回车
- 进入到revovery menu,选择 root Drop to root shell prompt
- 若直接 passwd 用户名 会出现如下错误

```shell
passwd: Authentication token manipulation errror
passwd: passwd unchanged
```
- 若要解决此问题,需要进行如下操作:

```shell
mount  -o  remount,rw /  //进入 remount
passwd 用户名 //然后输入两次新密码即可
reboot // 重启
```

若想更改登录密码

```shell
chmod 666 /dev/null  // 所有用户都有读写权限
mount -o remount,rw /  // 将根分区设置为读写模式
chmod 777 /etc/passwd  // 所有用户都有读写执行权限
pwconv  // 开启用户的shadow命令
passwd 用户名 //
```



#### 2.8 Ubuntu 打开 chrome 后出现 输入密码以解锁您的登录密钥环, 输入任何密码均无效
- 终端输入 seehorse
- 找到login的密码.删除
- 点旁边的加号,选择创建密码密钥环
- 填写密码名字(如chrome)以及密码
- 重启



#### 2.9 Ubuntu 中shell脚本无法使用 source 的原有及解决办法

描述： 运行 shell 脚本时显示 `source not found`

原因： 

运行如下命令


```shell
ls -l `which sh`
```

会显示如下信息

```shell
lrwxrwxrwx 1 root root 4 Feb 17  2016 /bin/sh -> dash
```

说明系统使用了dash进行解析

解决办法：


```shell
sudo dpkg-reconfig dash
```

将选项改为“否”，再运行上述命令变可以看到接续的方式变成了bash，如果不成功，可尝试重启



#### 2.10 Ubuntu 安装 Anaconda 后运行 Spyder 出现错误

错误信息： ModuleNotFoundError: No module named 'PyQt5.QtWebEngineWidgets'

解决办法：

```
conda install -c defaults pyqt=5 qt
```



#### 2.11 Ubuntu 开机报错,进入 initramfs

这个问题最扎心,如果直接按照指示选择 `fsck `并没法解决问题,后来在油管上找到了解决方案



 - 找一个U盘启动盘,打开电脑选择Boot into USB

 - 在 Search your computer 中找到 disks

 - 选中Ext4的盘点击 Unmount(自己的电脑上并没有需要unmount,但攻略上有介绍)

 - 打开Terminal,输入 `sudo fdisk -l | grep Linux | grep -Ev 'swap'` 找到使用的分区

 - 列出所有的 super block `sudo dumpe2fs /dev/sda1 | grep superblock` 其中 sda1 是所需要查找的盘,需要换成自己的,此时会出现

   ```
    Primary superblock at 0, Group descriptors at 1-30
    Backup superblock at 32768, Group descriptors at 32769-32798
   ```

   

 - 任意选中其中的编号(如32768),执行如下命令进行修复

```shell
sudo fsck -b 32768 /dev/sda1 -y
```

- reboot,选择自己的系统启动



#### 2.12 Ubuntu和Windows双系统时间不一致

这是由于Ubuntu和Windows看待硬件时间不一致导致的

- Windows把系统硬件时间当作本地时间（Local time），即操作系统中显示的时间跟BIOS中显示的时间是一样的
- Linux/Unix/Mac把硬件时间当作UTC（Universal Time Coordinated,协调世界时），操作系统中显示的时间是硬件时间经过换算得来



Ubuntu16.04之前：

```shell
sudo gedit /etc/default/rcS
sudo sed -i 's/UTC=no/UTC=yes/' /etc/default/rcS
```

Ubuntu16.04的配置文件中没有`UTC=yes`，此时可以用ntpdate来校准

```shell
# 安装ntpdate
sudo apt-get install ntpdate
# 校准时间
sudo ntpdate time.windows.com
# 讲时间更新到硬件上
sudo hwclock --localtime --systohc
```



## 参考

1. [ubuntu 查看内存大小](http://tiankonguse.com/record/record.php?id=43)
2. [Linux命令大全](http://man.linuxde.net/)
3. [How to resolve/fix initramfs error BusyBox issue in Ubuntu,Linux Mint](https://www.youtube.com/watch?v=4vGK6M-X6eo&list=PLvJnCrTH9jaJvF0dN3EsP42urzOgK9VsW)



