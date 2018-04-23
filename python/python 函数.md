## 定义函数

```
def my_abs(x):
    if x >= 0:
        return x
    else:
        return -x

```

## 调用函数

```
my_abs(-99)

```

## 函数的参数

##### 默认参数

```

def enroll(name, gender, age=6, city='Beijing'):
    print('name:', name)
    print('gender:', gender)
    print('age:', age)
    print('city:', city)
    
    
```

## 递归函数

```
def fact(n):
    if n==1:
        return 1
    return n * fact(n - 1)

```