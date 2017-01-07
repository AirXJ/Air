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