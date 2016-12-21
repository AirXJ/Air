<hr>
>pch原理:pch里面的内容被项目中的所有文件共有.会导致一个错误c语言文件里导入oc的
***

- pch文件名跟工程名字一样，但要提前编译，prefix[^pch注意点: 1.pch需要提前编译  2.需要做一些判断,判断下当前有没有c文件,如果有c,就不导入OC的语法]
如何设置(这里Precompile Prefix Header是YES，路径名是工程路径，不是整个工程文件夹GameLive/GameLive/...，第二层就可以)
![](/assets/pch文件文件路径设置生效.png)
***
- pch作用:
 - 1.存放一些公用的宏
 - 2.存放一些公用的头文件，分类或者第三方框架头文件  
 - 3.自定义LOG(输出日志)，下面的图片是设置
 ![](/assets/屏幕快照 2016-12-21 19.19.31.png)
 ![](/assets/屏幕快照 2016-12-21 17.56.07.png)
 
```
// __OBJC__每个OC文件都会自动定义这个宏
#ifdef __OBJC__

#define ABC 10
#import "UIImage+Image.h"

#ifdef DEBUG // 调试的时候会打印，发布的时候不会
// ...表示在宏里面的可变参数
// __VA_ARGS__ 表示函数里面的可变参数
#define XMGLog(...)  NSLog(__VA_ARGS__)
#else // 发布
#define XMGLog(...)
#endif
#endif
```

