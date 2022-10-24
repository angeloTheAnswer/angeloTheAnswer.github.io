---
title: pythonSection
top: false
cover: false
toc: true
mathjax: true
date: 2021-09-22 18:55:33
password:
summary: python切片操作
tags:
- python
- Solution
- Array
categories:
- 切片(slice)
---

#### 切片操作
在Python中，**切片**是对序列型对象的一种高级索引方法。普通索引只能取出序列中**一个下标**对应的元素，而切片取出序列中一个范围对应的元素。

*序列型对象：list列表、string字符串、tuple元组，*
#### 切片的格式以List为例

##### 描述
    切片是对列表进行截取操作。

##### 语法
简单切片<code>list[start:stop]</code> 
扩展切片<code>list[start:stop:step]</code>

##### 参数
start -- 列表需要开始切片位置的下标(截取时不包括下标对应的元素)，若为缺省值，那么默认从列表下标为0处开始切片；

stop -- 切片所需要切到的最终位置的下标（截取时包括该下标对应的元素），若为缺省值，那么默认截取至列表的最后一个元素（包括该元素）；

step -- 表示切片截取时的步幅，若为缺省值，那么默认为1。

##### 基本索引
nums中的元素|0|1|2|3|4|5|6|7|8|9
---|:--:|---:|---:|---:|---:|---:|---:|---:|---:|---:
正下标|nums[0]|nums[1]|nums[2]|nums[3]|nums[4]|nums[5]|nums[6]|nums[7]|nums[8]|nums[9]
负下标|nums[-10]|nums[-9]|nums[-8]|nums[-7]|nums[-6]|nums[-5]|nums[-4]|nums[-3]|nums[-2]|nums[-1]

##### 示例
```sh
    nums=[0,1,2,3,4,5,6,7,8,9]
    print('nums[5:9]-start、end都存在step缺省。从nums[5]开始step为1取到nums[9]结束，其结果不包括nums[9]这个元素。',nums[5:9])
    print('nums[5:]-end缺省。从nums[5]开始step为1取到nums[9]结束，其结果包括nums[9]这个元素。',nums[5:])
    print('nums[:9]-start缺省。从nums[0]开始step为1取到nums[9]结束，其结果不包括nums[9]这个元素。',nums[:9])
    print('nums[::2]-end缺省、start缺省、step为2。从nums[0]开始每隔两个元素取数，取到nums[9]结束。',nums[::2])
    print('nums[::-2]-end缺省、start缺省、step为-2。step为负值从右往左取，从nums[9]开始每隔两个元素取数，取到nums[0]。',nums[::-2])
    print('nums[:-1]-start缺省、end为负值。从nums[0]开始step为1取到nums[-1]结束，其结果不包括nums[-1]。',nums[:-1])
    print('nums[-10:]-end缺省、start为负值。从nums[-10]开始step为1取到nums[9]结束，其结果包括nums[9]。',nums[-10:])   
```
##### 输出结果

```sh
nums[5:9]-start、end都存在step缺省。从nums[5]开始step为1取到nums[9]结束，其结果不包括nums[9]这个元素。 [5, 6, 7, 8]
nums[5:]-end缺省。从nums[5]开始step为1取到nums[9]结束，其结果包括nums[9]这个元素。 [5, 6, 7, 8, 9]
nums[:9]-start缺省。从nums[0]开始step为1取到nums[9]结束，其结果不包括nums[9]这个元素。 [0, 1, 2, 3, 4, 5, 6, 7, 8]
nums[::2]-end缺省、start缺省、step为2。从nums[0]开始每隔两个元素取数，取到nums[9]结束。 [0, 2, 4, 6, 8]
nums[::-2]-end缺省、start缺省、step为-2。step为负值从右往左取，从nums[9]开始每隔两个元素取数，取到nums[0]。 [9, 7, 5, 3, 1]
nums[:-1]-start缺省、end为负值。从nums[0]开始step为1取到nums[-1]结束，其结果不包括nums[-1]。 [0, 1, 2, 3, 4, 5, 6, 7, 8]
nums[-10:]-end缺省、start为负值。从nums[-10]开始step为1取到nums[9]结束，其结果包括nums[9]。 [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

#### 常见的切片形式

##### 列表的复制

```sh
list1 = [0,1,2,3,4,5,6,7,8,9]
list2 = list1[:]
print('list2:',list2)
```

输出结果

```sh
list2: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

##### 列表的翻转

```sh
list = [0,1,2,3,4,5,6,7,8,9]
print('list翻转:',list[::-1])
```

输出结果

```sh
list翻转: [9, 8, 7, 6, 5, 4, 3, 2, 1, 0]
```

#### 旋转数组

**题目:**
**给你一个数组，将数组中的元素向右轮转 k 个位置，其中 k 是非负数。**



示例：
```sh
输入:nums=[1,2,3,4,5,6,7], k=3
输出:[5,6,7,1,2,3,4]
解释:
向右轮转1步:[7,1,2,3,4,5,6]
向右轮转2步:[6,7,1,2,3,4,5]
向右轮转3步:[5,6,7,1,2,3,4]
```


![图解](rotate.png)

*思路：*
*向右轮转K个位置，如果K大于数组长度len(nums),那么实际轮转k%len(nums)个位置。如果实际轮转的k%len(nums)个位置，那么就相当于把后k%len(nums)个元素按原来的顺序轮转到前面，第nums[n-k]轮转到最后一个位置,这里可以理解成两段list改变位置，第一段nums[n-k:],第二段nums[:n-k],这里nums[:n-k]不会取到nums[n-k]而nums[n-k:]会取到n-k*

```sh
class Solution:
    def rotate(self, nums: List[int], k: int) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        n=len(nums)
        k=k%n
        #nums = nums[n-k:]+nums[:n-k]
        nums[:] = nums[n-k:]+nums[:n-k]
```

***注意***
这个位置nums[:] = nums[n-k:]+nums[:n-k]，一开始是nums = nums[n-k:]+nums[:n-k]这样写的，但是一直返回的是原数组这里要把自己解释清楚。

***nums和nums[:]***
*nums = A： 更改nums这一变量名所指的对象，让nums变量指向A所指向的对象。
nums[:] = A： 对nums指向的对象赋值，把A变量指向的对象的值逐个复制到nums指向的对象中并覆盖nums指向的对象的原来值。*


[参考出处](https://zag666.blog.csdn.net/article/details/122896112?spm=1001.2101.3001.6650.7&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EOPENSEARCH%7ERate-7-122896112-blog-124011786.pc_relevant_aa&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EOPENSEARCH%7ERate-7-122896112-blog-124011786.pc_relevant_aa&utm_relevant_index=8)

```sh
nums=[0,1,2,3,4,5,6,7,8,9]
print(id(nums[:]),nums[:])
for i in nums[:]:
    print(i,id(i))
print(id(nums),nums)
for a in nums:
    print(a,id(a))

```

输出结果
```sh
2549611697480 [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
0 140713551756320
1 140713551756352
2 140713551756384
3 140713551756416
4 140713551756448
5 140713551756480
6 140713551756512
7 140713551756544
8 140713551756576
9 140713551756608
2549611697288 [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
0 140713551756320
1 140713551756352
2 140713551756384
3 140713551756416
4 140713551756448
5 140713551756480
6 140713551756512
7 140713551756544
8 140713551756576
9 140713551756608
```

*这里可以看出nums和nums[:] 地址不同，但是他们指向的元素地址相同，而nums = nums[n-k:]+nums[:n-k]方式会改变nums原地址，如果按照原地址去取值就得不到改变后的结果。nums[:] = nums[n-k:]+nums[:n-k]这种方式不会改变nums对象的地址，但是却改变的对象list中的值，这样如果用nums的对象地址去取会得到原来的list*