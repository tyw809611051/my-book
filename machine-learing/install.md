

#### 安装
系统版本

```
Ubuntu 16.04LTS
```

python版本
```
3.5.2
```

采用快速安装
1.下载tensorflow.whl
```
#网址
https://pypi.python.org/pypi/tensorflow/1.4.1
pip3 install --upgrade tensorflow-1.4.0-cp35-cp35m-manylinux_x86.whl
```
2.安装过程提示numpy not install报错

解决方案:
```
#下载对应版本
https://pypi.python.org/pypi/numpy
pip3 install --upgrade numpy-1.13.3-cp35-cp35m-manylinux1_x86_64.whl
```

3.测试
```
python3
import tensorflow as tf
#没报错即可
```
 
