# 04-程序启动原理
一.`首先找到程序入口,执行main函数`

main -> UIApplicationMain,在这之前，加载类的信息。

二.`UIApplicationMain底层做事情`

1.创建UIApplication对象

2.创建UIApplication的代理对象,而且给UIApplication对象的代理属性赋值

3.开启主运行循环,作用接收事件,让程序一直运行。(runloop，每一个线程都有runloop，主线程有一个runloop自动开启)

4.加载info.plist,判断下有木有指定main.storyboard,如果指定就会去加载:1.创建窗口 2.设置窗口根控制器 3.显示窗口[^成为UIApplication主窗口;开启窗口显示] 4.可视范围可能由LaunchImage决定
三.`函数介绍`:

NSStringFromClass:根据一个类名生成一个类名字符串

NSClassFromString: 根据一个类名字符串生成一个类名

四.思想,为什么使用NSStringFromClass
NSStringFromClass:输入类名有提示,避免输入错误