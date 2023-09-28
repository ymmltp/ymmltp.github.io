---
title: Bootstrap Table学习笔记
date: 2020-07-21 14:15:54
tags: 学无止境
---

## Bootstrap Select

### 1、常见配置

```javascript
function:
全选：data-none-selected-text="All" data-actions-box="true"
是否支持多选：multiple
多选最多：data-max-options="5" 
是否支持查询：data-live-search="true"
下拉框显示的option个数：data-size="6"

```

当设置`multiple`时，`.val()`获取的是一个Array对象
```javascript 
<select id="machine-select" class="form-control selectpicker" title="Select Machine"  multiple data-size="6" data-live-search="true" data-max-options="5" ></select>
```

### 2、可输入自定义内容的搜索框

#### 2.1 安装插件：jquery-editable-select

```js
<script src="js/lib/jquery.min.js"></script>
<script src="js/lib/jquery-editable-select.js"></script>
<link href="css/bootstrap.css" rel="stylesheet">
<link href="css/jquery-editable-select.css" rel="stylesheet">

//配置可编辑属性

<div class="col-lg-5">
    <label for="ca-machine" class="form-label text-right">Machine:</label>
    <select class="form-control" id='ca-machine' >
        <option value=""></option>
        <option value="aa">aa</option>
        <option value="bb">bb</option>
        <option value="cc">cc</option>
        <option value="dd">dd</option>
        <option value="ee">ee</option>
    </select>
</div>
<script>
    $(document).ready(function(){
        $("#ca-machine").editableSelect({ filter: true });
    });           
</script>
```

#### 2.2 使用 select2 模组

```js
//正常向 select 元素添加 option 之后再设置 select2
$("#ca-machine").select2({
    tags: false, //不允许用户输入新的选项，只能选择已有的选项。设为True 则可以输入自定义的内容
    maximumInputLength: 40, //最大可输入长度
    minimumInputLength: 2, //至少输入 2 个字符之后才会开始搜索。
    minimumResultsForSearch: 10, //只有当下拉列表中的选项数量大于等于10个时，才会显示搜索框。
    placeholder: "请输入设备ID"
});
```

### 参考文件

[bootstrap-select Document](https://developer.snapappointments.com/bootstrap-select/examples/)