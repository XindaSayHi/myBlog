---
title: 通过CSS的box-sizing属性控制盒模型的解析方式
categories: html/css
作者: 信达
date: 2017-12-02 22:35:34
tags: 
- CSS
---
HTML中的所有元素都可以看做是一个盒子，通过CSS中的box-sizing属性可以将HTML中盒模型的解析方式进行设置。

<!--more-->
设置content-box为标准解析方式，元素的宽度和高度由content+padding+border组成，为元素设置的宽高属性表示content部分；

设置为border-bo为IE传统盒模型(一般我们称之为怪异模式)，在这种模式下，我们为元素设置的宽度和高度属性表示的为content+padding+border部分。

下面的图说明的比较清楚：

![01](http://ouf94m87t.bkt.clouddn.com/01.png)

