##  Set 对象允许你存储任何类型的唯一值，无论是原始值或者是对象引用。

```
const set1 = new Set([1, 2, 3, 4, 5]);

console.log(set1.has(1));
// expected output: true

console.log(set1.has(5));
// expected output: true

console.log(set1.has(6));
// expected output: false

```

### 关于set的长度(含有多少个元素)

```
var mySet = new Set();

mySet.add(1);
mySet.add(2);

console.log(mySet.size);
// expected output: 2


```

### 添加（add）

```
var set = new Set();
set.add(1);
set.add(2);

```

### 清空一个set对象(clear)

```
var set = new Set([1,2,4,5]);
set.clear();

//返回值为underfined


```

### 删除元素(delete)

```
var set = new Set();
set.add("foo1");
set.add("foo2");
set.add("foo3");
set.delete("foo3");
set.has("foo3");//false


```

### 新的迭代器对象

> 一个新的包含 [value, value] 形式的数组迭代器对象，value 是给定集合中的每个元素，迭代器 对象元素的顺序即集合对象中元素插入的顺序。

```
var mySet = new Set();
mySet.add("foobar");
mySet.add(1);
mySet.add("baz");

var setIter = mySet.entries();

console.log(setIter.next().value); // ["foobar", "foobar"]
console.log(setIter.next().value); // [1, 1]
console.log(setIter.next().value); // ["baz", "baz"]

```

### forEach

```
function logSetElements(value1, value2, set) {
    console.log("s[" + value1 + "] = " + value2);
}

new Set(["foo", "bar", undefined]).forEach(logSetElements);

// logs:
// "s[foo] = foo"
// "s[bar] = bar"
// "s[undefined] = undefined"

```

### has 返回的值表示是否存在

### value 表示返回的值

```
var mySet = new Set();
mySet.add("foo");
mySet.add("bar");
mySet.add("baz");

var setIter = mySet.values();

console.log(setIter.next().value); // "foo"
console.log(setIter.next().value); // "bar"
console.log(setIter.next().value); // "baz"

```

### Set.prototype[@@iterator]()
```
var mySet = new Set();
mySet.add("0");
mySet.add(1);
mySet.add({});

var setIter = mySet[Symbol.iterator]();

console.log(setIter.next().value); // "0"
console.log(setIter.next().value); // 1
console.log(setIter.next().value); // Object

```

```
var mySet = new Set();
mySet.add("0");
mySet.add(1);
mySet.add({});

for (var v of mySet) {
  console.log(v);
}


```