## Why successfully installed opencv-contrib-python==3.4.2.16 but cv2.xfeatures2d.SIFT_create() still doesn't exist?
   明明指定安装了包含sift模块的OpenCV库，为什么python调用的时候依旧报错？
==========================================

先给解决方案：
利用“python2 -m pip list”和“python3 -m pip list”查看对应opencv版本  
然后根据需要进行“pythonX -m pip install opencv-contrib-python==3.4.2.16”，其中X代表你使用opencv的python版本。【版本对应真的很重要。。所以Monroe说建不同环境很对。。但是我懒 】  
后续可能会遇到 numpy版本冲突的问题，显示如下错误：
```
 Something is wrong with the numpy installation. While importing we detected an older version of numpy in ['/home/peiyao/.local/lib/python3.5/site-packages/numpy']. One method of fixing this is to repeatedly uninstall numpy until none is found, then reinstall this version.
```
需要卸载重装numpy，由于我需要python3环境下的更改，所以使用
```
python3 -m pip uninstall numpy
python3 -m pip install numpy
```
后面显示安装numpy最新版本成功，但是jupyter中依然报错。  
使用下面的命令，强行安装然后成功。
```
python3 -m pip install numpy --ignore-installed numpy

```
=====================================================  
这个问题说起来也是个一星入门的问题，多半是由于系统上存在两个版本的python。但我一开始没有找到原因，故记录一下。    
问题的来源是OpenCV 3.4.3以后版本中舍弃了sift算法的相关模块，由于专利问题。    
那么根据热情网友的推荐，我使用以下命令行进行排查：  
```
# 确认opencv-python 版本
import cv2
print(cv2.__version)

# 寻找python安装库路径
import sys
print(sys.path)

# 直接查找库路径（linux）
whereis xx

# 查询OpenCV版本
pkg-config opencv --modversion
```  
