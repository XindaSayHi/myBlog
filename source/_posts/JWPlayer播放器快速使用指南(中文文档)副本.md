---
title: JWPlayer播放器快速使用指南(中文文档)
categories: JavaScript
作者: 信达
date: 2017-08-07 22:09:20
tags:
---
> 文档最后更新时间 **2017年7月26日**

> 文档基于 **JWPlayer 7.12.2** 版本。

> 文档中除了官方API外，还有部分基于官方API封装的扩展功能，扩展部分在文档中有明显标识，若使用扩展功能，需要在项目中额外引用 **xy.jwplayer.js** ，获取方式在本文档快速使用部分。

## 快速使用

1. 下载JWPlayer引用文件，这里提供两种获取方式

   第一种：通过官方Github项目下载并打包生成（无法使用本文档中注明为扩展的功能）

   ```javascript
   // 克隆项目
   git clone https://github.com/jwplayer/jwplayer.git

   // 进入项目文件夹
   cd jwplayer

   // 下载依赖包
   npm i 

   // 打包
   npm run lint

   // 将bin-release/目录放到项目中，并引用jwplayer.js文件即可
   ```

   第二种：直接下载文件包（可使用本文档中注明为扩展的功能） [JWPlayer 7.12.2及扩展文件包（暂时不能下载）](www.baidu.com)



2. 若仅使用官方API，则在页面中引入 **jwplayer.js**；

   若需要使用官方API和扩展API，则在页面引入 **jwplayer.js** 和 **xy.jwplayer.js** 

3. 在html中为JWPlayer准备好容器，示例中为 **<div id="player"></div>**

4. 实例化一个JWPlayer对象

5. 调用setup()函数进行初始化

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

## JWPlayer初始化



```javascript
// 代码示例
var player = jwplayer('player');

player.setup({
    // 将要播放的视频地址
    file: "//content.jwplatform.com/videos/xJ7Wcodt-cIp6U8lV.mp4", 
    // 视频播放前显示的图片
    image: "http://userimage8.360doc.com/16/0813/20/9331441_201608132058320889648269.jpg",
    // 播放器加载完毕后是否自动播放视频，true自动播放，false不自动播放
    autostart:false,
    // 设置播放器的音量，1-100之间
    volume:100,
    // 设置播放器的宽度
    width:640,
    // 设置播放器的高度
    height:360,
    
    // 播放完当前视频后，是否继续播放播放列表中的下一个视频
    repeat:true,
    
    //还没搞清楚
    mute:false, // Toggles the player's mute attribute.
});
```





## Properties(JWPlayer属性)

### getWidth()  获取播放器宽度


```javascript
// 代码示例
var player = jwplayer('player');

player.setup({
    file: "//content.jwplatform.com/videos/xJ7Wcodt-cIp6U8lV.mp4",
});

var playerWidth = player.getWidth();

console.log(playerWidth); // log -> 播放器宽度
```

### getHeight()  获取播放器高度

```javascript
// 代码示例
var player = jwplayer('player');

player.setup({
    file: "//content.jwplatform.com/videos/xJ7Wcodt-cIp6U8lV.mp4",
});

var playerHeight = player.getHeight();

console.log(playerHeight); // log -> 播放器高度
```

### getPlaylist() 获取播放列表信息

```javascript
// 代码示例
var player = jwplayer('player');

player.setup({
    file: "//content.jwplatform.com/videos/xJ7Wcodt-cIp6U8lV.mp4",
});

var playList = player.getPlaylist();

console.log(playList); // 本例log -> [object]
// 如果播放列表中有多个播放项，log -> [object，object，···]
```

#### getContainer()  获取播放器完整DOM

```javascript
// 代码示例
var player = jwplayer('player');

player.setup({
    file: "//content.jwplatform.com/videos/xJ7Wcodt-cIp6U8lV.mp4",
});

var playerDOM = player.getContainer();

console.log(playerDOM); 
// log -> 播放器的文章DOM
```

### getPlaylistIndex()  获取当前视频在播放列表中的索引值

```javascript
// 代码示例
var player = jwplayer('player');

player.setup({
    file: "//content.jwplatform.com/videos/xJ7Wcodt-cIp6U8lV.mp4",
});

var playListIndex = player.getPlaylistIndex();

console.log(playListIndex); 
// log -> 当前视频在播放列表中的索引值，如：1
```

### getPlaylistItem(index)  获取播放列表中第N项的信息

```javascript
// 代码示例
var player = jwplayer('player');

player.setup({
    file: "//content.jwplatform.com/videos/xJ7Wcodt-cIp6U8lV.mp4",
});

var playListItem = player.getPlaylistItem(0);

console.log(playListItem); 
// log -> 播放列表中第一项的信息
```



## Methods方法



#### play() 开始播放视频

```javascript
// 代码示例
var player = jwplayer('player');

player.setup({
    file: "//content.jwplatform.com/videos/xJ7Wcodt-cIp6U8lV.mp4",
});

$('#btn').click(function(){
    // 视频将开始播放
    player.play();    
})
```

#### pause() 暂停

```javascript
// 代码示例
var player = jwplayer('player');

player.setup({
    file: "//content.jwplatform.com/videos/xJ7Wcodt-cIp6U8lV.mp4",
});

$('#btn').click(function(){
    // 视频将暂停
    player.pause();
})
```

#### playlistNext()  切换至播放列表中的下一项

```javascript
// 代码示例
var player = jwplayer('player');

player.setup({
    file: "//content.jwplatform.com/videos/xJ7Wcodt-cIp6U8lV.mp4",
});

$('#btn').click(function(){
    // 视频将切换至播放列表中的下一项
    player.playlistNext();
})
```



#### playlistItem(index)  切换至播放列表的第N项

```javascript
// 代码示例
var player = jwplayer('player');

player.setup({
    file: "//content.jwplatform.com/videos/xJ7Wcodt-cIp6U8lV.mp4",
});

$('#btn').click(function(){
    // 视频将切换到播放列表的第1项
    player.playlistItem(0);
})
```

#### seek(*position*)  当前播放视频切换至第N秒

```javascript
// 代码示例
var player = jwplayer('player');

player.setup({
    file: "//content.jwplatform.com/videos/xJ7Wcodt-cIp6U8lV.mp4",
});

$('#btn').click(function(){
    // 视频将切换到第10秒
    player.seek(10);
})
```

#### resize(*width*, *height*) 设置播放器宽高

```javascript
// 代码示例
var player = jwplayer('player');

player.setup({
    file: "//content.jwplatform.com/videos/xJ7Wcodt-cIp6U8lV.mp4",
});

$('#btn').click(function(){
    // 播放器宽度将改为640px，高度将改为360px
    player.resize(640,360);
})
```

#### load()  更新播放器的播放列表

```javascript
// 代码示例
var player = jwplayer('player');

player.setup({
    file: "//content.jwplatform.com/videos/xJ7Wcodt-cIp6U8lV.mp4",
});

// 准备好播放列表
var newPlayList = [
  {
    file:'//content.jwplatform.com/videos/xJ7Wcodt-cIp6U8lV.mp4'
  },
  {
    file:'//content.jwplatform.com/videos/xJ7Wcodt-cIp6U8lV.mp4'
  },{
    file:'//content.jwplatform.com/videos/xJ7Wcodt-cIp6U8lV.mp4'
  }
];

$('#btn').click(function(){
    // 更新播放器的播放列表
    player.load(newPlayList);
})
```

#### xyJWPlayerAddAddBefore(obj,url,isShut,shutImgUrl)  

#### 在视频前插入广告 [ 扩展方法 ]

```javascript
// 代码示例
var player = jwplayer('player');

player.setup({
    file: "//content.jwplatform.com/videos/xJ7Wcodt-cIp6U8lV.mp4",
});

/*
 * 监听视频准备完毕
 *   当视频准备完毕时，xyJWPlayerAddAd，在视频中插入一段广告
 *   调取插入广告方法，参数:
 *      1.播放器实例化对象
 *      2.广告地址
 *      3.广告是否允许跳过,true/false，默认为true
 *      4.广告图标地址，参数3为false，此参数则不会被使用
 * */
player.on('ready',function () {
  
  xyJWPlayerAddAddBefore(
    
    //第一个参数，播放器实例化对象
    player,
    
    // 第二个参数，广告地址
    '//content.jwplatform.com/videos/xJ7Wcodt-cIp6U8lV.mp4',
    
    // 第三个参数，广告是否允许跳过,true/false，默认为true
    true,
    
    // 第四个参数，广告图标地址，参数3为false，此参数则不会被使用
    './src/skip.png'
  );
  
 })
```

####  xyJWPlayerAddAd(obj,url,isShut,shutImgUrl)

#### 在视频播当前位置插入广告 [ 扩展方法 ]

```javascript
// 代码示例
var player = jwplayer('player');

player.setup({
    file: "//content.jwplatform.com/videos/xJ7Wcodt-cIp6U8lV.mp4",
});

/*
 * 点击按钮在视频当前位置插入一段广告
 *      1.播放器实例化对象
 *      2.广告地址
 *      3.广告是否允许跳过,true/false，默认为true
 *      4.广告图标地址，参数3为false，此参数则不会被使用
 * */
$('#btn').click(function(){
  
  	xyJWPlayerAddAd(
    
    //第一个参数，播放器实例化对象
    player,
    
    // 第二个参数，广告地址
    '//content.jwplatform.com/videos/xJ7Wcodt-cIp6U8lV.mp4',
    
    // 第三个参数，广告是否允许跳过,true/false，默认为true
    true,
    
    // 第四个参数，广告图标地址，参数3为false，此参数则不会被使用
    './src/skip.png'
  );
  
});
```

#### remove()  删除实例

```javascript
// 代码示例
var player = jwplayer('player');

player.setup({
    file: "//content.jwplatform.com/videos/xJ7Wcodt-cIp6U8lV.mp4",
});

// 调用后实例被销毁
player.remove();
```

## callbacks回调函数(监听)



### ready（播放器初始化）

```javascript
// 代码示例
var player = jwplayer('player');

player.on('ready',function(){
    // 在这里编写的代码将在播放器初始化完毕后执行
    // 这是一个最早触发的API
})
```

### all（任何事件）

```javascript
// 代码示例
var player = jwplayer('player');

player.on('all',function(){
    // 在这里编写的代码在播放器执行任何操作后都会执行
})
```

### buffer (开始缓冲，一般是第一次播放时)

```javascript
// 代码示例
var player = jwplayer('player');

player.on('buffer',function(){
    // 在这里编写的代码将在开始缓存时执行
    // 一般是第一次开始播放时触发
})
```

### setupError（初始化出现错误）

```javascript
// 代码示例
var player = jwplayer('player');

player.setup({
    file: "//content.jwplatform.com/videos/xJ7Wcodt-cIp6U8lV.mp4",
});

player.on('setupError',function(){
    // 在初始化出现错误时执行
})
```

### remove（实例被销毁）

```javascript
// 代码示例
var player = jwplayer('player');

player.on('remove',function(){
	// 当实例被销毁时执行
})
```

### playlist（更新播放列表）

```javascript
// 代码示例
var player = jwplayer('player');

player.on('playlist',function(){
	// 当更新播放列表时执行
})
```

### playlistItem（切换播放列表中播放项）

```javascript
// 代码示例
var player = jwplayer('player');

player.on('playlistItem',function(){
	// 当切换播放列表中的项时执行，如：播放下一个视频
})
```

### playlistComplete（播放列表全部播放完毕）

```javascript
// 代码示例
var player = jwplayer('player');

player.on('playlistComplete',function(){
	// 当播放列表全部播放完毕时出发
    // Ps:当播放器设置为循环播放时，该回调方法不会执行
})
```



## Api - Interactive - 交互按钮

#### addButton()  增加一个交互按钮的通用方法

```javascript
// 代码示例
var player = jwplayer('player');

player.setup({
    file: "//content.jwplatform.com/videos/xJ7Wcodt-cIp6U8lV.mp4",
});

// 增加一个交互按钮
player.addButton(
    // 第一个参数，用来指定添加图形按钮的图片地址
    "//icons.jwplayer.com/icons/white/download.svg",
    
    // 第二个参数，用来指定鼠标移到按钮上的提示文字
    "快点击我！",
    
    // 第三个参数，用来指定点击按钮后所执行的代码
    function() {
       // code
    },
    
    // 第四个参数，用来为按钮指定一个唯一名称，jwplayer内部使用
    "btn"
);    
```
#### removeButton()  删除一个交互按钮的通用方法

```javascript
// 代码示例
var player = jwplayer('player');

player.setup({
    file: "//content.jwplatform.com/videos/xJ7Wcodt-cIp6U8lV.mp4",
});

// 删除一个已定义过的交互按钮
player.removeButton('btn'); // btn为交互按钮的标识，在定义此按钮时指定，addButton()的第四个参数
```

