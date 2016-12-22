苹果单例实现
> 什么是单例,整个应用程序只有一份内存,并不会分配很多内存

- 内部创建一次单例,什么时候创建,程序一启动的时候创建单例,使用静态全局变量保存单例对象
  -  +(void)load方法比main函数先调用，打印就能判断先后[^load方法，每次程序一启动,就会把所有的类加载进内存，类方法，静态变量等等所有类的内容]
- 禁止别人第二次调用alloc方法，一调用就崩掉，断言或者异常
- 提供一个方法给外界获取单例

```

@implementation Person
// 程序启动时候创建对象
// 静态变量
static Person *_instance = nil;

// 作用:加载类
// 什么调用:每次程序一启动,就会把所有的类加载进内存
+ (void)load
{
    NSLog(@"%s",__func__);
   
 
}

+ (instancetype)sharePerson
{
    static dispatch_once_t onceToken;
    dispatch_once(&onceToken, ^{
    _instance = [[self alloc] init];
      });
    return _instance;
}

+ (instancetype)alloc
{
    
    if (_instance) {
        // 标示已经分配好了,就不允许外界在分配内存
        
        // 抛异常,告诉外界不运用分配
        // 'NSInternalInconsistencyException', reason: 'There can only be one UIApplication instance.'

        // 创建异常类
        // name:异常的名称
        // reson:异常的原因
        // userInfo:异常的信息
        NSException *excp = [NSException exceptionWithName:@"NSInternalInconsistencyException" reason:@"There can only be one Person instance." userInfo:nil];
        
        // 抛异常
        [excp raise];
        
    }
    // super -> NSObject 才知道怎么分配内存
    // 调用系统默认的做法, 当重写一个方法的时候,如果不想要覆盖原来的实现,就调用super
    return [super alloc];
}

```


