---
title: eCharts
date: 2022-03-08 17:04:22
tags: 学无止境
---


## eCharts

### 配置项

```javascript
option = {
  title: {            //坐标的title
    text: 'Stacked Line',
    subtext
  },
  tooltip: {
    trigger: 'item',  //悬浮提示框:"axis":显示该列所有数据;"item":显示当前悬浮对象的内容
    formatter:function(e){   //自定义显示内容
      if(e.data.value)
        return e.name+":"+e.data.value+":"+e.data.label;
      else
        return e.name+":"+e.value;
    }
  },
  legend: {   //图例/系列
    data: ['Email', 'Union Ads', 'Video Ads', 'Direct', 'Search Engine']
  },
  grid: { //可以使用数组，表示多个坐标轴
    left: '3%',
    right: '4%',
    bottom: '3%',
    width:'80%',
    height:'80%',
    containLabel: true,//是否将坐标轴包含在内
  },  
  toolbox: {
    feature: {
      saveAsImage: {}
    }
  },
  xAxis: {   //如果grid为多个坐标轴，也可以使用数组，增加{gridIndex: 0}属性，对每个坐标轴进行设置。
    type: 'category',
    boundaryGap: false,
    data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
  },
  yAxis: {   //同xAxis
    type: 'value'
  },
  series: [
    {
      name: 'Email',
      type: 'line',
      data: [{value:200,label:"hahahha"}, 132, 101, 134, 90, 230, 210]       //data中的内容可以是对象，但是值的属性一定要是Value,其他可以自定义一些属性。
    },
    {
      name: 'Union Ads',
      type: 'line',
      data: [220, 182, 190, 234, 290, 330, 310]
    },
    {
      name: 'Video Ads',
      type: 'line',

      data: [150, 232, 201, 154, 190, 330, 410]
    },
    {
      name: 'Direct',
      type: 'line',

      data: [320, 332, 301, 334, 390, 330, 320]
    },
    {
      name: 'Search Engine',
      type: 'line',
      data: [820, 932, 901, 934, 1290, 1330, 1320]
    }
  ]
};
```

### 使用数据集作为Data

```javascript
option = {
  dataset: [
    {
      dimensions: ['name', 'age', 'profession', 'score', 'date'],
      source: [
        ['Hannah Krause', 41, 'Engineer', 314, '2011-02-12'],
        ['Zhao Qian', 20, 'Teacher', 351, '2011-03-01'],
        ['Jasmin Krause ', 52, 'Musician', 287, '2011-02-14'],
        ['Li Lei', 37, 'Teacher', 219, '2011-02-18'],
        ['Karle Neumann', 25, 'Engineer', 253, '2011-04-02'],
        ['Adrian Groß', 19, 'Teacher', '-', '2011-01-16'],
        ['Mia Neumann', 71, 'Engineer', 165, '2011-03-19'],
        ['Böhm Fuchs', 36, 'Musician', 318, '2011-02-24'],
        ['Han Meimei', 67, 'Engineer', 366, '2011-03-12']
      ]
    },
    {
      transform: {
        type: 'sort',
        config: { dimension: 'age', order: 'desc' }
      }
    }
  ],
  xAxis: {
    type: 'category',
    axisLabel: { interval: 0, rotate: 30 }
  },
  yAxis: {},
  series:[ {
    type: 'bar',
    encode: { x: 'name', y: 'age' },
    datasetIndex: 1
  },
   {
    type: 'bar',
    encode: { x: 'name', y: 'score' },
    datasetIndex: 1
  }]
};
```

## 点击事件

自定义按钮

```javascript
toolbox: {
    feature: {
        myTool1: {
            show: true,
            title: '自定义扩展方法1',
            icon: 'path://M432.45,595.444c0,2.177-4.661,6.82-11.305,6.82c-6.475,0-11.306-4.567-11.306-6.82s4.852-6.812,11.306-6.812C427.841,588.632,432.452,593.191,432.45,595.444L432.45,595.444z M421.155,589.876c-3.009,0-5.448,2.495-5.448,5.572s2.439,5.572,5.448,5.572c3.01,0,5.449-2.495,5.449-5.572C426.604,592.371,424.165,589.876,421.155,589.876L421.155,589.876z M421.146,591.891c-1.916,0-3.47,1.589-3.47,3.549c0,1.959,1.554,3.548,3.47,3.548s3.469-1.589,3.469-3.548C424.614,593.479,423.062,591.891,421.146,591.891L421.146,591.891zM421.146,591.891',
            onclick: function (){
                alert('myToolHandler1')
            }
        },
        myTool2: {
            show: true,
            title: '自定义扩展方法',
            icon: 'image://https://echarts.apache.org/zh/images/favicon.png',
            onclick: function (){
                alert('myToolHandler2')
            }
        }
    }
}
```

自定义界面图形、文本……

```javascript
  graphic: [
    {
        type: 'image',
        right: 40,
        top: 20,
        style: {
            image: '/img/arrowleft.png',
        }, 
        invisible: false,                                       
        onclick: function () {
            if (dataFloor) {
                dataFloor -= 1;
            }
            myChart1.setOption(optionArray[dataFloor]);
        }
    }
  ]

```

## 参考文件

1、[echart官网](https://echarts.apache.org/examples/zh/index.html)
