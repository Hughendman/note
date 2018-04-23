## title
> Given two binary strings, return their sum (also a binary string).

## code

```
//es6
var addBinary = function(a, b) {
    let [i, j, c, s] = [a.length - 1, b.length - 1, 0, '']

    while (i >= 0 || j >= 0 || c === 1) {
        c += +(a[i--] || 0) + +(b[j--] || 0)
        s = (c & 1) + s
        c = c >> 1
    }
    return s
};

```

```
//es5
'use strict';

var addBinary = function addBinary(a, b) {
    var i = a.length - 1,
        j = b.length - 1,
        c = 0,
        s = '';


    while (i >= 0 || j >= 0 || c === 1) {
        c += +(a[i--] || 0) + +(b[j--] || 0);
        s = (c & 1) + s;
        c = c >> 1;
    }
    return s;
};

```