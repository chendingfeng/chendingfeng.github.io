---
title: 关于layui 多文件上传一些问题 
date: 2019-08-08 17:08:05
categories: 
- 前端 
tags: 
copyright: true
---
#### 前言：
最近使用layui文件上传模块实现批量上传图片遇到一些问题，包含：批量上传实时进度条，选中文件总数统计以及上传完成的文件统计。这篇文章主要是总结使用layui上传模块过程中遇到一些问题以及解决思路，这里不对layui文件上传模块做过多介绍，使用前建议阅读  
layui官方文档：https://www.layui.com/doc/modules/upload.html   
github源码：https://github.com/sentsin/layui/blob/master/src/lay/modules/upload.js  
#### 问题一
**目标：** 实现上传前选中文件之后统计选中文件的数量  
**问题描述：** 通过官方文档可以知道choose参数后面是选中文件之后的回调函数
![](https://youdaoyun-img.oss-cn-shanghai.aliyuncs.com/choose01.png)  

下面是示例选中两个图片文件，可以看到files队列中已经push两个文件，这两个文件是以map形式存入，但是obj中并没有提供获取队列长度的方法    
![](https://youdaoyun-img.oss-cn-shanghai.aliyuncs.com/choose03.png) 
![](https://youdaoyun-img.oss-cn-shanghai.aliyuncs.com/choose02.png)   

**问题解决：** 这个问题其实很简单，files是一个Object类型，我们都知道，在js中，Object有一个`Object.keys(obj)`方法，该方法传入一个obj对象，返回值为一个表示给定对象的所有可枚举属性的<font color="red">字符串数组</font>  
直接上代码:  

```   
choose: function choose(obj) {
			files = this.file = obj.pushFile();
			obj.preview(function (index, file, result) {
				imgCount = Object.keys(files).length;

			});
		}  

```

![](https://youdaoyun-img.oss-cn-shanghai.aliyuncs.com/choose04.png)    
上图可以看到我们已经获取到选中文件的个数！  

#### 问题二  
**目标：** 实现上传时进度条展示  
**问题描述：** 目前layui的文件上传模块是没有引入进度条显示的  
**问题解决1：** 参考文章：https://blog.csdn.net/qq_36311372/article/details/82117417  
我们需要修改layui文件上传模块的源码（src/lay/modules/upload.js）
![](https://youdaoyun-img.oss-cn-shanghai.aliyuncs.com/xhr01.png)  

**代码片段：**    

```
xhr:function () {
    var newXhr = i.ajaxSettings.xhr();
    // 给xhr的upload添加progress的监听
    newXhr.upload.addEventListener('progress' , function (e) {
    	var percent = Math.floor(e.loaded / e.total * 100); //计算出进度
    	typeof l.progress === 'function' && l.progress(e , percent); // 传递给upload的progress回调
    });
    return newXhr;
}
 
```

在upload.render中使用：  

```
	progress: function(e , percent) {
		element.progress('progressBar',percent  + '%');
	},
	choose: function(obj) {
    	files = this.file = obj.pushFile();
    	obj.preview(function (index, file, result) {
    		imgCount = Object.keys(files).length;
    
    	});
	}
 
```
<font color="red">但是这里实现的是单个文件上传的进度条，那批量上传就会出现进度条不断重复的问题（这里指的是批量上传文件时只展示一个进度条）</font>，如下图所示  

![](https://youdaoyun-img.oss-cn-shanghai.aliyuncs.com/importImage.gif)

**问题解决2：** 既然我们知道这个进度条是针对一个文件的，那我们只要把文件的完成个数/文件总数就能得到百分比，这里我们就要使用到问题一中刚刚得到的文件总数量。  
**代码片段：**   

```
	progress: function(e , percent) {
		if(percent == 100) content++; //content是图片上传完成的个数
		var per = Math.floor(content / imgCount * 100); //per是批量完成进度
		element.progress('progressBar', per + '%');
	}
```  

实现效果：  

![](https://youdaoyun-img.oss-cn-shanghai.aliyuncs.com/importImage02.gif) 

#### 问题三  
**问题描述：**  layui文件上传模块的选中文件队列只提供了pushFile方法，并没有提供清除队列的方法（可能是我对源码理解不透，有大神知道的欢迎来指出）。在这种场景下，要是选错文件又不能清除之前选错的文件，那就很尴尬了。  
**问题解决：**  参考文章：https://blog.csdn.net/u014598014/article/details/90559211   
只要在每次选择文件的回调函数（也就是choose）中加入以下代码即可  
**代码片段：**  

```  
	choose: function(obj) {
		for (let x in files) {  //先来个for循环清空队列
			delete files[x];
		}
    	files = this.file = obj.pushFile();
    	obj.preview(function (index, file, result) {
    		imgCount = Object.keys(files).length;
    
    	});
	}
```  

#### 问题四  
**问题描述：**  统计上传成功与失败的文件个数  
**问题解决：**  layui上传文件模块其中有三个回调函数：done 、allDone 、error  
<font color="red">done:</font> 每个文件上传完的回调  
<font color="red">allDone:</font> 全部文件上传完的回调  
<font color="red">error:</font> 文件上传失败时的回调  
**代码片段：**  

![](https://youdaoyun-img.oss-cn-shanghai.aliyuncs.com/uploadCount.png)  

### 未完待续  
暂时先到这，以后遇到关于该模块的问题，再做更新  

### 后语  

>  若有错误不当之处，还望大家批评指正。一起学习进步


