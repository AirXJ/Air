# UIView的一个属性

1.CGAffineTransformMake与CGAffineTransform的区别?

只有x，y轴，所以结构体里就2组数据。  
动画相对于原来位置或者外观的变化，带make的只变化一次。  
旋转\(旋转的度数, 是一个弧度\) CGAffineTransformRotate  
缩放 CGAffineTransformMakeScale CGAffineTransformScale  
平移 CGAffineTransformMakeTranslation

