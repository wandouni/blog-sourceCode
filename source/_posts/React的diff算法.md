---
title: React的diff算法
date: 2020-05-26 21:59:21
tags: ['react','diff算法']
---

#### 调和
将Virtual DOM树转换成actual DOM树的最少操作的过程称为`调和` 。

#### 复杂度
O(n^3) -> O(n)

#### diff策略
React用 三大策略 将O(n^3)复杂度 转化为 O(n)复杂度

##### 策略一（tree diff）：
Web UI中DOM节点跨层级的移动操作特别少，可以忽略不计。

##### 策略二（component diff）：
拥有相同类的两个组件 生成相似的树形结构，
拥有不同类的两个组件 生成不同的树形结构。

##### 策略三（element diff）：
对于同一层级的一组子节点，通过唯一id区分。

- tree diff
- component diff
- element diff

#### 描述a b c d节点变化成b a d c的过程
a b c d
| | | |
b a d c

#### 描述a b c d节点变化成b e c a的过程
a b c d
| | | |
b e c a

#### 描述a b c d节点变化成d a b c的过程
a b c d
| | | |
d a b c




参考文章[https://www.jianshu.com/p/3ba0822018cf](https://www.jianshu.com/p/3ba0822018cf)