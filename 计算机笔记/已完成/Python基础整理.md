# Python基础整理

## 目录

[toc]

## 一、学前准备

### 1.1 安装

建议直接下载anaconda的发行版。同时还包括了所有以后会经常使用到的包。

### 1.2 编程环境

可以下载并使用pycharm、也可以使用jupyter notebook作为环境。

---



## 二、Python的语言基础

### 2.1 缩进

python中缩进是一切的根本，使用缩进来标识了语言的范围

### 2.2标量类型

2.2.1 **数值类型**

​		python中只有两个基本数值类型：int与float

​		int可以储存任意大小的整数值而没有范围限制，float是双精度的64位数值。

	备注：整数的除法会自己变成浮点的类型，如果只要整数部分可以使用：//

2.2.2 **布尔类型**

​		只有正确和错误两种，分别是true和false

	备注：在整型中代表着1与0。

2.2.3 **字符串类型**

​		使用单（双）引号包裹的一个不可变对象。是Unicode字符的序列。是一个可迭代的对象。

2.2.4 **None型**

​		是Python中的null，表示没有东西

### 2.3 控制语句

2.3.1 **判断语句**

```python
if condition1:
    code 1
elif condition2:
    code 2
else:
    code 3
```

2.3.2 **循环语句**

for语句用于遍历一个集合或者一个迭代器。

```python
for i in collection:
    # 用i来做什么
    
# 也可以让for与range（）配合实现计数
for i in range (10)
```

while语句用于在符合一定条件的情况下执行代码块

```python
while conditional:
    # 代码块
```

有两个方式可以改变循环的结构

1. continue：用于跳过本次循环进入下一次的循环之中
2. break：结束这一个循环

### 2.4 数据结构

2.4.1 **元组**

元组是一种长度固定的，不可变的对象序列

```python
# 元组的创建
tup=1,2,3

# 使用tuple函数将其他可迭代的变成元组
tuple([1,2,3])
tuple("abc")

# 使用[]索引元组（从0开始）
tup[0]
```

拆包

```python
#将tup的元素拆到三个变量之中去
a,b,c=tup

#拆包的应用（快速交换两个元素）
a,b=b,a

#只拆部分元素
a,*_=tup  #后面的元素*_会存a之后的所有元素，可以舍弃，也可以更换名作为继续用的元组
```

元组方法

```python
# 计数
tup.couut(1)
```

2.4.2 **列表**

一个不指定里面的类型，可以任意改变内容的高端数组。

```python
# 创建列表
list=[1,2,3]

#使用迭代器创建
list=range(10)
```

**增加元素**

```python
# 末尾增加一个
list.append()

# 指定位置加入一个
list.insert(1,"123")

# 加入多个元素
list.extend([1,2,3])

```

**删除元素**

```python
# 移去指定位置的元素
list.pop(1)

#移去第一个出现的符合要求的元素
list.remove("123")
```

**其他方法**

```python
# 排序（内部排序不会新建对象）
list.sort()
括号内可以设定排序的key
如list.sort(key=len)

# 排序（新建对象的排序）
list2=list1.sorted（）

#将列表倒置
list.reversed()

# 二分查找和插入数据
import bisect
其中bisect.bisect(c,2)是向c列表插入元素2

# 缝合两个列表，按顺序两两搭配为元组，构成新列表
list3=zip（list，list2）

# 返回列表内元素的内容以及其索引
enumerate(list)
常用于：for i in enumerate (list)
```

2.4.3 **字典**

又被成为哈希表或者是关联数组，是有灵活尺寸的键值对集合

```python
# 创建字典
d1={1:"st",2:[123]}

# 根据键来获取值
d1[1]

# 序列生成字典（因为字典的本质上是一个二元组）
d1=dict(zip(list1,list2))

# 检查是否存在
'st' in d1

# 判断一个对象能不能作为键（不可变、可哈希化）
hash(keys)
```

加入与删除

```python
# 加入一个新的元素
d1[key]=元素

# 直接根据键来删除元素
del d1[1]

# 删除对应的元素并返回他的键
d1.pop ('st')
```

获取与分类

```python
# 获取一个字典中的元素，且在没有时候返回特定的值
d1.get(key,returnvalue)

# 将列表进行分类进入字典
for word in list:
    d1.setdefault(key,[]).append(word)
```

其他方法

```python
# 迭代字典（没有特定的迭代顺序）
d1.keys() # 迭代字典键
d2.values() # 迭代值

# 合并字典
d1.update(d2)


```

2.4.4 **集合**

无序且唯一的元素的容器

```python
# 创建集合
set([1,2,3])
{1,2,3}
```

对集合内元素进行操作

```python
# 加入元素
a.add

# 清空集合
a.clear

# 删除某个元素
a.remove
```

对多个集合的操作

```python
# 并集
a|b
# 交集
a&b
# 补集(在a但不在b)
a-b
# 在a在b，但不是同时在a和b
a^b
# 判断a是否包含（包含于）b
a.issubet(b)(a.issuperset(b))
```



2.4.5  **序列推导式**

过滤一个容器的元素。

```python
# 列表推导式
[x for x i list if condition]
```

这个语句可以以列表的形式返回满足condition的所有在list中的元素

```python
# 字典推导式
{key:value for value in collection if condition}
# 集合推导式
{x for value in collection if condition}
```

**嵌套列表推导**

*内层在前，外层在后*

---



## 三、Python函数

​		如果有多条可以重复的代码，可以使用一个函数来简化代码量

```python
def function (x,y):
    #your code
    return a,b   #python的函数可以同时返回多个值
```

### 3.1 命名空间

​		在函数内第一次使用的变量在函数结束后会销毁，而函数内想要对函数外的变量进行使用则应该使用`global`进行声明。使得外部的变量在内部也可以进行使用。

### 3.2 函数=对象

可以将函数作为对象传到另一个函数之中

### 3.3 匿名（Lambda）函数

​		通过单个语句生成函数，结果是返回值。使用**Lambda**关键字进行定义。可以用在将一个判断函数传入另一个函数的过程中。

```python
lambda variable :code

# 根据字符串中不同字符的数量进行排序
st.sort(key=lambda x:len(set(list(x))))
```

### 3.4 迭代器与生成器

​		**迭代器**：用于在上下文中向python解释器生成对象的对象。

​		**生成器**：构造新的可遍历对象的方式。

通过将函数的return改为yield，使得调用该生成器的时候代码不会立刻被执行，而在请求其中的元素后才会被执行。

```python
def squares(n=10):
    for i in range(1,n+1):
        yield i**2
        
gen = squares() #此处的gen还没有值

for x in gen: #调用生成器
    print(x,end=' ')
```

可以利用生成器表达式来创建一个生成器（将列表推导式内的括号换成小括号）

如上面的可以改写为

```python
gen=(x**2 for x in range(1,n+1))

for x in gen: #调用生成器
    print(x,end=' ')
```

可以使用生成器表达式来代替我们的列表推导式



## 四、错误与异常

### 4.1 捕获异常

```python
def tryfunction(x):
    try:
        # 想要测试的内容
    except（#可以选择想要捕获的错误类型）:
        # 测试失败后执行
    finally:
        # 无论如何都要执行的代码
```



## 五、操作系统与文件

### 5.1 对文件的基础操作

5.1.1 **打开与关闭**

```python
f=open(path) #打开
f.close #关闭

#自动关闭方式
with open(path) as f:
    # use path
#with内代码结束后自动关闭
```

默认打开是在只读模式下进行。

打开模式：

```python
r #只读模式
w #只写模式（创建新文件并覆盖同名文件）
x #只写模式（如果有同名则创建失败）
a #添加已存在文件
r+ #读写模式
```

5.1.2 **对文件的方法**

```python
read([size]) #将文件数据作为字符串返回
readlines([size]) #返回文件中行内容的列表
write(str) #将字符串写入文件
writelines(string) #将字符串序列写入文件
close() #关闭文件
seek(pos) #移动到指定位置
tell() #返回当前的文件位置
```

