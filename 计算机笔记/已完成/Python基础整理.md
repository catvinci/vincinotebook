# Python基础整理

## 目录

[toc]

## 一、学前准备

### 1.1 安装

​		建议直接下载anaconda的发行版。同时还包括了所有以后会经常使用到的包。

### 1.2 编程环境

​		可以下载并使用pycharm、也可以使用jupyter notebook作为环境。

---



## 二、Python的语言基础

### 2.1 缩进

​		python中缩进是一切的根本，使用缩进来标识了语言的范围

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

​		元组是一种长度固定的，不可变的对象序列

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

# 使用方法来增加元素不创建新的对象，而使用+则创建返回一个新的对象。
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


# 以得到下标的方式来遍历一个列表
for i in range(len(list)):
    list[i]
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
# 判断子集
a<=b
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

### 3.5 可变长参数元组

函数可以接受不指定个数的参数

```python
def pr(*args):
    pass
```

上面的这个函数可以读取多个参数，到一个args元组中。

相反，除了**收集**也有**分散**方法，可以在调用的时候前面加上`*`来实现把参数列表里面的元组打散

```python
t=(1,2)
divmod(*t)
```

很多可以接受不止一个变量的函数也是使用了**分散**方法来完成多个参量的读取。

*关键字参数的收集*：

​		只使用`*`并不会收集关键字实参，而使用`**`则可以收集所有的关键字实参，并将其变成一个映射字典。当处理很多关键字的函数十分有用。

---

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

---

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

### 5.2 path（os）

```python
import os
os.getcwd() # get current working directory
os.path.abspath() # 寻找绝对路径
os.path.exists() # 检查一个文件是否存在
os.path.isdir() # 检查是否为目录
os.listdir() # 返回指定目录的列表
os.path.join(,) # 接受一个目录和一个文件名字，并将它们拼成一个完整的path
```

### 5.3 数据库与封存

我们可以使用`dbm`模块来创建和更新数据库，来达到储存类似字典的对象。

```python
import dbm
db=dbm.open('name',c) # 打开创建一个数据库，如果不存在则创建
db['a'] ='a' # 向数据库内储存一个字符
db['a']='b' # 更新储存的内容
db.close() # 关闭文件
```

dbm有个严格的限制，键和值都必须是字符串或者字节，不能使用其他类型。

对此我们可以使用`pickle`模块来进行封存。

```python
import pickle
# 将t列表转换为一个字符串对象，进行在数据库内的储存
t=[1,2,3]
st=pickle.dumps(t)

# 将封装好的对象重新打开
pickle.loads(st) # 打开后的对象虽然与封装之前的对象相等，但并不是同一个对象
```

---

## 六、面向对象编程

### 6.1 类

Python是一门面向对象的编程语言

1. 程序包括类的定义和方法的定义
2. 大部分计算操作是通过面向对象来实现的
3. 由对象之间的交互组成

6.1.1 类的定义

```python
class name:
    '''
    note
    '''
```

6.1.2 类的初始化（`__init__`)

init方法(initialization)，可以在对象被初始化的时候会调用

```python
class name:
    '''
    note
    '''
    def __init__(self,first=firstname,last=lastname)
    	self.first=first
        self.last=last
```

### 6.2 实例

6.2.1 创建实例

我们可以使用类来实例化一个对象。

`n=name(bob,shen)`这样可以把n变成一个name类型的对象，此时具有了first与last两个**属性**。

为了判断一个属性是否被对象所拥有，我们可以使用`hasattr`函数

```python
hasattr(name,first)
```

我们也可以给n这个实例来增加新的属性，但一般建议都在初始化的时候确定。

另外，我们也可以使用`vars`函数来把一个对象的所有属性名称和值进行字典映射。

**==注意==**：在进行类的初始化过程中尽量避免`def __init__(*self*, *name*, *contents*=[]):`的写法，因为这样会导致每一个定义的对象指向的列表都是同一个，会导致数据的错乱。

```python
    def __init__(self, name, contents=None):
        self.name = name
        if contents == None:
            contents = []
        self.pouch_contents = contents
```



### 6.3 复制

​		实例是一个可变的对象，而传递给函数的实例这是一个指针而不是一个新的对象，所以在函数内修改实例（即使使用的是别名），仍然会直接修改原本的对象。

​		为了不使原本的对象发生修改，可以使用copy中的copy函数，将一个对象进行复制，只修改新的对象。而复制的对象与原本的对象，无论是`is`还是=都是不一样的。

​		但如果有对象的嵌套，即一个对象的参数是另一个对象，则只复制地址，仍然会导致两个不一样的对象指向了一个对象，为了防止这种情况，可以使用深复制（deep copy），这样复制的对象会把对象的属性的对象也进行复制。

### 6.4 更好的打印

我们可以使用`__str__`这个特殊来返回对象的字符串表达式。

```python
def __str__(self):
    return '%c %c'% (self.first,self.last)
```

我们在使用print打印的时候会调用这个方法，并按照我们给定的格式来输出。

*我们写一个新的类，使用 init 来初始化，又使用 str 来打印调试*

### 6.5 操作符重载

6.5.1 基本重载

​		通过定义其他的特殊方法，可以指定各种操作符的行为。

```python
# 使用add重载+
def __add__ (self,other):
    return self+other
'''
使用上面这个方式只能使用左加法，为了可以右加法一样可以，我们可以使用如下代码
'''
def __radd__(self,other):
    return self.__add__(other)
```

6.5.2 基于类型的分发

​		我们使用`+`的时候可能两者的类型并不是我们所希望的样子，我们可以通过if等方式对不同的类型进行相应的处理，使得其可以进行运算。

6.5.3 多态

​		比起基于类型的方法，我们更可以使用能处理多个类型的函数：多态。

​		如：sum函数可以用于任何有定义`__add__`的对象之间。

### 6.6 继承

​		继承是指定义一个新类，继承旧的类的大部分属性，再对一部分属性和方法进行修改。

​		优点：可以大量减少代码的重复量，优化程序结构

```python
class Hand(Deck):
    def __init__(self):
        pass
```

​		使用上述代码，在类的定义后面追加的写另一个类，会首先把括号内的类全部都继承下来，而对于要修改的部分，我们可以在这个类里面进行重新的覆盖式定义。

​		*我们在进行继承或者重载的时候，尽可能要保持接口的一致性，防止代码逻辑混乱*

### 6.7 数据封装

1. 从编写函数、读取全局变量开始。
2. 当程序可以完美运行后，查看全局变量和函数之间的关系。
3. 将变量封装成对象的属性，将函数封装为对象的方法。

### 6.8 案例（扑克牌）

```python
import random

class Card:
    '''创建了一个单张卡片对象'''
    def __init__(self,suit=0,rank=2):
        self.suit=suit
        self.rank=rank
        
    suit_name=['草花','方块','红心','黑桃']
    rank_name=[None,'ace','2','3','4','5','6','7','8','9','10','Jack','queen','king']
    
    def __str__(self):
        return '%s %s' %(Card.suit_name[self.suit],Card.rank_name[self.rank])

    def __lt__(self,other):
        return (self.suit,self.rank)<(other.suit,other.rank)
    
class Deck:
    '''使用单张卡片对象，创建了完整的一套卡牌'''
    def __init__(self):
        self.cards=[]
        for suit in range(4):
            for rank in range(1,14):
                card=Card(suit,rank)
                self.cards.append(card)
                
    def __str__(self):
        res=[]
        for card in self.cards:
            res.append(str(card))
        return '\n'.join(res)
    
    def pop_card(self):
        return self.cards.pop()
    
    def add_card(self,card):
        self.cards.append(card)
    
    def shuffle(self):
        random.shuffle(self.cards)
        
 class Hand(Deck):
    '''继承了一套完整的卡牌的方法，对于初始化做了修改'''
    def __init__(self,label=''):
        self.cards=[]
        self.label=label
```

**快速定义类**：我们也可以使用命名元组的方式，用简短的语句快速定义一个简单的只具有`init`和`str`方法的类

```python
from collections import namedtuple
point=namedtuple('point',['x','y'])
```

上面这段代码的第一个参数是类的名字，第二个是参数的列表。