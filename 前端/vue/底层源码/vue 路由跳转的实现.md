> 前端路由是直接找到与地址匹配的一个组件或对象并将其渲染出来

## 改变浏览器地址而不向服务器发出请求的方法

> 在地址中加入#以欺骗浏览器，地址的改变是由于正在进行页内导航
> 使用H5的window.history功能，使用url的Hash来模拟一个完整的url

当打包构建应用时，js包会变得非常的大，影响页面加载，如果我们能把不同路由对应的组件分割成不同的代码块，然后当路由被访问的时候才加载对应组件，这样更加高效

![component](https://raw.githubusercontent.com/Hughendman/picture/master/%E5%89%8D%E7%AB%AF%E7%9F%A5%E8%AF%86%E6%A6%82%E5%86%B5/vue/router.png)

在vue中.use(plugin)用来安装插件，vue-router就是这样一种使用的插件，VueRouter 对象是在 src/index.js 中暴露出来的，这个对象有一个静态的 install 方法：

```
/* @flow */
// 导入 install 模块
import { install } from './install'
// ...
import { inBrowser, supportsHistory } from './util/dom'
// ...

export default class VueRouter {
// ...
}

// 赋值 install
VueRouter.install = install

// 自动使用插件
if (inBrowser && window.Vue) {
  window.Vue.use(VueRouter)
}

```

可以看到这是一个 Vue.js 插件的经典写法，给插件对象增加 install 方法用来安装插件具体逻辑，同时在最后判断下如果是在浏览器环境且存在 window.Vue 的话就会自动使用插件。

```
// router-view router-link 组件
import View from './components/view'
import Link from './components/link'

// export 一个 Vue 引用
export let _Vue

// 安装函数
export function install (Vue) {
  if (install.installed) return
  install.installed = true

  // 赋值私有 Vue 引用
  _Vue = Vue

  // 注入 $router $route
  Object.defineProperty(Vue.prototype, '$router', {
    get () { return this.$root._router }
  })

  Object.defineProperty(Vue.prototype, '$route', {
    get () { return this.$root._route }
  })
  // beforeCreate mixin
  Vue.mixin({
    beforeCreate () {
      // 判断是否有 router
      if (this.$options.router) {
        // 赋值 _router
        this._router = this.$options.router
        // 初始化 init
        this._router.init(this)
        // 定义响应式的 _route 对象
        Vue.util.defineReactive(this, '_route', this._router.history.current)
      }
    }
  })

  // 注册组件
  Vue.component('router-view', View)
  Vue.component('router-link', Link)
// ...
}

```

* 在 Vue.js 中所有的组件都是被扩展的 Vue 实例，也就意味着所有的组件都可以访问到这个实例原型上定义的属性。
* 

## 实例化 VueRouter
> 在入口文件中，首先要实例化一个 VueRouter ，然后将其传入 Vue 实例的 options 中。现在继续来看在 src/index.js 中暴露出来的 VueRouter 类：

```
// ...
import { createMatcher } from './create-matcher'
// ...
export default class VueRouter {
// ...
  constructor (options: RouterOptions = {}) {
    this.app = null
    this.options = options
    this.beforeHooks = []
    this.afterHooks = []
    // 创建 match 匹配函数
    this.match = createMatcher(options.routes || [])
    // 根据 mode 实例化具体的 History
    let mode = options.mode || 'hash'
    this.fallback = mode === 'history' && !supportsHistory
    if (this.fallback) {
      mode = 'hash'
    }
    if (!inBrowser) {
      mode = 'abstract'
    }
    this.mode = mode

    switch (mode) {
      case 'history':
        this.history = new HTML5History(this, options.base)
        break
      case 'hash':
        this.history = new HashHistory(this, options.base, this.fallback)
        break
      case 'abstract':
        this.history = new AbstractHistory(this)
        break
      default:
        assert(false, `invalid mode: ${mode}`)
    }
  }
// ...
}
```

#### 里边包含了重要的一步：创建 match 匹配函数。 
## match 匹配函数 
> 匹配函数是由 src/create-matcher.js 中的 createMatcher 创建的：

```
/* @flow */

import Regexp from 'path-to-regexp'
// ...
import { createRouteMap } from './create-route-map'
// ...

export function createMatcher (routes: Array<RouteConfig>): Matcher {
  // 创建路由 map
  const { pathMap, nameMap } = createRouteMap(routes)
  // 匹配函数
  function match (
    raw: RawLocation,
    currentRoute?: Route,
    redirectedFrom?: Location
  ): Route {
// ...
  }

  function redirect (
    record: RouteRecord,
    location: Location
  ): Route {
// ...
  }

  function alias (
    record: RouteRecord,
    location: Location,
    matchAs: string
  ): Route {
// ...
  }

  function _createRoute (
    record: ?RouteRecord,
    location: Location,
    redirectedFrom?: Location
  ): Route {
    if (record && record.redirect) {
      return redirect(record, redirectedFrom || location)
    }
    if (record && record.matchAs) {
      return alias(record, location, record.matchAs)
    }
    return createRoute(record, location, redirectedFrom)
  }
  // 返回
  return match
}
// ...

```

### src/create-route-map.js 中的 createRouteMap 函数

```
/* @flow */

import { assert, warn } from './util/warn'
import { cleanPath } from './util/path'

// 创建路由 map
export function createRouteMap (routes: Array<RouteConfig>): {
  pathMap: Dictionary<RouteRecord>,
  nameMap: Dictionary<RouteRecord>
} {
  // path 路由 map
  const pathMap: Dictionary<RouteRecord> = Object.create(null)
  // name 路由 map
  const nameMap: Dictionary<RouteRecord> = Object.create(null)
  // 遍历路由配置对象 增加 路由记录
  routes.forEach(route => {
    addRouteRecord(pathMap, nameMap, route)
  })

  return {
    pathMap,
    nameMap
  }
}

// 增加 路由记录 函数
function addRouteRecord (
  pathMap: Dictionary<RouteRecord>,
  nameMap: Dictionary<RouteRecord>,
  route: RouteConfig,
  parent?: RouteRecord,
  matchAs?: string
) {
  // 获取 path 、name
  const { path, name } = route
  assert(path != null, `"path" is required in a route configuration.`)
  // 路由记录 对象
  const record: RouteRecord = {
    path: normalizePath(path, parent),
    components: route.components || { default: route.component },
    instances: {},
    name,
    parent,
    matchAs,
    redirect: route.redirect,
    beforeEnter: route.beforeEnter,
    meta: route.meta || {}
  }
  // 嵌套子路由 则递归增加 记录
  if (route.children) {
// ...
    route.children.forEach(child => {
      addRouteRecord(pathMap, nameMap, child, record)
    })
  }
  // 处理别名 alias 逻辑 增加对应的 记录
  if (route.alias !== undefined) {
    if (Array.isArray(route.alias)) {
      route.alias.forEach(alias => {
        addRouteRecord(pathMap, nameMap, { path: alias }, parent, record.path)
      })
    } else {
      addRouteRecord(pathMap, nameMap, { path: route.alias }, parent, record.path)
    }
  }
  // 更新 path map
  pathMap[record.path] = record
  // 更新 name map
  if (name) {
    if (!nameMap[name]) {
      nameMap[name] = record
    } else {
      warn(false, `Duplicate named routes definition: { name: "${name}", path: "${record.path}" }`)
    }
  }
}

function normalizePath (path: string, parent?: RouteRecord): string {
  path = path.replace(/\/$/, '')
  if (path[0] === '/') return path
  if (parent == null) return path
  return cleanPath(`${parent.path}/${path}`)
}
```

> 可以看出主要做的事情就是根据用户路由配置对象生成普通的根据 path 来对应的路由记录以及根据 name 来对应的路由记录的 map，方便后续匹配对应。

### 实例化 History 

> 这也是很重要的一步，所有的 History 类都是在 src/history/ 目录下，现在呢不需要关心具体的每种 History 的具体实现上差异，只需要知道他们都是继承自 src/history/base.js 中的 History 类的：

```
/* @flow */

// ...
import { inBrowser } from '../util/dom'
import { runQueue } from '../util/async'
import { START, isSameRoute } from '../util/route'
// 这里从之前分析过的 install.js 中 export _Vue
import { _Vue } from '../install'

export class History {
// ...
  constructor (router: VueRouter, base: ?string) {
    this.router = router
    this.base = normalizeBase(base)
    // start with a route object that stands for "nowhere"
    this.current = START
    this.pending = null
  }
// ...
}

// 得到 base 值
function normalizeBase (base: ?string): string {
  if (!base) {
    if (inBrowser) {
      // respect <base> tag
      const baseEl = document.querySelector('base')
      base = baseEl ? baseEl.getAttribute('href') : '/'
    } else {
      base = '/'
    }
  }
  // make sure there's the starting slash
  if (base.charAt(0) !== '/') {
    base = '/' + base
  }
  // remove trailing slash
  return base.replace(/\/$/, '')
}
// ...

```

[参考](http://blog.csdn.net/caoxinhui521/article/details/77688512)