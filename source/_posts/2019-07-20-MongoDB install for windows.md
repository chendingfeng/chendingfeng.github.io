---
title: MongoDB安装为Windows服务 错误1053：服务没有及时响应启动或控制请求
data: 2019-07-20 11:01:05
categories: 
- JAVA
tags:
- 报错处理
---
### MongoDB安装为Windows服务 错误1053：服务没有及时响应启动或控制请求
----
先将之前安装的服务删除
```
sc delete MongoDB
```

配置路径按照以下格式
```
mongod --bind_ip 0.0.0.0 --logpath C:\mongodb\data\log\mongod.log --logappend --dbpath C:\mongodb\data\db --port 27017 --serviceName="MongoDB" --serviceDisplayName "MongoDB" --install
```
配置完成即可成功启动服务