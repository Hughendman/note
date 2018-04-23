#### 引用

```
<script src="jquery.min.js"></script>
<script type="text/javascript" src=".js/handlebars.js"></script>  

```

#### 基本使用方法

```
<-- 模板 -->
<script type="text/x-handlebars-template" id="tpl">
　　{{#each}}
　　　　...
　　{{/each}}
</script>

```

```
//获取到模板
var tpl = $("#tpl").html();
//预编译模板
var template = Handlebars.compile(tpl);
//模拟数据（也可以是获取的json数据）
var context = {};
//匹配数据
var html = template(context);
//输入模板
$('body').html(html);

```

#### 语法

##### 判断语句

```
{{#if true}}
  <div>为true的时候显示<div>
{{else}}
  <div>为false的时候显示<div>
{{/if}}

```

```
{{#unless false}}
  <div>为false的时候显示<div>
{{else}}
  <div>为true的时候显示<div>
{{/unless}}

```

##### with 语句

json:
```
{
  title : "标题1",
  author: {
        first:"1",
        second:"2"  
    }    
}

```
code：
```
<div>
    <h1>{{title}}</h1>
    {{#with author}}
        <p>{{firstName}}</p>
        <p>{{lastName}}</p>
    {{/with}}
</div>

```

##### 遍历
json:

```
{name:["html","css","javaScript"]}

```
code:
```
<ul>
    {{#each name}}
　　　　<li>{{@index}} 索引<li>
        <li>{{this}}</li>
    {{/each}}
</ul>

```