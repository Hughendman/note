
```

1）安装npm install text-loader --save-dev
2）在webpack.config.js中添加
{
test: /.md$/,
loader: ‘text-loader’
}
然后通过import XXX from ‘xxx.md’，即可正确获取.md文件中的md原始内容。
3）安装md解析器如vue-markdown，

npm install vue-markdown --save-dev
template:
<vue-markdown>{{msg}}</vue-markdown>
js:

import VueMarkdown from 'vue-markdown’
import xxx from 'XXX.md’
export default {
components: {
VueMarkdown
},
data () {
return {
msg: xxx
}
}
}

```

注：

```
let style = {
        ul: `
              margin: 10px 20px;
              list-style-type: square;
              padding: 0;
            `,
        ol: `
              margin: 10px 20px;
              list-style-type: decimal;
              padding: 0;
            `,
        li: `
              display: list-item;
              padding: 0;
            `,
        hr: `
              margin: 15px 0;
              border-top: 1px solid #eeeff1;
            `,
        pre: `
              display: block;
              margin: 10px 0;
              padding: 8px;
              border-radius: 4px;
              background-color: #f2f2f2;
              color: #656565;
              font-size: 14px;
             `,
        blockquote: `
                      display: block;
                      border-left: 4px solid #ddd;
                      margin: 15px 0;
                      padding: 0 15px;
                    `,
        img: `
               margin: 20px 0;
             `,
        a: `
            color: #41b883;
           `,
        table: `
                 border: 1px solid #eee;
                 border-collapse: collapse;
               `,
        tr: `
              border: 1px solid #eee;
            `,
        th: `
              padding: 8px 30px;
              border-right: 1px solid #eee;
              background-color: #f2f2f2;
            `,
        td: `
              padding: 8px 30px;
              border-right: 1px solid #eee;
            `
      }

```


```
<pre>标签 
pre 元素可定义预格式化的文本。被包围在 pre 元素中的文本通常会保留空格和换行符。而文本也会呈现为等宽字体。 
<pre> 标签的一个常见应用就是用来表示计算机的源代码。 
可以导致段落断开的标签（例如标题、<p> 和 <address> 标签）绝不能包含在 <pre> 所定义的块里。尽管有些浏览器会把段落结束标签解释为简单地换行，但是这种行为在所有浏览器上并不都是一样的。 
pre 元素中允许的文本可以包括物理样式和基于内容的样式变化，还有链接、图像和水平分隔线。当把其他标签（比如<a>标签）放到 <pre>块中时，就像放在 HTML/XHTML 文档的其他部分中一样即可
<code>标签 
code标签的应用，应该是只用在表示计算机程序源代码或者其他机器可以阅读的文本内容上。<code>标签的功能有：将文本变成等宽字体；还有一个功能就是暗示这段文本是源程序代码。那么根据第二个功能，将来浏览器可能会根据自己的实际情况添加效果。例如，程序员的浏览器可能会寻找 <code> 片段，并执行某 些额外的文本格式化处理，如循环和条件判断语句的特殊缩进等。 
code标签和pre标签可以嵌套使用，如下
<pre> <code> hello world </code> </pre>


```