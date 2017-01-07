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
``