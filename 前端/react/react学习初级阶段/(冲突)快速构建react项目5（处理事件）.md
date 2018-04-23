## 处理事件

通过React元素处理事件跟在DOM元素上处理事件非常相似，但是有一些语法上的区别

* React 事件使用驼峰命名，而不是全部小写。
* 通过JSX，你传递一个函数作为事件处理程序，而不是一个字符串
* 在react中你不能通过返回false来阻止默认行为，必须调用preventDefault

### 将参数传递给事件处理程序

在循环内部，通过需要将一个额外的参数传递给事件处理程序。

```
<button onClick = {(e)=>this.deleteRow(id,e)}>Delete Row</button>


<button onClick = {this.deleteRow.bind(this,id)}>Delelte Row </button>

```

上面两种方法等效的

