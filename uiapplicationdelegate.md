一.UIApplication代理作用

1.在app受到干扰时，会产生一些系统事件，这时UIApplication会通知它的delegate对象，让delegate代理来处理这些系统事件

2.delegate可处理的事件包括：

2.1应用程序的生命周期事件(如程序启动和关闭)

2.2系统事件(如来电)

2.3内存警告