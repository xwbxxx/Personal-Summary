# gather函数的用法

首先，先给出torch.gather函数的函数定义：

```python
torch.gather(input, dim, index, out=None) → Tensor
# 或：
input.gather(dim, index, out=None) → Tensor
    
```

官方给出的解释是这样的：沿给定轴dim，将输入索引张量index指定位置的值进行聚合。对一个3维张量，输出可以定义为：

```python 
out[i][j][k] = tensor[index[i][j][k]]  [j][k] # dim=0
out[i][j][k] = tensor[i] [index[i][j][k]] [k] # dim=1
out[i][j][k] = tensor[i][j]  [index[i][j][k]] # dim=3
```

例1：

```python
import torch

y_hat = torch.tensor([[0.1, 0.2, 0.3], [0.4, 0.5, 0.6]])
y_gather = y_hat.gather(1, torch.LongTensor([[2], [0]])) 
# 行数必须相同，列标、列数可以不同

print(y_hat, '\n', y_gather)  # gather 不改变原tensor的结构
```

结果：y_gather的元素即为按列(dim=1)聚合,根据索引：

- 第一行输出y_hat [0] [==2==]=0.3
- 第二行输出 y_hat [1] [==0==] =0.4

```
tensor([[0.1000, 0.2000, 0.3000],
        [0.4000, 0.5000, 0.6000]]) 
tensor([[0.3000],
        [0.4000]])
```

例2：

```python
>>>z_gather = y_hat.gather(0, torch.LongTensor([[0, 1, 0]])) 
	# 列数必须相同，行标、行数可以不同
```

结果：y_gather的元素即为按行(dim=0)聚合,根据索引：

- 第一列输出y_hat [==0==] [0] = 0.1

- 第二列输出y_hat [==1==] [1] = 0.5

- 第二列输出y_hat [==0==] [2] = 0.3

  ```tensor([[0.1000, 0.5000, 0.3000]])```

==！！！特别注意一下，index的类型必须是LongTensor类型的！！！== 

