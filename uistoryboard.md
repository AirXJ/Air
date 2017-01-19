### 模拟系统加载Main故事板

```
// 1.创建窗口
    self.window = [[UIWindow alloc] initWithFrame:[UIScreen mainScreen].bounds];
    // 2.加载main.storyboard,创建main.storyboard描述的控制器
    // UIStoryboard专门用来加载stroyboard
    // name:storyboard文件名称不需要后缀
    UIStoryboard *stroyboard = [UIStoryboard storyboardWithName:@"Main" bundle:nil];
    // 加载storyboard描述的控制器
    // 默认是加载箭头指向的控制器
    UIViewController *vc = [stroyboard instantiateInitialViewController];
//    UIViewController *vc = [stroyboard instantiateViewControllerWithIdentifier:@"blue"];

    // 设置窗口的根控制器
    self.window.rootViewController = vc;
    // 3.显示窗口
    [self.window makeKeyAndVisible];
    return YES;
```

* `-  (void)loadView`
> 控制器才用init创建，只要进入了这个方法就不会根据其它了。
> loadView作用:加载控制器的view  
>  loadView什么调用:当控制器的view第一次使用的时候就会调用
>
> 开发中什么情况使用:只要想自定义控制器的view就调用这个方法或者采用storyboard关联view。里面控件唤醒

* `- (void)awakeFromNib`

> 从xib或storyboard加载控件，只调用一次

#####  LaunchScreen
优先级:LaunchScreen > LaunchImage
    在xcode配置了,不起作用 1.清空xcode缓存 2.直接删掉程序 重新运行
    如果是通过LaunchImage设置启动界面,那么屏幕的可视范围由图片决定
    注意:如果使用LaunchImage,必须让你的美工提供各种尺寸的启动图片
    
    LaunchScreen:Xcode6开始才有
    LaunchScreen好处:1.自动识别当前真机或者模拟器的尺寸 2.只要让美工提供一个可拉伸图片
    3.展示更多东西
 
    LaunchScreen底层实现:把LaunchScreen截屏,生成一张图片.作为启动界面

