Learning torch
==============

Today read Chapter 5. Have learned the mechanics of learning.

## basic torch operation
- \* / mul 对应位的元素直接乘（broadcast参看boradcast的说明）
- mm / matmul 矩阵乘
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
