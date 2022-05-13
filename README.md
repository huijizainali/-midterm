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
本实验中采用的学习率衰减策略为余弦退火。余弦退火（Cosine annealing）可以通过余弦函数来降低学习率。余弦函数中随着x的增加余弦值首先缓慢下降，然后加速下降，再次缓慢下降。在本实验中，一共选择了两种，分别是随机梯度下降和Adam算法，区别在于Adam 通过计算梯度的一阶矩估计和二阶矩估计而为不同的参数设计独立的自适应性学习率。因此在全模型训练阶段，为了提升速度，采用Adam优化器；而在冻结了诶backbone训练中，采用了随机梯度下降优化器。在本实验中，对类别损失，采用了交叉熵的损失函数，原因在于面对多分类任务时，交叉熵损失函数计算效率要高于均方误差损失函数，可以使得梯度下降更快；而对于回归损失，采用了均方误差作为损失函数。而在汇报训练与验证损失时，将两部分损失进行了求和最为模型最终损失。总共训练epoch数为150。

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
