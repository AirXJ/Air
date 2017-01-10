# UIView的一个属性

CG动画也是绕着锚点的。anchorPoint

>只绕着z轴做旋转，因为矩阵里第三列永远是001.transform并没有修改center.它修改的是frame。假如绕其他轴，就需要用核心动画。绕着中心的锚点旋转  

1.CGAffineTransformMake与CGAffineTransform的区别?

只有x，y轴，所以结构体里就2组数据。  
动画相对于原来位置或者外观的变化，带make的只变化一次。  
旋转(旋转的度数, 是一个弧度) CGAffineTransformRotate  
缩放 CGAffineTransformMakeScale CGAffineTransformScale  
平移 CGAffineTransformMakeTranslation

