Learning torch
==============

Today read Chapter 5. Have learned the mechanics of learning.

## basic torch operation
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

## Mechanics of learning
- compute the derivative of loss.

```python
#d loss_fn / d w = (d loss_fn / d t_p) * (d t_p / d w)
```
