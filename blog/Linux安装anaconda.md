# Linux安装anaconda

# 1、Anaconda安装包下载
（1）[官网下载](https://www.anaconda.com/products/individual#download-section)，下载速度较慢
（2）[清华大学开源软件镜像站](https://mirrors.tuna.tsinghua.edu.cn/help/anaconda/)
百度网盘Linux的anaconda安装包：TODO
# 2、安装Anaconda
（1）进入文件下载目录
```
cd ~/software
```
（2）运行安装包
```
bash Anaconda3-2020.07-Linux-x86_64.sh 
或者参照下图
bash +“copy file path的内容”
```
![image.png](https://cdn.nlark.com/yuque/0/2021/png/1572900/1612428745265-291892c3-f09f-4d2f-a911-386dc23bbe44.png#align=left&display=inline&height=255&margin=%5Bobject%20Object%5D&name=image.png&originHeight=510&originWidth=743&size=58569&status=done&style=none&width=371.5)


（3）回车键，进入注册信息页面
（4）按q跳过阅读，yes
（5）默认安装在用户目录下，直接回车即可安装；若想自定义安装目录，直接输入安装目录，回车即可。
（6）Do you wish the installer to initialize Anaconda3 by running conda init ? 输入 no，回车
![image.png](https://cdn.nlark.com/yuque/0/2021/png/1572900/1612324953578-32066da6-a43a-42bf-ba17-d5fc582de6f1.png#align=left&display=inline&height=388&margin=%5Bobject%20Object%5D&name=image.png&originHeight=775&originWidth=946&size=83450&status=done&style=none&width=473)
# 3、修改环境变量
将Anaconda添加到用户环境变量中
```
vim ~/.bashrc
```
添加下面内容
```
# 2.在.bashrc文件底部添加  
 # 为了避免与其他服务器用户产生命令冲突,使用自己的英文名+Python替代python 
alias fortunePython='/root/anaconda3/bin/python'   
#这里写anaconda的安装路径
export PATH='/root/anaconda3/bin:$PATH'

```
source一下
```
source ~/.bashrc
```
# 4、检查是否安装成功
```
conda --version
#conda 4.5.11
fortunePython
```
![image.png](https://cdn.nlark.com/yuque/0/2021/png/1572900/1612442159865-8909ecc2-34cf-49e2-8c7a-179d09c8a2e8.png#align=left&display=inline&height=44&margin=%5Bobject%20Object%5D&name=image.png&originHeight=87&originWidth=776&size=12250&status=done&style=none&width=388)
退出python：exit()
# 5.修改anaconda的源，变为国内源
### 
[知乎-Anaconda国内源解决方法](https://www.zhihu.com/question/322862374/answer/1662070278)

Anaconda 的发行版默认是国外的源，因此下载一些 Python 包会比较慢。因此，我们需要更换成国内的源，一般是清华源或者中科大源。Linux 用户在 bash 命令行输入更换命令。


```cpp
将以上配置文件写在 ~/.condarc 中
vim ~/.condarc

若安装了 sublime  的也可在终端使用  ：subl ~/.condarc

channels:
  - https://mirrors.ustc.edu.cn/anaconda/pkgs/main/
  - https://mirrors.ustc.edu.cn/anaconda/cloud/conda-forge/
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
  - defaults
show_channel_urls: true

也可以把 anaconda 仓(https://repo.continuum.io/)的添加进去：

这是在anaconda安装 tensorflow1.4.1 的时候遇到的问题，把这个 anaconda 仓添加进去问题就解决了

channels:
  - https://mirrors.ustc.edu.cn/anaconda/pkgs/main/
  - https://mirrors.ustc.edu.cn/anaconda/cloud/conda-forge/
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
  - https://repo.continuum.io/pkgs/main
  - defaults
show_channel_urls: true
              

channels:
  - defaults
show_channel_urls: true
default_channels:
  - https://mirrors.bfsu.edu.cn/anaconda/pkgs/main
  - https://mirrors.bfsu.edu.cn/anaconda/pkgs/free
  - https://mirrors.bfsu.edu.cn/anaconda/pkgs/r
  - https://mirrors.bfsu.edu.cn/anaconda/pkgs/pro
  - https://mirrors.bfsu.edu.cn/anaconda/pkgs/msys2
custom_channels:
  conda-forge: https://mirrors.bfsu.edu.cn/anaconda/cloud
  msys2: https://mirrors.bfsu.edu.cn/anaconda/cloud
  bioconda: https://mirrors.bfsu.edu.cn/anaconda/cloud
  menpo: https://mirrors.bfsu.edu.cn/anaconda/cloud
  pytorch: https://mirrors.bfsu.edu.cn/anaconda/cloud
  simpleitk: https://mirrors.bfsu.edu.cn/anaconda/cloud
```
```bash
# 更换清华源
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
conda config --set show_channel_urls yes

# 更换中科大源
conda config --add channels https://mirrors.ustc.edu.cn/Anaconda/pkgs/main/  
 
conda config --add channels https://mirrors.ustc.edu.cn/Anaconda/pkgs/free/  
 
conda config --add channels https://mirrors.ustc.edu.cn/Anaconda/cloud/conda-forge/  
 
conda config --add channels https://mirrors.ustc.edu.cn/Anaconda/cloud/msys2/  

conda config --add channels https://mirrors.ustc.edu.cn/Anaconda/cloud/bioconda/  
 
conda config --add channels https://mirrors.ustc.edu.cn/Anaconda/cloud/menpo/  

conda config --set show_channel_urls yes
```

```cpp
git clone https://github.com/matpool/matools.git 
bash /matools/mirrors/switch_apt_source.sh 
bash /matools/mirrors/switch_conda_source.sh
bash /matools/mirrors/switch_pip_source.sh
```


若源不生效，试着把.condarc文件中的 - defaults那行去掉，就不会出现这个问题了
Anaconda国内源关闭了




# 5. 创建anaconda虚拟环境
这里我们用 Anaconda 的命令来创建虚拟环境。使用 conda create -n your_env_name python=X.X（2.7、3.6)，使用该命令创建 python 版本为 X.X，名字为 your_env_name 的虚拟环境。your_env_name 文件可以在 Anaconda 安装目录 envs 文件下找到。




```
#创建虚拟环境
conda create -n your_env_name python=X.X（3.6、3.7等）
 
#激活虚拟环境
source activate your_env_name(虚拟环境名称)
 
#退出虚拟环境
source deactivate your_env_name(虚拟环境名称)
 
#删除虚拟环境
conda remove -n your_env_name(虚拟环境名称) --all
 conda remove --name your_env_name package_name  # 删除环境中的某个包
#查看安装了哪些包
conda list
 
#安装包
conda install package_name(包名)
conda install scrapy==1.3 # 安装指定版本的包
conda install -n 环境名 包名 # 在conda指定的某个环境中安装包
 
#查看当前存在哪些虚拟环境
conda env list 
#或 
conda info -e
#或
conda info --envs
#检查更新当前conda
conda update conda
#更新anaconda
conda update anaconda
#更新所有库
conda update --all
#更新python
conda update python
```
```
3.安装requirements.txt依赖：pip install -r requirements.txt
```
# 参考：
[Ubuntu 20.04安装Anaconda3及简单使用](https://blog.csdn.net/m0_50117360/article/details/108403586)


