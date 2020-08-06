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

### 1、常用方法 

<span style="color:red">canvas是基于状态来绘制的</span>

#### 基本方法

```javascript
//js中定义画板的大小用width和height属性，
canvas.width=1024;
canvas.height=768;

//2D绘图
//获取画板对象
var context=canvas.getContext('2d');  //2d画板

//绘图接口
//画板左上角为原点，向右X正，向下Y正
context.moveTo(100,100);
context.lineTo(700,700);

//设置绘制范围 不一定要同时出现
context.beginPath(); //开始一个新的路径，beginPath + lineTo = moveTo
context.closePath(); //当绘制的图形不是闭合图形时，会自动闭合，对fill无效，可以避免线段宽度带来的间隙
//刷新画布内容
cxt.clearRect(0,0,WINDOW_WIDTH,WINDOW_HEIGHT);  

//3D绘图
var context=canvas.getContext('3d');  //3d画板

//点是否在画布内
context.isPointInPath(x,y);

//添加事件
canvs.addEventListener("mouseup",function);
```

#### 图形绘制

```javascript
//线条绘制
//设置画笔的属性
context.lineWidth = 5;
context.lineCap = "butt"/"round"/"square" //线条起始形状，默认，圆形，方形
context.lineJoin = "miter"/"bevel"/"round" //线条相交部分的效果 ，尖角（默认），平角，圆角
context.miterLimit = 10(默认值); //相交线段的内角与外角距离的最大像素差，一旦超过这个值，lineJoin默认bevel
context.strokeStyle = "#ff0000"; //支持css样式
//绘制线条
context.stroke();  

//图形填充
//设置填充属性
context.fillStyle= "rgb(2,100,222)";
//填充图形 （如果填充发生在绘制线条之后，会使线条的宽度发生变化。所以一般要先填充再绘线）
context.fill();

//绘制矩形
context.rect(x,y,width,height)//规划矩形路线，需要使用stroke和fill来绘图，矩形的位置，宽高
context.strokeRect(x,y,width,height)//绘制矩形边框，使用的属性和stroke一样
context.fillRect(x,y,width,height)//绘制填充的矩形，使用的属性和fill一样

//绘制圆 
//(3点钟方向为0*pi/2*pi,6点钟方向0.5*pi,9点钟方向1*pi,12点钟方向1.5*pi)
context.arc(300,300,200,0,0.5*Math.PI,false); //圆心坐标(X,Y),半径，起始弧度，结束弧度，是否逆时针
context.actTo(x1,y1,x2,y2,r); //配合moveTo(x0,y0可以绘制半径为r,同时相切与直线(x0,y0)-(x1,y1)和直线(x1,y1)-(x2,y2)的弧线(x0,y0)-(x1,y1)部分可能会有直线；起始点是(x0,y0)，但结束点是圆弧与直线(x1,y1)-(x2,y2)的切点
```

#### 贝塞尔曲线

```javascript
//二次曲线
context.moveTo(x0,y0);
context.quadraticCurveTo(x1,y1,x2,y2); // 绘制起始点为(x0,y0),控制点为(x1,y1),结束点为(x2,y2)的曲线

//三次曲线
context.moveTo(x0,y0);
context.bezierCurveTo(x1,y1,x2,y2,x3,y3); // 绘制起始点为(x0,y0),控制点为(x1,y1),(x2,y2),结束点为(x3,y3)的曲线
```

#### 图形变换

```javascript
context.translate(x,y); // 位移，位移的移动是叠加的，所以移动之后需要反向移回，或者使用save,restore
context.scale(a,b); //长宽，会放大图像的所有属性（起始点坐标，线宽,图形大小）
context.rotate(deg); //旋转

context.transform(a,b,c,d,e,f);//水平缩放，水平倾斜，垂直倾斜，垂直缩放，水平位移，垂直位移transform和位移类似，是叠加的，可以使用setTransform，将他设成初始值
context.setTransform(1,0,0,1,100,100);//不考虑之前所有的transform

//这两者应该成对出现,进行图型变换前最好先保存。
context.save();//保存当前状态
context.restore();//回复至前一次保存的状态
```

#### 渐变色（可作为fillStyle/strokeStyle的值）

```javascript
//线性渐变色
var grd = context.createLinearGradient(xstart,ystart,xend,yend); // 
grd.addColorStop(stop,color);
//放射性渐变
var grd = context.createRadialGradient(x0,y0,r0,x1,y1,r1); // 在两个圆中间进行渐变
grd.addColorStop(stop,color);
//图像做背景填充
var pattern = context.createPattern(img/canvas/video,repeat-style); //填充对象可以是图片，canvas,或vedio;repear-stylt = no-rapeat/repeat-x/repeat-y/repeat
```

#### 文字

```javascript
//配置文字属性
context.font = "bold 40px Arial"; //默认值20px sans-serif
//font属性的所有值font-style(normal italic oblique),font-variant(normal small-caps),font-weight(normal/400 bold/700 ),font-size(20px 20em 100%),font-family(支持多备选字体 @font-face)

//绘制填充文字
context.fillStyle ="#058"; //可以使用渐变色和图像为背景
context.fillText("Welcome...",40,100,200); //string,x,y,文字最大长度（选填）

//绘制边框文字
context.strokeStyle ="#058";  //可以使用渐变色和图像为背景
context.strokeText("Hello...",500,100，200);

//文字对齐
context.textAlign = center/right/left //文字水平对齐，针对指定的x坐标
context.textBaseline = top/middle/bottom //文字垂直对齐，针对指定的y坐标

//文本的度量
context.measureText(string).width

```

### 2、高级方法

#### 阴影

```javascript
//可用于文字，图片
context.shadowColor  //类似于fillStyle
context.shadowOffsetX
context.shadowOffsetY
context.shadowBlur   // 阴影模糊程度，越大越模糊
```

#### 全局变量

```javascript
context.globalAlpha = 0.7 //全局透明度属性
context.globalCompositeOperation = "source-over" //全局图像覆盖属性 
```

| 图2覆盖图1                                | 图1覆盖图2                                     | 其他特性               |
| ----------------------------------------- | ---------------------------------------------- | ---------------------- |
| source-over                               | destination-over                               | lighter:重叠处颜色叠加 |
| source-atop:显示图1以及图2在图1内部的部分 | destination-atop:显示图2以及图1在图2内部的部分 | copy:只绘制图2         |
| source-in:显示图2在图1内部的部分          | destination-in:显示图1在图2内部的部分          | xor:重叠处图像挖空     |
| source-out:显示图2在图1外部的部分         | destination-out:显示图1在图2内部的部分         |                        |

#### 剪辑区域

```javascript
context.clip()  //将之前绘制的封闭图形作为新的画布环境
```

**实例**

实现一个探照灯效果

```javascript
            function light(){
                setInterval( function(){ draw(context);
                        update(canvas.width,canvas.height); }, 40); }

            function draw(cxt)
            {
                var canvas = cxt.canvas;
                cxt.clearRect(0,0,canvas.width,canvas.height);
                
                cxt.save();

                cxt.beginPath();
                cxt.fillStyle="black";
                cxt.fillRect(0,0,canvas.width,canvas.height);

                cxt.beginPath();
                cxt.arc(cycle.x,cycle.y,cycle.radius,0,Math.PI*2);
                cxt.fillStyle="white";
                cxt.fill();
                cxt.clip();  //只会显示出圆形内部的内容

                cxt.font = "bold 150px Arial";
                cxt.textAlign = "center";
                cxt.textBaseline = "middle";
                cxt.fillStyle = "#058";
                cxt.fillText("CANVAS",canvas.width/2,canvas.height/4);  //文字是画在原来的方形画布上的
                cxt.fillText("CANVAS",canvas.width/2,canvas.height/2);
                cxt.fillText("CANVAS",canvas.width/2,canvas.height/4*3);

                cxt.restore();
            }

            function update(width,height){
                cycle.x += cycle.vx;
                cycle.y += cycle.vy;

                if(cycle.x-cycle.radius<=0)
                {
                    cycle.vx = -cycle.vx;
                    cycle.x =cycle.radius;
                }
                if(cycle.x+cycle.radius>=width)
                {
                    cycle.vx = -cycle.vx;
                    cycle.x = width - cycle.radius;
                }
                if(cycle.y-cycle.radius<=0)
                {
                    cycle.vy = -cycle.vy;
                    cycle.y = cycle.radius;
                }
                if(cycle.y+cycle.radius>=height)
                {
                    cycle.vy = -cycle.vy;
                    cycle.y = height - cycle.radius;
                }
            }

```



#### 路径方向和剪纸效果

<span style = "color:red">使用fill()的这个特性实现剪纸效果</span>

```javascript
context.fill();  //遵循非零环绕原则,绘图与路径方向有关
```

**例子**:

```javascript
context.beginPath();
context.arc(400,400,300,0,2*Math.PI,false); 
context.arc(400,400,150,0,2*Math.PI,true);  //context.arc(400,400,150,0,2*Math.PI,false); 
context.closePath();
context.fillStyle="blue";
context.shadowColor= "gray";
context.shadowOffsetX = 10;
context.shadowOffsetY = 10;
context.shadowBlur = 10;

context.fill();
```

#### Canvas交互实例

点击改变小球的颜色

````javascript
 var canvas = document.getElementById("cv");
 var context = canvas.getContext("2d");
 balls  = [];

window.onload=function (){
    canvas.width = 800;
    canvas.height = 800; 

    CreateBalls();
    drawBall();
    canvas.addEventListener("mouseup",detect);   //部署鼠标事件mousemove,mousedown
}

function CreateBalls(){
    for(var i =0;i<20;i++)
    {
        var ABall = {
        x:Math.random()*canvas.width,
        y:Math.random()*canvas.height,
        radius:Math.random()*20+20,
        }
        balls[i] = ABall;
    }
}

function drawBall(){
    for(var i =0;i <balls.length;i++)
    {
        context.beginPath();
        context.fillStyle = "#058";
        context.arc(balls[i].x,balls[i].y,balls[i].radius,0,2*Math.PI);
        context.fill();
    }
}

function detect(event){
    var x = event.clientX - canvas.getBoundingClientRect().left;  //获取鼠标点击在画布上的位置
    var y = event.clientY - canvas.getBoundingClientRect().top;
    
    for(var i = 0;i<balls.length;i++)
    {
        context.beginPath();
        context.arc(balls[i].x,balls[i].y,balls[i].radius,0,2*Math.PI);

        if(context.isPointInPath(x,y))  //判断(x,y)是否在所绘制的图形内部
        {
            context.fillStyle = "red";
            context.fill();
        }
    }
}
````

#### 在Canvas上使用HTML其他元素

1、Canvas标签内部的内容只有在Canvas无效时才能看见

2、使用绝对定位将一个新的div至于Canvas之上，在新的div中布置HTML元素

#### 扩充Canvas函数方法

增加一个方法

```javascript
CanvasRenderingContext2D.prototype.fillStar = function (r,R,x,y,rot)
{
    this.beginPath();
    for(var i =0;i<5;i++)
    {
        this.lineTo(Math.cos((18+i*72-rot)/180*Math.PI)*R+x,
                    -Math.sin((18+i*72-rot)/180*Math.PI)*R+y);
        this.lineTo(Math.cos((54+i*72-rot)/180*Math.PI)*r+x,
                    -Math.sin((54+i*72-rot)/180*Math.PI)*r+y);
    }
    this.closePath();
    this.fill();
}
```

复写一个方法（不推荐），增加一个属性

```javascript
var canvas = document.getElementById("canvas");
var context = canvas.getContext('2d');
var originalMoveTo = CanvasRenderingContext2D.prototype.moveTo;
CanvasRenderingContext2D.prototype.lastMoveToLoc = {};  //增加的新属性
CanvasRenderingContext2D.prototype.moveTo = function(x,y){
    originalMoveTo.apply(context,[x,y]);
    this.lastMoveToLoc.x = x;
    this.lastMoveToLoc.y = y;
} 
```

#### Canvas兼容

1、IE6,7,8可以添加explorecanvas库来兼容。

#### Canvas图形库

1、[canvasplus](https://code.google.com/archive/p/canvasplus)

2、[Artisan JS](https://northwardcompass.com/artisanjs-a-generative-art-and-canvas-extension/)

3、[Rgraph:图表图形库](https://www.rgraph.net/)

## 实例

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
    
    //绘制圆弧
    context.lineWidth = 5;
    context.strokeStyle  ="#005588";
    context.arc(300,300,200,0,0.5*Math.PI,true);
    context.stroke();
}
```



#### 如何绘制两个不同的线条

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



#### 绘制七巧板

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



#### 简单的球体掉落

```javascript
var ball = {x:512,y:100,r:20,g:2,vx:-4,vy:-10,color:"#005588"};
window.onload=function(){
    var canvas = document.getElementById("cv");
    canvas.width = 1024;
    canvas.height = 768;
    var context = canvas.getContext("2d");
    setInterval(
        function(){
            render(context);
            update();
        },20 //50ms执行一次，所以帧率是20
    );
};
function update (){
    ball.x+=ball.vx;
    ball.y+=ball.vy;
    ball.vy+=ball.g;
    if(ball.y>=768-ball.r)
    {
        ball.y = 768-ball.r;
        ball.vy = -ball.vy*0.5;  //0.5的摩擦系数
    }
}
function render(cxt){
    cxt.clearRect(0,0,cxt.canvas.width,cxt.canvas.height);
    cxt.fillStyle = ball.color;
    cxt.beginPath();
    cxt.arc(ball.x,ball.y,ball.r,0,2*Math.PI);
    cxt.fill();
}
```

#### 五角星

```javascript
function drawStar(cxt,x,y,R,rot)
{
    cxt.save();

    cxt.translate(x,y);
    cxt.rotate(rot/180*Math.PI);
    cxt.scale(R,R);
    starPath(cxt);

    cxt.fillStyle = "#fb3";
    //cxt.strokeStyle = "#fd5";
    //cxt.lineWidth = 3;  // scale()方法会影响该属性
    cxt.lineJoin = "round";
    cxt.fill();
    //cxt.stroke();

    cxt.restore();
}

function starPath(cxt)  //标准五角星
{
    cxt.beginPath();
    for(var i =0;i<5;i++)
    {
        cxt.lineTo(Math.cos((18+i*72)/180*Math.PI),
                   -Math.sin((18+i*72)/180*Math.PI));
        cxt.lineTo(Math.cos((54+i*72)/180*Math.PI)*0.5,
                   -Math.sin((54+i*72)/180*Math.PI)*0.5);
    }
    cxt.closePath();
}
```

**渐变色**

```javascript
var grd = context.createLinearGradient(0,0,800,800);
grd.addColorStop(0.0,"#f00");
grd.addColorStop(0.5,"#0f0");
grd.addColorStop(1.0,"#00f");
context.fillStyle = grd;
context.fillRect(0,0,800,600);
```

#### 图片填充

```javascript
var backgroundImage = new Image;
backgroundImage.src = "" ;
backgroundImage.onload=function(){
	var pattern = context.createPattern(backgroundImage,"no-repeat"); 
    context.fillStyle = pattern;
    context.fill(0,0,,widht,height);
}
```

### 参考文档

1、[Canvas,W3C标准](https://www.w3.org/TR/2dcontext/)

2、[WHATWG标准](https://html.spec.whatwg.org/)