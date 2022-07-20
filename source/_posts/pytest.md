---
title: pytest接口自动化框架搭建
top: true
cover: false
toc: true
mathjax: true
date: 2021-06-13 21:13:30
password:
summary: pytest & 接口自动化
tags:
- python
- 自动化
- pytest
categories:
- pytest
---

## 前言
*眼泪不是我们的答案。拼搏才是我们的选择*

## 环境
Java环境 java version "1.8.0_271"
Python环境 3.7.9


## 什么是自动化框架
作用：
1、提高测试效率，减低维护成本
2、减少人工干预，提高测试准确性，增加代码重用性
3、核心思想是让不懂代码的人也能够通过这个框架去实现自动化

## Pytest特性
1、比较灵活的单元测试框架  
2、pytest可以和selenium、request、appiium结合实现web自动化、接口自动化、app自动化  
3、pytest可以实现测试用例的跳过以及reruns失败用例重试  
4、pytest可以和allure生成美观的测试报告  
5、pytest可以和jenkins持续集成  
6、pytest有很多非常强大的插件。并且这些插件能够实现很多实用的操作

#### Pytest单元测试框架与自动化测试框架的关系
1、单元测试框架只是自动化测试框架的组成部分之一  
2、pom设计模式只是自动化测试框架中的组成部分  
3、数据驱动  
4、关键字驱动  
5、全局配置文件封装  
6、日志监控  
7、selenium，requests 二次封装  
8、断言  
9、报告邮件  



## 常用插件
1、pytest：单元测试框架  
2、pytest-html：生成HTML格式的报告  
3、pytest-xdist：测试用例分布式执行，多CPU分发  
4、pytest-ordering：用于改变测试用例的执行顺序  
5、pytest-rerunfailfures：用例失败重跑  
6、allure-pytest：用于生成美观的测试报告  

##### 常用插件批量安装
步骤1、新建.txt文件  
步骤2、把插件名放入文件中  
步骤3、通过pip install -r 文件.txt完成安装  
步骤4、验证是否安装成功 使用命令pytest --version  

##### allure测试报告安装
1、下载、解压  
下载地址：https://github.com/allure-framework/allure2/  releases  
2、配置环境变量  
在系统环境变量后追加解压路径 例如：E:\allure-2.13.7\bin  
3、验证是否安装成功：  
分别在dos和pycharm中验证    
```sh
allure --version
```
***注意：dos可以验证成功但是pycharm验证失败需重启pycharm***

#### jpype测试报告安装
*概述：JPype 是一个能够让 python 代码方便地调用 Java 代码的工具*
1、下载whl包JPype1-1.1.2-cp37-cp37m-win32.whl  
下载地址：https://www.lfd.uci.edu/~gohlke/pythonlibs/  
2、安装jpype  
1)命令行进入whl包所在目录  
2)执行安装命令  
```sh
python -m pip install JPype1-1.1.2-cp37-cp37m-win32.whl
```

## 框架搭建

### 框架结构图
![目录结构](jiagoutu.png)


### pytest.ini配置文件
1、文件位置：一般放在根目录  
2、文件编码：必须是ANSI，可以使用记事本修改编码格式  
3、文件作用：改变pytest默认行为  
4、不管是主函数的模式运行、命令行模式运行，都会去读取这个配置文件  
5、配置文件
```sh
[pytest]
#命令行的参数，用空格分隔
#addopts=-vs -k mingchen --alluredir ./temps --clean-alluredir
# addopts=-vs ./testcase/test_rqu_mingchenapi.py --alluredir ./temps --clean-alluredir
addopts=-vs ./testcase/test_api.py::TestApi::test_openapi_mingchen --alluredir ./temps --clean-alluredir
#测试用例路径
testpaths=testcase
#模块名的规则
python_files=test_*.py
#类名的规则
python_classes=Test*
#方法名的规则
python_functions=test
#标记测试用例
markers=
	smoke1:冒烟用例1
	smoke2:冒烟用例2
	smoke3:冒烟用例3


# 命令行窗口日志输出配置
# log_cli 可以输入0, False 代码不输出日志， 1、True 代表开启日志输出
# log_cli_level 代表日志输出级别
# log_cli_date_format 日期格式
# log_cli_format 日志模板格式

log_cli=1
log_cli_level=info
log_cli_date_format=%Y-%m-%d-%H-%M-%S
log_cli_format=%(asctime)s-%(filename)s-%(module)s-%(funcName)s-%(lineno)d-%(levelname)s-%(message)s


#  日志输出到文件配置
#  log_file 日志文件
#  log_file_level 代表日志输出级别
#  log_file_date_format 日期格式
#  log_file_format 日志模板格式

log_file=log/test.log
log_file_level=debug
log_file_date_format=%Y-%m-%d %H:%M:%S
log_file_format=%(asctime)s %(filename)s %(module)s %(funcName)s %(lineno)d %(levelname)s: %(message)s

```

### 默认用例规则
模块名必须以test_开头或者_test结尾  
测试类必须以Test开头，并且不能有init方法  
测试方法必须以test开头  
以上规则可以在pytest.ini进行配置

```sh
#模块名的规则
python_files=test_*.py
#类名的规则
python_classes=Test*
#方法名的规则
python_functions=test
```
### 测试用例运行方式
#### 主函数模式
```sh
#运行所有用例
pytest.main()
```
```sh
#指定模块运行
pytest.main(['-vs','test_modul1.py'])
```
```sh
#指定目录运行
pytest.main(['-vs','./list_testcase'])
```
通过nodeid指定运行用例：nodeid由模块名，分隔符，类名，方法名，函数名组成
```sh
#通过nodeid指定运行用例
pytest.main(['-vs','./模块名/文件名::函数名'])
```
```sh
#通过nodeid指定运行用例
pytest.main(['-vs','./模块名/文件名::类名::方法名'])
```

#### 命令行模式
1、运行所有用例
```sh
pytest
```
1、指定模块运行
```sh
pytest -vs test_modul.py
```
1、指定目录运行
```sh
pytest -vs ./list_testcase
```
1、指定函数运行
```sh
pytest -vs ./list_testcase/文件名::函数名
```
***小插曲：pytest命令参数***  
***-s：表示输出调试信息***  
***-v：显示更详细的信息***  
***-vs：两个参数一起用***  
***-n：支持多线程或者分布式运行测试用例***  
```sh
#多线程分布式执行用例
pytest -vs ./list_testcase/testcase.py -n 2
```
***--reruns NUM：失败用例重跑***  
***-x：表示只要有一个用例报错，那么测试停止***  
***--maxfail=2：比那时出现两个失败用例就停止***  
***-k：根据测试用例的部分字符串来指定执行测试用例***  
```sh
#多线程分布式执行用例
pytest -vs ./list_testcase/testcase.py -n 2
```
***--html ./report/report.html：在指定目录下生成报告***  

#### 通过读取pytest.ini配置文件执行
```sh
#pytest.ini配置文件执行用例
addopts=-vs ./testcase/test_api.py::TestApi::test_case_api
```


### 创建一个通过配置文件执行的测试用例demo

1、创建一个文件名为api_automation  
2、在api_automation目录下创建testcase文件夹  
3、在testcase下创建test_demo.py
```sh
[testcase/test_demo.py]
class TestDemoClass:
	def test_01_case1(self):
		print('\n测试用例1')
	def test_02_case2(self):
		print('\n测试用例2')
```
4、在api_automation目录下创建pytest.ini配置文件(注意编码格式)
```sh
#命令行的参数，用空格分隔
addopts=-vs ./testcase/test_demo.py::TestDemoClass::test_01_case1 
#测试用例路径
testpaths=testcase
#模块名的规则
python_files=test_*.py
#类名的规则
python_classes=Test*
#方法名的规则
python_functions=test
``` 
5、在api_automation下创建run.py主函数
```sh
import os
import time
import pytest

if __name__=='__main__':
	pytest.main()
	time.sleep(2)
    #生成报告
	# os.system('allure generate ./temps -o ./report --clean')
```

6、运行run.py

```sh
[运行信息]
PS D:\work\repository\project\api_automation> & D:/python/python.exe d:/work/repository/project/api_automation/run.py
======================================================= test session starts =======================================================
platform win32 -- Python 3.7.9, pytest-6.2.4, py-1.10.0, pluggy-0.13.1 -- D:\python\python.exe
cachedir: .pytest_cache
metadata: {'Python': '3.7.9', 'Platform': 'Windows-10-10.0.19041-SP0', 'Packages': {'pytest': '6.2.4', 'py': '1.10.0', 'pluggy': '0.13.1'}, 'Plugins': {'allure-pytest': '2.9.45', 'forked': '1.4.0', 'html': '3.1.1', 'metadata': '2.0.1', 'ordering': '0.6', 'rerunfailures': '10.2', 'xdist': '2.5.0'}, 'JAVA_HOME': 'D:\\java\\jdk1.8'}
rootdir: D:\work\repository\project\api_automation, configfile: pytest.ini
plugins: allure-pytest-2.9.45, forked-1.4.0, html-3.1.1, metadata-2.0.1, ordering-0.6, rerunfailures-10.2, xdist-2.5.0
collected 1 item

testcase/test_demo.py::TestDemoClass::test_01_case1
测试用例1
PASSED

======================================================== 1 passed in 0.11s ======================================================== 
PS D:\work\repository\project\api_automation> 
```

#### 测试用例执行顺序
pytest默认从上到下
unitest以ascii的大小决定执行顺序
##### pytest 改变默认执行顺序
使用mark标记
```sh
[testcase/test_demo.py]
class TestDemoClass:
	def test_01_case1(self):
		print('\n测试用例1')
	@pytest.mark.run(roder=1)
	def test_02_case2(self):
		print('\n测试用例2')
```
##### pytest 分组执行
pytest进行分组测试的方法是使用装饰器 @pytest.mark.标记名称，被标记为相同名称的用例可以看做为同一个组。  
分组执行可应用与冒烟用例执行、分模块执行、分接口和web执行。

###### 分组执行-冒烟用例
```sh
[testcase/test_demo.py]
class TestDemoClass:
	@pytest.mark.smoke1
	def test_01_case1(self):
		print('\n测试用例1')
	
	def test_02_case2(self):
		print('\n测试用例2')
```

```sh
[pytest.ini]
#命令行的参数，用空格分隔
addopts=-vs -m
#测试用例路径
testpaths=testcase
#模块名的规则
python_files=test_*.py
#类名的规则
python_classes=Test*
#方法名的规则
python_functions=test
#标记测试用例
markers=
	smoke1:冒烟用例1
``` 

完成配置后执行run.py即可

```sh
[运行信息]
PS D:\work\repository\project\api_automation> & D:/python/python.exe d:/work/repository/project/api_automation/run.py
========================================================================================= test session starts =========================================================================================
platform win32 -- Python 3.7.9, pytest-6.2.4, py-1.10.0, pluggy-0.13.1 -- D:\python\python.exe
cachedir: .pytest_cache
metadata: {'Python': '3.7.9', 'Platform': 'Windows-10-10.0.19041-SP0', 'Packages': {'pytest': '6.2.4', 'py': '1.10.0', 'pluggy': '0.13.1'}, 'Plugins': {'allure-pytest': '2.9.45', 'forked': '1.4.0', 'html': '3.1.1', 'metadata': '2.0.1', 'ordering': '0.6', 'rerunfailures': '10.2', 'xdist': '2.5.0'}, 'JAVA_HOME': 'D:\\java\\jdk1.8'}
rootdir: D:\work\repository\project\api_automation, configfile: pytest.ini, testpaths: testcase
plugins: allure-pytest-2.9.45, forked-1.4.0, html-3.1.1, metadata-2.0.1, ordering-0.6, rerunfailures-10.2, xdist-2.5.0
collected 54 items / 53 deselected / 1 selected

testcase/test_demo.py::TestDemoClass::test_01_case1
测试用例1
PASSED

================================================================================== 1 passed, 53 deselected in 2.61s =================================================================================== 
PS D:\work\repository\project\api_automation>
```

###### 同一个用例标记多个组
```sh
[testcase/test_demo.py]
class TestDemoClass:
	@pytest.mark.smoke1
	@pytest.mark.smoke2
	def test_01_case1(self):
		print('\n测试用例1')
	
	def test_02_case2(self):
		print('\n测试用例2')
```

```sh
[pytest.ini]
#命令行的参数，用空格分隔
addopts=-vs -m
#测试用例路径
testpaths=testcase
#模块名的规则
python_files=test_*.py
#类名的规则
python_classes=Test*
#方法名的规则
python_functions=test
#标记测试用例
markers=
	smoke1:冒烟用例1
	smoke2:冒烟用例2
``` 

###### 分组执行支持逻辑运算符
or连接多个标记名称会执行包含这些标记的用例



