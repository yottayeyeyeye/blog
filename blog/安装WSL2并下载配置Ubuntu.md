# 安装WSL2并下载配置Ubuntu

# Windows系统环境
[官方指南](https://docs.microsoft.com/zh-cn/windows/wsl/install-win10#troubleshooting-installation)
## 步骤 1 - 启用适用于 Linux 的 Windows 子系统
需要先启用“适用于 Linux 的 Windows 子系统”可选功能，然后才能在 Windows 上安装 Linux 分发。
以管理员身份打开 PowerShell 并运行：
```
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```
建议现在转到步骤 #2，更新到 WSL 2，但如果只想安装 WSL 1，现在可以重新启动计算机，然后继续执行[步骤 6 - 安装所选的 Linux 发行版](https://docs.microsoft.com/zh-cn/windows/wsl/install-win10#step-6---install-your-linux-distribution-of-choice)。 若要更新到 WSL 2，请等待重新启动计算机，然后继续执行下一步。
## 步骤 2 - 检查运行 WSL 2 的要求
若要更新到 WSL 2，需要运行 Windows 10。

- 对于 x64 系统：**版本 1903** 或更高版本，采用 **内部版本 18362** 或更高版本。
- 对于 ARM64 系统：**版本 2004** 或更高版本，采用 **内部版本 19041** 或更高版本。
- 低于 18362 的版本不支持 WSL 2。 使用 [Windows Update 助手](https://www.microsoft.com/software-download/windows10)更新 Windows 版本。

若要检查 Windows 版本及内部版本号，选择 Windows 徽标键 + R，然后键入“winver”，选择“确定”。 （或者在 Windows 命令提示符下输入 `ver` 命令）。 更新到“设置”菜单中的[最新 Windows 版本]()。
![](https://cdn.nlark.com/yuque/0/2021/png/1572900/1612252702223-4aa37c05-240c-4224-9a1f-44e852e7009e.png#align=left&display=inline&height=191&margin=%5Bobject%20Object%5D&originHeight=191&originWidth=432&size=0&status=done&style=none&width=432)


Microsoft Store 上面下载 Windows Terminal，集合了 powershell，WSL，Azure cloud shell 等。


## 步骤 3 - 启用虚拟机功能
安装 WSL 2 之前，必须启用“虚拟机平台”可选功能。 计算机需要[虚拟化功能](https://docs.microsoft.com/zh-cn/windows/wsl/troubleshooting#error-0x80370102-the-virtual-machine-could-not-be-started-because-a-required-feature-is-not-installed)才能使用此功能。
以管理员身份打开 PowerShell 并运行：
```
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```
**重新启动** 计算机，以完成 WSL 安装并更新到 WSL 2。
## 步骤 4 - 下载 Linux 内核更新包

1. 下载最新包：
   - [适用于 x64 计算机的 WSL2 Linux 内核更新包](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)
2.  备注
如果使用的是 ARM64 计算机，请下载 [ARM64 包](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_arm64.msi)。 如果不确定自己计算机的类型，请打开命令提示符或 PowerShell，并输入：`systeminfo | find "System Type"`。

2. 运行上一步中下载的更新包。 （双击以运行 - 系统将提示你提供提升的权限，选择“是”以批准此安装。）


安装完成后，请继续执行下一步 - 在安装新的 Linux 分发时，将 WSL 2 设置为默认版本。 （如果希望将新的 Linux 安装设置为 WSL 1，请跳过此步骤。）
注意，你是AMD卡不一定是ARM64位，比如我是联想拯救者R7000，但我是X64。具体原因我也不清楚。


## 步骤 5 - 将 WSL2 设为默认版本


意思是以后安装的所有发行版包括 docker 都是以 WSL2 去执行，


用管理员身份打开 Powershell 输入以下命令：


```
wsl --set-default-version 2
```


这行命令之后安装的所有 Linux 发行版都默认 WSL2 执行。
## 步骤 6 - 安装所选的 Linux 分发
第一种方式是在 Microsoft Store 上面安装，缺点默认安装在C盘不能更改。


第二种方式是：从网上下载一个喜欢的发行版，将下载好的发行版后缀 appx 改为 zip，然后解压到非系统盘上面。

还有一点就是尽量保存这个发行版的安装包，防止玩崩了重装又要去找地址下载。
我下了一个2004x64和1804AMD的，链接自取
链接：[https://pan.baidu.com/s/1TsMcJ1O76RYfmMNOTZ5NiQ](https://pan.baidu.com/s/1TsMcJ1O76RYfmMNOTZ5NiQ)
提取码：xean 
## 步骤 7 - 给下载好的发行版创建用户名和密码


下面我就以 Ubuntu 20.04 LTS 进行示例：


![](https://cdn.nlark.com/yuque/0/2021/png/1572900/1612252702348-54293272-ea63-4fef-963a-774ba0664653.png#align=left&display=inline&height=509&margin=%5Bobject%20Object%5D&originHeight=509&originWidth=965&size=0&status=done&style=none&width=965)
## 步骤 8 - 将 Ubuntu 20.04 LTS 设置为 WSL2 去执行


通过管理员 Powershell 执行以下命令查询分配的版本：


> wsl -l -v



在执行下面命令前把刚才建立用户那个程序关闭


> wsl --set-version <发行版全称> 2



![](https://cdn.nlark.com/yuque/0/2021/png/1572900/1612252702227-f692463a-e7ed-482b-9f25-aa48ea5f6402.png#align=left&display=inline&height=105&margin=%5Bobject%20Object%5D&originHeight=105&originWidth=476&size=0&status=done&style=none&width=476)




```
wsl --set-version Ubuntu-20.04 2
```
## 七、换国内镜像源


安装好了第一步之后当然是换源啦，因为大部分 linux 发行版的服务器都在国外所以下载速度都会很慢，使用国内的镜像下载速度就快很多，肯定比没换舒爽多了


这里以阿里源为例


1、将系统源文件复制一份备用


```
sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak
```


2、用 vi 编辑器打开源文件


```
sudo vi /etc/apt/sources.list
```


然后直接输入`49dd`，就可以清除所有内容了，然后输入`i`就可以进行编辑了


3、找到国内源复制粘贴


其他系统该页面也有，每个系统的操作都是大同小异，话不多说开 lu 它，进去之后了也是要选择跟系统版本相符合的源


```
deb http://mirrors.aliyun.com/ubuntu/ focal main restricted universe multiverse 
deb-src http://mirrors.aliyun.com/ubuntu/ focal main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ focal-security main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal-security main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ focal-updates main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal-updates main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ focal-proposed main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal-proposed main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ focal-backports main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal-backports main restricted universe multiverse
```


4、更新系统


```
sudo apt-get -y update && sudo apt-get -y upgrade
```




错误排查：
[https://docs.microsoft.com/zh-cn/windows/wsl/install-win10#step-5---set-wsl-2-as-your-default-version](https://docs.microsoft.com/zh-cn/windows/wsl/install-win10#step-5---set-wsl-2-as-your-default-version)
# 参考：
[https://blog.csdn.net/weixin_40004659/article/details/110362685](https://blog.csdn.net/weixin_40004659/article/details/110362685)


[https://www.jianshu.com/p/a14cb25ac0a9](https://www.jianshu.com/p/a14cb25ac0a9)


[https://docs.microsoft.com/zh-cn/windows/wsl/install-on-server](https://docs.microsoft.com/zh-cn/windows/wsl/install-on-server)
[https://docs.microsoft.com/zh-cn/windows/wsl/user-support](https://docs.microsoft.com/zh-cn/windows/wsl/user-support)
[https://docs.microsoft.com/zh-cn/windows/wsl/install-win10](https://docs.microsoft.com/zh-cn/windows/wsl/install-win10)
