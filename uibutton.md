- 设置按钮的类型只能在初始化的时候设置
-  修改按钮图片的尺寸
自定义按钮，重写imageRectForContentRect方法
![](/assets/屏幕快照 2017-01-08 15.18.06.png)
- 监听按钮点击事件

```obj
 [button addTarget:self action:@selector(demo:) forControlEvents:UIControlEventTouchUpInside];

```