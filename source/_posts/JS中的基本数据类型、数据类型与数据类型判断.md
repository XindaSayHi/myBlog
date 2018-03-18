---
title: JS中的基本数据类型、数据类型与数据类型判断
categories: JavaScript
作者: 信达
date: 2017-12-05 12:08:55
tags: 

---
本文总结了JS中所包含的数据类型，哪些是基本数据类型，以及这些数据类型在开发过程中如何进行判断。

<!--more-->

## 所有数据类型

截止目前，JS中共有7种数据类型：`undefined`  `null` `boolean` `number` `string` `object` `symbol`

PS：`symbol` 这种数据类型，是在ES6标准中新增的，它表示一个独一无二的值。

## 基本数据类型

JS中的基本数据类型有：`undefined`  `null` `boolean` `number` `string`  `symbol`

## 各数据类型

### Undefined类型

undefined类型只有一个值，就是undefined。

在使用var声明一个变量但未对其进行初始化时，变量的值就等于undefined，比如：

```javascript
var message;
console.log(message == undefined); // log => true
```

### Null类型

null类型同样只有一个值，就是null。从逻辑上来讲，null表示一个空的对象指针，因此使用typeof检测时会返回object，示例如下：

```javascript
var cat = null;
```



## 判断数据类型

开发中如果需要判断数据类型，我们可以根据不同的场景选择下面的几种方法，为了方便理解，我们先定义下面几个变量，这些变量涵盖了各种数据类型的数据，如下

```javascript
var a = undefined;  // undefined类型数据
var b = null;       // null类型数据
var c = 'str';      // string类型数据
var d = 111;        // number类型数据
var e = true;       // boolean类型数据
var f = Symbol();   // symbol类型数据
var g = [];         // Array类型数据，属于object数据的一种
var h = {};         // object类型数据,属于object数据的一种
var i = function () {}; // function
var j = new Date(); // date类型数据，属于object数据的一种
```

在定义了上面这几种数据类型之后，我们来看一下几种常用的数据类型判断方式如何进行实际使用

#### 通用方法，通过prototype判断

这种判断方式写起来相对比较麻烦，但优点是能够准确的判断各种类型的数据，算是很通用的方式，使用上方定义的数据进行测试，结果如下：

```javascript
console.log(Object.prototype.toString.call(a));  // log -> [object Undefined]
console.log(Object.prototype.toString.call(b));  // log -> [object Null]
console.log(Object.prototype.toString.call(c));  // log -> [object String]
console.log(Object.prototype.toString.call(d));  // log -> [object Number]
console.log(Object.prototype.toString.call(e));  // log -> [object Boolean]
console.log(Object.prototype.toString.call(f));  // log -> [object Symbol]
console.log(Object.prototype.toString.call(g));  // log -> [object Array]
console.log(Object.prototype.toString.call(h));  // log -> [object Object]
console.log(Object.prototype.toString.call(i));  // log -> [object Function]
console.log(Object.prototype.toString.call(j));  // log -> [object Date]
```

#### 简单判断，通过typeof判断

在有些开发场景下，我们可能不需要非常准确的知道数据的类型，只是需要知道数据大致是哪种类型即可，这种场景下可以使用较为简单的typeof进行判断，注意这种判断方式无法区分null类型和各object的具体类型，使用上面定义的数据进行测试，结果如下：

```javascript
console.log(typeof a);  // log -> undefined
console.log(typeof b);  // log -> object
console.log(typeof c);  // log -> string
console.log(typeof d);  // log -> number
console.log(typeof e);  // log -> boolean
console.log(typeof f);  // log -> symbol
console.log(typeof g);  // log -> object
console.log(typeof h);  // log -> object
console.log(typeof i);  // log -> function
console.log(typeof j);  // log -> object
```

#### 已知为对象，判断具体类型，通过instanceod进行判断

在某些场景下，我们已知一个数据是对象类型，需要确定数据究竟是哪种类型，这时我们可以使用instanceod的方式进行判断，需要注意instanceof只能用来判断object类型的数据，判断其他类型的数据会报错，测试结果如下：

```javascript
console.log(g instanceof Array );  // log -> ture
console.log(h instanceof Object );  // log -> true
console.log(i instanceof Function );  // log -> true
console.log(j instanceof Date );  // log -> true
```



