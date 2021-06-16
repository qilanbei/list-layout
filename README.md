## CSS 列表项布局技巧

### 一、元素宽度已知，即知道每行最多多少个，且所有元素都在一个容器中

公用的一些样式
```css
  /* reset css */
  ul, li { 
    margin: 0; 
    padding: 0; 
  }

  ul { 
    list-style: none;
  }
  p {
    margin: 0;
    padding: 0;
  }

  /* common style */
  .clearfix {
    *zoom: 1 
  }
  .clearfix:after { 
    display: table; 
    content: ''; 
    clear: both;
  }
  .fl {
    float: left;
  }
  .oh { 
    overflow: hidden; 
  }
  h1 {
    text-align: center;
  }
  h2 {
    text-align: center;
  }
  .text-center {
    text-align: center;
  }
  .text {
    color: #ffffff;
    width: 100%;
    text-align: center;
  }
  .flex-center {
    display: flex;
    align-items: center;
    justify-self: center;
  }
  .taj {
    text-align: justify; 
  }

  .item {
    height: 80px;
    background-color: #4c5fe2; 
    opacity: 0.5; 
    border-radius: 8px;
  }
```

1. 元素宽度已知，display: inline-block 实现，注意 <code>display: inline-block </code>间隔问题

html 模板如下：
```html
<!-- 元素宽度已知 display: inline-block 实现，注意 display: inline-block 间隔问题 -->
<div class='container'>
  <ul class="clearfix">
    <li class='item'></li>
    <li class='item'></li>
    <li class='item'></li>
    <li class='item'></li>
    <li class='item'></li>
    <li class='item'></li>
    <li class='item'></li>
  </ul>
</div>
```
css 样式如下：
```css
.container {
  max-width: 800px;
  display: table;
  margin: 16px auto;
  padding-top: 20px;
  background-color: rgba(0,0,0,0.1); 
  /* 解决 item display: inline-block; 间隔问题 */
  font-size: 0;
  -webkit-text-size-adjust:none;
}
.container .item {
  width: 185px;
  display: inline-block;
  margin-right: 20px;
  margin-bottom: 20px;
  /* 防止item里面的添加元素之后 塌下去问题 */
  overflow: hidden;
  font-size: 16px;
}
.container .item:nth-child(4n) { 
  margin-right: 0; 
}
```

效果图：

![](/images/width_inline_block.png)

2. 元素宽度已知，float 方式实现

html 模板如下：
```html
<div class="container">
  <div class="float-fixed-list oh">
    <ul class="clearfix">
      <li class="item fl"></li>
      <li class="item fl"></li>
      <li class="item fl"></li>
      <li class="item fl"></li>
      <li class="item fl"></li>
      <li class="item fl"></li>
      <li class="item fl"></li>
    </ul>
  </div>
</div>
```

css 样式如下：
```css
.container {
  max-width: 800px; 
  margin: 16px auto; 
  padding: 20px 0;
  background-color: rgba(0,0,0,0.1); 
}
.container .item {
  height: 80px;
  background-color: #4c5fe2; 
  opacity: 0.5; 
  border-radius: 8px; 
}
.float-fixed-list ul {
  margin-right: -20px;
}
.float-fixed-list .item {
  width: 185px;
  margin-right: 20px;
  margin-bottom: 20px;
}
```

效果如下：

![](/images/width_float.png)

### 二、元素宽度未知，流式布局

1. 元素宽度未知，流式布局内容和卡槽都是等比缩放的方式

html 模板如下：
```html
<div class="container">
    <div class="float-fulid-list">
      <ul class="clearfix">
        <li class="item fl"></li>
        <li class="item fl"></li>
        <li class="item fl"></li>
        <li class="item fl"></li>
        <li class="item fl"></li>
        <li class="item fl"></li>
        <li class="item fl"></li>
      </ul>
    </div>
  </div>
```

css 样式如下：
```css
.container {
  padding: 20px 0;
  max-width: 800px; 
  margin: 16px auto; 
  background-color: rgba(0,0,0,0.1); 
}
.float-fulid-list .item {
  width: 23%;
  margin: 0 1% 2%; 
}
```
效果图如下：

![](/images/width_auto_margin.png)

2. 流式布局内容按比例缩放，卡槽固定大小。dom结构需要fl嵌套item，同时需要 <code>box-sizing</code> 属性

html 模板如下：

```html
<div class="container">      
  <div class="float-fulid-list oh">
    <ul class="clearfix">
      <li class="fl">
        <div class="item"></div>
      </li>
      <li class="fl">
        <div class="item"></div>
      </li>
      <li class="fl">
        <div class="item"></div>
      </li>
      <li class="fl">
        <div class="item"></div>
      </li>
      <li class="fl">
        <div class="item"></div>
      </li>
      <li class="fl">
        <div class="item"></div>
      </li>
    </ul>
  </div>
</div>
```

css 样式如下：

```css
.container {
  padding: 20px 0;
  max-width: 800px; 
  margin: 16px auto; 
  background-color: rgba(0,0,0,0.1); 
}
.container .item {
  height: 80px;
  background-color: #4c5fe2; 
  opacity: 0.5; 
  border-radius: 8px; 
}
.float-fulid-list ul {
  margin-bottom: -20px;
}
.float-fulid-list li {
  width: 25%;
  box-sizing: border-box;
  padding: 0 10px;
}
.float-fulid-list .item {  
  margin-bottom: 20px;
}
```

效果图如下:

![](/images/width_auto_boxsizing.png)

3. 元素宽度未知，Grid方式

html 模板如下：
```html
<div class="container">
  <ul class="grid-list">
    <li class="item"></li>
    <li class="item"></li>
    <li class="item"></li>
    <li class="item"></li>
    <li class="item"></li>
    <li class="item"></li>
    <li class="item"></li>
  </ul>
</div>
```

css 样式如下：

```css
.container {
  padding: 20px 0;
  max-width: 800px; 
  margin: 16px auto; 
  background-color: rgba(0,0,0,0.1); 
}
.container .item {
  height: 80px;
  background-color: #4c5fe2; 
  opacity: 0.5; 
  border-radius: 8px; 
}
.grid-list {
  display: grid;
  /* 为了方便表示比例关系，grid网格布局提供了fr关键字（fraction 的缩写，意为"片段"）
  如果两列的宽度分别为1fr和2fr，就表示后者是前者的两倍 */
  grid-template-columns: repeat(4, 1fr);
  grid-gap: 20px;
}

```

效果图如下：

![](/images/width_auto_grid.png)

持续更新~