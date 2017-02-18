__有个html文件介绍runtime的，在应该图片目录里，下载下来后可以查看__
>写runtime要搞清楚一件事，以谁开头[^学习方法]
<hr>
经常要用到的头文件:
- objc/NSObjCRuntime.h
- objc/NSObject.h

***
__runtime Xcode调试,结局方法中不带有参数__,必须要修改成NO，不然不能编译通过。解决消息机制方法提示步骤
// 查找build setting -> 搜索msg![](/assets/屏幕快照 2016-12-02 22.36.42.png)

