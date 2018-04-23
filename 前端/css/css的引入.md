* 行内式
* 内嵌式
* 导入式-link
* 导入式-@import

link与@import的区别:

          1.link是XHTML标签，除了加载CSS外，还可以定义RSS等其他事务；@import属于CSS范畴，只能加载CSS。

          2.link引用CSS时，在页面载入时同时加载；@import需要页面网页完全载入以后加载，所以一般我们不推荐使用@import方法。

          3.link是XHTML标签，无兼容问题；@import是在CSS2.1提出的，低版本的浏览器不支持，从这点来说，我们同样不推荐使用@import方法。

          4.link支持使用Javascript控制DOM去改变样式；而@import不支持。
         