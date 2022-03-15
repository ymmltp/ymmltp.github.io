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
    text: 'Stacked Line'
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
