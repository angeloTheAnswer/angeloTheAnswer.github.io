---
title: decoratorPython
top: false
cover: false
toc: true
mathjax: true
date: 2021-09-23 16:43:51
password:
summary: python装饰器
tags:
- python
- 装饰器
- 特性
categories:
- python装饰器
---


#### 为什么会存在装饰器

**在Python中一切都是对象：**
一个实例是一个对象，一个函数也是一个对象，甚至类本身也是一个对象。
在Python中，可以将一个函数作为参数传递给另一个函数，也可以将一个类作为参数传递给一个函数。

**Python中的特殊功能：**
在Python中，函数可以作为一个参数传递给另一个函数，也可以在函数中返回一个函数，还可以在函数内部在定义函数。

***以上是函数可以被装饰的关键***


#### 装饰器修饰函数
**装饰器的作用：**
包装一个函数，并改变（拓展）他的行为


**示例**

```sh
import logging
logging.basicConfig(level=logging.INFO)

def loggingDecorator(func): # 装饰函数
'''记录日志的装饰器'''
    def wrapperLogging(*args,**kwargs): # 包装函数
        logging.info("开始执行%s()...",func.__name__)
        func(*args,**kwargs)
        logging.info("%s()执行完成！",func.__name__)
    return wrapperLogging

@loggingDecorator # 表示用loggingDecorator装饰器来修饰showMin函数
def showMin(a,b):
    print("%d、%d 中的最小值是：%d" %(a,b,a if a < b else b ) )
showMin(2,3)
```


#### 装饰器修饰类

装饰器可以是一个函数，也可以是一个类（必须要实现__call__方法，使其是callable的）。同时装饰器不仅可以修改一个函数，还可以修饰一个类


**示例**

```sh
class ClassDecorator:
    '''类装饰器，记录一个类被实例化的次数'''
    def __init__(self,func):
        self.__numOfCall = 0
        self.__func = func 
    def __call__(self, *args, **kwds):
        self.__numOfCall+=1
        obj = self.__func(*args, **kwds)
        print("创建%s的第%d个实例:%s"%(self.__func.__name__, self.__numOfCall,id(obj)))
        return obj

@ClassDecorator
class TestClass:
    def __init__(self,name):
        self.__name = name
    def getName(self):
        return self.__name
tester01 = TestClass("Test01")
tester02 = TestClass("Test02")
print(id(tester01))
print(id(tester02))
```

