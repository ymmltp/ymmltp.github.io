---
title: Bootstrap Table学习笔记
date: 2020-07-21 14:15:54
tags:学无止境
---

## Bootstrap Table基础用法

##### 1、使用js注册一个bootstrap-table

```html
<table id="table"> </table> 
```

```javascript
$('#table').bootstrapTable({
    columns: [{
        field: 'id',
        title: 'ID'
    }, {
        field: 'name',
        title: 'Name'
    }, {
        field: 'root',
        title: 'Root'
    }],
    data[{
    	id:"1",
    	name:"Jack",
    	root:"User"
	},{
    	id:"2",
    	name:"Emily",
    	root:"Admin"
	}]
});
```

##### 2、html注册bootstrap-table

```html
<table
  data-toggle="table"
  data-url="data1.json">
  <thead>
    <tr>
      <th data-field="id">ID</th>
      <th data-field="name">Name</th>
      <th data-field="root">Root</th>
    </tr>
  </thead>
</table>
```



## Bootstrap Table其他功能

（参考官网文档）

##### 1、使用html开启相关功能

​	data-[属性名称]

```html
<table
  data-toggle="table"
  data-url="data1.json"  
  data-pagination="true"
  data-search="true"
  data-sortable="true">
</table>
```

##### 2、使用js配置相关功能

```javascript
//初始化主表格
$('#table').bootstrapTable({
    url: 'Ashx/Select.ashx?type=equipmentHistory', //请求后台的URL（*）
    method: 'get',                      //请求方式（*）
    search: true,                       //开启搜索框
    striped: true,                      //是否显示行间隔
    sortable: true,                     //是否启用排序
    sortName: 'id',
    sortOrder: "desc",                  //排序方式
    queryParams: oTableInit.queryParams,//传递参数（*）
    sidePagination: "client",           //分页方式：client客户端分页，server服务端分页（*）
    pageNumber: 1,                      //初始化加载第一页，默认第一页
    pageSize: 10,                       //每页的记录行数（*）
    pageList: [10, 25, 50, 100],        //可供选择的每页的行数（*）
    height: 500,                        //行高，如果没有设置height属性，表格自动根据记录条数觉得表格高度  
    detailView: true,                   //显示详情，左侧加号
    detailFormatter:"detailFormatter",  //通过detailFormatter()修改详情内容
    columns: [{
        checkbox: true
    }, 
        field: 'id',
        title: 'ID'
    }, {
        field: 'name',
        title: 'Name'
    }, {
        field: 'root',
        title: 'Root'
    }],
     //注册加载子表的事件。注意下这里的三个参数！需要设置detailView:true
     onExpandRow: function (index, row, $detail) {
         InitSubTable(index, row, $detail);
     }
});

//设置详情内容
function detailFormatter(index, row) {
    var html = []
    $.each(row, function (key, value) {
        html.push('<p><b>' + key + ':</b> ' + value + '</p>')
    });
    return html.join('');
}

//初始化子表格
function InitSubTable (index, row, $detail) {
    var eqid = row.idEquipment;
    var cur_table = $detail.html('<table class="tablewhite"></table>').find('table');
    $(cur_table).bootstrapTable({
        url: 'Ashx/Select.ashx?type=equipmentPMInfo&eqID='+eqid,
        rowStyle:"rowStyleChild",  //通过rowStyleChild()根据数据修改行的样式
        columns:[  {
            field: 'PMCategory',
            title: 'PM Type'
        }, {
            field: 'AlarmDate',
            title: 'Alarm Date',
            formatter: function (value, row, index) {
                return changeDateFormat(value)  //通过changeDateFormat()修改时间格式
            }
        }, {
            field: 'PmResult',
            title: 'Pm Result'
        }],
    });
};

//根据条件修改行样式
function rowStyleChild(row, index) {
    var style = {};     
    if (row.PmResult !== "PASS") {
        style={css:{'color':'#d9534f'}};    
    }           
    return style;
}

//修改时间格式
function changeDateFormat(cellval) {
    if (cellval != null) {
        var d = new Date(cellval);
        var times = d.getFullYear() + '-' + (d.getMonth() + 1) + '-' + d.getDate();
        return times;
    } else {
        return cellval;
    }
}
```

##### 2、js 动态加载数据

```javascript
//方法1
var url = ""; //动态修改url的值
$('#table').bootstrapTable('refresh', { 'url': url });//注意：url返回值应为json格式
//方法2
$('#table').bootstrapTable('load', data); //注意：此处的data应为json格式，且key值和column的field名相对应
```

## 参考资料

1、[Bootstrap Table官网实例](https://www.bootstrap-table.com.cn/examples/options/table-height/)

2、[bootstrap-table父子表](https://www.cnblogs.com/landeanfen/p/4993979.html)

