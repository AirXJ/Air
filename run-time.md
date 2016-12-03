请到文件夹里找html，详细内容
实例对象(的类) 是类对象(的类) 是元类对象(的类) 是根元类
runtime Xcode调试![](/assets/屏幕快照 2016-12-02 22.36.42.png)

runtime发送消息和交换方法,功能需求的实现
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