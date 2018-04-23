## 强大的for-of循环(数组)

```
for (var value of myArray) {
  console.log(value);
}

```

## [模板字符串](https://www.cnblogs.com/bfc0517/p/6700849.html)

##### 可以包涵换行
> 在反引号以内，可以有多个换行，都能够在使用的时候被识别
##### 可以嵌入变量
> 使用美元符号和大括号包裹变量 ${对象名.属性名}
##### 可以原生输出 
> 原生输出包含转义字符串的内容String.raw模板字符串

```
$('#result').append(
  'There are <b>' + basket.count + '</b> ' +
  'items in your basket, ' +
  '<em>' + basket.onSale +
  '</em> are on sale!'
);

```
上面的代码可以写为

```
$('#result').append(`
  There are <b>${basket.count}</b> items
   in your basket, <em>${basket.onSale}</em>
  are on sale!
`);

```

##### 大括号内部可以放入任意的JavaScript表达式，可以进行运算，以及引用对象属性，而且还能调用函数

```
let x = 1,
    y = 2;
console.log(`${x} + ${y * 2} = ${x + y * 2}`)//  "1 + 4 = 5"


let obj = {x: 1, y: 2};
console.log(`${obj.x + obj.y}`)//  3


function fn() {
    return "Hello World";
        }
console.log(`foo ${fn()} bar`)// foo Hello World bar

```