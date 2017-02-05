具体看代码
block作用:保存一段代码
block定义:三种方式(block声明:返回值(^block变量名)(参数))
block类型:int(^)(NSString *)[^可以typedef,代码块快捷方式设置好了]
block调用: block4(@"调用别忘记传上参数2货");
block定义快捷方式 inline

block变量传递:如果是局部变量,Block是值传递;如果是静态变量,全局变量,__block修饰的变量,block都是指针传递

block应用:在一个类中定义,在另外一个类中调用