---
title: GPU不兼容Ubuntu安装指南
date: 2016-08-21 16:01:07
tags:
---
<div align="center">
![jpg](/images/gpu-config/sxnet.jpg)
</div>
用台式机对MXNET 的Scala版本进行开发（项目名称为SXNET，还在开发过程中,暂且不提），带独立显卡GTX980，与ubuntu不是很兼容，安装带GPU的系统很麻烦，下面把具体过程记录如下：
## 1.sudo apt-get install openssh-server（保证电脑在黑屏的情况下，可ssh）
## 2.teamviewer(optional)
`https://www.teamviewer.com/zhCN/download/linux/`
## 3.下载jdk
这一步是重中之重！
1）添加JAVA_HOME路径：
export JAVA_HOME=/xxx/xxxx/jdk1.7.0_60
该目录是你JDK解压后的目录，比如小编，解压后的目录为：
/opt/software/java/jdk1.7.0_60
所以小编的路径为：
export JAVA_HOME=/opt/software/java/jdk_1.7.0_60
2)添加JRE路径
小编的为：
export JRE_HOME=/opt/software/java/jdk_1.7.0_60/jre
3)配置CLASSPATH路径
export CLASSPATH=.:$CLASSPATH:$JAVA_HOME/lib:$JRE_HOME/lib
4）配置PATH路径
export PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin
## 4.装gpu后，电脑黑屏，用电脑A，ssh连接
4.1 用ssh远程连接，控制电脑安装NVIDIA显卡驱动
## 5. 进入界面，装cuda
https://developer.nvidia.com/cuda-downloads
http://www.open-open.com/lib/view/open1448030000650.html
最后，在.bashrc中，设置环境变量cuda enviroment:
export PATH=$PATH:/usr/local/cuda/
此时，在terminal中输入nvidia-smi命令，出现下图，说明安装cuda成功！
![jpg](/images/gpu-config/cuda-shell.jpg)
## 6. mxnet装依赖
sudo apt-get update
sudo apt-get install -y build-essential git libblas-dev libopencv-dev
ubuntu的atlas实现:
sudo apt-get install libatlas-base-dev或者sudo apt-get install libopenblas-dev
最后在根目录下进行make,生成动态链接库，供Scala调用。
## 7. 配环境变量
配置动态链接库，使得程序调用JNI接口的时候，能够准确找到动态链接库位置：
`export LD_LIBRARY_PATH＝$LD_LIBRARY_PATH:/home/agen/mxnet/lib`
至此，已经可以编译MXNET了，我用Scala开发，展示如下：
![jpg](/images/gpu-config/environment.png)
## 8.装opencv
　　看官方文档靠谱些：
http://docs.opencv.org/2.4/doc/tutorials/introduction/linux_install/linux_install.html#linux-installation
　　make过程中如果出现：unsopported gpu architecture compute 11
采用：http://blog.csdn.net/sysuwuhongpeng/article/details/45485719 
　　opencv安装好后，在安装目录中找opencv.jar,Scala可以通过该jar文件，利用opencv对图像进行处理。
 
## 9.python library配置
* scikit-image        
        http://scikit-image.org/docs/stable/install.html
* hdf5:
        sudo apt-get install libhdf5-dev
         sudo pip install h5py
* fuel:
`pip install git+git://github.com/mila-udem/fuel.git@v0.0.1`
`#environment`
`export FUEL_DATA_PATH=/mnt/data`
* blocks:
`http://blocks.readthedocs.io/en/latest/setup.html`
`pip install git+git://github.com/mila-udem/blocks.git@v0.0.1`
* pandas:
`pip install pandas`
