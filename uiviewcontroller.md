`调用的方法的顺序`
```obj/*
- (void)loadView{

 [super loadView];

 NSLog(@"%s", __func__);

}
*/
```



/**

 1. 系统调用

 2. 控制器的view加载完毕的时候调用

 3. 控件的初始化,数据的初始化(懒加载)

 */

- (void)viewDidLoad {

 [super viewDidLoad];

 //TODO:待会补上

}


－ **`只有在这个方法中能删除self.view，它的父控件是UIWindow`**
- (void)viewDidAppear:(BOOL)animated{
 [super viewDidAppear:animated];

 NSLog(@"viewDidAppear-----%@", self.view.superview);

}





/**
1. 系统调用

2. 当控制器接收到内存警告调用

3. 去除一些不必要的内存,去除耗时的内存

*/


```obj
-(void)didReceiveMemoryWarning {

  [super didReceiveMemoryWarning\];


self.dataArr = nil;

}
```

