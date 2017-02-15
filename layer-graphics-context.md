绘图view要有背景颜色
![](/assets/屏幕快照 2016-12-27 16.49.40.png)
```
    //1.获取上下文(获取,创建上下文 都 以uigraphics开头)
    CGContextRef ctx = UIGraphicsGetCurrentContext();
    //2.绘制路径
    UIBezierPath *path = [UIBezierPath bezierPath];

    //上下文的状态
    //设置线的宽度
    CGContextSetLineWidth(ctx, 10);
    //设置线的连接样式
    CGContextSetLineJoin(ctx, kCGLineJoinRound);
    //设置线的顶角样式
    CGContextSetLineCap(ctx, kCGLineCapRound);
    
    //设置颜色
    [[UIColor redColor] set];
//3.把绘制的内容添加到上下文当中.
    //UIBezierPath:UIKit框架 ->    CGPathRef:CoreGraphics框架
    CGContextAddPath(ctx, path.CGPath);
    //4.把上下文的内容显示到View上(渲染到View的layer)(stroke fill)
    CGContextStrokePath(ctx);
```

1.框架坐标系

首先让我们先来看看CoreText坐标系和UIKit坐标系的不同
　　![](/assets/Snip25600215_1.png)
>对UIView上下文进行变形,坐标系不再是左上，现在是左下了

```
    //CGContextScaleCTM(ctx, 0.5, .5);
    CGContextTranslateCTM(ctx, 40, 70);
```    
