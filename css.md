### CSS
> 注释不再是　<!-- 一段注释 -->而是和计算机语言一样了

- 行内样式(内联样式）,直接在表现的style属性中书写
  &lt;p style="color: red; font-size: 60px; border:5px dashed purple"&gt;
- 页内样式，在本网页的style标签中书写
```
      <style>
        div{
            color:red;
            font-size: 30px;
            border: 4px solid yellow;
        }
        p{
            color: blue;
            font-size: 44px;
            background-color: yellowgreen;
        }
    </style>
```
- 外部样式 ：写在单独的CSS文件中,通过link标签引用
<head>
<!--引用外部的样式-->
<link rel="stylesheet" href="css/index.css">
</head>

- 总结css的规律:
```
<!--
      css的规律:
      1. 就近原则，有的会用最下面的。
      2. 叠加原则,没有的可以拿来用。
    -->
    <link href="css/index.css" rel="stylesheet">
    <style>
        div{
            color:red;
            font-size: 30px;
            border: 4px solid yellow;
        }

        p(标签选择器){
            color(属性): blue;
            font-size: 44px;
            background-color: yellowgreen;
        }
    </style>
```
#### CSS两个重点，属性(样式)和选择器(标签名)
- 伪类
![](/assets/屏幕快照 2016-12-07 17.36.27.png)

- 标签选择器
```
p(标签选择器){
color(属性): blue;
font-size: 44px;
background-color: yellowgreen;
}
```
- 类选择器
```
     .test1{
           color: green;
        }
<p class="test1">我是段落标签我是段落标签</p>
```
- id选择器

```
        #first{
           color: green;
        }
<p id="first">我是段落标签我是段落标签</p>
```
- 并列选择器,选择器通过逗号组合，或

```
.test1,#first{
           color: green;
        }
```
- 复合选择器，中间没逗号
```
<p class="test1">
p.test1{
     color: black;
}
```
- 后代选择器，了解
  用空格隔开，前面是老子，后面是儿子，孙子也可以
![](/assets/屏幕快照 2016-12-07 15.37.54.png)

-  伪元素
![](/assets/屏幕快照 2016-12-07 17.43.05.png)

- 直接后代选择器 必须是儿子，孙子不行
div > p {
     color: black;
}

- 相邻兄弟选择器，兄弟选择器而且在上面一个或者下面一个
![](/assets/屏幕快照 2016-12-07 15.53.21.png) 

- 属性选择器
![](/assets/屏幕快照 2016-12-07 15.54.53.png)
![](/assets/屏幕快照 2016-12-07 15.55.13.png)
![](/assets/屏幕快照 2016-12-07 15.56.18.png)

- 通配符,优先级几乎最低，设置所有的标签的样式
```
*{
    color: black;
}

```