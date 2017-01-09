```
//复制层
    CAReplicatorLayer *repL = [CAReplicatorLayer  layer];
    repL.backgroundColor = [UIColor redColor].CGColor;
    repL.frame = self.contentV.bounds;
    [self.contentV.layer addSublayer:repL];
    
    
    //添加音量震动条
    CALayer *layer = [CALayer layer];
    layer.frame = CGRectMake(20, 30, 30, 50);
    layer.backgroundColor = [UIColor greenColor].CGColor;
    [repL addSublayer:layer];

    
    CALayer *layer2 = [CALayer layer];
    layer2.frame = CGRectMake(20, 100, 30, 50);
    layer2.backgroundColor = [UIColor blueColor].CGColor;
    [repL addSublayer:layer2];
    
    //复制的份数(包括它自己)
    repL.instanceCount = 3;
    //对复制出来的子层做形变操作(每一个都是相对于上一个子层做的形变)
    repL.instanceTransform = CATransform3DMakeTranslation(45, 0, 0);
    //设置复制出来的子层动画的延时执行时长
    repL.instanceDelay = 1;
    ```