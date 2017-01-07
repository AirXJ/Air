```
  //1.创建动画对象(设置layer的属性值.)
    CABasicAnimation *anim = [CABasicAnimation animation];
    //2.设置属性值
    anim.keyPath = @"position.x";
    anim.toValue = @300;
    
    //动画完成时, 会自动删除动画,还需要固定状态
    anim.removedOnCompletion = NO;
    anim.fillMode = @"forwards";
    
    //3.添加动画
    [self.redView.layer addAnimation:anim forKey:nil];
```

```


-(void)touchesBegan:(NSSet<UITouch *> *)touches withEvent:(UIEvent *)event {
    
    //创建动画对象
    CABasicAnimation *anim = [CABasicAnimation animation];
    
    //设置属性值
    anim.keyPath = @"transform.scale";
    anim.fromValue = @0;
    anim.toValue = @1;
    

    //设置动画执行次数
    anim.repeatCount = MAXFLOAT;
    
    //设置动画执行时长
    anim.duration = 3;
    
    //自动反转(怎么样去 怎么样回来)
    anim.autoreverses = YES;
    
    //添加动画
    [self.imageV.layer addAnimation:anim forKey:nil];
    
    
}
```