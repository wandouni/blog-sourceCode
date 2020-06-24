---
title: react vdom
date: 2020-05-26 21:22:35
tags: ['react','vdom']
---
### vdom本质是什么
描述渲染内容的js对象，形如：
```
{
  "$$typeof": "Symbol(react.element)",
  "type":"div",
  "key":null,
  "ref":null,
  "props":{
    "children":[
      "这是一个tag",
      {
        "$$typeof": "Symbol(react.element)",
        "type":"div",
        "key":null,
        "ref":null,
        "props":{"children":"555"},
        "_owner":null,"_store":{}
      },
      {
        "type": "class Tag",
        "key":null,
        "ref":null,
        "props":{},
        "_owner":null,
        "_store":{}
      }
    ]
  },
  "_owner":null,
  "_store":{}
}
由创建
```
### createElement
```
React.createElement(
  type,
  [props],
  [...children]
)
```