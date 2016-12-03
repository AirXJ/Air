请到文件夹里找html，详细内容

实例对象(的类) 是类对象(的类) 是元类对象(的类) 是根元类
什么时候使用runtime，runtime方法都是有前缀的，项目需要的时候，调用一些私有方法或者修改某些系统方法的功能需求。
```
### 方法调用流程
怎么去调用eat方法 ,对象方法:类对象的方法列表 类方法:元类中方法列表，所以runtime拿方法开头是class_
1.通过isa去对应的类对象的方法列表中查找
2.注册方法编号
3.根据方法编号到对应的类对象的方法列表中去查找对应方法分,通过哈希表实现。
4.找到只是最终函数实现地址,根据地址去方法区调用对应函数，
```
runtime Xcode调试,结局方法中不带有参数
![](/assets/屏幕快照 2016-12-02 22.36.42.png)

runtime发送消息和交换方法，方法交换的本质是，交换方法列表映射到方法区的地址。
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

Runtime动态添加方法(performSelector)：app中有一些功能是会员机制的，不需要马上添加到内存中去，消耗资源，oc 懒加载机制，只要方法实现就会添加到方法列表中，在内存中分配资源。