## - 添加图片毛玻璃效果

```obj
 // 1.创建UIImageView对象
 UIImageView *imageView = [[UIImageView alloc] init];
 // 2. 设置尺寸
// imageView.frame = CGRectMake(0, 0, self.view.frame.size.width, self.view.frame.size.height);
 imageView.frame = self.view.bounds;
 // 3. 设置背景颜色
 imageView.backgroundColor = [UIColor redColor];
 // 4. 设置背景图片,只会去主bundle里找
 imageView.image = [UIImage imageNamed:@"1"];
 // 5.设置图片的内容模式
 imageView.contentMode = UIViewContentModeScaleAspectFill;
 // 6.加毛玻璃
 // 6.1 创建UIToolBar对象

 UIToolbar *toolBar = [[UIToolbar alloc] init];

 // 6.2 设置toolBar的frame

 toolBar.frame = imageView.bounds;

 // 6.3 设置毛玻璃的样式

 toolBar.barStyle = UIBarStyleBlack;

 toolBar.alpha = 0.98;

 // 6.4 加到imageView中

 [imageView addSubview:toolBar];

```

## - 设置UIImageView的frame的三种方式

```obj
// 设置frame的方式

 // 方式一

 UIImageView *imageView = [[UIImageView alloc] init];

 imageView.image = [UIImage imageNamed:@"1"];



// imageView.frame = CGRectMake(100, 100, 267, 400);

// imageView.frame = (CGRect){{100, 100},{267, 400}};

 */



 // 方式二

 /*

 UIImageView *imageView = [[UIImageView alloc] init];

 // 创建一个UIImage对象

 UIImage *image = [UIImage imageNamed:@"1"];

 // 设置frame

 imageView.frame = CGRectMake(100, 10, image.size.width, image.size.height);

 // 设置图片

 imageView.image = image;

 */



 // 方式三

 /*

 // 创建一个UIImage对象

 UIImage *image = [UIImage imageNamed:@"1"];

 UIImageView *imageView = [[UIImageView alloc] initWithFrame:CGRectMake(100, 10, image.size.width, image.size.height)];

 imageView.image = image;

 */



 // 方式四



 // 创建一个UIimageview对象

 // 注意: initWithImage 默认就有尺寸--->图片的尺寸

 UIImageView *imageView = [[UIImageView alloc] initWithImage:[UIImage imageNamed:@"1"]];



 // 改变位置

// imageView.center = CGPointMake(200, 150);



 imageView.center = CGPointMake(self.view.frame.size.width * 0.5, self.view.frame.size.height * 0.5);

```

## 加载图片方式的区别:

```obj
/**
 1. imageNamed:一直在内存里

 2. imageWithContentsOfFile: 可以清空缓存，通过赋值nil

 图片的两种加载方式:

 1> imageNamed:
 a. 就算指向它的指针被销毁,该资源也不会被从内存中干掉
 b. 放到Assets.xcassets的图片,默认就有缓存
   1> 打包后变成Assets.car
   2> 拿不到路径 
   3> 只能通过imageNamed:来加载图片
   4> 不能通过imageWithContentsOfFile:来加载图片
 c. 使用场景:图片经常被使用

 2> imageWithContentsOfFile:
 a. 指向它的指针被销毁,该资源会被从内存中干掉
 b. 放到项目中的图片就没有缓存
   1> 可以拿到路径
   2> 能通过imageNamed:来加载图片
   3> 也能通过imageWithContentsOfFile:来加载图片
 c. 使用场景:不经常用,大批量的图片
 */
```

