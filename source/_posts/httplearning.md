---
title: AJAX
date: 2020-08-19 16:32:24
tags: 学无止境
---

## ajax

### 1、ajax基本用法

```javascript
$.ajax({
    url: "https://www.e-pm.com.cn/api/user/Adduser",
    type: "POST/GET",
    asycn: false,       //是否同步
	contentType: “json”       //文件类型
	success:function(res){
	 	//success funciton
	},
	fail:function(err){
		//fail funcion
	}
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

