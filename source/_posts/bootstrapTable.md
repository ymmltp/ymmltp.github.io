---
title: Bootstrap Table学习笔记
date: 2020-07-21 14:15:54
tags: 学无止境
---

## Bootstrap Table基础用法

##### 1、使用js注册一个bootstrap-table

```html
<table id="table"> </table> 
```

```javascript
$('#table').bootstrapTable('destroy').bootstrapTable({
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

data-[属性名称]

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
$('#table').bootstrapTable('destroy').bootstrapTable({
    url: 'Ashx/Select.ashx?type=equipmentHistory', //请求后台的URL（*）
    method/type: 'get',                      //请求方式（*）
    cache: false,                       //清除缓存
    queryParams: {                      //参数
        Department: $("#department-select").val(),
        Project: $("#project-select").val(),
        Line: $("#line-select").val(),
        Station: $("#station-select").val(),
    },
    ajaxOptions: {                      //传参ajax设置
        traditional: true,              //允许传递数组类型的参数
    },
    dataType: 'json',
    search: true,                       //开启搜索框
    visibleSearch: true,
    showSearchButton: true,
    showColumns: true,                  //可以自主选择显示哪些列
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
    showExport: function (row, index) { //增加\Helper\html资料\bootstrap-table-excel-export中的js文件，实现表格内容导出功能
        var sUserAgent = navigator.userAgent.toLowerCase();
        var bIsIpad = sUserAgent.match(/ipad/i) == "ipad";
        var bIsIphoneOs = sUserAgent.match(/iphone os/i) == "iphone os";
        var bIsMidp = sUserAgent.match(/midp/i) == "midp";
        var bIsUc7 = sUserAgent.match(/rv:1.2.3.4/i) == "rv:1.2.3.4";
        var bIsUc = sUserAgent.match(/ucweb/i) == "ucweb";
        var bIsAndroid = sUserAgent.match(/android/i) == "android";
        var bIsCE = sUserAgent.match(/windows ce/i) == "windows ce";
        var bIsWM = sUserAgent.match(/windows mobile/i) == "windows mobile";
        if (bIsIpad || bIsIphoneOs || bIsMidp || bIsUc7 || bIsUc || bIsAndroid || bIsCE || bIsWM) {
            return false;
        } else {
            return true;
        }
    },
    clickToSelect: true,                   //是否启用点击选中行
    exportDataType: "selected",            //导出内容的范围'basic', 'all', 'selected'.
    exportTypes: ['csv', 'excel', 'xlsx'], //导出类型
    exportOptions: {
        fileName: 'QN Report - ' + formatDate(new Date()), //文件名称设置
        worksheetName: 'Sheet1',           //表格工作区名称
        tableName: 'Laeq&Lex',
        excelstyles: ['background-color', 'color', 'font-size', 'font-weight'],
    },
    columns: [
    [{    //增加表头
            title: '已绑定的设备',
            colspan: 6,
            align: 'center',
            rowStyle: function (row, index) {
                return { css: { "color": "#888", "background-color":"white" } };
            }
        }
    ],[{
        checkbox: true
    }, {
        field: 'id',
        title: 'ID'
    }, {
        field: 'name',
        title: 'Name',
        align: 'center',    //文字水平居中
        valign: 'middle',   //文字垂直居中
        visible: false,     //该列不可见
    }, {
        field: 'root',
        title: 'Root'
    }，{
        field: 'option',
        title: 'Option',
        align: 'center',
        valign: 'middle',
        formatter: function (value, row, index) {    //自定义该列的样式
                return ['<button type="button" class="btn bad text-light" id="start">Start</button>'];           
        },
        events: {                                    //自定义功能
            "click #delete": function (e, value, row, index) {
                
                }
            }
    }]],
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
//方法2
$('#table').bootstrapTable('updateCell', {
    index: i,
    field: 'DRI',
    value: data.DisplayName,
}); //formatter中不支持ajax异步查询更换值，只能加载完table之后再使用updateCell方法。更新
```

##### 3、edit Table

插件 bootstrap-editable.js 和 bootstrap-table-editable.js

```javascript
<script src="~/Scripts/bootstrap-table.min.js"></script>
<script src="~/Scripts/bootstrap-editable.js"></script>
<script src="~/Scripts/bootstrap-table-editable.js"></script>

$("#table").bootstrapTable('destroy').bootstrapTable({
    cache: false,
    type: 'GET',
    url: '/User/QuerybyRange',
    queryParams: {
        NTID: $("#ntid-input").val(),
        EmployeeID: $("#epid-input").val(),
        Department: $("#departsele").val()[0] == null ? getCookie("epm-Department") == "ALL" ? null : getCookie("epm-Department") : $("#departsele").val(),
    },
    dataType: 'json',
    pagination: true,  //设置为 true 会在表格底部显示分页条。
    paginationLoop: false, //设置为 true 启用分页条无限循环的功能。
    pageSize: 10,//每页初始显示的条数
    pageList: [10, 15, 20],
    columns: [
        {
            field: 'Index',
            title: 'Index',
            formatter: function (value, row, index) {
                return index + 1;
            }
        }, {
            field: 'UserName',
            title: 'User Name'
        }, {
            field: 'EmployeeID',
            title: 'Employee ID'
        }, {
            field: 'NTID',
            title: 'NTID'
        }, {
            field: 'Department',
            title: 'Department'
        }, {
            field: 'Project',
            title: 'Project',
            editable: {
                title: 'Project',
                type: 'checklist',
                separator: ",",
                source: res[0],
                mode: 'inline',
                validate: function (value) {
                    if ($.trim(value) == '') return 'Value can not be empty.';
                }
            }
        }, {
            field: 'eMail',
            title: 'e-Mail'
        }, {
            field: 'PhoneNum',
            title: 'Phone'
        }, {
            field: 'role',
            title: 'Role',
            editable: {
                title: 'Role',
                type: 'select',
                separator: ",",
                source: res[1],
                mode: 'inline',
                validate: function (value) {
                    if ($.trim(value) == '') return 'Value can not be empty.';
                }
            }
        }, {
            field: 'Operate',
            title: 'Operate',
            events: operateEvents,
            formatter: function (value, row, index) {
                return ['<a href="#" id="delete">Delete</a>'];
            }
        }],
    onEditableSave: function (field, row, oldValue, $el) {
        console.log(field);
        var tmp = {
            id: row['id'],
            NTID: row['id'],
        }
        tmp[field] = field == 'Project' ?  row[field].join(',') : row[field];
        $.ajax({
            url: '/User/Edit',
            method: 'POST',
            data: tmp,
            success: function (data) {
                console.log(data);
            },
            error: function (err) {
                alert(err.responseText);
            },
            complete: function (res) {
                $("#table").bootstrapTable("refreshOptions", { url: "/User/QuerybyRange" });
            }
        })
    },
});
```

## 参考资料

1、[Bootstrap Table官网实例](https://www.bootstrap-table.com.cn/examples/options/table-height/)

2、[bootstrap-table父子表](https://www.cnblogs.com/landeanfen/p/4993979.html)

3、[在table内添加按钮](https://blog.csdn.net/qq_39215166/article/details/74452366?utm_medium=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase)