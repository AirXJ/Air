	1.帧动画介绍:
		CAKeyframeAnimation它可以在多个值之间进行动画.
		设置多值之间的属性为:
		后面是一个数组,就是要设置的多个值.
		anim.values = @[];
		
		它还可以根据一个路径做动画.
		anim.path = 自己创建的路径.
```
//1.创建动画对象
    CAKeyframeAnimation *anim = [CAKeyframeAnimation animation];
    
    anim.duration = 2;
    
    UIBezierPath *path = [UIBezierPath bezierPath];
    [path moveToPoint:CGPointMake(50, 50)];
    [path addLineToPoint:CGPointMake(300, 50)];
    [path addLineToPoint:CGPointMake(300, 400)];
    
    
    anim.keyPath =  @"position";
    anim.path = path.CGPath;
    
    
    [self.imageV.layer addAnimation:anim forKey:nil];

    
    
    
}



//图标抖动
- (void)icon {
    
    //1.创建动画对象
    CAKeyframeAnimation *anim = [CAKeyframeAnimation animation];
    
    //2.设置属性值
    anim.keyPath = @"transform.rotation";
    anim.values = @[@(angle2Rad(-3)),@(angle2Rad(3)),@(angle2Rad(-3))];
    
    //3.设置动画执行次数
    anim.repeatCount =  MAXFLOAT;
    
    anim.duration = 0.5;
    
    //anim.autoreverses = YES;
    
    
    [self.imageV.layer addAnimation:anim forKey:nil];
    
    
}

```