---
title: RabbitMQ安装与相关配置
data: 2019-06-27 10:08:05
categories:
- JAVA
tags: 
- 消息中间件
---
# RabbitMQ安装与相关配置

## 1. Erlang安装配置
> RabbitMQ 是一个由 Erlang 语言开发的 AMQP 的开源实现，故需需要安装支持的 Windows 版Erlang 

#### 1.1 版本对应 
查看对应版本链接:https://www.rabbitmq.com/which-erlang.html 下载对应版本Erlang （下载地址自行官网下载）

![](https://youdaoyun-img.oss-cn-shanghai.aliyuncs.com/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20190628203426.png)
#### 1.2 安装  
安装一直next（略过） 安装完毕  
#### 1.3 配置环境变量
定义erl环境变量---系统变量
win+R 输入sysdm.cpl 回车 选中高级-系统环境变量
```
ERLANG_HOME=C:\Program Files\erl9.1     //新建系统变量,自定义的安装路径
%ERLANG_HOME%\bin;                      //Path中加入  
```
测试是否安装配置正确，win+r cmd，命令窗口输入erl，显示如下：
![](https://youdaoyun-img.oss-cn-shanghai.aliyuncs.com/erl.PNG)

## 2. RabbitMQ安装配置
#### 2.1 下载安装
官网每个版本都有详细说明，自行查阅: https://www.rabbitmq.com/changelog.html  
下载地址: https://www.rabbitmq.com/download.html  
安装步骤一直next 自行定义安装路径（这里略过...）

#### 2.2 配置环境变量
定义RaabbitMQ环境变量  
同上，进入环境设置页面
```
RABBITMQ_SERVER=D:\RabbitMQ\rabbitmq_server-3.6.14       //新建系统变量
%RABBITMQ_SERVER%\sbin                                   //Path中加入
```
#### 2.3 激活RabbitMQ
在CMD中输入
```
D:\RabbitMQ\rabbitmq_server-3.6.14\sbin>rabbitmq-plugins.bat enable rabbitmq_management
```
如下:
![](https://youdaoyun-img.oss-cn-shanghai.aliyuncs.com/RabbitMQ.PNG)
#### 2.4 启动/关闭服务
```
net start RabbitMQ              //启动服务 (激活完默认已经开启服务)
net stop RabbitMQ               //关闭服务 
```
## 3. RabbitMQ测试
测试地址 http://localhost:15672/  
默认初始用户名：guest  
默认初始用户密码：guest  
进入界面如下：
![](https://youdaoyun-img.oss-cn-shanghai.aliyuncs.com/%E6%B5%8B%E8%AF%95RabbitMQ.PNG)

## 4. RabbitMQ添加用户  
在导航栏选择 Admin->Add a user  
如下：
![](https://youdaoyun-img.oss-cn-shanghai.aliyuncs.com/RabbitMQ_addUser.png)
## 5. 远程连接RabbitMQ
我示例添加一个用户 admin  
下图指示的地方是设置允许被虚拟机访问，用于远程连接RabbitMQ
![](https://youdaoyun-img.oss-cn-shanghai.aliyuncs.com/RabbitMQ_access.png) 
点击用户名进去设置为"/"即可  
![](https://youdaoyun-img.oss-cn-shanghai.aliyuncs.com/RabbitMQ_setAccess.png) 

### 完成之后就可以远程连接RabbitMQ了！


