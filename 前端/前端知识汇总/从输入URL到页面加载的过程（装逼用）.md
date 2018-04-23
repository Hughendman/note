[从输入URL到页面加载的过程](http://www.dailichun.com/2018/03/12/whenyouenteraurl.html)

[进程和线程之间的区别](https://www.zhihu.com/question/25532384)(进程=线程a+线程b...)

[回流与重绘](http://www.css88.com/archives/4996)

url分为大致6部分

* protocol，协议头，譬如有http，ftp等

* host，主机域名或IP地址

* port，端口号

* path，目录路径

* query，即查询参数

* fragment，即#后的hash值，一般用来定位到某个位置
* 
## 开启网络线程到发出一个完整的http请求

> 每次网络请求时都会开辟单独的线程进行，当url解析到http协议，就会新建一个网络线程去处理资源下载

> 这一部分包括dns查询，tcp/ip请求构建，五层因特网协议栈等等

> dns查询的到ip: 如果浏览器有缓存，直接使用浏览器缓存，否则使用本机缓存，在没有的话使用host。如果本地没有，就像dns域名服务器查询，得到ip

> tcp/ip请求：http的本质三次握手建立连接以及四次挥手断开；tcp将http长报文划分为短报文，通过三次握手与服务端建立连接，进行可靠传输（三次握手步骤：“客户端：hello，你是server吗？；服务端：我是，你是client吗？；客户端：我是。”）。建立成功后就是正式传输数据，然后断开时四次挥手（四次挥手步骤：“主动方：关闭主动通道，只能被动接受；被动方:收到消息；被动方：我这边的主动通道也关闭；主动方：最后接受数据；双方无法通信”）

### get和post的区别

get和post虽然本质都是tcp/ip，但两者除了在http层面外，在tcp/ip层面也有区别。

get会产生一个tcp数据包，post两个

具体就是：

* get请求时，浏览器会把headers和data一起发送出去，服务器响应200（返回数据），

* post请求时，浏览器先发送headers，服务器响应100 continue， 浏览器再发送data，服务器响应200（返回数据）。

再说一点，这里的区别是specification（规范）层面，而不是implementation（对规范的实现）