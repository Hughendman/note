## 安装

> cnpm install echarts --save

## 引入在main.js中

> import echarts from 'echarts'

> Vue.prototype.$echarts = echarts 

## 使用请参考以下模式

```
<template>
  <div class="charts">
    <div id="myChart" :style="{width: '100%', height: '500px'}"></div>
  </div>
</template>

<script>
  import {bubble} from '../../assets/eCharts/bubble';
  export default {
    name: "bubble",
    mounted(){
      this.drawLine();
    },
    methods: {
      drawLine(){
        // 基于准备好的dom，初始化echarts实例
        let myChart = this.$echarts.init(document.getElementById('myChart'));
        // 绘制图表
        let option = bubble(JSON.parse(localStorage.getItem("data")));
        myChart.setOption(option);
      }
    }
  }
</script>

<style scoped>
  .charts {
    padding: 20px;
    position: relative;
  }
</style>

```
### 参数的配置

还需要引入一个option的配置文件


```
function bubble(data) {
  let rowLen = data.conf.row_n.length;
  //legend数据开始
  let legendData = data.head[0].map(function(col, i) {
    return data.head.map(function(row) {
      return row[i];
    })
  });
  legendData.forEach(function (item, index) {
    legendData[index] = item.join("-");
  });
  legendData = legendData.splice(rowLen,legendData.length-1);
  //legend数据完成；
  //x轴数据开始
  let xData = [];
  data.data.forEach(function (item, index) {
    xData.push(item.splice(0,rowLen).join("-"));
  });
  //x轴数据完成
  //渲染数据开始
  let seriesData = data.data[0].map(function(col, i) {
    return data.data.map(function(row) {
      return row[i];
    })
  });
  seriesData.forEach(function (item, index) {
    let obj = {
      name: legendData[index],
      type: 'scatter',
      data: item
    };
    seriesData[index] = obj;
  });
  //渲染数据完成
  let option = {
    title: {
      // text: '世界人口总量',
      // subtext: '数据来自网络'
    },
    toolbox: {
      show : true,
      x: 'right',
      y: 'top',
      orient: 'vertical',
      feature : {
        mark : {show: true},
        dataZoom: { //数据缩放视图
          show: true
        },
        dataView : {show: true, readOnly: false},
        magicType: {show: true, type: ['line', 'bar']},
        restore : {show: true},
        saveAsImage : {show: true}
      }
    },
    tooltip: {
      trigger: 'axis',
      axisPointer: {
        type: 'shadow'
      }
    },
    legend: {
      data: legendData
    },
    grid: {
      left: '1%',
      right: '7%',
      bottom: '3%',
      containLabel: true
    },
    yAxis: {
      type: 'value',
      boundaryGap: [0, 0.01]
    },
    xAxis: {
      type: 'category',
      data: xData
    },
    series: seriesData
  };
  return option;
}
export {
  bubble
}


```
