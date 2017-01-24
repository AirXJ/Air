# UIViewController调用的方法的生命周期

* `小提示`

  为什么创建控制器，而不是视图直接添加到UIWindow上

  因为UIViewController有loadview方法,可以自定义view，而且一个萝卜一个坑，好管理。  
  在iOS7开始,状态栏默认交给控制器的管理，prefersStatusBarHidden

* 苹果是怎么创建UIViewController的：故事板，xib,手动（view全是手写或者loadview）

* 底层实现  
  ![](/assets/屏幕快照 2016-12-24 23.23.14.png)

```
//这个方法是系统自动调用的，在里面可以自定义view
- (void)loadView{
//懒加载，不要在里面写get方法，会屎人的
 [super loadView];

 NSLog(@"%s", __func__);

}
```

##### 调用顺序,very important!

> 从故事板、xib加载系统会自动调用  
> ｀- initWithCoder:`｀- (void)awakeFromNib`
>
> ```
> - (void)viewDidLoad 这里打印view尺寸不准 self.view.bounds
> - (void)viewWillAppear:(BOOL)animated
> - (void)viewWillLayoutSubviews
> - (void)drawRect:(CGRect)rect 
> - (void)viewDidAppear:(BOOL)animated 这里打印view尺寸准
> - viewWillDisappear
> //清空缓存，图片缓存。调用Unload方法，判断view有没有显示
> -(void)didReceiveMemoryWarning
> MRC下
> //控制器view没有显示的时候会调用
> - viewWillUnload
> //清空没必要的数据
> － viewDidUnload
> ```



