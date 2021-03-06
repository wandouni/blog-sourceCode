---
title: Object.keys循环出来的对象属性顺序到底遵循什么规律'
date: 2020-06-24 17:16:42
tags: js
---
今天在写业务代码的时候定义了一个这样的对象数据结构
```
let Map = {
  '00': {
    name: '未修改未计算',
  },
  '01': {
    name: '未修改已计算',
  },
  '10': {
    name: '已修改未计算',
  },
  '11': {
    name: '已修改已计算',
  },
};
```
循环它
```
Object.keys(Map)

for(let k in Map){
  console.log(k)
}
```
结果输出
```
10
11
00
01
```
🤣这个结果实在让人困惑，但也说明并不是照我想象的按照定义顺序输出，那为啥是这么个顺序呢。

首先先去MDN !

先查看`Object.keys()`
```
Object.keys() 方法会返回一个由一个给定对象的自身可枚举属性组成的数组，数组中属性名的排列顺序和正常循环遍历该对象时返回的顺序一致 。
```
没啥东西，那看看`for...in`

在提到`数组迭代和 for...in`时，有这么一段话
```
因为迭代的顺序是依赖于执行环境的，所以数组遍历不一定按次序访问元素。因此当迭代访问顺序很重要的数组时，最好用整数索引去进行for循环（或者使用 Array.prototype.forEach() 或 for...of 循环）
```
在迭代数组的时候可能不一定按次序访问数组元素，那这里我们定义的对象是有点类数组的，不按照顺序访问元素，那按照什么规则访问数组元素呢？

然后找到了这篇文章:

[Chrome Opera 中 for-in 语句遍历出对象属性的顺序与定义的不同](https://blog.csdn.net/yesicatt/article/details/53557962)

可以发现：

for-in 语句的属性遍历的顺序在 `ECMA-262（ECMAScript）`版本迭代的过程中定义是有变化的。

第三版是`对象定义时属性的书写顺序决定的`

第五版是`属性遍历的顺序是没有被规定的`

那么根据不同版本规范实现的js解析引擎对for-in的处理是有区别的！

这篇文章总结为
```
Chrome Opera 中使用 for-in 语句遍历对象属性时会遵循一个规律，它们会先提取所有 key 的 parseFloat 值为非负整数的属性， 然后根据数字顺序对属性排序首先遍历出来，然后按照对象定义的顺序遍历余下的所有属性。其它浏览器则完全按照对象定义的顺序遍历属性。
```
在这里我们定义的第一个key '00' parseFloat('00')等于0，0属于非负整数，那么这么说应该在循环输出的第一个，然而并不是，那要怎么理解呢？

知乎大法好，于是找到了这个：

[JS for...in 循环出来的对象属性顺序到底是什么规律？](https://zhuanlan.zhihu.com/p/58401380)

总结是：
```
先遍历出整数属性（integer properties，按照升序），然后其他属性按照创建时候的顺序遍历出来。
```
那什么是整数属性呢？
```
String(Math.trunc(Number(prop)) === prop;
// 当上面的判断结果为 true，prop 就是整数属性，否则不是。
```
然后我发现他参考了

[https://javascript.info/object#the-for-in-loop](https://javascript.info/object#the-for-in-loop)

🤣 一个宝藏js外文网站


