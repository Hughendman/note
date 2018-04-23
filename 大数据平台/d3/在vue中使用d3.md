## [实例](https://github.com/Hughendman/risk)

## 安装

> npm install d3 --save-dev

## 使用

>  在项目中引入 import * as d3 from 'd3'

[这是一篇不错的文章](https://tyronetudehope.com/2016/12/13/composing-d3-visualizations-with-vuejs/)

> 以上方法全部不好使
在dist文件夹下面有一个webpack.base.conf.js文件，在module.exports下添加

```
plugins: [
    new webpack.ProvidePlugin({
      jQuery: "jquery",
      $: "jquery",
      d3: "d3"
    })
  ],

```

