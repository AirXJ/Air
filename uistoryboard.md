``` 
 // 1.创建窗口
    self.window = [[UIWindow alloc] initWithFrame:[UIScreen mainScreen].bounds];
    
    
    // 2.加载main.storyboard,创建main.storyboard描述的控制器
    // UIStoryboard专门用来加载stroyboard
    // name:storyboard名称不需要后缀
    UIStoryboard *stroyboard = [UIStoryboard storyboardWithName:@"Main" bundle:nil];
    
    // 加载sotryboard描述的控制器
    // 默认是加载箭头指向的控制器
    UIViewController *vc = [stroyboard instantiateInitialViewController];
//    UIViewController *vc = [stroyboard instantiateViewControllerWithIdentifier:@"blue"];
    
    // 设置窗口的根控制器
    self.window.rootViewController = vc;
    // 3.显示窗口
    [self.window makeKeyAndVisible];
    
    
    return YES;
```


//从xib或storyboard加载控件，只调用一次

- (void)awakeFromNib
