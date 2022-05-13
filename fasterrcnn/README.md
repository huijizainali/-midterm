## 模型权重文件
主干的网络权重可以在百度云下载。  
下载后需要在模型类的py文件中修改相应的权重路径

## VOC数据集
VOC数据集需自行下载并进行划分。 

## 训练步骤
1. 数据集的准备   
**训练前需要下载好VOC数据集，解压后放在根目录**  

2. 数据集的处理   
修改voc_annotation.py里面的annotation_mode=2，运行voc_annotation.py生成根目录下的2007_train.txt和2007_val.txt。   

3. 开始网络训练   
train.py的默认参数用于训练VOC数据集，直接运行train.py即可开始训练。   

## 预测步骤  
1. 查看最终预测结果
训练结果预测需要用到两个文件，分别是frcnnpre.py和predict.py。需要去frcnnpre.py里面修改model_path，改为训练后模型权重路径。   
**model_path指向训练好的权值文件，在logs文件夹里。   
classes_path指向检测类别所对应的txt。**   
完成修改后就可以运行predict.py进行检测了。运行后输入图片路径即可检测。  

2. 查看第一阶段Proposal结果
方法类似1，但需要在frcnnrpn.py中修改model_path,再于predict.py中导入frcnnrpn模块，运行predict.py即可。