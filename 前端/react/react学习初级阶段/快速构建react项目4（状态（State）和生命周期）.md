## state

state 和 props类似，但是它是私有的并且由组件本身完全控制。用类定义的组件有一些额外的特性。这个类专有的特性指的就是局部状态。

### 把函数式组件转换成类组件

可以遵循以下五部

* 创建一个继承自React.Component 类的ES6 class同名类。
* 添加一个名为render()的空方法
* 把原函数中的所以内容移至render()中
* 在render() 方法中使用this.props代替props
* 删除保留的空函数声明


```

class Clock extends React.Component {
    render(){
        return {
            <div>
                <h1>Hello , yinxs</h1>
                <h2>It is {this.props.date.toLocaleTimeString()}</h2>
            </div>
        }
    }
}

```

现在Clock被定义为类组件，而不是函数式组件
类允许我们在其中添加本地状态（state）和生命周期构子。


### 在类组件中添加本地状态

把date从属性（props）改为状态（state）；

1、替换render()方法中的this.props.date为this.state.date；

```
class Clock extends React.Component {
    render(){
        return {
            <div>
                <h1>Hello,yinxs</h1>
                <h2>It is {this.state.date.toLocaleTimeString}</h2>
            </div>
        }
    }
}

```

2、添加一个类构造函数（class constructor）初始化this.state

```
class Clock extends React.Component {
    constructor(props){
        super(props);
        this.state = {date: new Date()};
    }
    render(){
        return {
            <div>
                <h1>Hello,yinxs</h1>
                <h2>It is {this.state.date.toLocaleTimeString)</h2>
            </div>
        }
    }
}

```

注意我们如何将props传递给基础构造函数

```
constructor(props){
    super(props);
    this.state = {date:new Date()};
}

```

类组件应始终使用props调用基础构造函数

3、移除<Clock/>元素中的date属性

```
ReactDOM.render(
    <Clock/>,
    document.getElementById('root')
);

```

现在整合的代码如下

```
class Clock extends React.Component {
    constructor(props){
        super(props);
        this.state = {date:new Date()};
    }
    render() {
        return {
            <div>
                <h1>Hello,yinxs</h1>
                <h2>It is {this.state.date.toLocaleTimeString}</h2>
            </div>
        }
    }
}

ReactDOM.render(
    <Clock/>,
    document.getElementById('root');
);
```
### 在类中添加生命周期方法

在一个具有许多组价的应用程序中，在组件被销毁时释放所占用的资源是非常重要的。
当Clock第一次渲染到DOM时，我们要设置一个定时器，这在React中称为挂载（mounting）
当Clcok产生的DOM被销毁时，我们也想清除计时器，这在React中称为卸载（unmounting）

当组件挂载和卸载时，我们可以在组件类上声明特殊的方法运行一些代码

```
class Clock extends React.Component {
    constructor(props){
        super(props);
        this.state = {date:new Date()};
    }
    
    componentDidMount(){
        
    }
    
    componentWillUnmount(){
        
    }
    
    
    
    render() {
        return {
            <div>
                <h1>Hello,yinxs</h1>
                <h2>It is {this.state.date.toLocaleTimeString}</h2>
            </div>
        }
    }
}

```

这些方法叫声明周期构子。ng，vue，ember就react的周期名字感觉最难打出来。

componentDidMount()构子在组件输出被渲染到DOM之后运行。


```
componentDidMount (){
    this.timeID = setInterval(
        () => this.tick(),
        1000
    );
}


```

最后我们将实现每秒运行tick()方法
它将使用this.setState()来周期性地更新组件本地状态

```
class Clock extends React.Component {
    constructor(props){
        super(props);
        this.state = {date:new Date()};
    }
    
    componentDidMount (){
        this.timeID = setInterval(
            () => this.tick(),
            1000
        );
    }
    
    componentWillUnmount(){
        clearInterval(this.timerID);
    }
    
    tick(){
        this.setState({date:new Date()})
    }
    
    render() {
        return {
            <div>
                <h1>Hello,yinxs</h1>
                <h2>It is {this.state.date.toLocaleTimeString}</h2>
            </div>
        }
    }
}

```

### 正确地使用State（状态）

关于setState()：


第一，不要直接修改state（状态）

要用setState()代替

```
this.state.comment = 'yinxs'//错误代码

this.setState({'comment':'yinxs'})//正确代码

```
唯一可以分配this.state的地方是构造函数。



第二，state（状态）更新可能是异步的
要想解决这个问题，需要使用如下方式

```
this.setState((prevState,props) => ({
    counter: prevState.counter + props.increment
}));

```
也可以这么使用

```
this.setState(function(prevDate,props){
   return {
        counter: prevState.counter + props.increment
       
   }
});

```

第三，state更新会被合并

当你调用setState()，React将会合并你提供的对象到当前的状态中。

```
constructor(props){
    super(props);
    this.state = {
        posts: []，
        comments: []
    };
}

```
然后通过调用独立的setState()调用分辨更新它们

```
componentDidMount(){
    fetchPosts().then(response => {
        this.setState({posts: response.posts});
    });
    
    fetchComments().then(response => {
        this.setState({comments: response.posts});
    });
}


```
合并是浅合并，所以this.setState({commnets})不会改变this.state.posts的值，但会完全替换this.state.comments的值

### 数据向下流动

无论作为父组件还是子组件，它都无法获悉一个组件是否有状态，同时也不需要关心另一个组件是定义为函数组件还是类组件。

一个组件可以选择将state向下传递，作为其子组件的props

```
<h2>It is {this.state.date.toLocaleTimeString()}</h2>


```

同样适用于自定义组件

 ```
 <FormattedDate date = {this.state.date}/>
 
 
 ```
 
 这通常被称为一个从上到下的单向数据流


























