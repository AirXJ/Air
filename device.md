### 设备方向
```
/*************判断设备方向:水平启动无法获得方向******************/
     UIDeviceOrientation orientation= [UIDevice currentDevice].orientation;
    //控制器的方向
    orientation = [self interfaceOrientation];
    [[UIApplication sharedApplication] statusBarOrientation];// 获取状态条相关的方向
```


### CMMotionManager来对方向进行判断，CMMotionManager是从属于Core Motion框架，利用iPhone上的重力加速计芯片来捕捉手机的各种加速值。