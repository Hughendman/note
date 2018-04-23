## 这是webpack的路径别名

> 这个文件在webpck.base.conf.js

```
resolve: {
    // 自动补全的扩展名
    extensions: ['.js', '.vue', '.json'],
    // 默认路径代理
    // 例如 import Vue from 'vue'，会自动到 'vue/dist/vue.common.js'中寻找
    alias: {
        '@': resolve('src'),
        '@config': resolve('config'),
        'vue$': 'vue/dist/vue.common.js'
    }
    //@代表的是引入模块时，可以使用@来代替/src目录
    //$vue表示必须精确匹配vue
}

```