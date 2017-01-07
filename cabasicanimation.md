06-CABasicAnimation基础核心动画 
	
	核心动画之作用在层上面.
	动画的本质是改图层的某一个属性.
	CABasicAnimation *anim = [CABasicAnimation animation];
	图层有那些属性,这里才能写那些属性.
	anim.keyPath = @"transform.scale";
	anim.toValue = @0.5;
	告诉动画完成的时候不要移除
	anim.removedOnCompletion = NO;
	保存动画最前面的效果.
	anim.fillMode = kCAFillModeForwards;
	把动画添加到层上面.
	[_redView.layer addAnimation:anim forKey:nil];
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