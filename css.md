CSS
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

- CSS两个重点，属性(样式)和选择器(标签名)
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
/*类选择器*/
        .test1{
           color: green;
        }
<p class="test1">我是段落标签我是段落标签</p>
```
 - id选择器
```
/*类选择器*/
        #first{
           color: green;
        }
<p id="first">我是段落标签我是段落标签</p>
```
 - 并列选择器
```
.test1,#first{
           color: green;
        }
```
