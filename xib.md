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

- 关联控制器步骤
  - 1. xib必须要有view去描述控制器,创建xib的时候如果没有view，要拖一个进去
  - 2. xib要和控制器关联，告诉xib描述哪一个控制器，绑定
  - 3. xib中的view要跟控制器关联，告诉xib描述的是哪一个view，连线

```
//nib是xib或storyboard经过编译后的的文件名，不是放在mainbundle的xib不会编译，一般都是放图片到bundle里，懒加载，一定要绑定控制器
ViewController *vc = [[ViewController alloc] initWithNibName:@"VC" bundle:nil];
```


- xib还能设置view的类，封装管理
```
//这个方法是创建view的, 而且不是懒加载的,而且一般不要绑定控制器，而且要addsubview
UIView *vc1 = [[NSBundle mainBundle]loadNibNamed:@"View1" owner:self options:nil].lastObject;
    vc.view = vc1;
```

xib还能设置view的类，封装管理
- 不会进入initWithFrame方法