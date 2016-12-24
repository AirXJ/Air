###  `xib加载控制器的步骤`

- 1. xib必须要有view去描述控制器,创建xib的时候如果没有view，要拖一个进去
- 2. xib要和控制器关联，告诉xib描述哪一个控制器，绑定
- 3. xib中的view要跟控制器关联，告诉xib描述的是哪一个view，连线

```
ViewController *vc = [[ViewController alloc] initWithNibName:@"VC" bundle:nil];

```