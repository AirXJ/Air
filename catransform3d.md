02-CATransform3D

layer的CATransform3D属性.只有旋转的时候才可以看出3D的效果.
##### 设置默认transform或者修改图片大小
```
 //近大远小
    CATransform3D transform = CATransform3DIdentity;
    //眼睛离屏幕的距离
    transform.m34 = -1 / 300.0;
    
    self.gradientL.opacity = transP.y * 1 / 200.0;
    
    
    //self.topImageV.layer.transform  = CATransform3DMakeRotation(-angle, 1, 0, 0);
    self.topImageV.layer.transform = CATransform3DRotate(transform, -angle, 1, 0, 0 );

self.topImageV.layer.transform = CATransform3DIdentity;
```
有4组数据，有3个轴。

旋转  
x,y,z分别代表x,y,z轴.CATransform3DMakeRotation(M_PI, 1, 0, 0)[^绕x轴旋转,都是绕着锚点进行的！];

平移  
CATransform3DMakeTranslation(x,y,z)  
缩放  
CATransform3DMakeScale\(x,y,z);

可以通过KVC的形式进行设置属性.  
但是CATransform3DMakeRotation它的值,是一个结构体,所以要把结构转成对象.  
NSValue *value = [NSValue valueWithCATransform3D:CATransform3DMakeRotation(M_PI, 1, 0, 0)];[_imageView.layer setValue:value forKeyPath:@"transform.scale"];

什么时候KVC?  
当需要做 些快速缩放,平移,维的旋转时KVC.  
如: [_imageView.layer setValue:@0.5 forKeyPath:@"transform.scale"];快速的进 缩放.后forKeyPath属性值不是乱写的.苹果 档当中给了相关的属性.
![](/assets/屏幕快照 2017-01-07 11.37.00.png)

