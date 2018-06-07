---
title: flow.js基础
categories: 技术笔记本
作者: 信达
date: 2018-06-06 11:14:33
---

flow.js是一个JavaScript静态类型检查工具，由Facebook开发维护，通过flow.js，能够轻量级的为JavaScript提供静态语法检查的能力，相比于TypeScript，其使用成本低且对代码侵入性更小。

## 语法

#### 文件标识

在需要flow.js检查的文件头部，通过注释增加 @flow 声明即可，如：

```js
// example-project/example.js

// @flow

// code...
// 当前文件将会被flow.js检查
```

#### 基础类型检查

flow.js中定义了5种基础类型，他们分别是：boolean、number、string、null、viod，对于这5种基础类型的检测，只需要在定义时声明需要的类型即可，比如：

```javascript
// example-project/example.js

// @flow

var num:number = 1;
var str:string = 'abc';
```

Ps：即使声明了@flow ，也可以不使用类型检查，使用普通的JavaScript写法即可。

#### 复杂类型检查

除了5种基础类型外，还有些比较复杂的类型，主要包含4种：Object、Array、Function、自定义Class，这几种类型比较复杂，而且可以互相嵌套，需要根据不同场景进行检查，flow.js中也提供了许多种不同的检查语法，这里只列举几个比较基础的

##### 对象 Object

```javascript
//@flow

//Object大写的O
var o:Object = {
  hello:'h'
};

//声明了Object的key
var o2:{key:string} = {
  key:'z233'
};
```

##### 数组 Array

```javascript
//@flow

//数组内都是相同类型
var numberArr:number[] = [12,3,4,5,2];
//另一个写法
var numberAr2r:Array<number> = [12,3,2,3];

var stringArr:string[] = ['12','a','cc'];
var booleanArr:boolean[] = [true,true,false];

//数组内包含各个不同的类型数据
//第4个原素没有声明，则可以是任意类型
var arr:[number,string,boolean] = [1,'a',true,function(){},]
```

##### 函数 Function

函数比较特殊，核心是参数与返回值

```javascript
//@flow

/**
 * 声明带类型的函数
 * 这里是声明一个函数fn，规定了自己需要的参数类型和返回值类型。
 */
function fn(arg:number,arg2:string):Object{
  return {
    arg,
    arg2
  }
}
//同理，ES2015箭头函数的写法
var fn2 = (arg:number,arg2:string):Object => {
  return {
    arg,
    arg2
  }
}

/**
 * 这里是声明变量fn2，规定了它所需的函数的特征:
 * 参数： (arg:string,arg2:number)
 * 返回值：Object
 */
var fn3:(arg:string,arg2:number)=>Object = function(){
  return {}
}

/**
 * 对比下面这种写法,
 * 两者的声明的地方不一样，造成的意义也不同。
 */
var fn4 = function(arg:string,arg2:Object):number{
  return 1;
}
```

##### 自定义类

```javascript
//@flow

class MyClass{
  name:string;
  constructor(n){
    this.name = n;
  }
}

var myClass : MyClass = new MyClass('abc');
```

## 运行

使用flow.js语法的js浏览器显然不能直接解析，可以使用babel进行编译，对应的babel插件如下

> babel-plugin-transform-flow-strip-types

