---
title: '使用antd组件遇到的坑'
date: 2018-04-25 11:19:58
tags: 'antd'
---

#### div不能是p的子元素
错误代码提示如下图所示：

```
Error:<div> cannot appear as a descendant of <p>
```
意思是，div不能是p的子元素。

一开始审查自己的代码结构，发现并没有什么不对，code里面虽然有p标签，但我不至于犯在p标签里面，嵌套div标签的低级错误。

但是F12审查文档元素的时候，发现生成的html文档里面的确是p嵌套了div。

原因是我在p标签里面，使用了antd的组件，组件内部结构有div标签，导致报错！
