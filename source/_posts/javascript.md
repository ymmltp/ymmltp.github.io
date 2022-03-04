---
title: javascript
date: 2020-08-20 09:39:35
tags: 学无止境
---

## 1、基础知识

1、判断数组是否包含某个元素：indexOf




## 2、知识提升
1、a标签不跳转
2、js直接给input元素赋值不能触发onchange事件：

```javascript
使用trigger方法，手动触发
 $("input").trigger("focus");  //触发focus的事件，也实际执行了focus方法，input获得焦点
 $("input").triggerHandler( "focus" );  //触发focus的事件，不执行focus方法，input不获得焦点
 ```


## 3、参考资料

[1、const,var,let的区别](https://www.cnblogs.com/zhaoxiaoying/p/9031890.html)

