# -midterm
### 使用CNN网络模型(自己设计或使用现有的CNN架构，如AlexNet，ResNet-18)作为baseline在CIFAR-100上训练并测试；对比cutmix, cutout, mixup三种方法以及baseline方法在CIFAR-100图像分类任务中的性能表现；对三张训练样本分别经过cutmix, cutout, mixup后进行可视化，一共show 9张图像。
### 在VOC数据集上训练并测试目标检测模型Faster R-CNN和YOLO V3；在四张测试图像上可视化Faster R-CNN第一阶段的proposal box；两个训练好后的模型分别可视化三张不在VOC数据集内，但是包含有VOC中类别物体的图像的检测结果（类别标签，得分，boundingbox），并进行对比，一共show六张图像；

## Resnet-18
1. 数据集准备：在网络上下载好CIFAR10数据集，解压后放入根目录中，也可以直接用torchvision.datasets.CIFAR10函数下载。    
**本文使用VOC格式进行训练，训练前需要下载好VOC07+12的数据集，解压后放在根目录**  

2. 直接运行mixup、cutmix、baseline、cutout文件即可开始训练和测试。
3. 本次实验由于主要目的是比较mixup、cutup和cutmix三种方法的性能表现，因而不对Resnet网络结构进行调整。
将Batch_size设置为128，将epoch设置为100,
优化器则选择最简单的SGD，其中将momentum参数设置为0.9，weight_decay值即权值衰减率设置为0.0005。初始学习率定位0.1。损失函数才用交叉熵损失函数，对模型的预测结果的评价指标采用Accuracy = 1 – 总体错分率。

## Faster R-CNN
### 模型权重文件
主干的网络权重可以在百度云下载。  
下载后需要在模型类的py文件中修改相应的权重路径

### VOC数据集
VOC数据集需自行下载并进行划分。 

### 训练步骤
1. 数据集的准备   
**训练前需要下载好VOC数据集，解压后放在根目录**  

2. 数据集的处理   
修改voc_annotation.py里面的annotation_mode=2，运行voc_annotation.py生成根目录下的2007_train.txt和2007_val.txt。   

3. 开始网络训练   
train.py的默认参数用于训练VOC数据集，直接运行train.py即可开始训练。   

### 预测步骤  
1. 查看最终预测结果
训练结果预测需要用到两个文件，分别是frcnnpre.py和predict.py。需要去frcnnpre.py里面修改model_path，改为训练后模型权重路径。   
**model_path指向训练好的权值文件，在logs文件夹里。   
classes_path指向检测类别所对应的txt。**   
完成修改后就可以运行predict.py进行检测了。运行后输入图片路径即可检测。  

2. 查看第一阶段Proposal结果
方法类似1，但需要在frcnnrpn.py中修改model_path,再于predict.py中导入frcnnrpn模块，运行predict.py即可。

## YOLO
### 训练步骤
#### a、训练VOC07+12数据集
1. 数据集的准备   
**本文使用VOC格式进行训练，训练前需要下载好VOC07+12的数据集，解压后放在根目录**  

2. 数据集的处理   
修改voc_annotation.py里面的annotation_mode=2，运行voc_annotation.py生成根目录下的2007_train.txt和2007_val.txt。   

3. 开始网络训练   
train.py的默认参数用于训练VOC数据集，直接运行train.py即可开始训练。   

4. 训练结果预测   
训练结果预测需要用到两个文件，分别是yolo.py和predict.py。我们首先需要去yolo.py里面修改model_path以及classes_path，这两个参数必须要修改。   
**model_path指向训练好的权值文件，在logs文件夹里。   
classes_path指向检测类别所对应的txt。**   
完成修改后就可以运行predict.py进行检测了。运行后输入图片路径即可检测。
