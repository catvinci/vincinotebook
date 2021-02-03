# 利用Python数据分析（工具篇）

## 目录

[toc]

## 一、NumPy基础

`import numpy as np`

### 1.1 ndarry——多维数组对象

1.1.1 **创建ndarray**

```python
array（list，dtype=） # 将输入的序列类型转换为ndarray，如果不指定类型则自动判断
arange(num) # 返回一个等差数列

eye()  identity() #生成与给定形状一样的全1数组

ones（） #生成与给定形状一样的全1数组
zeros（） #生成与给定形状一样的全0数组
empty() #生成与给定形状一样的空数组
full(size,num) #根据给定形状和数据类型生成数值一样的数组
#以上的函数可以加_like 变成根据一个数组的大小来生成

reshape((x,y)) #使得一个序列进行array样式变化
```

1.1.2 **ndarray的数据类型**

数据类型，是dytpe属性，代表了数组里面每个数据的类型。

```python
# 常见的类型
int 64 #有符号的64位整数
uint64 #无符号的64位整数

float64 # 单精度浮点数。兼容c语言的float
float64 # 双精度浮点数。兼容c语言的double

comple #64位的复数

boll #布尔类型
object #对象类型
string_ #字符串类型
```

可以使用`astype`来转换数据的类型，使用他转换时会生成一个全新的数组对象。



### 1.2 基本运用

1.2.1 **算数运算**

优点：以ndarry为对象可以进行批量运算而不用使用`for`语句。

使用：使用带有标量的运算符的时候，会把每一个都对应到元素内。

*即使是乘法也是把里面的每个元素相乘*

也可以使用=判断两个矩阵是否完全一样。

1.2.2 **基础索引与切片**

*切片提取的时候需要注意，并没有重新复制一个数组，新得到的还是指向原本是数组*

一纬数组的切片和读取与自带的列表一样。

对于多维的数组(都是从0开始)

```python
#方法一
arr[1][3]
#方法二
arr[1,3]
```

我们也可以在方法一的情况下省略后面的值，返回降低一个维度的内容。

我们也可以对于高维数组的部分进行切片

```python
我们可以使用 :2 来代表前面2（行，列）#这只能用在使用方法2进行读取
使用一个：就是代表全部
```

对一个切片赋值的时候，会对全部赋值。

1.2.3  **布尔索引**

在进行索引的时候使用和行数对应的bool值。

```python
# 基础用法（bool值的数量与行数和列数一样）
data[[ True, False,True]] #读取输出date的1，3两行
data[:,[True,False]] #读取date的第一列

# 常见用法（读取符合是bob与alex名字位置对应的data行）
name=np.array(['bob','jone','bob'，'Alex'])
data[(name=='bob') | (alex=='alex') ]

#也可以用来设置数组的值（将负数都变成0）
data[data<0] =0
```

1.2.4 **神奇索引**

神奇索引又可以称为整数索引，可以使用一个整数数组来索引并*复制*出那一块的所有行。

```python
#基础用法
arr[[4,3,2,5]] #复制出arr里面的4，3，2，5列

#交错取值
arr[[4,3,2],[1,3,2]]  #取出4行1列的元素……
```

1.2.5 **数组换轴与转置**

计算矩阵的内积：`np.dot()`

转置，可以直接使用数组的`T`属性，得到转置后的样子，也可以使用`.transpose`方法使数组进行转置（都不改变原数组）

而对于更高纬度的数组，使用转置可以达到置换轴的作用。



### 1.3 通用函数（ufunc）

对于简单函数向量化的封装。

常见的一元通用函数：

```python
abs,fabs #计算实数或者复数的绝对值
sqrt #取每一个的绝对值
square #取每一个的平方
exp #取每一个的e^x
log,log10,log1p #取每一个的loge log10 以及log（1+x）

sign #计算每一个的符号值
ceil #计算比这个元素大的第一个整数
floor #计算比这个元素小的第一个整数
rint #在不改变类型的情况下将元素保留到整数位
modf #将小数与整数两个部分分别返回

isnan #返回元素是否是一个非数值类型
isfinite,isinf # 返回数组内元素是否有限是否无限

sin,cos,tan #三角函数
arccos,arccosh,arcsin #反三角函数

logical_not #全部取反
max #计算数组内的最大值
min #计算数组内的最小值
```

常见的二元通用函数

```python
add = +
multiply = *
divide,floor_divide = /,//
mod #求模计算
power # 将第二个作为第一个的幂次方

subtract #在第二个数组中将第一个所包含的元素去除
maximun,fmax #两个对应的元素相互比较，计算元素的最大值（第二个可以忽略num）
minimum,fmin #两个对应的元素相互比较，计算元素的最小值（第二个可以忽略num）

copysign #将第一个的符号改为第二个的符号
```



### 1.4 面向数组编程

1.4.1 **将条件逻辑作为数组操作**

我们可以使用`np.where`来代替原生python的三元运算

```python
result=np.where(cond,true,false)

# 第一个参数是判断条件，二三两个代表的是选项
# 之后两个可以不是向量而是标量
```

1.4.2 **数学和统计方法**

我们可以使用聚合函数（如sum，mean，std），他们可以作为顶层函数使用，也可以作为数组实例的一个方法来使用。

```python
arr.mean与np.mean(arr)等价

# 基础的数学统计方法

sum  #按照轴向计算所有元素的累加
mean #按照轴向计算元素的平均值
std，var # 计算标准差与方差
min，max # 计算最小（大）值
cumsun # 从0开始元素的累加
cumprod #从0开始元素的累乘
## 以上函数自带一个参数：axis来给定轴向，0代表按行求和，1代表按列求和
argmin，argmix # 找到最小（大）的位置
```

1.4.3  **布尔数组的使用方法**

布尔类型的数组有两个常用的方法

```python
any #检查数组内是否有一个true
all #检查数组内是否全都是true
```

对于非布尔类型使用的时候，除了0都是true

1.4.4 **排序方法**

我们可以使用python自带的sort方法对数组进行排序

```python
arr.sort(axis=) #来指定排序的轴
```

也可以使用numpy的sort，来返回一个排序好的拷贝数组（并未对元素组进行排序）

1.4.5 **唯一值和其他集合逻辑**

```python
unique(x) #计算x中唯一值，并进行排序
intersectld(x,y) #计算x与y的交集再排序
unionld (x,y) #计算x与y的并集再排序
inld(x,y) #计算x的元素是否都在y里面（返回bool）
setdiffld(x,y) # 计算差集，在x中单不在y中的x的元素
setxorld(x,y) #异或集，在x或y中，但不同时在x与y中的元素
```



### 1.5 对文件的使用

我们可以使用numpy的内置函数对文件进行基础的读取。

```python
np.save('name',arr) #保存文件
np.load('name') #加载文件
no.savez('name',a=arr1,b=arr2) #保存多个文件
```



### 1.6 线性代数使用

在python的矩阵运算中，矩阵的加法减法与线性代数没有区别，其中的乘法不一样。

矩阵的乘法使用dot函数或@操作符完成，在作用于一维数组的时候，是向量的点乘，即把对应元素相乘再求和，而对于矩阵等高纬度，就是矩阵的叉乘，即一般的矩阵乘法。

**常用的运算函数列表**

```python
dot() #向量点乘，矩阵乘法
trace() #计算对角元素和
diag() #将一个方阵的对角元素作为一个一维数组返回，或者将一维数组转换成一个方阵，并且在非对角线上都为零。
det() #计算矩阵的行列式
eig() #计算方阵的特征值和特征向量
inv() #计算方阵的逆矩阵
pinv() #计算矩阵的Moore-Penrose伪逆
qr() #计算QR分解
svd() #计算奇异值分解
solve() #计算线性系统 Ax=b
lstsq() #计算Ax=b的最小二乘解
```

### 1.7 伪随机数使用

Numpy中的random模块填补了普通随机数生成的不足，可以高效的生成各种模式的样本。

这些随机数是由具有确定性行为的算法根据随机数生成器中的*随机数种子*来生成的。

在np.random中常用的生成函数

```python
normal #从正态高斯分布中抽取样本
seed #向随机数生成器传递随机状态种子
permutation #返回一个数列的随机排列。或者返回一个乱序的整数范围序列
shuffle #随机排列一个序列
rand #从均匀分布中抽取样本
randint #根据给定的由低到高的范围抽取随机整数
randn #从均值0方差1的正态分布中抽取样本
binomial #从二项分布中抽去样本
beta #从beat分布中抽取样本
chisquare#从卡方分布中抽取样本
gamma #从伽马分布中抽取样本
uniform #从均匀[0,1)分布中抽取样本
```

numpy的随机数使用一个全局随机数种子，为了避免这种全局状态，我们可以用`RandomState`创建一个随机数生成器。

---



## 二、Pandas基础

`import pandas as pd`

### 2.1 serise

Series是一个一维数组对象，他包含了一个值序列，同时还有数据标签（索引，*index*）。

也可以理解为长度固定并且有序的字典。

```python
# 基本创建
obj = pd.series([list]) #只添加序列值，索引将从0到n-1
obj = pd.series([list],index=list2) #指定索引序列创建
obj1 =pd.series(dir) # 我们也可以使用字典类型直接声称一个series

# 我们可以获取信息
obj.values # 获取序列值
obj.index # 获取索引
```

于ndarry相比，使用series对象来创建可以使用索引值进行索引。

对于在np中可以使用的函数，对于series也同样可以使用。

```python
# 对于serise中可以存在缺失数据的情况
obj.isnull
obj.notnull
#可以进行判断
```

同时，series对象自身和索引都有name属性，可以和其他功能一起使用。

series的索引可以通过按位赋值方式进行改变。

### 2.2 DataFrame

2.2.1 **创建与删除列**

DataFrame表示的是矩阵数据表，包含已排序的列集合，每一列可以是不同类型。

与excle相似，dataframe有行索引与列索引，数据被储存为一个二维块。

```python
# 创建dataframe
常见的方法是使用包含等长度的列表或者numpy数组的字典来生成
data={'a':[list1],'b':[list2],'c',[list3]}
# 其中的list也可以换为字典类型，而字典的所有值将变成每一行的索引。
frame=pd.DataFrame(data)
#我们也可以指定排列的顺序,指定每一行的索引
frame=pd.DataFrame(data,columns=['b','a','c']，index=['1','2','3'])
```

对于大型的dataframe，我我们可以使用head方法来只选出头部的五行。

使用del方法，移除创建的列。

2.2.2 **索引与赋值**

我们也可以直接根据列的名字进行索引。

```python
# 索引一个列
frame[columnsname] #返回的是一个series对象，返回的series对象的索引和frame是同一个，而序列的名字就是dataframe的列名。
# 索引一个行
frame.loc[index]
#赋值
frame[columnsname] =
```

当你的列表或数组赋值给一个列的时候，长度如果不匹配，会报错。

如果被赋值的列不存在，那么会*产生新的列*

**注意：与numpy一样，我们索引出的都是原对象的内容，如果需要复制应该显性的使用copy**

### 2.3 基本功能

2.3.1 **pandas的索引**

pandas的索引对象是用于储存标签和其他元数据的。在构造的时候，任意的数组或者标签序列都可以在内部转化为索引对象。

索引对象是不可变的，可以使对于索引的操作更加安全。

*索引是可以包含重复标签的*

```python
# 索引对象的方法和属性
append # 将一个索引粘贴到另一个索引后产生一个新的索引
difference #计算两个索引的差集
intersection #计算索引的交集
union #计算索引的并集
isin #计算每一个值是否在传值容器中的布尔数组
delete # 给出将位置i的元素删除的新的索引
drop # 根据传参删除指定的索引值，产生新的索引
inster #在位置i插入新元素并产生索引
is_monotonic # 索引递增就返回true
is_unique #索引都唯一返回true
unique # 计算索引的唯一序列
```

2.3.2 **重建索引**

pd中有reindex方法来重建一个新的索引。

```python
# series的索引重建
obj2=obj.reindex(['a','b','c','d','e']) #将obj中的索引重建后给obj2，本身不改变

# dataframe的索引重建
data.reindex(['oh','co','ut','ny','aa'])# 对于行标的转换
data.reindex(columns=['oh','co','ut','ny','aa'])# 对于列标的转换
```

2.3.3 **轴向删除目录**

我们通常使用`drop`方法来返回一个删除后的对象

```python
# 对于series对象
obj.drop(indexlist) # 返回去掉索引列表内索引值的对象
# 对于DataFeame对象，一般情况下会根据轴向为0的删除（按照行标签）
data.drop(list) 
# 如果要删除竖列，则应该设置参数axis
data.drop(list,axis=1)
# 如果要直接更改元对象 要使用inplace=True参数
```

2.3.4 **基本索引**

series的索引功能十分强大，不光可以使用index，也可以使用位置，以及值的内容

series的切片功能与python自带的列表不一样，series的索引双闭区间。

对于DataFrame的索引，可以直接从中索引出一个或多个列

```python
data[list] # 列索引
data[:2]# 行索引
```

直接索引都是对列进行索引，而有数字范围选择的是行索引，也可以使用自己索引自己，如`data[data<10]=5`

*在索引的时候，可能出现 index 也是数字的情况，因此可能出现歧义，请保持统一性，或者使用下面的 loc 来索引*

2.3.5 **选择数据区域**

我们可以使用**loc与iloc**来选择数据

loc：轴标签

iloc：整数标签

```python
data.loc['列标'，[行标]]
data.iloc['列数'，[行数]]
```

2.3.6 **算术与数据对齐**

pandas会按照索引对进行求和，如果两个索引对不相同，则会取两个索引的并集

不是同时存在于两个索引的，则求和之后会是空位置（NaN），并不会取一半的数值。

*如果是两个完全不同索引的对象进行数学运算，则全部为空*

而如果我们不想出现NaN而是需要其他的值来填充，我们可以使用函数，并给定fill_value参数

```python
df1.add(df2,fill_value=0) #如果两个有不一样的序列，那么我们会使用0来填充
```

### 2.4 更多操作

2.4.1 series与DataFrame之间的操作

在numpy中，如果我们使用一个二维的矩阵减去一个一维的数组，那么每一行都会减去这个数组（这就是广播机制）

而这一做法在pandas中也被继续沿用，在默认状况下，会将s与d的索引进行匹配，并广播到每一行。

而如果有索引无法匹配，也会和和算数运算一样产生NaN值。

如果要改为在列上传播，我们可以增加一个axis值

```python
# 示例代码
d.sub(s) # 直接在行上对每一行相减（默认axis=1）
d.add(s,axis=0) #在列上进行广播
```

2.4.2 **函数的应用与映射**

我们也可以将在np中使用的通用函数直接在pd中使用。将直接对每一个元素产生作用。

而如果只想对某一行或者一列进行作用，则可以使用匿名函数和apply方法的搭配使用。

```python
f = lambda x: x.max() - x.min()
frame.apply(f) #对每一列求最大值与最小值的差，然后以列表为索引，变成一个series
#如果对行进行操作，可以加上anxi = 1这一参数

#而如果对每一个元素要进行一次自定义，可以使用
Frame.applymap()
```

2.4.3 **排序**

```python
# 使用sort_index方法可以按照索引值进行排序
series.sort_index() #默认是升序，可以给ascending=false参数来变成逆序
# 在frame中使用这个类型，可以通过给定参数来在不同的轴上排序

# 使用sort_values方法可以按照数值进行排序
data.sort_values()
# 对于dataframe来说可以使用一列或者多列作为排序的关键序列
data.sort_values(by=indexlist)
```

默认情况下，所有的缺失值都会排到队尾。

2.4.4 **排名**

使用排名`rank`方法可以得到一个将数值改变成为排名的对象。

一般情况下如果出现同级情况就会产生小数来平均分配，也可以使用	`method`来改变方式。

```python
obj.rank() # 基础
obj.rank(ascending=false,method='first') # 倒着排序，第一次出现的大
```

常见的平级处理方法

```python
average #默认方法取平均
min #使用最小的排名
max # 使用最大排名
first #先出现的先排
dense #与min类似，但排名总是增加一
```

### 2.5 统计用法

2.5.1 描述性统计

我们可以使用很多方法来对数值进行操作

```python
df.sum() # 每一行求和
#通常情况下是以横向为轴，自动忽略了不存在值的位置，也可以通过参数来改变
df.sum(axis=1,skipna=false)
```

比较常用的方法

```python
count # 计算非NA的个数
describe #给出部分统计结果
min,max #计算最大值或最小值
argmin,argmax #分别计算最大值最小值的索引位置
idmin,idmax #给出最大值最小值的标签
sum #求和
mean #求均值
median #求中位数
prod # 求所有值的积
var #所有值的分差
std #所有值的标准差
cunsum #求累计值
cumprod #求累计值
pct_change # 求百分比
```

2.5.2 **相关性和协方差**

```python
# 获得相关性（协方差）矩阵
DF.corr()
DF.cov()
# 计算一个列于另一个列的相关性
DF.corrwith(DF.A)
```

2.5.3 **唯一值、计数和成员属性**

`unique`:给出series中的唯一值（去掉重复出现的内容）。

*使用这个方法返回的不一定是排序后的*

`value_counts`:降序返回出现元素的次数。

可以通过加入`sort=False`来关闭排序。

`inis`:通过给定一个列表，判断列表里面的元素是否存在。

`match`:计算数组中每个值的整数索引，形成一个唯一值的数值。