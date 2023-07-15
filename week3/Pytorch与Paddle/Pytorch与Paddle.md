## Pytorch与Paddle

### 一、Pytorch快速笔记

参考：https://pytorch.apachecn.org/1.4/blitz/tensor_tutorial/

#### 1.张量

`Tensor`(张量）类似于`NumPy`的`ndarray`，但还可以在GPU上使用来加速计算

```python
x = torch.zeros(5, 3, dtype=torch.long)
print(x)
print(x.size())
#torch.Size本质上还是tuple，所以支持tuple的一切操作。
```

张量可以创建，进行多种运算

```python
result = torch.empty(5, 3)
torch.add(x, y, out=result)
print(result)
```

这里特意提出原地操作

```python
# adds x to y
y.add_(x)
print(y)
```

> 任何一个in-place改变张量的操作后面都固定一个`_`。例如`x.copy_(y)`、`x.t_()`将更改x

也可以使用像标准的NumPy一样的各种索引操作：

```python
print(x[:, 1])
#取所有行，然后取第一列 （从0开始）
```

如果想改变形状，可以使用`torch.view`

如果是仅包含一个元素的tensor，可以使用`.item()`来得到对应的python数值

#### 2.Pytorch与Numpy

将一个Torch张量转换为一个NumPy数组是轻而易举的事情，反之亦然。

Torch张量和NumPy数组将共享它们的底层内存位置，因此当一个改变时,另外也会改变。

看改变NumPy数组是如何自动改变Torch张量的：

```python
import numpy as np
a = np.ones(5)
b = torch.from_numpy(a)
np.add(a, 1, out=a)
print(a)
print(b)
```

张量可以使用`.to`方法移动到任何设备(device）上：

```python
# 当GPU可用时,我们可以运行以下代码
# 我们将使用`torch.device`来将tensor移入和移出GPU
if torch.cuda.is_available():
    device = torch.device("cuda")          # a CUDA device object
    y = torch.ones_like(x, device=device)  # 直接在GPU上创建tensor
    x = x.to(device)                       # 或者使用`.to("cuda")`方法
    z = x + y
    print(z)
    print(z.to("cpu", torch.double))       # `.to`也能在移动时改变dtype
```

输出：

```python
tensor([1.0445], device='cuda:0')
tensor([1.0445], dtype=torch.float64)
```

#### 3.自动求导

`torch.Tensor` 是这个包的核心类。如果设置它的属性 `.requires_grad` 为 `True`，那么`autograd`将会追踪对于该张量的所有操作。当完成计算后可以通过调用 `.backward()`，来自动计算所有的梯度。这个张量的所有梯度将会自动累加到`.grad`属性.

要阻止一个张量被跟踪历史，可以调用 `.detach()` 方法将其与计算历史分离，并阻止它未来的计算记录被跟踪。

为了防止跟踪历史记录(和使用内存），可以将代码块包装在 `with torch.no_grad():` 中。在评估模型时特别有用，因为模型可能具有 `requires_grad = True` 的可训练的参数，但是我们不需要在此过程中对他们进行梯度计算。

更多例子详见下面的网站

https://pytorch.apachecn.org/1.4/blitz/autograd_tutorial/

**疑问点：** 举雅个比的例子  如果不是标量，则传递参数

雅可比向量积的这一特性使得将外部梯度输入到具有非标量输出的模型中变得非常方便。

现在我们来看一个雅可比向量积（vector-Jacobian product）的例子:

```python
x = torch.randn(3, requires_grad=True)

y = x * 2
while y.data.norm() < 1000:
    y = y * 2

print(y)
```

输出：

```python
tensor([-278.6740,  935.4016,  439.6572], grad_fn=<MulBackward0>)
```

在这种情况下，`y` 不再是标量。`torch.autograd` 不能直接计算完整的雅可比矩阵，但是如果我们只想要雅可比向量积，只需将这个向量作为参数传给 `backward`：

```python
v = torch.tensor([0.1, 1.0, 0.0001], dtype=torch.float)
y.backward(v)

print(x.grad)
```

输出：

```python
tensor([4.0960e+02, 4.0960e+03, 4.0960e-01])
```



#### 4.torch.nn 来构建神经网络

一个神经网络的典型训练过程如下：

- 定义包含一些可学习参数(或者叫权重）的神经网络
- 在输入数据集上迭代
- 通过网络处理输入
- 计算loss(输出和正确答案的距离）
- 将梯度反向传播给网络的参数
- 更新网络的权重，一般使用一个简单的规则：`weight = weight - learning_rate * gradient`

同时学习损失函数和优化器调用

其他更多例子详见官网，后续再补充



