# test1
使用ifly3588s作为边缘设备，进行车辆识别检测需自备数据集或下载https://pan.baidu.com/s/1joXajlCEedpIrWlsfZCiug?pwd=echo 提取码: echo 网盘中的现有数据集进行训练

# 设备
ifly3588s内置NPU模块，处理性能最高可达6TOPS。使用该NPU需要下载RKNN的SDK开发包。
RKNN SDK 为NPU提供ifly3588s的AI编程接口，能够帮助用户部署使用RKNN模型，加速AI应用的落地。
# RKNN模型
RKNN是Rockchip NPU平台使用的模型类型，以.rknn后缀结尾的模型文件，用户可以通过RKNNSDK提供的工具将自主研发的算法模型转换成RKNN模型。
# 非RKNN模型
对于 Caffe、TensorFlow 等其他模型，想要在 RK3588 平台运行，需要先进行模型转换。可以使用
RKNN-Toolkit2 工具将模型转换成 RKNN 格式。
# rknn-toolkit2安装
通过Tools/RKNN_V1.6.0目录下提供的文件直接获得rknn-toolkit2-1.6.0.tar.gz，这个是1.6.0的版
本，后续也会基于这个版本来演示和验证AI应用的开发。

也可以通过官方源码下载：git clone https://github.com/rockchip-linux/rknn-toolkit2.git

安装Python相关依赖环境

sudo apt-get update
sudo apt-get install python3 python3-dev python3-pip
sudo apt-get install libxslt1-dev zlib1g zlib1g-dev libglib2.0-0 libsm6 libgl1-
mesa-glx libprotobuf-dev gcc

安装rknn-toolkit2的版本依赖包

cd rknn-toolkit2
pip3 install -r packages/requirements_cp38-1.6.0.txt -i
https://mirror.baidu.com/pypi/simple

安装rknn-toolkit2 SDK工具包

pip3 install packages/rknn_toolkit2-1.6.0+81f21f4d-cp38-cp38-linux_x86_64.whl

在命令行输入python

test@test-virtual-machine:~/rknn-toolkit2/packages$ python
Python 3.8.10 (default, Mar 13 2023, 10:26:41)
[GCC 9.4.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> from rknn.api import RKNN

进入python环境后，输入 
from rknn.api import RKNN 
若没有出现错误，说明安装成功。同时按住
Ctrl+D 退出 Python环境。


# YOLOv5模型下载
cp rknn_model_zoo_models/examples/yolov5/yolov5s_relu.onnx
rknn_model_zoo/examples/yolov5/model/
# 模型转换
#进入源代码目录

cd rknn_model_zoo/examples/yolov5/model/

#模型转换

python convert.py ../model/yolov5s_relu.onnx rk3588 i8
../model/yolov5s_relu.rknn

转换后的模型保存路径为 rknn_model_zoo/examples/yolov5/model/yolov5s_relu.rknn。
