# 注意d3版本四改动太大，已弃
## [参考](http://blog.csdn.net/ligang2585116/article/details/52653830)
```
<template>
    <div id="canvas" ></div>
</template>

<script>
    export default {
        name: "d3-first",
        mounted(){
          d3.select('#canvas').text('Hello,yiifaa!')
        }
    }
</script>

<style scoped>

</style>

```
### 矩形
```
<svg width="1000" height="200" version="1.1" xmlns="http://www.w3.org/2000/svg">
    <!-- 直角矩形 -->
    <rect x="20" y="20" width="200" height="100" style="fill: steelblue; stroke: blue; stroke-width:4; opacity: 0.5"></rect>
    <!-- 圆角矩形 -->
    <rect x="250" y="20" rx="10" ry="10" width="200" height="100" style="fill: steelblue; stroke: blue; stroke-width:4; opacity: 0.5"></rect>
  </svg>
  
```

### 圆角

```
<svg width="1000" height="300" version="1.1" xmlns="http://www.w3.org/2000/svg">
    <!-- 圆形 -->
    <circle cx="150" cy="50" r="50" fill="blue"></circle>
    <!-- 椭圆 -->
    <ellipse cx="350" cy="150" rx="110" ry="80" style="fill: yellow; stroke: blue; stroke-width: 3"></ellipse>
</svg>

```

### 直线

```
<svg width="1000" height="500" version="1.1" xmlns="http://www.w3.org/2000/svg">
    <!-- 直线 -->
    <line x1="20" y1="20" x2="150" y2="50"
        style="stroke: black; stroke-width: 3"></line>
</svg>

```

### 多边形

```
<svg width="1000" height="500" version="1.1" xmlns="http://www.w3.org/2000/svg">
    <!-- 多边形 -->
    <polygon points="100,20 20,90 60,160 140,160 180,90"
        style="fill: green; stroke: black; stroke-width: 3"></polygon>
    <!-- 折线 -->
    <polyline points="400,220 320,290 360,360 440,360 480,290"
        style="fill:white; stroke: black; stroke-width: 3"></polyline>
</svg>

```