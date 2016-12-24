###  `xib加载控制器的步骤`

- 1. xib必须要有view去描述控制器,创建xib的时候如果没有view，要拖一个进去
- 2. xib要和控制器关联，告诉xib描述哪一个控制器，绑定
- 3. xib中的view要跟控制器关联，告诉xib描述的是哪一个view，连线

```
//nib是xib或storyboard经过编译后的的文件名，不是放在mainbundle的xib不会编译，一般都是放图片到bundle里
ViewController *vc = [[ViewController alloc] initWithNibName:@"VC" bundle:nil];

```