# UIViewController调用的方法的顺序
- `小提示`

 为什么创建控制器，而不是视图直接添加到UIWindow上
 
 因为UIViewController有loadview方法，会让view重新布局，而且一个萝卜一个坑，好管理。
 
- 苹果是怎么创建UIViewController的
```
 // 2.加载main.storyboard,创建main.storyboard描述的控制器
// UIStoryboard专门用来加载stroyboard
// name:storyboard名称不需要后缀
UIStoryboard *stroyboard = [UIStoryboard storyboardWithName:@"Main" bundle:nil];
// 加载storyboard描述的控制器
// 默认是加载箭头指向的控制器
UIViewController *vc = [stroyboard instantiateInitialViewController];
// UIViewController *vc = [stroyboard instantiateViewControllerWithIdentifier:@"blue"];
```

- 底层实现:判断下有没有指定storyboard,如果有,就会帮你创建storyboard描述的控制器的view,如果没有,创建一个空的view

```
- (void)loadView{

 [super loadView];

 NSLog(@"%s", __func__);

}
```


```
/**

 1. 系统调用

 2. 控制器的view加载完毕的时候调用

 3. 控件的初始化,数据的初始化(懒加载)

 */

- (void)viewDidLoad {

 [super viewDidLoad];


}
```


－ **`只有在这个方法中能删除self.view，它的父控件是UIWindow`**

如果包含在一个viewController中的view被直接添加到一个view上，就像这样：
[view1 addSubView: viewController.view];，这样我们的viewController就不会收到viewDidAppear:的消息。按这种方式添加视图的话，我们一般需要手动发送这个消息，也就是调用viewController的viewDidAppear方法。否则的话相关的动画都无法正常显示。
```
- (void)viewDidAppear:(BOOL)animated{
 [super viewDidAppear:animated];

 NSLog(@"viewDidAppear-----%@", self.view.superview);

}
```





1. 系统调用
2. 当控制器接收到内存警告调用
3. 去除一些不必要的内存,去除耗时的内存

```
-(void)didReceiveMemoryWarning {

  [super didReceiveMemoryWarning\];


self.dataArr = nil;

}
```

