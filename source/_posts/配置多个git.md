---
title: 配置多个git
top: false
cover: false
toc: true
mathjax: true
date: 2021-08-11 17:35:38
password:
summary: git配置
tags:
- git
categories:
- git
---

#### 生成SSH

第一个账号生成ssh key

```sh
ssh-keygen -t rsa -C "your1@email.com"
```

第二个账号生成ssh key

```sh
ssh-keygen -t rsa -C "your2@email.com"
```

#### 部署SSH KEY
在GitLab/GitHub上部署SSH KEY

#### 创建配置文件
新建config没有后缀名

##### 配置说明
```sh
Host    　　主机别名
HostName　　服务器真实地址
IdentityFile　　私钥文件路径
PreferredAuthentications　　认证方式
User　　用户名
```

##### 配置内容
```sh
# 别名可以随意写 服务器真实地址是ip就是ip 是域名就是域名
# 配置Github账号
Host user1.github.com
HostName github.com
IdentityFile C:\\Users\\TheAnswer\\.ssh\\id_rsa
PreferredAuthentications publickey
User user1

# 配置GitLab
Host xxxx
HostName xx.xx.xx.xx
IdentityFile C:\\Users\\TheAnswer\\.ssh\\id_rsa2
PreferredAuthentications publickey
User user2
```