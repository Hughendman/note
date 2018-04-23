场景还原：

```
created(){
    this.fetchPostList()
},
watch: {
    searchInputValue(){
        this.fetchPostList()
    }
}

```

组件创建的时候我们获取一次列表，同时监听input框，每当发生变化的时候重新获取一次筛选后的列表这个场景很常见，有没有办法优化一下呢？

招式解析：

首先，在watchers中，可以直接使用函数的字面量名称；其次，声明immediate:true表示创建组件时立马执行一次。

```

watch: {
    searchInputValue:{
        handler: 'fetchPostList',
        immediate: true
    }
}

```