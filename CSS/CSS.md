# CSS

## 0. 开篇

```css
// style.css 文件
h1{
     color:red;
}

// index.html
// 链接式
<link rel = "stylesheet" href ="css/style.css">

<h1>标题</h1>

<!--
规范 ，<style> 可以编写CSS的代码， 没一个声明，最好使用分号分割
语法：
    选择器{
        声明1;
        声明2;
        声明3;
    }
-->
```



CSS的优势：

- 内容和表现分离
- 网页结构表现统一，可以实现复用

CSS

- 链接式：

  ```html
  <!--外部样式-->
  <link rel = "stylesheet" href="css/style.css">
  ```

- 导入式

  `@import` 是css2.1特有的

  ```html
  <style>
      @import url("css/style.css");
  </style>
  ```

## 1. 选择器

### 1.1 基本选择器

- 标签选择器

```html
<style>
    /*标签选择器，会选择页面上所有的这个标签*/
    h1{
        color: red
        background: #3cbda6
        border-radius: 24px
    }
</style>

<h1>标题</h1>
```

- 类选择器 class

```html
<style>
    /*类选择器的格式 .class的名称{}*/
    .111{
        color: red
        background: #3cbda6
        border-radius: 24px
    }   
</style1>
    
<h1 class ="lll">标题1</h1>
    
```

- ID 选择器

```html
<style>
    /*
    	#id名称 // id必须全局唯一
    */
    #1111{
        
    }

</style>

<h1 id ="1111"></h1>
```

id选择器> class选择器 >标签选择器

### 1.2 层次选择器

- 后代选择器
- 子选择器
- 相邻兄弟选择器
- 通用兄弟选择器

### 1.3 属性选择器

```html
/* a标签下，存在id属性的元素*/
a[id]{
	background: yellow;
}

/* class是links的元素*/
a[class="links"]{
	background: yellow;
}

/* class中含有links的元素*/
a[class*="links"]{
	background: yellow;
}

/* class中以links开头的元素*/
a[class^="links"]{
	background: yellow;
}

/*
属性名： 属性名 = 属性值（正则）
=  绝对等于
*= 包含这个元素
^= 以某开头
$= 以某结尾
*/
```

## 2. 美化网页元素

### 2.1

`span`：重点要突出的字，使用`span`套起来。

字体样式： `font-xxx` 

文本样式：`text-xxx`

### 2.2 文本样式

- 颜色： `color` ，`rgb`， `rgba`(模糊)
- 文本对齐的方式：`text-align= center`
- 首行缩进：`text-indent:2em`
- 行高 ：`line-height`   单行文字上下居中 `line-height = height`
- 装饰 ：`text-decoration`
- 文本图片水平对齐：`vertical-align:middle`

### 2.3 盒子模型

![1593175679759](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1593175679759.png)

`margin`：外边距

`padding`：内边距

`border`：边框

### 2.4 浮动模型

块级元素：独占一行

```html
h1~h6  p div 列表...
```

行内元素：不独占一行

```html
span   a  img  strong...
```

行内元素可以包含在块级元素中，反之则不可以

但是可以通过 `float`和 `display`做浮动操作。

### 2.5 父级边框塌陷的问题

`clear`

```html
clear : right ;  //右侧不允许有浮动元素
clear : left ;   //左侧不允许有浮动元素
clear : both ;   //两侧不允许有浮动元素
clear : none ;
```

解决方案:

1. 增加一个空的div标签，清楚浮动

```html
<div class = "clear"></div>

.class{
	clear: both;
	margin:0;
	padding:0;
}

```

2. `overflow`

```html
在父级元素中添加一个 overflow:hidden;
```

3. **在父类中添加一个伪类： `after`**

```css
#father:after{
	content: '';
	display: block;
	clear:both;
}
```

小结：

- 浮动元素后面增加空`div`，简单，代码中尽量避免空`div`
- 设置父元素的高度，简单，元素假设有了固定的高度，就会被限制
- `overflow`，简单，下拉的一些场景避免使用
- 在父类中添加一个伪类，推荐使用

对比：

- `display`：方向不可控制
- `float`：浮动起来的话会脱离标准文档流，所以要解决父级边框塌陷的问题

## 3. 定位

### 3.1 相对定位

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>

    <style>
        #box{
            width:300px;
            height:300px;
            padding: 10px;
            border:2px solid red;
        }
        a{
            width:100px;
            height: 100px;
            text-decoration: none;
            background: #ffa1f2;
            line-height: 100px;
            text-align: center;
            color: white;
            display: block;
        }
        a:hover{
            background: #47a4ff;
        }
        .a2{
            position: relative;
            left: 200px;
            top: -100px;
        }
        .a3{
            position: relative;
            left: 100px;
            top: -100px;
        }
        .a4{
            position: relative;
            top: -100px;
        }
        .a5{
            position: relative;
            left: 200px;
            top: -200px;
        }

    </style>
</head>
<body>

<div id = "box">
    <a class="a1" href="#">链接1</a>
    <a class="a2" href="#">链接2</a>
    <a class="a3" href="#">链接3</a>
    <a class="a4" href="#">链接4</a>
    <a class="a5" href="#">链接5</a>
</div>


</body>
</html>
```

相对定位： `position :relative;`

相对于原来的位置，进行指定的偏移，相对定位的话，它仍然在标准文档流中，原来的位置会被保留。

### 3. 绝对定位

定位：基于XXX的定位，上下左右

- 没有父级元素定位的前提下，相对于浏览器进行定位
- 假设父级元素存在定位，通常会相对于父级元素进行偏移
- 在父级元素范围内移动

相对于父级或者浏览器的位置，进行指定的位置偏移，绝对定位，不在标准文档流中，原来的位置会被保留。

```html
position : absolute
```

固定定位：

```html
position : fixed
```

### 3.1 `z-index`

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    
    <link rel = "stylesheet" href = "css/style.css">
    
</head>
<body>

<div id="content">
    <ul>
        <li><img sr = "images/ba.jpg" alt = ""></li>
        <li class="tipText">学习</li>
        <li class="tipBg"></li> 
        <li>时间：</li>
    </ul>

</div>

</body>
</html>
```

```css
#content{
    width:380px;
    padding: 0px;
    margin: 0px;
    overflow: hidden;
    font-size: 12px;
    line-height: 25px;
    border: 1px #000 solid;
}
ul,li{
    padding: 0px;
    margin: 0px;
    list-style:none;
}
/*父级元素相对定位*/
#content ul{
    position: relative;
}
.tipText,.tipBg{
    position: absolute;
    width: 380px;
    height: 25px;
    top: 216px;
}
#tipText{
    color: white;
    z-index: 999; /*是层级的概念*/
}
.tipBg{
    background: #000;
    opacity: 0.5;  /*背景透明度*/
}
```













