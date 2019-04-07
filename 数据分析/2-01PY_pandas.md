# Python科学计算: Pandas
1.Series

- Series是一个定长的字典序列
- Series有两个基本属性:index和values
- 示例代码

```python
import pandas as pd
from pandas import Series, DataFrame
x1 = Series([1,2,3,4])
x2 = Series(data=[1,2,3,4], index=['a', 'b', 'c', 'd'])
print x1
print x2

```


2.DataFrame

- DataFrame类型数据结构类似数据库
- 虚构王者荣耀考试场景输出几位英雄的考试成绩
- 示例代码
```python
import pandas as pd
from pandas import Series, DataFrame
data = {'Chinese': [66, 95, 93, 90,80],'English': [65, 85, 92, 88, 90],'Math': [30, 98, 96, 77, 90]}
df1= DataFrame(data)
df2 = DataFrame(data, index=['ZhangFei', 'GuanYu', 'ZhaoYun', 'HuangZhong', 'DianWei'], columns=['English', 'Math', 'Chinese'])
print(df1)
print(df2)
```

- 删除语法drop函数
- 删除列
```python
df2 = df2.drop(columns=['Chinese'])
```

- 删除行
```python
df2 = df2.drop(index=['ZhangFei'])
```

- 重命名列名columns，让列表名更容易识别
- 使用rename(columns=new_names, inplace=True)函数
```python
df2.rename(columns={'Chinese': 'YuWen', 'English': 'Yingyu'}, inplace = True)

```

- 去除重复的值
```python
df = df.drop_duplicates() # 去除重复行
```

- 格式问题
- 更改数据格式:astype()函数
```python
df2['Chinese'].astype('str') 
df2['Chinese'].astype(np.int64) 
```

- 数据间的空格:strip()函数
```python
# 删除左右两边空格
df2['Chinese']=df2['Chinese'].map(str.strip)
# 删除左边空格
df2['Chinese']=df2['Chinese'].map(str.lstrip)
# 删除右边空格
df2['Chinese']=df2['Chinese'].map(str.rstrip)
```

- 删除某个特殊符号
```python
df2['Chinese']=df2['Chinese'].str.strip('$')
```

- 大小写转化:upper(),lower(),title()函数
```python
# 全部大写
df2.columns = df2.columns.str.upper()
# 全部小写
df2.columns = df2.columns.str.lower()
# 首字母大写
df2.columns = df2.columns.str.title()

```

- 查找空格
```python
df.isnull()
de.isnull().any()
```

- 使用apply函数对数据进行清洗
- apply是自由度非常高的函数，使用频率也非常高
```python
df['name'] = df['name'].apply(str.upper)
```
对name列的数值都进行大写转化

- describe()函数
```python
df1 = DataFrame({'name':['ZhangFei', 'GuanYu', 'a', 'b', 'c'], 'data1':range(5)})
print df1.describe()
```