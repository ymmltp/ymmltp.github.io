---
title: javascript
date: 2020-08-20 09:39:35
tags: 学无止境
---

### 基础知识javascript原生方法

1、判断数组是否包含某个元素：indexOf
2、添加Dom元素

```javascript
  function showmessage(msg){
    var log = document.getElementById('logdebug');
    if(!log){
        var log = document.createElement('div');
        log.id='logdebug';
        log.innerHTML='<h2>Log Debug</h2>';
        document.body.appendChild(log);
    }
    var pre = document.createElement('pre');
    var text = document.createTextNode(msg);
    pre.appendChild(text);
    log.appendChild(pre);
}
```

3、给元素添加属性

```javascript
//添加原始属性
dom.style.display = 'none';
dom.style.visiblity = 'hidden';
//添加自定义css样式
if(!dom.className) dom.className = 'mystyle';
else dom.className += 'mystyle';
```

4、给元素注册事件

```javascript
if(image.addEventListener)
    image.addEventListener('click',myfunction,params);
else
    image.attachEvent('click',myfunction);  //兼容IE8及之前的版本
```

### jQuery以及一些新的方法

#### 注册jQuery对象

```javascript
//一个参数
$('#elementID')   //返回id为elementID  一个元素
$('.elementCSS')  //返回class为elementID  一组元素
$('input :text')  //返回类型为text的  一组input元素
$("ul li:first")  //ul中的第一个li
$("[href$='.jpg']")  //所有带有以 ".jpg" 结尾的属性值的 href 属性

//两个参数
$('<img/>',       //创建一个img元素，并附带这些属性
{
    src:url,
    css:{'border': 'blue solid 15px'},   
    text:,
    val:,
    html:,
    width:,
    height:,
    offset:,
    data:, 
    click:myfunction(),
})
$('.elementCSS',document.body) //查询出document.body中所有css='elementCSS'的元素。
```

#### 函数与方法

jq中通常函数和方法都是成对出现的，用法参考each

|方法|描述|
|--|--|
|$.each(myele,f1)|each函数：对ele中的每个元素都调用一次f1方法|
|$myele.each(f1(index));|each方法：作用同上,在方法中可以直接使用$(this)表示当前对象，或者使用第二个参数|
|**forEach()与each()的区别**|each()的遍历，如果有一个元素返回false,则结束遍历,forEach不会;each()类似于Promise,可用于链式调用|
|$myele.map(f1(index,this))|作用同上,返回一组对象作为方法运行的结果|
|**each,foreach,map的差别和使用场景**|--|
|$myele.width()|设置和获取对象的宽度|
|$myele.height()|设置和获取对象的高度|
|$myele.scrollTop()|设置和获取竖向滚动条的位置，**不接受函数作为参数**|
|$myele.scrollLeft()|设置和获取横向滚动条的位置，**不接受函数作为参数**|
|$myele.data('mydata')|获取 ```<div data-mydata="我的数据"></div>```中的data标签的值，第一个参数，指定data的对象**不接受函数作为参数**；设置第二个参数可以给该对象赋值|
|$myele.reomveData('x')|移除 ```<div data-x="我的数据"></div>```中的data-x标签，不赋值则移除所有data标签|

#### 插入和替换

当插入的对象已经是页面中的一部分时，此时如果只插入一个位置，那么会直接移动这个对象，而不会执行复制并添加的动作，执行复制动作，```$('追加的内容').clone().appendTo($myele)```
|方法|描述|
|--|--|
|$myele.append('追加的内容')|在对象内，尾部 追加内容;对调主宾的用法：appendTo|
|$myele.prepend('追加的内容')|在对象内，头部 追加内容;对调主宾的用法：prependTo|
|$myele.before('追加的内容')|在对象外，前面 追加内容;对调主宾的用法：insertBefore|
|$myele.after('追加的内容')|在对象外，后面 追加内容;对调主宾的用法：insertAfter|
|$('hr').replaceWith('```<br/>```')|将```'<hr/>'```替换成```<br/>```;对调主宾的用法：replaceAll|

#### 删除元素

|方法|描述|
|--|--|
|$myele.empty()|删除元素内部的所有子节点|
|$myele.remove()|删除元素本身以及内部的所有子节点，包括绑定在元素上的事件处理程序和数据|
|$myele.detach|类似remove()，但不移除事件处理程序和数据|
|filter()|从选择器中进行筛选，而不会在界面上进行处理|

#### 事件处理方法

<b style="color:red">注意：某些方法，在文档树上会向上冒泡</b>

|方法|描述|
|--|--|
|blur()|**不支持冒泡**|
|click()||
|change()||
|dbclick()||
|error()||
|focus()|**不支持冒泡**|
|focusin()|**支持冒泡**|
|focusout()|**支持冒泡**|
|keydown()||
|keypress()||
|keyup()||
|load()||
|mousedown()||
|mouseenter()||
|mouseleave()||
|mousemove()||
|mouseout()||
|mouseover()||
|mouseup()||
|resize()||
|scroll()||
|select()||
|submit()||
|unload()||

#### js原生变成jq对象

```javascript
function showmessage(msg){
    var log = document.getElementById('logdebug');
    if(!log){
        var log = document.createElement('div');
        log.id='logdebug';
        log.innerHTML='<h2>Log Debug</h2>';
        document.body.appendChild(log);
    }
    var pre = document.createElement('pre');
    var text = document.createTextNode(msg);
    var img = $('<input/>',       //创建一个img元素，并附带这些属性
    {
        value:"hahaha",
        src:'mypic.png',
        css:{'border': 'blue solid 15px'},                   
    })
    //用$()将js对象变成jquery对象
    $(pre).append(text);
    $(pre).append(img);
    $(log).append(pre);
}
```

### 知识提升

1、a标签不跳转
2、js直接给input元素赋值不能触发onchange事件：

```javascript
使用trigger方法，手动触发
 $("input").trigger("focus");  //触发focus的事件，也实际执行了focus方法，input获得焦点
 $("input").triggerHandler( "focus" );  //触发focus的事件，不执行focus方法，input不获得焦点
 ```

### 参考资料

[1、const,var,let的区别](https://www.cnblogs.com/zhaoxiaoying/p/9031890.html)
