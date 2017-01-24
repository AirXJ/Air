###  `xib加载控制器的步骤`
- xib和storyboard的比较。

>共同点：
都用来描述软件界面
都用Interface Builder工具来编辑
都会被编译成nib

>不同点:
Xib是轻量级的，用来描述局部的UI界面
Storyboard是重量级的，用来描述整个软件的多个界面，并且能展示多个界面之间的跳转关系
NIB其实是一个文件夹，里面有可执行的二进制文件

#####   - 关联控制器步骤
>- 1. xib必须要有view去描述控制器,创建xib的时候如果没有view，要拖一个进去
- 2. xib要和控制器关联，告诉xib描述哪一个控制器，绑定
- 3. xib中的view要跟控制器关联，告诉xib描述的是哪一个view，连线

```
//nib是xib或storyboard经过编译后的的文件名，不是放在mainbundle文件夹里的xib不会编译，一般都是放图片到bundle里，懒加载，一定要绑定控制器
ViewController *vc = [[ViewController alloc] initWithNibName:@"VC" bundle:nil];
```

###xib加载控制器
    - initWithNibName:如果指定了特定的名称的xib,会去加载指定的xib;如果指定是nil
    - 1.判断有没有当前控制器相同名称的xib,如果有,自动加载跟它相同名称的xib(XMGViewController.xib)
    - 2.如果没有跟它相同名称的xib.自动加载跟它相同名称并且是去掉controller(XMGView.xib)
    
    
    //init底层自动调用initWithNibName.


### xib获取UIView
- 如果一个view从xib中加载,就不能用[xxx alloc] init] 和 [xxx alloc] initWithFrame:]创建[^代码创建控件会调用init，然后就会自动调用initWithFrame方法，代码创建不会调用initWithCoder和awakeFromNib方法,有时候写在awakeFromNib中的方法在initWithFrame中还要写一次,或者直接写viewDidLoad方法就不用2个都写]
- 如果一个xib经常被使用,应该提供快速构造类方法,将下面的方法封装到view类里
```
//这个方法是创建view的, 而且不是懒加载的,而且一般不要绑定控制器，而且要addsubview
UIView *vc1 = [[NSBundle mainBundle]loadNibNamed:@"View1" owner:self options:nil].lastObject;
    vc.view = vc1;
```
- `initWithCoder:`如果View从xib中加载,就会调用此方法[^如果子控件是从xib中创建,是处于未唤醒状态
]

- `- (void)awakeFromNib`，从xib中唤醒,添加 xib中创建的子控件 的子控件用此方法，也可以添加xib的子控件
    

