---
title: AJAX
date: 2020-08-19 16:32:24
tags: 学无止境
---

## ajax

### 1、ajax基本用法
```javascript
.ajaxSend( Event event, jqXHR jqXHR, PlainObject ajaxOptions)   //在ajax request发送前触发
.ajaxStart()       //when the first Ajax request begins
.ajaxSuccess(Event event, jqXHR jqXHR, PlainObject ajaxOptions, PlainObject data)     //whenever an Ajax request completes successfully
.ajaxComplete(Event event, jqXHR jqXHR, PlainObject ajaxOptions)  //ajax完成时触发
.ajaxError( Event event, jqXHR jqXHR, PlainObject ajaxSettings, String thrownError ) //ajax完成，但是返回码不是200时触发
.ajaxStop()  //when all Ajax requests have completed

```

```javascript
$.ajax({
    url: "https://www.e-pm.com.cn/api/user/Adduser",
    type: "POST/GET",         //jquery-1.9.0及之后改为method
    cache:false,              //只在Get方法中生效 It works by appending "_={timestamp}" to the GET parameters
    traditional: true,        //是否传递数组类型的参数
    crossDomain:false,         //是否跨域  crossDomain (default: false)
    asycn: true,             //是否异步  async (default: true)
    contentType: 'json',      //发送的文件类型 (default: 'application/x-www-form-urlencoded; charset=UTF-8')
    processData:true         //通过contentType的属性将data中的内容转义成string(default:true) If you want to send a DOMDocument, or other non-processed data, set this option to false.
    data:{},                  //传递的参数
    dataType:'json',          //服务器返回的文件类型（"xml","json"返回的数据不是json格式或者{}/null都会报错,"text","script"）
    converters:"* text",      //修改返回参数的类型 (default: {"* text": window.String, "text html": true, "text json": jQuery.parseJSON, "text xml": jQuery.parseXML})
    dataFilter:Function( String data, String type ){
        //data:服务器返回的参数，type:dataType中定义的参数
        //对返回值进行预处理，作用于Success之前,返回的结果共后续的方法使用
    },
    statusCode: {
        404: function() {
            alert( "page not found" );
        }
    }
    success:function(res,status,xhr){
    //success funciton
    },
    fail:function(err){
    //fail funcion
    },
    error:function(err,status,xhr){
        
    },
    complete:function( jqXHR jqXHR, String textStatus ){

    },
});


//ajaxSetup:ajax配置。此后，每一个ajax方法都将使用setup中的参数。
//ajax中的所有参数都可以配置到setup中，注意，该方法全局生效。
$.ajaxSetup({
  url: "/xmlhttp/",
  global: false,
  type: "POST"
});
$.ajax({ 
    // url not set here; uses /xmlhttp/
    data: myData 
});

```

### 2、ajax上传文件

```html
<img src="" id="eq-img" class="eq-img" />
<input type="file" id="eq-img-input" onchange="selectImage(this)" />
```

```javascript
function selectImage(file) {
    var item = file.files[0];
    var index = item.name.lastIndexOf(".")+1;
    var type = item.name.substring(index).toLowerCase();
    if (type !== "jpg" && type !== "png"){
        alert("只能上传jpg和png格式的图片！");
        return;
    }
    else{
        var HTMLimgID = $(file)[0].id.replace("-input", "");
        if (!file.files || !file.files[0]) {
            return;
        }
        var reader = new FileReader();
        reader.readAsDataURL(file.files[0]);
        reader.onload = function (evt) {
            document.getElementById(HTMLimgID).src = evt.target.result;  //在img中加载图片
            //把文件加载到form里，利用form上传
            var formData = new FormData();
            formData.append('name', file.files[0]);   //上传的应该是一个file对象，name是服务器端需要的对象名
            $.ajax({
                url: "https://www.e-pm.com.cn/api/image/SaveImages2",
                data: formData,
                type: "post",
                cache:false,
                contentType: false,
                processData: false,
                success: function (res) {
                    //success funciton
                },
                fail: function (err) {
                    //fail funcion
                }
            });
        }
    }
}
```



## 参考资料
1、[ajax库](https://api.jquery.com/category/ajax/)