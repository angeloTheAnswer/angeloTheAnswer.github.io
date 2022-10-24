---
title: allureTitle
top: false
cover: false
toc: true
mathjax: true
date: 2021-09-27 10:54:42
password:
summary: allure报告Title显示问题处理
tags:
- python
- pytest
- Allure
categories:
- allure.dynamic.title
---

**遇到的问题：给allure报告中的case加上标题后发现显示有点问题**

![修改前](title.png)

**解决方法：**
修改allure_pytest中的listener.py 
文件位置Lib\site-packages\allure_pytest\listener.py

修改下面代码

```sh
    test_result.parameters.extend(
        [Parameter(name=name, value=represent(value)) for name, value in params.items()])
```

为

```sh
    test_result.parameters.extend([])
```

**修改后的效果**
![修改后](uptitle.png)


[参考出处](https://www.cnblogs.com/shukeshu/p/15777918.html)

