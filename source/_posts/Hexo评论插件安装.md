---
title: Hexo yilia主题安装评论插件
date: 2019-07-18 11:08:05
categories: 
- Hexo
tags:
---
## Hexo yilia主题安装评论插件
#### **前言：该插件支持QQ微信登录，支持表情，gif动图评论！很帅有木有！插件采用韩国服务器的来必力评论插件 https://livere.com/**
**本文参考帖子** https://www.cnblogs.com/pengwenzheng/p/8407479.html

### 1、注册账号登录（支持QQ邮箱注册）---安装---复制代码
![](https://youdaoyun-img.oss-cn-shanghai.aliyuncs.com/laibili02.png)

### 2、本地配置
**进入本地仓库的主题目录 Shift+右键 打开终端**
![](https://youdaoyun-img.oss-cn-shanghai.aliyuncs.com/pinglunchajian.png)
**在该目录下新建一个livere.ejs文件**  
`git add livere.ejs`  
**编辑livere.ejs文件**  
`vim livere.ejs`  
**将第1步复制的代码粘贴进来，保存退出**

**回到上一级目录**  
`cd ..`  
**查看当前所在目录**  
`pwd`
![](https://youdaoyun-img.oss-cn-shanghai.aliyuncs.com/_partial.png)  
**查看当前目录所有文件列表**
![](https://youdaoyun-img.oss-cn-shanghai.aliyuncs.com/article.png)
**编辑article.ejs文件**   
`vim article.ejs`  
**找到下图代码位置并插入代码块**
![](https://youdaoyun-img.oss-cn-shanghai.aliyuncs.com/article02.png)  
```
<% if (theme.livere){ %>
  <%- partial('post/livere', {
        key: post.slug,
        title: post.title,
        url: config.url+url_for(post.path)
    }) %>
  <% } %>
```
**保存退出**  

**最后就是把插件放到主页面，进行加载，操作如下：

打开你主题的设置项：_config.yml（注意不是hexo的_config.yml，而是yilia的文件夹里的_config.yml）**
![](https://youdaoyun-img.oss-cn-shanghai.aliyuncs.com/article03.png)

**编辑_config.yml文件**
![](https://youdaoyun-img.oss-cn-shanghai.aliyuncs.com/article04.png)
<font color=red>注意：livere后面要有空格</font>

### 3、部署到github
**将文件部署到github上**  
`hexo g -d`  
#### 开始撸评论吧！！！！！