## 组件和属性

组件使你可以将UI划分为一个个独立可以复用的小部件，并可以对每个部件进行单独的设计。

从定义上来说，组件就像JavaScript的函数，组件可以接受任意输入（俗称props），并反回React元素，用以描述屏幕显示内容。

注释： Props，即属性（property），在代码中写作props，所以可以用props指代properties

### 函数式组件和类组件

简单的定义组件： JavaScript函数

```
function com (props){
    return <h1>Hello,{props.name}!!</h1>;
}

```

这个函数是一个有效的组件，它接收一个props参数，并返回一个React元素。这类组件叫函数式组件


也可以使用class，ng4使用的就是，给我的体感不是很好
我还是喜欢使用vue。

```
class Welcome extends React.Component {
    render(){
        return <h1>Hello,{this.props.name}</h1>；
    }
}

```

### 渲染一个组件

看下面的案例

```
function Welcome(props){
    return <h1>Hello,{props.name}</h1>;
}

const element = <Welcome name = 'Sara' />；

ReactDOM.render(
    element,
    document.getElementById('root')
);

```
上面这个和vue中的自定义组件类似,还有angularjs的自定义组件也是.

[vue组件注册](http://note.youdao.com/noteshare?id=8d96befba01b643769755be09de3687b&sub=392C52B15DF149E8A31C8DCC90B508A5)

[在vue中创建局部组件](http://note.youdao.com/noteshare?id=d8dbf51fe099fc4e24851b2e241eba0d&sub=C492B6263E364D4C823AA8153E8BE091)

[angularjs如何使用指令](http://note.youdao.com/noteshare?id=c9b643fddb0af140c4c7b8110fbb8da9&sub=02159A1E4E7448F98669423249467C45)

上面的代码解析：
 
 * 我们调用ReactDOM.render()方法并向其传入了<Welcome name = 'Sara' />元素
 * React调用Welcome组件，并向其传入{name: 'Sara'} 作为对象。
 * Welcome组件返回`<h1>Hello,Sara</h1>`
 * ReactDOM迅速更新更新DOM，使其为 `<h1>Hello,Sara</h1>`
 

注意： 组件名称总是以大写字母开始`<Welcome name = 'Sara' />`

### 构成组件

组件可以在它们的输出中引用其它组件，例如我们可以创建一个App组件，并可以在其内部多次渲染Welcome；

### props是只读的

这代表的是这种函数式纯函数。而react规定所有的react组件必须为纯函数，并禁止修改其自身的props。但是UI是动态的。所以我们使用state来动态的改变输出。



 