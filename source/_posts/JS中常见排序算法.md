---
title: JS中常见排序算法
categories: JavaScript
作者: 信达
date: 2017-12-04 23:50:59
tags: 
- 算法
---

排序是开发中常见的场景，本文梳理了JS里几种常见的排序算法。
<!--more-->

#### 冒泡排序

```javascript
var arr = [21,321,32,65,3,6,6,122,552,32,3];

/*冒泡排序*/
function maopao(arr) {
  var len = arr.length;
  for(var i=0;i<len;i++){
    for(var j=0;j<len-i-1;j++){
      if (arr[j]>arr[j+1]){
        var num = arr[j];
        arr[j] = arr[j+1];
        arr[j+1] = num;
      }
    }
  }
  return arr;
}

```

### 插入排序

```javascript
/*插入排序*/
    function charu(arr) {
        var len = arr.length;
        var i,j,tmp,newArr;

        newArr = arr.slice(0);

        for(i=1;i<len;i++){
            tmp = newArr[i];
            j = i - 1;
            while(j>=0 && tmp < newArr[j]){
                newArr[j+1] = newArr[j];
                j--;
            }
            newArr[j+1] = tmp;
        }
        return newArr;
    }
```

