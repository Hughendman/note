## vue的路由

> 注意： component后面的值不要有引号，父级不要有名字name属性

```
[
    {
      path: '/',
      component: Bigdata,
      children: [
        {
          path: '',
          redirect: { name: 'Table' }
        },{
          path: 'table',
          name: 'Table' ,
          component: Table
        }
      ]
    }
  ]

```