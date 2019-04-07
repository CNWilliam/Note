# 使用 NumPy 让你的 Python 科学计算更高效


- 创建数组（示例代码）
```python
import numpy as np
a = np.array([1, 2, 3])
b = np.array([[1, 2, 3, ], [4, 5, 6], [7, 8, 9]])
b[1,1] = 10
print(a.shape)
print(b.shape)
print(a.dtype)
print(b)
```

- 结构数组（示例代码）
```python

import numpy as np
persontype = np.dtype({
    'names':['name', 'age', 'chinese', 'math', 'english'],
    'formats':['S32','i', 'i', 'i', 'f']})
peoples = np.array([("ZhangFei",32,75,100, 90),("GuanYu",24,85,96,88.5),
       ("ZhaoYun",28,85,92,96.5),("HuangZhong",29,65,85,100)],
    dtype=persontype)
ages = peoples[:]['age']
chineses = peoples[:]['chinese']
maths = peoples[:]['math']
englishs = peoples[:]['english']
print(np.mean(ages))
print(np.mean(chineses))
print(np.mean(maths))
print(np.mean(englishs))
print(peoples.dtype)
```

- 连续数组
```python
x1 = np.arange(1,11,2)
x2 = np.linspace(1,9,5)
```
- 算数运算
```python

x1 = np.arange(1,11,2)
x2 = np.linspace(1,9,5)
print (np.add(x1, x2)) #相加
print (np.subtract(x1, x2))#相减
print (np.multiply(x1, x2))#相乘
print (np.divide(x1, x2))
print (np.power(x1, x2))
print (np.remainder(x1, x2))#取余数
print (np.mod(x1, x2))#取余数

```

- 统计函数（amin、amax）
```python
a = np.array([[1, 2,3 ], [4, 5, 6], [7, 8, 9]])
print(np.amin(a))
print(np.amin(a,0))
print(np.amin(a,1))
print(np.amax(a))
print(np.amax(a,0))
print(np.amax(a,1))

```

- 统计最大值和最小值之差 ptp()

```python
a = np.array([[1,2,3], [4,5,6], [7,8,9]])
print(np.ptp(a))
print(np.ptp(a,0))
print(np.ptp(a,1))
```

- 统计数组的百分位数percentile()
```python
a = np.array([[1,2,3], [4,5,6], [7,8,9]])
print(np.percentile(a, 50))
print(np.percentile(a, 50, axis = 0))
print(np.percentile(a, 50, axis = 1))
```
*p = 0是求最小值，p = 50是求平均值， p = 100是求最大值

- 统计数组中的中位数median()、平均数mean()

```python
a = np.array([[1,2,3], [4,5,6], [7,8,9]])
# 求中位数
print(np.median(a))
print(np.median(a, axis=0))
print(np.median(a, axis=1))
# 求平均数
print(np.mean(a))
print(np.mean(a, axis=0))
print(np.mean(a, axis=1))
```

- 统计数组中的加权平均值 average()

```python
a = np.array([1,2,3,4])
wts = np.array([1,2,3,4])
print(np.average(a))
print(np.average(a,weights=wts))
```

- 统计数组中的标准差std()、方差var()

```python
a = np.array([1,2,3,4])
print(np.std(a))
print(np.var(a))
```

*方差= mean((x - x.mean())** 2)

## Numpy排序
*排序是算法中使用频率最高的一种，也是数据分析工作中常用的方法*
使用sort函数:
sort(a,axis=-1,kind='quicksort',order=None),
默认情况下使用的是快速排序；
在kind里可以指定quicksort、mergesort、heapsort分别表示快速排序、合并排序、堆排序
同样axis默认也是-1，沿着数组的最后一个轴进行排序，也可以取不同的axis轴,或者axis=None代表采用扁平化的方式作为一个向量进行排序。
order字段，对于结构化的数组可以指定按照某个字段进行排序

```python
a = np.array([[4,3,2],[2,4,1]])
print(np.sort(a))
print(np.sort(a, axis=None))
print(np.sort(a, axis=0))
print(np.sort(a, axis=1))
```

- 作业