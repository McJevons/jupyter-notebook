
## Series
- Series类似一维数组，由一组数据`values属性`以及一组与之对应的索引`index属性`组成；
- 可以在生成Series时指定索引，也可以修改索引，在未指定索引的情况下，会自动创建0开始的整数型索引；
- 可通过索引方式选取Series中的单个或一组值，也可使用字典方式进行取值；
- 对于Series的运算不会影响到索引值；
- 也可以使用字典直接创建Series；


```python
import pandas as pd
```


```python
obj=pd.Series([4,-3,0,9])
```


```python
obj
```




    0    4
    1   -3
    2    0
    3    9
    dtype: int64




```python
obj.index # index属性选取索引值
```




    RangeIndex(start=0, stop=4, step=1)




```python
obj.values # values属性选取数据
```




    array([ 4, -3,  0,  9], dtype=int64)




```python
obj.index=['a','b','c','d'] # 修改索引值，可以使用字符串
```


```python
obj
```




    a    4
    b   -3
    c    0
    d    9
    dtype: int64




```python
obj['a'] # 使用单个索引值选取单个数据
```




    4




```python
obj[['b','c','d']] # 使用一个索引列表选取一组数据
```




    b   -3
    c    0
    d    9
    dtype: int64




```python
obj.d # 使用字典方式取值
```




    9




```python
obj[obj>0] # 对于Series的运算不会影响索引值
```




    a    4
    d    9
    dtype: int64




```python
obj*2
```




    a     8
    b    -6
    c     0
    d    18
    dtype: int64




```python
obj3=pd.Series({'m':7,'n':4}) # 使用字典直接创建Series
obj3
```




    m    7
    n    4
    dtype: int64



- 可以传入一组索引到已经存在的Series中，Series里数据的顺序将按传入的索引顺序进行排序，若有不存在的索引值，则该索引对应values为NaN；
- 使用`isnull`和`notnull`函数检测缺失的数据，可以是pandas函数也可以是实例方法；
- Series之间的运算结果，会根据索引自动对齐数据；


```python
obj1=pd.Series([4,-3,0,9],index=['w','x','y','z']) # 在生成Series时直接指定索引值
obj1
```




    w    4
    x   -3
    y    0
    z    9
    dtype: int64




```python
obj2=pd.Series(obj1,index=['y','x','u','w']) # 用传入的索引值进行排序，其中u值不存在，值为NaN
obj2
```




    y    0.0
    x   -3.0
    u    NaN
    w    4.0
    dtype: float64




```python
pd.isnull(obj2) # pandas函数
```




    y    False
    x    False
    u     True
    w    False
    dtype: bool




```python
obj2.notnull() # 实例方法
```




    y     True
    x     True
    u    False
    w     True
    dtype: bool




```python
'z' in obj2 # 判断索引是否存在
```




    False




```python
obj1,obj2
```




    (w    4
     x   -3
     y    0
     z    9
     dtype: int64, y    0.0
     x   -3.0
     u    NaN
     w    4.0
     dtype: float64)




```python
obj1+obj2 # 自动对齐数据，相同索引的数据进行计算，其余索引计算结果为NaN
```




    u    NaN
    w    8.0
    x   -6.0
    y    0.0
    z    NaN
    dtype: float64



- Series对象本身及其索引都有`name`属性。


```python
obj2.name='Series对象name'
```


```python
obj2.index.name='索引name'
```


```python
obj2
```




    索引name
    y    0.0
    x   -3.0
    u    NaN
    w    4.0
    Name: Series对象name, dtype: float64


