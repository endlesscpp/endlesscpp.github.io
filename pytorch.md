Learning torch
==============

Today read Chapter 7. Have learned full connected network.

## basic torch operation
- \* / mul 对应位的元素直接乘（broadcast参看boradcast的说明）
- mm / matmul 矩阵乘
- unsqueeze(input, dim) 
        
        在dim处插入一维 [1,2,3,4], dim=0 => [[1,2,3,4]]; dim=1 =>[[1],[2],[3],[4]]
        src shape是(4), dim=0时，shape为(1，4); dim=1时，shape为(4,1)
- view(*shape)

        参数中-1表示根据其它维数，算出剩余的维数。比如：
        
```python
        x = torch.randn(4,4)
        torch.Size([4,4])
        y = x.view(-1,2)
        torch.Size([8,2])
        z = x.view(-1)
        torch.Size([16])
```

- concat
- stack

        ```python
        x1 = torch.ones(3, 4)
        x2 = torch.ones(3, 4)
        print(x1)
        ans = torch.stack([x1, x2], dim=1)
        print(ans.shape)
        ```

        ans
        - dim == 0: [2,3,4]
        - dim == 1: [3,2,4]
        - dim == 2: [3,4,2]

- numel
   - How many elements in each tensor instance

### broadcast
1. 如果某一个维度size==1（假设值为a），另一个tensor中该维度所有元素都乘以这个值a
2. 如果所有的size都大于1，那么size必须相等
3. 如果一个tensor a 比另一个b维度高，那么a * b相当于先把b复制扩充到和a同纬度，然后对应相乘。和某个维度size=1类似：

```python
a = torch.tensor([1,2])
b = torch.tensor([[3,4], [5,6]])
d = a * b
tensor([[3, 8],
        [5,12]])
```

## Mechanics of learning
- compute the derivative of loss.

```python
#d loss_fn / d w = (d loss_fn / d t_p) * (d t_p / d w)
```

## Use neural network to fit the data
- curve is caused by activation function, such as nn.Tanh()
- neural network has a tendency to overfit.
- optim.SGD: Stochastic Gradient Descent(随机梯度下降) 为了批量优化

tips:
how to control the color of matplotlib
```python
plt.plot(t_u.numpy(), t_c.numpy(), 'o', color='red')
plt.plot(t_range.numpy(), seq_model(0.1 * t_range).detach().numpy(), 'c-')
plt.plot(t_u.numpy(), seq_model(0.1 * t_u).detach().numpy(), 'kx')
```

## Learning from images
nn.CrossEntropyLoss 等于 nn.LogSoftmax和nn.NLLLoss的组合
用DataLoader每个epoch训练一小批样本


全连接模型的局限性：
- 没有平移不变性
- 消耗算力过多

## Using convolutions to generalize
- conv weight tensor:
    - out_ch * in_ch * kernel_width * kernel_height
- conv:
    一个输入channel个数（比如RGB），一个输出channel个数
- subclass nn.Module
- functional API
    - torch.tanh
    - nn.functional.max_pool2d
- 模型是状态的容器，以Parameters,submodules和instructions一起做forward.
- 保存和加载模型
- 在GPU上训练时:
     - 把从dataloader中得到的tensor传入GPU(nn.tensor.to) 
     - 把参数传入GPU（nn.Module.to)
    
- add memory capacity: width
- 模型规范化：
    - weight penality(权重惩罚）: L2 regularization(weight decay): 权重衰减
    - dropout: 不依赖太多单一输入
    - batch normalization (需要重看）
    
- depth:
    - 浅的网络能识别人的形状
    - 深的网络能识别脸上的嘴巴
    
- residual network
    - 做了一个skip connection（短路连接）


