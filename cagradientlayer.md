***
######  [^像阴影一样的]
```
//渐变层
    CAGradientLayer *gradientL = [CAGradientLayer layer];
    gradientL.frame = self.bottomImageV.bounds;
    //设置渐变的颜色
    gradientL.colors = @[(id)[UIColor clearColor].CGColor,(id)[UIColor blackColor].CGColor];
    
    //设置渐变透明
    gradientL.opacity = 0;

    self.gradientL = gradientL;
    
     //设置一个渐变到另一个渐变的起始位置
    gradientL.locations = @[@0.2,@0.6];
    
    [self.bottomImageV.layer addSublayer:gradientL];
    ```