### 01-项目中常见的文件(LaunchScreen)
LaunchScreen原理:会自动加载LaunchScreen是因为在Target当中,指定了Launch Screen file,如果没有指定的话,就不会去加载LaunchScreen作为启动界面.
如果没有设置启动图片,模拟器默认的尺寸大小是4s的尺寸大小.(可以打印屏幕尺寸验证.)
模拟器默认的尺寸是由启动界面决定的.它的底层实现其实把LaunchScreen上的东西,生成了一张图片,然后把这张图片设为程序的启动图片.

>可以进入沙盒当中查看, 查看方法,找到应用程序根目录.获取方法: NSLog(@"%@",NSHomeDirectory());打印出来,后前往文件夹.找到Library->Caches->Snapshots目录下面.最后一层就是程序自动生成的图片.
