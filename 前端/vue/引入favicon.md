[看这篇文章](https://segmentfault.com/q/1010000010239649)

```

// build/webpack.dev.conf.js

new HtmlWebpackPlugin({
    filename: 'index.html',
    template: 'index.html',
    inject: true,
    favicon: path.resolve('favicon.ico')   // 加上这个
})
```

favicon.ico 放在根目录下