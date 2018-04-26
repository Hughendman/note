ECharts 提供了丰富的自定义配置选项，并且能够从全局、系列、数据三个层级去设置数据图形的样式。

## 绘制南丁格尔图

```
option = {
    backgroundColor: '#2c343c',
    visualMap: {
      show: false,
      min: 80,
      max: 600,
      inRange: {
        colorLightness: [0, 1]
      }
    },
    series : [
      {
        name: '访问来源',
        type: 'pie',
        radius: '55%',
        data:[
          {value:235, name:'视频广告'},
          {value:274, name:'联盟广告'},
          {value:310, name:'邮件营销'},
          {value:335, name:'直接访问'},
          {value:400, name:'搜索引擎'}
        ],
        roseType: 'angle',
        label: {
          normal: {
            textStyle: {
              color: 'rgba(255, 255, 255, 0.3)'
            }
          }
        },
        labelLine: {
          normal: {
            lineStyle: {
              color: 'rgba(255, 255, 255, 0.3)'
            }
          }
        },
        itemStyle: {
          normal: {
            color: '#c23531',
            shadowBlur: 200,
            shadowColor: 'rgba(0, 0, 0, 0.5)'
          }
        }
      }
    ]
  };

```