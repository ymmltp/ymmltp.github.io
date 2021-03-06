---
title: Css详细讲解
date: 2020-06-30 15:24:49
tags: 学无止境
---

# CSS布局

## 尺寸

1、块级元素auto,是随父元素变化的

2、一旦元素被设为浮动，该元素的width就由内容元素决定

### PX/EM/REM

#### 1、PX(像素)

#### 2、EM

EM继承父元素字体大小，默认1em=16px, 0.875em=4px, 0.75em=12px, 0.625em=10px

```css
body{font-size: 62.5%;}/*简化换算*/
p {font-size: 1.2em;}  /*这样1.2em=12px*/
```

```html
<style>
body{font-size: 62.5%;}	   /*简化换算 1em=10px*/
.con1{font-size: 1.2em;}   /*这样1.2em=12px*/
.con2{font-size: 1em;}     /*由于em继承父元素字体大小，此时font-size=1em=12px*/
.con3{font-size: 1.2em;}   /*由于em继承父元素字体大小，此时font-size=1.2em=12px*1.2=14.4px*/
</style>

<body>
<div class="con1">
    <div class="con2">
        <div class="con3">
        </div>
    </div>
</div>
</body>
```

#### 3、REM

REM类似于EM，但是他的大小只相对于html的根元素，可以忽略继承的层级关系。



## Grid

## Flex

## [Float](https://www.imooc.com/learn/121)(少用)

float会使父容器高度塌陷（父容器的高度无法定位和使用）

float原本是用来实现文字环绕效果的

#### 1.清除float的影响

* 在block元素底部插入clear:both属性的元素【可以使用CSS after伪元素(IE6,IE7不识别)】 

* BFC/haslayout(IE6/IE7)：使内部元素和外部完全隔绝
```css
IE8及以上浏览器：.clearfix:after{content:'';display:table;clear:both}
IE6/IE7使用：.clearfix{*zoom:1;}
```

<p style="color:red">.clearfix只应该用在包含浮动子元素的父级元素上</p>

#### 2.float的滥用

* 使元素block块状化
* 去空格化,使元素紧密排列(将空格的文字元素置后了,实现文字环绕)
* float在低版本的IE(6,7)下会有很多问题

#### 3.float与流体布局

```css
左侧：width + float:left;
右侧：padding-left/margin-left =  width
```

自适应的流体布局:

```css
左侧：float
右侧：display:table-cell(IE8+)/inline-block(IE7)
```



## [Absolute](https://www.imooc.com/learn/192)



## [Margin](https://www.imooc.com/learn/680)

#### 1. 百分比margin的计算规则
* 普通元素：不管是何种margin(margin-top;margin-bottom;margin-left;mergin-right)都是相对于父级元素的width计算的
* 绝对定位(position:absolute)元素：相对于第一个具有定位属性的祖先元素（relative/absolute/fixed）的width计算

#### 2. margin重叠
* **通常特性：**
	只发生在block属性的元素上(不含float,absolute元素)
	不考虑writing-mode,只发生在垂直方向上(只有margin-top和margin-bottom会有此现象)
* **种情景**
  相邻的兄弟元素
  父级和第一个/最后一个子元素
  空block元素

* **margin计算法则**
   正正取最大
   正负取相加
   负负取最负

