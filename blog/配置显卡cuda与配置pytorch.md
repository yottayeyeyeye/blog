# 配置显卡cuda与配置pytorch

本文相关包下载：
链接：[https://pan.baidu.com/s/1-kYKr8YB6BBok5MvX02Buw](https://pan.baidu.com/s/1-kYKr8YB6BBok5MvX02Buw)
提取码：fuet 
# 一、CUDA与cuDNN版本的选择
方法一：
win+R打开cmd，输入nvidia-smi，我的显卡是nvidia 2070super，支持的cuda版本是11.0
![](https://cdn.nlark.com/yuque/0/2021/webp/1572900/1612617638475-a2b814a0-656b-4f96-a5e3-0d2793d9f483.webp#align=left&display=inline&height=259&margin=%5Bobject%20Object%5D&originHeight=259&originWidth=656&size=0&status=done&style=none&width=656)
图1 cmd查看显卡支持的cuda版本
方法二：
1、打开NVIDIA设置，点击“帮助”
2、进入“系统信息”，显卡及驱动版本如红框所示
![image.png](https://cdn.nlark.com/yuque/0/2021/png/1572900/1612503925750-5ac0d4f8-744f-4543-b785-e78f3c1a153a.png#align=left&display=inline&height=471&margin=%5Bobject%20Object%5D&name=image.png&originHeight=613&originWidth=752&size=35975&status=done&style=none&width=578)
3、根据驱动版本和CUDA的对应关系，在此确定CUDA版本为CUDA11.0（根据自己电脑配置）_
_[驱动版本和CUDA的对应关系表](https://docs.nvidia.com/cuda/cuda-toolkit-release-notes/index.html#cuda-major-component-versions)_
![image.png](https://cdn.nlark.com/yuque/0/2021/png/1572900/1612617450691-1542d074-9102-45d4-9373-8ec7edf90129.png#align=left&display=inline&height=301&margin=%5Bobject%20Object%5D&name=image.png&originHeight=601&originWidth=986&size=86232&status=done&style=none&width=493)
# 二、安装vs2019
  先安装vs再安装cuda，这样安装cuda的时候vs的路径会加入到cuda中，出错几率可能小一些。vs在官网下载community就够用了，有需求的可以下载其他版本。插件选择使用**c++桌面程序**，其他插件如果没选择，打开vs创建项目时会提示再安装，由于我已经安装了所以没放图。


# 三、安装CUDA
1.上CUDA官网下载CUDA11.0版本及其补丁
_[CUDA10.2版本下载链接](https://developer.nvidia.com/cuda-10.2-download-archive?target_os=Windows&target_arch=x86_64&target_version=10&target_type=exelocal)、[最新版链接](https://developer.nvidia.com/cuda-downloads)_
_![image.png](https://cdn.nlark.com/yuque/0/2021/png/1572900/1612524466593-66b09da5-0c39-4f84-80a4-2d9330821bb0.png#align=left&display=inline&height=339&margin=%5Bobject%20Object%5D&name=image.png&originHeight=852&originWidth=1677&size=93816&status=done&style=none&width=668)_
2）下载后点击exe文件运行，一路默认安装。到下图时选择自定义。
![](https://cdn.nlark.com/yuque/0/2021/webp/1572900/1612618098416-311999ec-0f5b-4324-bfa1-c96e3358bb76.webp#align=left&display=inline&height=278&margin=%5Bobject%20Object%5D&originHeight=278&originWidth=601&size=0&status=done&style=none&width=601)
3）第一次安装全选，第多次安装只选择这几个。我当时第一次安装只选了第一个好像也可以。
Note:在安装过程中发现，如果第N次安装，最好不要选择CUDA下面的nsight system两个选项，不然后续安装会报错。
![](https://cdn.nlark.com/yuque/0/2021/webp/1572900/1612618114134-62359a49-c1e7-4a43-9b40-79080cbae76b.webp#align=left&display=inline&height=278&margin=%5Bobject%20Object%5D&originHeight=278&originWidth=601&size=0&status=done&style=none&width=601)
![](https://cdn.nlark.com/yuque/0/2021/png/1572900/1612618220888-283ad562-bff8-4b12-95e1-d20f4b2bdb49.png#align=left&display=inline&height=488&margin=%5Bobject%20Object%5D&originHeight=555&originWidth=742&size=0&status=done&style=none&width=653)
4）路径我选择的是默认位置。后面一路默认就OK，安装成功关闭。


5）安装结束后，右键 我的电脑-->属性-->高级系统设置-->环境变量，系统变量中已经加入了cuda的两个路径。
![](https://cdn.nlark.com/yuque/0/2021/webp/1572900/1612618335951-45660dd5-874d-4851-b756-216e71792cb1.webp#align=left&display=inline&height=101&margin=%5Bobject%20Object%5D&originHeight=101&originWidth=586&size=0&status=done&style=none&width=586)


6）在系统变量中加入下面的路径，点击确定。
```bash
CUDA_BIN_PATH: %CUDA_PATH%\bin

CUDA_LIB_PATH: %CUDA_PATH%\lib\x64

CUDA_SDK_PATH: C:\ProgramData\NVIDIA Corporation\CUDA Samples\v11.0

CUDA_SDK_BIN_PATH: %CUDA_SDK_PATH%\bin\win64

CUDA_SDK_LIB_PATH: %CUDA_SDK_PATH%\common\lib\x64
```
7）在系统变量path中加入下面的的变量：
```bash
%CUDA_BIN_PATH%
%CUDA_LIB_PATH%
%CUDA_SDK_BIN_PATH%
%CUDA_SDK_LIB_PATH%
```
# 三、检测cuda是否安装成功
1.运行cmd，输入`nvcc --version `即可查看版本号；
_`set cuda`，可以查看cuda设置的环境变量。_
_![](https://cdn.nlark.com/yuque/0/2021/png/1572900/1612618685640-91b61771-5ea5-433d-91b2-38b656587e62.png#align=left&display=inline&height=172&margin=%5Bobject%20Object%5D&originHeight=244&originWidth=749&size=0&status=done&style=none&width=528)_
2、cd两次到c目录下，复制cuda安装目录下的deviceQuery.exe 和 bandwidthTest.exe两个程序的路径。分别运行这两个程序，result=pass则安装成功，否则就重新安装。
deviceQuery.exe 和 bandwidthTest.exe  路径
![](https://cdn.nlark.com/yuque/0/2021/webp/1572900/1612618742717-2cdc06bd-e7f9-4a40-933f-7c0a7abce38d.webp#align=left&display=inline&height=328&margin=%5Bobject%20Object%5D&originHeight=588&originWidth=1122&size=0&status=done&style=none&width=625)


找到两个程序的路径
![](https://cdn.nlark.com/yuque/0/2021/webp/1572900/1612618742544-04366cf3-f5ff-480e-86d2-e6e5c9baf11e.webp#align=left&display=inline&height=335&margin=%5Bobject%20Object%5D&originHeight=519&originWidth=993&size=0&status=done&style=none&width=640)
运行后result=pass则成功
![](https://cdn.nlark.com/yuque/0/2021/webp/1572900/1612618742902-46c1a58d-78f9-4966-a0da-808c1e95015f.webp#align=left&display=inline&height=517&margin=%5Bobject%20Object%5D&originHeight=855&originWidth=1187&size=0&status=done&style=none&width=718)
result=pass则成功


# 四、根据CUDA版本，安装cudnn
cuDNN官网：_[https://developer.nvidia.com/rdp/cudnn-archive#a-collapse742-10](https://developer.nvidia.com/rdp/cudnn-archive#a-collapse742-10)_
找自己cudn对应的
![image.png](https://cdn.nlark.com/yuque/0/2021/png/1572900/1612524526703-0873761f-b6b5-458b-a6c2-e6a240bc9cba.png#align=left&display=inline&height=341&margin=%5Bobject%20Object%5D&name=image.png&originHeight=681&originWidth=933&size=59242&status=done&style=none&width=466.5)
# 五、pytorch的安装与配置：
根据对应的CUdA版本安装对应的pytorch
官网：_[https://pytorch.org/](https://pytorch.org/)_
下载pytorch
![image.png](https://cdn.nlark.com/yuque/0/2021/png/1572900/1612503773142-ef78e4df-f068-4bf2-b097-b50a4a22820e.png#align=left&display=inline&height=213&margin=%5Bobject%20Object%5D&name=image.png&originHeight=426&originWidth=1094&size=43908&status=done&style=none&width=547)
pip install torch===1.7.1+cu110 torchvision===0.8.2+cu110 torchaudio===0.7.2 -f [https://download.pytorch.org/whl/torch_stable.html](https://download.pytorch.org/whl/torch_stable.html)
[https://pytorch.org/get-started/locally/](https://pytorch.org/get-started/locally/)
# 六、验证是否安装成功
为了确保PyTorch安装成功，我们需要运行简单的样例代码测试，例如打印出随机生成的张量矩阵，以及gpu是否可以使用。
首先在命令行输入python，进入python的解释器，输入以下语句：
```bash
import torch
x = torch.rand(5,3)
print(x)
```
输出如下：
> tensor([[0.9943, 0.2830, 0.5508],
>  [0.0765, 0.6474, 0.0059],
>  [0.7241, 0.1868, 0.5398],
>  [0.3217, 0.4664, 0.4242],
>  [0.3351, 0.2482, 0.7371]])

说明PyTorch安装成功。
接下来再输入
```
torch.cuda.is_available()
```
输出为`True`即证明支持GPU了。
# 参考：


[下载pytorch](https://pytorch.org/get-started/locally/)
[https://www.jianshu.com/p/1fd15d2408bf](https://www.jianshu.com/p/1fd15d2408bf)
[链接一](https://www.cnblogs.com/arxive/p/11198420.html)_，_[链接二](https://www.jianshu.com/p/1fd15d2408bf)
[Win10系统安装CUDA10.0和cuDNN](https://blog.csdn.net/SpadgerZ/article/details/89454247)
[PyTorch-GPU环境配置](https://www.cnblogs.com/diralpo/p/12596475.html)
[linux配置](https://zhuanlan.zhihu.com/p/122286055)
