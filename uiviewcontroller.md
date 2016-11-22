`最先调用的方法`
```obj/*
- (void)loadView{

 [super loadView];

 NSLog(@"%s", __func__);

}
*/
```



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

