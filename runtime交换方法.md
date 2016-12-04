
>方法交换的本质是:交换方法列表映射到方法区的地址。
>Runtime(交换方法):修改系统方法的实现  
              
>需求:比如说有一个项目,已经开发了2年,忽然项目负责人添加一个功能,每次UIImage加载图片,告诉我是否加载成功
>给系统的imageNamed添加功能,只能使用runtime(交互方法)
- 给系统的方法添加分类
- 自己实现一个带有扩展功能的方法
- 交互方法,只需要交互一次,

```
#import "UIImage+Image.h"
#import <objc/message.h>
@implementation UIImage (Image)
// 把类加载进内存的时候调用,只会调用一次；oc写这里
+ (void)load{
 Method imageNamedMethod = class_getClassMethod(objc_getClass("UIImage"), sel_registerName("imageNamed:"));
 // 获取xmg_imageNamed
 Method xmg_imageNamedMethod = class_getClassMethod(objc_getClass("UIImage"), sel_registerName("xmg_imageNamed:"));
 // 交换方法实现:runtime
 method_exchangeImplementations(xmg_imageNamedMethod, imageNamedMethod);
}
// 会调用多次，swift写这个
//+ (void)initialize
//{ static dispatch_once_t onceToken;
// dispatch_once(&onceToken, ^{});}
// 在分类中,最好不要重写系统方法,一旦重写,把系统方法实现给干掉
//+ (UIImage *)imageNamed:(NSString *)name{
// // super -> 父类NSObject，没有imageNamed：方法}
//修改系统方法的实现，通过runtime交换方法实现
+ (UIImage *)xmg_imageNamed:(NSString *)name
{//因为交互了，所以不能掉imageNamed:不然死循环
 UIImage *image = objc_msgSend(objc_getClass("UIImage"), sel_registerName("xmg_imageNamed:"),name);
 if (image == nil) {
 NSLog(@"加载失败");
 }
 return image;
}
@end
```