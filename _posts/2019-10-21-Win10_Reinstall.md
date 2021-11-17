---
layout: post
title: Windows10重置系统时找不到恢复环境
category: 环境配置
tags: 
  - linux
---



最近旧的 windows 电脑越来越卡了，曾经有意的无意的装的各种 XX 助手怎么也删除不掉，就决定使用 win10自带的重置系统，主要步骤如下：

选择开始键 -> 设置 -> 更新和安全 -> 初始化此电脑 -> 选择是否保留个人文件

但在这一步遇到了问题，显示 `找不到恢复环境`，网上查找问题后发现是**系统文件丢失**，需要重新下载，判断方式如下：

- win + x 打开 `命令提示符(管理员)(A)`
- 输入命令 `reagentc /info`
- 如果显示 `Windows RE 状态： Disable ` 则证明系统恢复文件已丢失



**解决办法：**

- 官网下载win10的 iso 镜像，[下载路径](https://www.microsoft.com/zh-cn/software-download/windows10ISO)
- 解压镜像，或者将压缩文件中的 `source`复制到指定路径，例如 `D:\source`
- 进入管理员命令提示符（ win+x）
- 解压 `install.wim` 到指定路径，例如 `D:\test`，在命令为 `dism /mount-wim /wimfile:"D:\sources\install.wim" /index:1 /mountdir:D:\test`
- 找到 `Winre.wim` 文件，复制到 `C:/Recovery/WindowsRE` ( 在我的电脑上是`C:/Windows/System32/Recovery/WindowsRE`，且在 C 盘根目录直接新建 Recovery 文件夹也会跳转到这一路径，推测存在链接)，
- 如果直接复制失败，可尝试先复制 `Winre.wim` 到其他路径，例如 D 盘，然后在复制进系统恢复的文件夹
- 重设恢复文件路径，输入 `reagentc /setreimage /path C:\Recovery\WindowsRE`
- 激活 Windows RE 状态，输入 `reagentc /enable`
- 重新输入 `reagentc /info` 查看状态，会显示 `Windows RE 状态： Enable `


重新执行初始化，仍然出现问题，显示 `Windows10重置电脑时出现问题，未进行任何更改`，尝试如下解决办法：

- 在管理员命令提示符下键入以下命令：`Dism /Online /Cleanup-Image /ScanHealth`，这条命令将扫描全部系统文件并和官方系统文件对比，扫描计算机中的不一致情况
- 在前一条命令执行完以后，发现系统文件有损坏时，输入 `Dism /Online /Cleanup-Image /CheckHealth`
- 把那些不同的系统文件还原成官方系统源文件，`DISM /Online /Cleanup-image /RestoreHealth`
- 重启，输入 `sfc /SCANNOW`





#### 参考

[1] [重置或重新安装 Windows 10](https://support.microsoft.com/zh-cn/help/4026528/windows-10-reset-or-reinstall)

[2] [win10重置与创建恢复出现问题](https://answers.microsoft.com/zh-hans/windows/forum/all/win10%E9%87%8D%E7%BD%AE%E4%B8%8E%E5%88%9B%E5%BB%BA/164f93f0-fa75-4b64-aaec-7e94c19bc3ae) 

[3] [解决win10重置找不到恢复环境 / 镜像文件解决方案](https://blog.csdn.net/keylion_/article/details/79385841)

[4] [怎么从微软原版ISO镜像中获取WinRE.wim映像](https://answers.microsoft.com/zh-hans/windows/forum/all/%E6%80%8E%E4%B9%88%E4%BB%8E%E5%BE%AE%E8%BD%AF/5d61baee-2034-41fe-b939-6073f0cbcfc2)
