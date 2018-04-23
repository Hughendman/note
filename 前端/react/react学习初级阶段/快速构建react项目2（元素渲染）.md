## 元素渲染

元素是React应用中最小的构建部件（构建块）
不同于浏览器的DOM元素，React元素是普通的对象，非常容易创建。React DOM会负责新的DOM，以匹配React元素（DOM元素和Ract元素保持一致）

注意：不要把元素和组件搞混

### 渲染一个元素到DOM

单纯的用React构建应用程序通常只有一个单独的根DOM节点，但是如果把react整合进现有的app中，那你可能会有多个相互独立的root DOM节点。

要渲染一个React元素到一个root DOM节点，我们需要把它传递给ReactDOM.render()方法；

```
const element = <h1> Hello,yinxs </h1>;

ReactDOM.render(
    element,
    document.getElementById('root')
)

```
### 更新已渲染的元素

React 元素是 不可突变的，一旦你创建了一个元素，就不能在修改其子元素或任何属性，一个元素表示一个特定时间点的UI。

实际上，大多说react应用只会调用ReactDOM.render()一次

### React只更新必须要更新的部分

ReactDOM 会将元素及其子元素与之前版本逐一对比，并只对有必要更新的DOM进行更新，以达到DOM所需的状态。
