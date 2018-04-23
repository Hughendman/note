### JXS介绍

下面这种语法既不是HRML也不是字符串，而是JXS
```
const element = <h1>Hello, world</h1>

```

JXS是react是JavaScript的一种扩展语法，推荐react中使用这种语法来描述UI信息，JXS可能会让你想起模板语言，但是它具备JavaScript的全部能力

### JXS中嵌入表达式

你可以用任意花括号把任意JavaScript的表达式嵌入JXS中

如下代码展示

```
function formatName(user) {
    return user.firstName + ' ' + user.lastName;
}

const user = {
    firstName : 'xuesong'，
    lastName : 'yin'
};

const element = {
    <h1>
        Hello,{formatName(user)};
    </h1>
};

ReactDOM.render(element,document.getElementById('root'));


```

### JXS 也是一个表达式

编译之后，JXS表达式就变成了常规的JavaScript对象；

可以在  if  语句或者  for  循环语句中使用JXS，用它给变量赋值，当做参数接收，或者作为函数的返回值

```
function yinxs(user){
    if(user){
        return <h1>Hello, yinxs</h1>;
    }
    return <h1>Hello, boy</h1>;
}

```

### 用JSX指定属性值

可以使用双引号来指定字符串字面量作为属性值

```
const element = <div tabIndex = '0'> </div>

```

也可以用花括号嵌入一个JavaScript表达式作为属性值

```
const element = <img src = {user.currentUrl}><img>

```

在属性中嵌入JavaScript表达式时，不要使用引号来包裹大括号。使用引号后会成为字符串。

注意： 字符串使用引号，表达式使用大括号

### 指定子元素

到现在的感想感觉写起来和模板引擎并没有什么不同

```
const element = (
    <div>
        <h1> Hello!! </h1>
        <h2> yinxs!! </h2>
    </div>
);

```

注意：JXS更接近JavaScript，所以ReactDOM使用驼峰命名（camelCase）属性命名约定，所以class在JXS中要写成className


### JSX防止注入攻击
在JSX中嵌入用户输入时安全的：

```
const title = 'yinxs';

const element = <h1>{title}</h1>

```
默认情况下，在渲染前，ReactDom会格式化（escapes）JSX中的所有值，从而保证用户无法注入任何应用之外的代码，在被渲染之前，所有的数据都被转义成字符串处理，以避免xss（跨站脚本）攻击。

### JSX表示对象

 Babek将JSX编译成React.creatElement()调用
 
 ```
 const element = (
    <h1 className = 'greeting'>
        Hello,yinxs!
    </h1>
 );
 //上面这段代码编译之后
 
 const element = React.creatElement(
    'h1'
    {className: 'greeting'},
    'Hello,yinxs!'
    
 );
 ```
 
 
 React.creatElement()执行一些检查来帮助你编写没有bug的代码，但基本上它会创建一个如下所示的对象：
 
 ```
 const element = {
    type: 'h1',
    props: {
        className: 'greeting',
        children: 'Hello,yinxs!'
    }
 
 }
 
 ```
 
 这些对象被成为“React元素”。React读取这些对象，用他们来构建DOM，并保持它们不到更新