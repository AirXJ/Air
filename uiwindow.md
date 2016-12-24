# 04-UIWindow

一.`什么时候创建`

1.加载info.plist,判断有没有指定main.storyboard,指定了main.storyboard,就会去加载main.storyboard,执行main.storyboard的时候创建.

二.`main.storyboard步骤`

2.1创建窗口

2.2加载控制器

2.3设置窗口的根控制器,显示窗口

三.`手动创建窗口`

1.什么时候创建?

1.在加载info.plist文件之后,程序启动才完成,启动完成之后,就要显示窗口,因此在程序启动完成的时候创建窗口.

```objc
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    // 窗口显示的注意点:
    // 1.一定要强引用
    // 2.控件要想显示出来,必须要有尺寸

    // 1.创建窗口
    self.window = [[UIWindow alloc] initWithFrame:[UIScreen mainScreen].bounds];

    // 2.创建根控制器,在设置窗口的根控制器
    UIViewController *vc = [[UIViewController alloc] init];

    // 设置窗口的根控制器,底层会自动把根控制器的view添加到窗口上,并且让控制器的view有旋转功能
    self.window.rootViewController = vc;

    // 3.显示窗口,下面2步是它的底层实现，当不想设置主窗口但又要显示window可以用方法1
     1.显示窗口 self.window.hidden = NO;
     2.成为应用程序的主窗口  application.keyWindow = self.window;
    // makeKeyAndVisible:让窗口成为应用程序的主窗口,并且显示窗口
    [self.window makeKeyAndVisible];
    return YES;
}

```

四.`窗口补充`

1.应用程序中那些控件属于窗口,1.状态栏 2.键盘

2.窗口层级关系
UIWindowLevelAlert > UIWindowLevelStatusBar > UIWindowLevelNormal

`设置窗口的层级,层级谁大就显示在最外面`

3.UITextField显示键盘

注意点:`如果一个键盘想要弹出来,必须把textField添加到一个控件上.`