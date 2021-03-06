# （四）view用法

在pytorch中view函数的作用为重构张量的维度，相当于numpy中resize()的功能（见文末），但是用法可能不太一样。如下例所示：

```python
>>> import torch
>>> tt1=torch.tensor([-0.3, -0.6,  0.7,  0.4,  0.3,  0.1])
>>> result=tt1.view(3,2)
>>> result
tensor([[-0.3, -0.6],
        [ 0.7,  0.4],
        [ 0.3,  0.1]])
```

1、torch.view(参数a，参数b，...)

​		在上面例子中参数a=3和参数b=2决定了将一维的tt1重构成3x2维的张量。

2、torch.view(-1)或者torch.view(参数包含-1)，转换成一维结构：

```python
>>> import torch
>>> tt2=torch.tensor([[-0.1, -0.2],
...         [ 0.3,  0.4],
...         [ 0.5,  0.6]])
>>> result=tt2.view(-1)
>>> result
tensor([-0.1, -0.2,  0.3,  0.4,  0.5,  0.6])
```

3、torch.view(参数a=-1，或参数b=-1)，则表示在参数**部分未知**情况下自动补齐列向量长度。

例：a=-1,b=3，tt3总共由6个元素，则a=6/3=2。

```python
>>> import torch
>>> tt3=torch.tensor([[-0.1, -0.2],
...         [ 0.3,  0.4],
...         [ 0.5,  0.6]])
>>> result=tt3.view(-1, 3)
>>> result
tensor([[-0.1, -0.2,  0.3],
       [0.4,  0.5,  0.6]])
```



---

## 附：numpy中，resize()、reshape()用法比较：

```python
>>>import numpy as np
...
...a = np.arange(20).reshape(4,5)
...a
OUT[]:array([[ 0,  1,  2,  3,  4],     
	  		 [ 5,  6,  7,  8,  9],    
	   		 [10, 11, 12, 13, 14],   
			 [15, 16, 17, 18, 19]])
>>>a.reshape(2,10) #  有返回值的函数
OUT[]:array([[ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9],  
		     [10, 11, 12, 13, 14, 15, 16, 17, 18, 19]])
>>>a
OUT[]:array([[ 0,  1,  2,  3,  4],     
	  		 [ 5,  6,  7,  8,  9],    
	   		 [10, 11, 12, 13, 14],   
			 [15, 16, 17, 18, 19]])
#reshape()后，a的形状没有改变

>>>a.resize(2,10) #  void函数
...a
OUT[]:array([[ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9],   
	  		 [10, 11, 12, 13, 14, 15, 16, 17, 18, 19]])
#resize()后，a的形状发生改变    
    
```
两个函数都是改变数组的形状。但是resize会修改自身参数；reshape返回修改参数之后的矩阵，但原参数不变。
