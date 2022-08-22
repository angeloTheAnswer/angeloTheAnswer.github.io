---
title: removeDuplicates
top: false
cover: false
toc: true
mathjax: true
date: 2020-12-01 12:19:02
password:
summary: 删除排序数组中的重复项
tags:
- python
- Solution
- Array
categories:
- Solution
---
**题目:**
**给你一个 升序排列 的数组 nums ，请你 原地 删除重复出现的元素，使每个元素 只出现一次 ，返回删除后数组的新长度。元素的 相对顺序 应该保持 一致 。**
**由于在某些语言中不能改变数组的长度，所以必须将结果放在数组nums的第一部分。更规范地说，如果在删除重复项之后有 k 个元素，那么 nums 的前 k 个元素应该保存最终结果。**
**将最终结果插入 nums 的前 k 个位置后返回 k 。**
**不要使用额外的空间，你必须在 原地 修改输入数组 并在使用 <code>O\(1\)</code> 额外空间的条件下完成。**

```sh
class Solution(object):
    def removeDuplicates(self,nums: List[int]) -> int:
        for i in range(len(nums),0,-1):
            if nums[i] == nums[i-1]:
                del(nums[i])
        return len(nums)        
```

函数中参数后面的冒号是参数的类型建议符
函数后面的箭头是函数返回值的类型建议符

python中的<code>range\(\)</code>函数

range()函数用于生成一个整数序列

第一种只有一个参数<code>range\(stop\)</code>
```sh
#range(10)指的是默认从0开始，步长为1，不包括10
print('示例结果：',list(range(10)))
```

```sh
示例结果： [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

第二种有两个参数<code>range\(start,stop\)</code>
```sh
#range(1,10)指的是1开始，步长为1，不包括10
print('示例结果：',list(range(1,10)))
```

```sh
示例结果： [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

第三种有三个参数<code>range\(start,stop,step\)</code>
```sh
#range(1,10,2)指的是1开始，步长为2，不包括10
print('示例结果：',list(range(1,10,2)))
```

```sh
示例结果： [1, 3, 5, 7, 9]
```

```sh
#range(10,0,-1)指的是10开始，步长为-1，不包括0
print('示例结果：',list(range(10,0,-1)))
```

```sh
示例结果： [10, 9, 8, 7, 6, 5, 4, 3, 2, 1]
```

**range类型的优点**
不管range对象表示的整数序列有多长，所有range对象占用的内存空间都是相同的，因为仅仅需要储存start,stop,step，只有当用到range对象时，才会去计算序列中的相关元素

**python中数组的del,remove,pop**

```sh
#remove()删除首个符合条件的元素，并非特定的索引
remove_array=['a','b','b','c']
print('remove()的返回值',remove_array.remove('b'))
print('remove()操作后数组的长度',len(remove_array))
print('remove()操作后数组的内容',list(remove_array))

#pop返回的是你弹出的那个元素，参数为索引
pop_array=['a','b','c']
print('pop()的返回值',pop_array.pop(1))
print('pop()操作后数组的长度',len(pop_array))
print('pop()操作后数组的内容',list(pop_array))

#del它是根据索引也就是元素所在位置来删除
del_array=['a','b','c']
del del_array[1]
print('del()操作后数组的长度',len(del_array))
print('del()操作后数组的内容',list(del_array))  
```

```sh
remove()的返回值 None
remove()操作后数组的长度 3
remove()操作后数组的内容 ['a', 'b', 'c']
pop()的返回值 b
pop()操作后数组的长度 2
pop()操作后数组的内容 ['a', 'c']
del()操作后数组的长度 2
del()操作后数组的内容 ['a', 'c']
```