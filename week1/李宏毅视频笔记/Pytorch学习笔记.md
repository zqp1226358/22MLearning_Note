## Pytorch的学习

### 一、总体概述

在pytorch的网络训练是不断训练验证最后再测试的过程

使用pytorch 这个框架我们经常会用到以下工具：

- Dataset & Dataloader  帮助我们进行数据加载
- Tensors  数据的形式
- torch.nn  （Models，Loss Functions） 创建网络模型，选择一些损失函数
- torch.optim: Optimization  选择优化函数  找到最优解
- Save/load models  保存模型权重

基本网络模型训练都会用到以上工具，下面进行详细介绍

### 二、数据加载 Dataset & Dataloader

首先展示一个基本模板

```python
from torch.utils.data import Dataset,DataLoader

class MyDataset(data.Dataset):
    # Read data & preprocess
    def __init__(self,imgsPath):
        self.imgs_path=imgsPath    # 图片路径  
    
    #Returns one sample at a time
    #由给定的key获取数据集中每一个图片的操作函数
    def __getitem__(self,index):
        return self.imgs_path[index]
    
    #return the size of the dataset
    #获取数据集中图片大小的函数
    def __len__(self):
        return len(self.imgs_path)
```

> https://blog.csdn.net/weixin_45662399/article/details/127386185

 DataLoader是一个可迭代的数据装载器，组合了数据集和采样器，并在给定数据集上提供[可迭代对象](https://so.csdn.net/so/search?q=可迭代对象&spm=1001.2101.3001.7020)。可以完成对数据集中多个对象的集成。



pytorch中数据常见的形式是张量，我们可以对张量做各种操作，需要注意维度这个点。

有些方法和numpy 类似

根据电脑情况使用cpu或者gpu

### 三、网络模型构建 torch.nn

可以使用module模块或Sequential层两种方式去实现，后者一般适合顺序的，前者可以自定义传播。

####module模块：

- 所有神经网络模块的基类，既可以表示神经网络中的某个层(layer)，也可以表示一个包含很多层的神经网络。

- 需要重写两个方法 init方法和forward方法

```python
import torch.nn as nn
import torch.nn.functional as F
 
class Model(nn.Module):
    def __init__(self):
        super().__init__()
        self.conv1 = nn.Conv2d(1, 20, 5)
        self.conv2 = nn.Conv2d(20, 20, 5)
 
    def forward(self, x):
        x = F.relu(self.conv1(x))
        return F.relu(self.conv2(x))
```

####Sequential层使用

```python
model = nn.Sequential(
          nn.Conv2d(1,20,5),
          nn.ReLU(),
          nn.Conv2d(20,64,5),
          nn.ReLU()
        )

```

####卷积

torch.nn.functional.conv2d(input, weight, bias=None, stride=1, padding=0, dilation=1*, groups=1) → [Tensor](https://pytorch.org/docs/stable/tensors.html#torch.Tensor)

input 和weight要求的shape为四维，需要reshape

#### 池化

```python
 # 设置池化
 self.maxpool1 = MaxPool2d(kernel_size=3,ceil_mode=False)
```

#### 非线性激活层

非线性变换的主要目的就是给网中加入一些非线性特征，非线性越多才能训练出符合各种特征的模型。常见的非线性激活函数有：relu、sigmond等。

####线性层

torch.nn.Linear(*in_features*, *out_features*, *bias=True*, *device=None*, *dtype=None*)

### 四、损失函数Loss

**预测值和真实值的差值成为损失**

可以选择MSELoss函数或者CrossEntropyLoss函数

### 五、优化 函数optimization

常见的有SGD等

### 六、整体流程组合

```python
#前期准备
dataset = MyDataset(file) 
tr_set = DataLoader(dataset, 16, shuffle=True) 
model = MyModel().to(device) 
criterion = nn.MSELoss() 
optimizer = torch.optim.SGD(model.parameters(), 0.1)

#多次epoch 训练
for epoch in range(n_epochs): 
    model.train() 
    for x, y in tr_set: 
        optimizer.zero_grad() 
        x, y = x.to(device), y.to(device) 
        pred = model(x) 
        loss = criterion(pred, y) 
        loss.backward() 
        optimizer.step()

#验证数据集 Neural Network Evaluation (Validation Set)
model.eval() 
total_loss = 0 
for x, y in dv_set: 
    x, y = x.to(device), y.to(device) 
    with torch.no_grad():#不希望进行梯度计算 
        pred = model(x) 
        loss = criterion(pred, y) 
        total_loss += loss.cpu().item() * len(x) 
        avg_loss = total_loss / len(dv_set.dataset)

#测试数据集 Neural Network Evaluation (Testing Set)
model.eval() 
preds = [] 
for x in tt_set: 
    x = x.to(device) 
    with torch.no_grad(): 
        pred = model(x) 
        preds.append(pred.cpu())
```



### 七、保存模型/加载模型  Save/load models

```python
#Save 
torch.save(model.state_dict(), path) 
# Load 
ckpt = torch.load(path) 
model.load_state_dict(ckpt)
```







> **References** 
>
> ● Machine Learning 2021 Spring Pytorch Tutorial 
>
> ● Official Pytorch Tutorials 
>
> ● https://numpy.org/ 