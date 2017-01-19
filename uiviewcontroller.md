# UIViewController调用的方法的生命周期
- `小提示`

 为什么创建控制器，而不是视图直接添加到UIWindow上
 
 因为UIViewController有loadview方法,可以自定义view，而且一个萝卜一个坑，好管理。
 在iOS7开始,状态栏默认交给控制器的管理，prefersStatusBarHidden


 
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
![](/assets/屏幕快照 2016-12-24 23.23.14.png)

```
/**

 1. 系统调用

 2. 控制器的view加载完毕的时候调用

 3. 控件的初始化,数据的初始化(懒加载)
- `initWithCoder:``- (void)awakeFromNib`
 */

- (void)loadView{
懒加载
 [super loadView];

 NSLog(@"%s", __func__);

}
```



 #####调用顺序,very important!

```
- (void)viewDidLoad {
- (void)viewWillAppear:(BOOL)animated
- (void)drawRect:(CGRect)rect 
- (void)viewDidAppear:(BOOL)animated{
```





1. 系统调用
2. 当控制器接收到内存警告调用
3. 去除一些不必要的内存,去除耗时的内存

```
-(void)didReceiveMemoryWarning {

  [super didReceiveMemoryWarning\];



}
```

