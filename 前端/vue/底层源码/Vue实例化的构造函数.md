### 生命周期

> vue2.0的生命周期分为4主要个过程

> create。 创建---实例化Vue(new Vue) 时，会先进行create。

> mount。挂载---根据el, template, render方法等属性，会生成DOM，并添加到对应位置。

> update。更新---当数据发生变化后，更新DOM。

> destory。销毁---销毁时执行。

![vue的生命周期](https://images2015.cnblogs.com/blog/675289/201703/675289-20170310000248672-1522982858.png)

##### new vue()

> new的过程js做了那几步骤，创建一个新对象，将这个新对象的proto指向这个新的创建的对象，将构造函数的this指针指向这个新创建的对象

> new Vue的过程主要涉及到三个对象：vm、compiler、watcher。其中，vm表示Vue的具体对象；compiler负责将template解析为AST render方法；watcher用于观察数据变化，以实现数据变化后进行re-render。


##### 位置

> src\core\instance\index.js

> 里面的具体代码

```
import { initMixin } from './init'
import { stateMixin } from './state'
import { renderMixin } from './render'
import { eventsMixin } from './events'
import { lifecycleMixin } from './lifecycle'
import { warn } from '../util/index'

function Vue (options) {
  if (process.env.NODE_ENV !== 'production' &&
    !(this instanceof Vue)) {
    warn('Vue is a constructor and should be called with the `new` keyword')
  }
  this._init(options)
}

initMixin(Vue)
stateMixin(Vue)
eventsMixin(Vue)
lifecycleMixin(Vue)
renderMixin(Vue)

export default Vue

```

> 寻找init

```

Vue.prototype._init = function (options?: Object) {
    const vm: Component = this
    // a uid
    vm._uid = uid++
    // ...
```

> 这里写的是flow代码

[Vue 2.0 为什么选用 Flow 进行静态代码检查而不是直接使用 TypoScript](https://www.zhihu.com/question/46397274)