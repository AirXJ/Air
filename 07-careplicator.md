
```
#import "VCView.h"

@implementation VCView


//修改UIView.layer的类型威复制层
//返回当前UIView内容layer类型
+(Class)layerClass {
    return [CAReplicatorLayer class];
}




@end

//复制层
    CAReplicatorLayer *repL = [CAReplicatorLayer  layer];
    repL.backgroundColor = [UIColor redColor].CGColor;
    repL.frame = self.contentV.bounds;
    [self.contentV.layer addSublayer:repL];
    
    //绕着复制层的锚点进行旋转
    repL.instanceTransform = CATransform3DMakeRotation(M_PI, 1, 0, 0);
    
    //阴影
    repL.instanceRedOffset -= 0.1;
    repL.instanceGreenOffset -= 0.1;
    repL.instanceBlueOffset -= 0.1;
    repL.instanceAlphaOffset -= 0.1;
    
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
    //设置复制出来的子层动画的延时执行时长,视觉上感觉动画慢慢出来，粒子效果和音乐震动条波浪形变
    repL.instanceDelay = 1;
    ```