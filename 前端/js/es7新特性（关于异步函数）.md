## 参考

[es7异步函数](https://www.cnblogs.com/YMaster/p/6920441.html)

## 举例
```
let sleep = function (time) {
    return new Promise(function (resolve, reject) {
        setTimeout(function () {
            resolve();
        }, time);
    })
};

let howLongToSleep = async function () {
    // 在这里使用起来就像同步代码那样直观
    console.time();
    console.log('start');
    await sleep(3000);  //sleep 为一个执行需要耗费 3s 的函数
    console.timeEnd('end');
};

howLongToSleep();

//先是打印出了 start,3s后打印 end: 1496124446501.106ms
```

### include

```
let arr = [1,2,3,4,5];
console.log(arr.includes(1));

```

> 返回true


> 而且还可以根据索引来进行判断

```
let arr = [1,2,3,4,5];
console.log(arr.includes(1,2));
      
```

> 返回false,因为1的所以应该是0，而不是2，所以为false


## 关于generator
> 这种函数是可以暂停的

```
function* gen(x){
  var y = yield x + 2;
  return y;
}

var g = gen(1);
g.next() // { value: 3, done: false }
g.next() // { value: undefined, done: true }

```

