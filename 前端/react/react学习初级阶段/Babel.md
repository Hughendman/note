## Babel是一个JavaScript编译器

Babel通过语法转换器支持最新版本的JavaScript。这些插件允许立刻使用新语法，无需浏览器支持

### polyfill

由于Babel只转换语法（例如箭头函数），可以使用babel-polyfill支持新的全局变量，例如Promise、新的原生方法如
String.padStart(left-pad)等。

### JSX和Flow

Babel能够转换JSX语法并去除类型注释。

