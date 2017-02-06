具体看代码
block作用:保存一段代码
block定义:三种方式(block声明:返回值(^block变量名)(参数))
block类型:int(^)(NSString *)[^可以typedef,代码块快捷方式设置好了]
block调用: block4(@"调用别忘记传上参数2货");
block定义快捷方式 inline

block变量传递:如果是局部变量,Block是值传递;如果是静态变量,全局变量,__block修饰的变量,block都是指针传递

block应用:在一个类中定义,在另外一个类中调用


### block内存管理
 - block是一个对象
 >如何判断当前文件是MRC,还是ARC
 ```
    1.dealloc 能否调用super,只有MRC才能调用super
    2.能否使用retain,release.如果能用就是MRC
    3.#if __has_feature(objc_arc)
    ARC管理原则:只要一个对象没有被强指针修饰就会被销毁,默认局部变量对象都是强指针,存放到堆里面
 
    MRC了解开发常识:1.MRC没有strong,weak,局部变量对象就是相当于基本数据类型
                  2.MRC给成员属性赋值,一定要使用set方法,不能直接访问下划线成员属性赋值,会造成内存泄漏

 ```
 
- 总结:只要block没有引用外部局部变量,block放在全局区
 ```
 MRC:管理block
            只要Block引用外部局部变量,block放在栈里面.
            block只能使用copy,不能使用retain,使用retain,block还是在栈里面

  ARC:管理block
        只要block引用外部局部变量,block放在堆里面
        block使用strong.最好不要使用copy
```

### block使用语法
return 一个block：直接return block变量名就行。
调用block ^{
           }();可以这样写，很拉风。
           或者block(参数名);
