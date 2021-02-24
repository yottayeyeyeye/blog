# win10的wsl2安装cuda并配置pytorch

# 1.准备工作


1.windows预览体验计划开启，升级系统内部版本
按住Windows 键+R键打开运行，在输入框内中输入services.msc，并按下回车查看版本号。
Windows  Update服务再尝试检查更新和安装。


2.安装wsl2(见往期文章)
3.安装Ubuntu
# 2.安装cuda on wsl驱动


![image.png](https://cdn.nlark.com/yuque/0/2021/png/1572900/1612870055545-986682f9-d54e-4c91-83b1-ea069fa13a7f.png#align=left&display=inline&height=208&margin=%5Bobject%20Object%5D&name=image.png&originHeight=416&originWidth=789&size=97336&status=done&style=none&width=394.5)
一路默认（可以不安一些东西，网上可以查到）


# 3.换源安装cuda-toolkit
```bash
sudo apt-key adv --fetch-keys http://mirrors.aliyun.com/nvidia-cuda/ubuntu1804/x86_64/7fa2af80.pub

sudo sh -c 'echo "deb http://mirrors.aliyun.com/nvidia-cuda/ubuntu1804/x86_64 /" > /etc/apt/sources.list.d/cuda.list'

sudo apt-get update

sudo apt-get install -y cuda-toolkit-11-0
```
![image.png](https://cdn.nlark.com/yuque/0/2021/png/1572900/1612879592619-10b05128-d547-4560-a58e-ec747ac43f18.png#align=left&display=inline&height=301&margin=%5Bobject%20Object%5D&name=image.png&originHeight=602&originWidth=1021&size=418163&status=done&style=none&width=510.5)


# 4.设置cuda环境变量
在主目录下的~/.bashrc文件添加如下路径：
```
sudo su -
```
```
vim ~/.bashrc
```
末尾添加并保存：
```bash
export CUDA_HOME=/usr/local/cuda
export PATH=$PATH:$CUDA_HOME/bin
export LD_LIBRARY_PATH=/usr/local/cuda-10.1/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
```
如果提示缺少相应的依赖库，直接执行如下代码自动安装相应的依赖库
```
sudo apt-get install freeglut3-dev build-essential libx11-dev libxmu-dev libxi-dev libgl1-mesa-glx libglu1-mesa libglu1-mesa-dev
```
查看cuda是否安装成功：
```
nvcc -V
```
![](https://cdn.nlark.com/yuque/0/2021/png/1572900/1612960532190-7db32a13-4074-434c-9f8c-b12b110c085d.png#align=left&display=inline&height=102&margin=%5Bobject%20Object%5D&originHeight=102&originWidth=458&size=0&status=done&style=none&width=458)


# 5.安装cudnn
安装cudnn的时候也需要登录Nvidia账号，直接下载:**cuDNN Library for Linux (x86)**
![](https://cdn.nlark.com/yuque/0/2021/png/1572900/1612960558233-29da8889-293c-4f0a-a672-34937dd74087.png#align=left&display=inline&height=809&margin=%5Bobject%20Object%5D&originHeight=809&originWidth=1344&size=0&status=done&style=none&width=1344)
然后打开终端执行：
```
tar -zxvf cudnn-10.2-linux-x64-v8.0.4.30.tgz
sudo cp -P cuda/lib64/libcudnn* /usr/local/cuda-11.0/lib64/
sudo cp  cuda/include/cudnn.h /usr/local/cuda-11.0/include/
```
为所有用户设置读取权限：
```
sudo chmod a+r /usr/local/cuda-11.0/include/cudnn.h 
sudo chmod a+r /usr/local/cuda-11.0/lib64/libcudnn*
```


# 6.验证cuda是否安装成功
![image.png](https://cdn.nlark.com/yuque/0/2021/png/1572900/1612880416005-334578d7-e8c0-4e70-ba8b-b09a90894e04.png#align=left&display=inline&height=312&margin=%5Bobject%20Object%5D&name=image.png&originHeight=474&originWidth=1035&size=701490&status=done&style=none&width=682)
![image.png](https://cdn.nlark.com/yuque/0/2021/png/1572900/1612880534991-9b165880-ee5c-43f1-9a48-e03150e03646.png#align=left&display=inline&height=256&margin=%5Bobject%20Object%5D&name=image.png&originHeight=511&originWidth=1019&size=1066757&status=done&style=none&width=509.5)
```bash
cd /usr/local/cuda/samples/4_Finance/BlackScholes
sudo make
./BlackScholes
#好像是11.0可以这样
```
![image.png](https://cdn.nlark.com/yuque/0/2021/png/1572900/1612960639881-715029d8-c45e-42c9-9a84-59e060ba1e98.png#align=left&display=inline&height=152&margin=%5Bobject%20Object%5D&name=image.png&originHeight=303&originWidth=943&size=25853&status=done&style=none&width=471.5)
成功标志
# 7.安装pytorch
```bash
pip install torch==1.7.1+cu110 torchvision==0.8.2+cu110 torchaudio===0.7.2 -f https://download.pytorch.org/whl/torch_stable.html
```
根据对应的CUdA版本安装对应的pytorch
官网：_[https://pytorch.org/](https://pytorch.org/)_
下载pytorch
![image.png](https://cdn.nlark.com/yuque/0/2021/png/1572900/1612503773142-ef78e4df-f068-4bf2-b097-b50a4a22820e.png#align=left&display=inline&height=213&margin=%5Bobject%20Object%5D&name=image.png&originHeight=426&originWidth=1094&size=43908&status=done&style=none&width=547)
pip install torch===1.7.1+cu110 torchvision===0.8.2+cu110 torchaudio===0.7.2 -f [https://download.pytorch.org/whl/torch_stable.html](https://download.pytorch.org/whl/torch_stable.html)
[https://pytorch.org/get-started/locally/](https://pytorch.org/get-started/locally/)
网速不行就需要下载好再安装：
```
pip install "/home/fortuneye/download/torch-1.7.1+cu110-cp37-cp37m-linux_x86_64.whl"
```
![image.png](https://cdn.nlark.com/yuque/0/2021/png/1572900/1612970230689-d0f36e8e-3246-417a-ac81-101f977390da.png#align=left&display=inline&height=99&margin=%5Bobject%20Object%5D&name=image.png&originHeight=197&originWidth=1594&size=48611&status=done&style=none&width=797)
# 8.验证是否安装成功
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
[在WSL中使用GPU：WSL2 + Ubuntu 18.04 + CUDA + Gnome图形界面环境配置](https://blog.csdn.net/Ashken/article/details/108974058)
[官方安装指南](https://docs.nvidia.com/cuda/wsl-user-guide/index.html#installing-nvidia-drivers)


扩容移空间
[https://www.cnblogs.com/JiangOil/p/13869178.html](https://www.cnblogs.com/JiangOil/p/13869178.html)


错误指南
[https://blog.csdn.net/LaughingMei/article/details/109962838](https://blog.csdn.net/LaughingMei/article/details/109962838)


[https://blog.csdn.net/haozihuang/article/details/109544443](https://blog.csdn.net/haozihuang/article/details/109544443)
