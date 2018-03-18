---
title: JavaScript中的this
categories: JavaScript
作者: 信达
date: 2018年03月18日 15:55:59
tags: JavaScript
---
js中的this总是会指向一个对象，具体指向哪个对象会根据运行时函数的运行环境动态绑定，而不是在函数声明的时候确定的。在实际的应用过程中，this的指向大致可以分为以下4种：

<!--more-->

- 作为函数的方法调用
- 作为普通函数调用
- 构造器调用
- Function.prototype.call 或 Function.prototype.apply调用

## 1. 作为函数的方法调用

当函数作为对象的方法被调用时，this指向该对象：

```javascript
var obj = {
    name: 'timo',
    getName: function () {
        console.log(this.name);
    }
};
obj.getName();  // log => 'timo'
```

## 2. 作为普通函数调用

当函数不作为对象的方法被调用时，也就是我们平时的普通函数调用，此时的this总是会指向全局对象，在js中全局对象是window对象。

下面是两种情况：

```javascript
window.name = 'timo';
var getName = function () {
    return this.name;
};
console.log(getName()); // log => 'timo'
```

```javascript
window.name = 'timo';
var obj = {
    name: 'anni',
    getName: function () {
        return this.name;
    }
};
var getName = obj.getName;
console.log(getName()); // 'timo'
```

## 3.构造器调用

js中没有类，但是可以从构造器中创建函数，同时提供了new运算符，使得构造器看起来更像一个类。除了部分宿主提供的内置函数，大部分JS函数都可以当做构造器来使用。构造器的外表和普通函数一模一样，他们的主要区别是调用方式，当用new运算符调用函数时，该函数会返回一个对象，通常情况下，构造器里的this就指向返回的这个对象，代码如下：

```javascript
var obj = {
    this.name = 'timo';
};
var newObj = new obj();
console.log(newObj.name); // log => 'timo'
```

如果使用new调用构造器时，构造器显式的返回了一个object类型的对象，那么此次运算结果最终会返回这个对象，而不是我们之前期待的this，示例代码如下：

```javascript
var obj = {
    name: 'timo',
    return: {
        name: 'anni'
    }
};
var newObj = new myClass();
console.log(newObj.name()); // log => 'anni'
```

## 4.Function.prototype.call或Function.prototype.apply调用

使用call和apply可以动态的改变传入函数的this，示例代码如下：

```javascript
var obj1 = {
    name: 'timo',
    getName: function () {
        return this.name;
    }
};
var obj2 = {
    name: 'anni'
};
console.log(obj1.getName()); // log => 'timo'
console.log(obj1.getName.call(obj2)); // log => 'anni'
```

