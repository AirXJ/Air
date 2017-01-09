***
######  03-position和anchorPoint(默认值0～1)
[^锚点默认是(0.5,0.5),无论是旋转,缩放都是绕着锚点进行的.]
![](/assets/屏幕快照 2017-01-06 15.01.09.png)

>position和anchorPoint是CAlayer的两个属性,位置重合.

>我们以前修改一个控件的位置都是能过Frame的方式进行修改，其实UIView的frame由position决定,所以center和position同一个点。.

>现在利用CALayer的position和anchorPoint属性也能够修改控件的位置.

[^知识扩充:layery.contentsRect决定layer的图片的contents的显示范围，取值范围是)(CGRect){0,0,1,1},它的锚点也会跟着范围缩小:具体查看代码图片翻折]


```
这两个属性是配合使用的.

position:它是用来设置当前的layer在父控件当中的位置的.

所以它的坐标原点.以父控件的左上角为(0,0)点.

anchorPoint:它是决点CALayer身上哪一个点会在position属性所指的位置

anchorPoint它是以当前的layer左上角为原点(0,0)

它的取值范围是0~1,它的默认在中间也就是(0.5,0.5)的位置.

anchorPoint又称锚点.就是把锚点定到position所指的位置.

两者结合使用.想要修改某个控件的位置,我们可以设置它的position点.

设置完毕后.layer身上的anchorPoint会自动定到position所在的位置.
```
