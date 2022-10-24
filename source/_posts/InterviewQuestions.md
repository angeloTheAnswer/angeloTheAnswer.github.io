---
title: InterviewQuestions
top: false
cover: false
toc: true
mathjax: true
date: 2021-10-11 12:14:22
password:
summary: 面试
tags:
- python
- InterviewQuestions
categories:
- Answer
---

#### 字符串切换大小写

将小写字符转换成大写字符
<code>str.uppe()</code>

将大写字符转换成小写字符
<code>str.lower()</code>

示例
```sh
str = 'TheAnswer'
print(str.upper())
print(str.lower())
```

输出
```sh
THEANSWER
theanswer
```

#### 枚举函数

对于一个可迭代的（iterable）/可遍历的对象（如列表、字符串），enumerate将其组成一个索引序列，利用它可以同时获得索引和值

示例
```sh
for index, item in enumerate("TheAnswer"):  
    print(index, item)
```

输出
```sh
0 T
1 h
2 e
3 A
4 n
5 s
6 w
7 e
8 r
```


#### 元组和列表的区别

**元组和list声明与赋值**
示例
```sh
tuple = ('tuple','The','Ansewer','Blog')
list = ['list','The','Ansewer','Blog']
print(tuple)
for itemTuple in tuple:
    print(itemTuple)
print(list)
for itemList in list:
    print(itemList)
```

输出结果
```sh
('tuple', 'The', 'Ansewer', 'Blog')
tuple
The
Ansewer
Blog
['list', 'The', 'Ansewer', 'Blog']
list
The
Ansewer
Blog
```
**区别一：列表属于可变序列，他的元素可随时修改和删除，而元组属于不可变序列，其中的元素不可以修改，除非整体替换**

示例
```sh
tuple = ('tuple','The','Ansewer','Blog')
list = ['list','The','Ansewer','Blog']

list[1] = "The1"
print(list)

tuple = ('tuple','The1','Ansewer','Blog')
print(tuple)

tuple[1] = "The2"
print(tuple)
```

控制台输出
```sh
['list', 'The1', 'Ansewer', 'Blog']
('tuple', 'The1', 'Ansewer', 'Blog')
Traceback (most recent call last):
  File "d:/my/test/leetcode/Solution.py", line 185, in <module>
    tuple[1] = "The2"
TypeError: 'tuple' object does not support item assignment
```

元组修改某个元素时会报错，整体替换的时候可以替换成功


**区别二：列表可以使用append()、extend()、insert()、remove()和pop()等方法实现添加和修改列表元素，而元组则没有这几个方法**

示例
```sh
tuple = ('tuple','The','Ansewer','Blog')
listextend = ['The','Ansewer','Blog']
listappend = ['The','Ansewer','Blog']
listinsert = ['The','Ansewer','Blog']
listremove = ['The','Ansewer','Blog']
listpop = ['The','Ansewer','Blog']
listextend.extend('extend')
listappend.append('append')
listinsert.insert(1,'insert')
listremove.remove('Blog')
listpop.pop(2)
print(listextend,'\n',listappend,'\n',listinsert,'\n',listremove,'\n',listpop)
```


控制台输出
```sh
['The', 'Ansewer', 'Blog', 'e', 'x', 't', 'e', 'n', 'd'] 
['The', 'Ansewer', 'Blog', 'append'] 
['The', 'insert', 'Ansewer', 'Blog']
['The', 'Ansewer']
['The', 'Ansewer']
```

**区别三：列表可以使用切片访问和修改列表中的元素。元组也支持切片，但是它只支持通过切片访问元组中的元素，不支持修改**

示例
```sh
tuple = ('tuple','The','Ansewer','Blog')
list = ['list','The','Ansewer','Blog']
print('list:',list[0:1] )
print('tuple:',tuple[0:1])
list[0:1] = ['list1']
print('list:',list )
tuple[0:1] = ('tuple1',)
print('tuple:',tuple )
```

控制台输出
```sh
list: ['list']
tuple: ('tuple',) #输出内容带有“,”表明他是一个元组
list: ['list1', 'The', 'Ansewer', 'Blog']
Traceback (most recent call last):
  File "d:/my/test/leetcode/Solution.py", line 217, in <module>
    tuple[0:1] = ('tuple1',)
TypeError: 'tuple' object does not support item assignment
```

**区别四：元组比列表的访问和处理速度快。所以如果只需要对其中的元素进行访问，而不进行任何修改，建议使用元组而不使用列表**

访问元素示例
```sh
t1 = timeit.Timer('t=tuple[9]','tuple=(0,1,2,3,4,5,6,7,8,9)')
print(t1.timeit())
t2 = timeit.Timer('l=list[9]','list=(0,1,2,3,4,5,6,7,8,9)')
print(t2.timeit())
```

控制台输出
```sh
0.0210157
0.025395600000000018
```

初始化示例
```sh
t1 = timeit.Timer('tuple=(0,1,2,3,4,5,6,7,8,9)')
print(t1.timeit())
t2 = timeit.Timer('list=(0,1,2,3,4,5,6,7,8,9)')
print(t2.timeit())
```

控制台输出
```sh
0.009790700000000013
0.011623500000000009
```


**区别五：列表不能作为字典的键，而元组可以**

示例
```sh
tuple = (1,2)
list = [1,2]
dicttuple = {tuple,'TheAnswer'}
print(dicttuple)
dictlist = {list,'TheAnswer'}
print(dictlist)
```


控制台输出
```sh
{(1, 2), 'TheAnswer'}
Traceback (most recent call last):
  File "d:/my/test/leetcode/Solution.py", line 240, in <module>
    dictlist = {list,'TheAnswer'}
TypeError: unhashable type: 'list'
```


#### 元组和列表相互转换

将列表转换成元组
<code>tuple()</code>

将元组转换成列表
<code>list()</code>

示例
```sh
list1 = ['l','i','s','t']
tuple1 = ('t','u','p','l','e')
print(list1)
print(tuple1)
print('列表转换成元组：',tuple(list1))
print('元组转换成列表：',list(tuple1))
```


控制台输出
```sh
['l', 'i', 's', 't']
('t', 'u', 'p', 'l', 'e')
列表转换成元组： ('l', 'i', 's', 't')
元组转换成列表： ['t', 'u', 'p', 'l', 'e']
```