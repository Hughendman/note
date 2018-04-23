## 安装

> cnpm install less less-loader --save

> 在webpack.base.config.js在loaders里面加上


```

{

test: /\.less$/,

loader: "style-loader!css-loader!less-loader",

},
```