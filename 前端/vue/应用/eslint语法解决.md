```
在webpack.base.conf.js里面删掉下面:

preLoaders: [
      {
        test: /\.vue$/,
        loader: 'eslint',
        include: projectRoot,
        exclude: [/node_modules/, /ignore_lib/]
      },
      {
        test: /\.js$/,
        loader: 'eslint',
        include: projectRoot,
        exclude: [/node_modules/, /ignore_lib/]
      }
    ]
```

```

删除以下代码就可以
{

    test: /\.(js|vue)$/,
    loader: 'eslint-loader',
    enforce: 'pre',
    include: [resolve('src'), resolve('test')],
    options: {
      formatter: require('eslint-friendly-formatter')
    }
```

> 然后需要重新编辑生效