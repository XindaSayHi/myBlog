---
title: JWPlayer播放器快速使用指南(中文文档)
categories: JavaScript
作者: 信达
date: 2017-08-07 22:09:20
tags:
---
> 文档基于 **JWPlayer 7.12.2** 版本。

> 文档中除了官方API外，还有部分基于官方API封装的扩展功能，扩展部分在文档中有明显标识，若使用扩展功能，需要在项目中额外引用 **xy.jwplayer.js** ，获取方式在本文档快速使用部分。

## 快速使用

### 下载文件

第一种(推荐)：直接下载 **JWPlayer7.12.2 + xy.jwplayer.min.js** 文件包   [点此下载](http://ouh8ga02y.bkt.clouddn.com/xy-jwplayer.zip)

第二种：通过官方Github下载并打包生成，不包含 **xy.jwplayer.min.js** 文件  [Github地址](https://github.com/jwplayer/jwplayer)

### 引入文件

若仅使用官方API，则在页面中引入 **jwplayer.js**；

若需要使用官方API和扩展API，则在页面引入 **jwplayer.js** 和 **xy.jwplayer.js** 

### 写入HTML代码

在html中为JWPlayer准备好容器，示例中为 **<div id="player"></div>**


1. 实例化一个JWPlayer对象
2. 调用setup()函数进行初始化

> 快速使用完整示例：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="./资源路径/jwplayer.js"></script>
    <!--如果你需要使用文档中标注为扩展的功能，则需要引用xy.jwplayer.js-->
  	<script src="./资源路径/xy.jwplayer.js"></script>
</head>
<body>
<div id="player"></div>
</body>
<script type="text/javascript">

    var player = jwplayer('player');

    player.setup({
        file: "//content.jwplatform.com/videos/xJ7Wcodt-cIp6U8lV.mp4", // 视频地址
      
      	// Ps：示例中仅传入了视频地址(file)一个参数，实际可以根据需要配置许多参数，具体参数列表可以查看下方[Api - setup - 初始化配置项]部分     
    });
 
</script>

</html>
```
