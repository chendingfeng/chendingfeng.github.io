---
title: IDEA连接数据库时区问题
date: 2019-07-18 12:10:05
categories: 
- JAVA
tags:
- 报错处理
---
## idea连接MySQL数据库报错
#### 错误日志：
```
java.lang.RuntimeException: com.mysql.cj.exceptions.InvalidConnectionAttributeException: The server time zone value 'ÖÐ¹ú±ê×¼Ê±¼ä' is unrecognized or represents more than one time zone. You must configure either the server or JDBC driver (via the serverTimezone configuration property) to use a more specifc time zone value if you want to utilize time zone support.
			at sun.reflect.NativeConstructorAccessorImpl.newInstance0(Native Method)
			at sun.reflect.NativeConstructorAccessorImpl.newInstance(NativeConstructorAccessorImpl.java:62)
			at sun.reflect.DelegatingConstructorAccessorImpl.newInstance(DelegatingConstructorAccessorImpl.java:45)
			at java.lang.reflect.Constructor.newInstance(Constructor.java:423)
			at com.mysql.cj.exceptions.ExceptionFactory.createException(ExceptionFactory.java:61)
			at com.mysql.cj.exceptions.ExceptionFactory.createException(ExceptionFactory.java:85)
			at com.mysql.cj.util.TimeUtil.getCanonicalTimezone(TimeUtil.java:132)
			at com.mysql.cj.protocol.a.NativePro... (show balloon)
```
#### 解决方法：
在连接数据库的URL中如下填写：
```
jdbc:mysql://localhost:3306/test?useUnicode=true&characterEncoding=UTF-8&useJDBCCompliantTimezoneShift=true&useLegacyDatetimeCode=false&serverTimezone=UTC
```
![](https://youdaoyun-img.oss-cn-shanghai.aliyuncs.com/MySQL_URL.png)
![](https://youdaoyun-img.oss-cn-shanghai.aliyuncs.com/MySQL_URL02.png)