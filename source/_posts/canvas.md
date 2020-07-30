---
title: Canvas Learning
date: 2020-07-30 20:55:38
tags: 学无止境
---

## Canvas的定义

<span style="color:red">html属性中的width和height，不要使用css样式，因为这个属性除了定义画板大小，还定义了画板的分辨率</span>

```html
<!DOCTYPE html>
<html>
    <head lang="zh-CN">
        <meta charset="UTF-8">
        <title>Canvas Demo</title>
    </head>
    <body>
        <canvas id="canvas" width="800" height="800" style="border:1px solid gray;margin:50px auto;display:block">
            当前浏览器不支持canvas(只有浏览器不支持canvas时才会显示这段话)/或者在js中判断canvas.getContext('2d')是否为空。
        </canvas>
        <script>
            //canvas是基于状态来绘制的
            window.onload=function(){
                var canvas=document.getElementById("canvas");
                //使用Context绘制
                var context=canvas.getContext('2d');
            }
        </script>
    </body>
</html>
```

## Canvas的用法

#### 1、属性  

```js
//*****canvas是基于状态来绘制的，只使用最后一次赋值的属性*****//

//js中定义画板的大小用width和height属性，
canvas.width=1024;
canvas.height=768;

//设置画笔的属性
context.lineWidth = 5;
context.strokeStyle = "#ff0000"; //支持css样式
//设置填充属性
context.fillStyle= "rgb(2,100,222)";
```

#### 2、主要方法

```javascript
//获取画板对象
var context=canvas.getContext('2d');  //2d画板
var context=canvas.getContext('3d');  //3d画板

//绘图接口
//画板左上角为原点，向右X正，向下Y正
context.moveTo(100,100);
context.lineTo(700,700);
//设置绘制范围
context.beginPath();
context.closePath();

//绘制线条
context.stroke();  
//填充图形
context.fill();

```



#### 3、实例

```javascript
//canvas是基于状态来绘制的，只使用最后一次赋值的属性
window.onload=function(){
    var canvas=document.getElementById("canvas");
    //使用Context绘制
    var context=canvas.getContext('2d');
    context.moveTo(100,100);
    context.lineTo(700,700);
    context.lineTo(100,700);
    context.lineTo(100,100);

    //设置画笔的属性
    context.fillStyle= "rgb(2,100,222)";
    context.fill();

    //设置画笔的属性
    context.lineWidth = 5;
    context.strokeStyle = "#ff0000";
    context.stroke();  

    context.moveTo(200,100);
    context.lineTo(800,700);
    context.strokeStyle = "black";  //black会覆盖上面的 "#ff0000"，所以最后都是黑色线条
    context.stroke();  
}
```

**如何绘制两个不同的线条**

```javascript
//绘制第一个图形
context.beginPath();
context.moveTo(100,100);
context.lineTo(700,700);
context.lineTo(100,700);
context.lineTo(100,100);
context.closePath();
context.lineWidth = 5;
context.strokeStyle = "#ff0000";
context.stroke();  

//绘制第二个图形
context.beginPath();
context.moveTo(200,100);
context.lineTo(800,700);
context.closePath();
context.strokeStyle = "black";
context.stroke();  
```

**绘制七巧板**

```html
<!DOCTYPE html>
<html>
    <head lang="zh-CN">
        <meta charset="UTF-8">
        <title>Canvas Demo</title>
    </head>
    <body>
        <canvas id="canvas" width="800" height="800" style="border:1px solid gray;margin:50px auto;display:block">
            当前浏览器不支持canvas.../或者在js中判断canvas.getContext('2d')是否为空。
        </canvas>
        <script>
            //定义七巧板
            let tangram = [
                {p:[{x:0,y:0},{x:800,y:0},{x:400,y:400}],color:"#caff67"},
                {p:[{x:0,y:0},{x:400,y:400},{x:0,y:800}],color:"#67becf"},
                {p:[{x:800,y:0},{x:800,y:400},{x:600,y:600},{x:600,y:200}],color:"#ef2d61"},
                {p:[{x:600,y:200},{x:600,y:600},{x:400,y:400}],color:"#f9f51a"},
                {p:[{x:400,y:400},{x:600,y:600},{x:400,y:800},{x:200,y:600}],color:"#a594c0"},
                {p:[{x:200,y:600},{x:400,y:800},{x:0,y:800}],color:"#fa8ecc"},
                {p:[{x:800,y:400},{x:800,y:800},{x:400,y:800}],color:"#f6ca29"},
            ]

            window.onload=function(){
                var canvas=document.getElementById("canvas");
                var context=canvas.getContext('2d');    //使用Context绘制
                tangram.forEach(function(item){
                    draw(item,context);
                })
            }

            //画图方法
            function draw(piece,cxt)
            {
                cxt.beginPath();
                cxt.moveTo(piece.p[0].x,piece.p[0].y);
                for (var i = 1; i < piece.p.length; i++)
                {
                    cxt.lineTo(piece.p[i].x,piece.p[i].y);
                }
                cxt.closePath();
                //设置画笔的属性
                cxt.fillStyle= piece.color;
                cxt.fill();
                cxt.strokeStyle="black";
                cxt.lineWidth=2;
                cxt.stroke();
            }
        </script>
    </body>
</html>
```

