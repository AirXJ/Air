# UIResponder 内部提供了一些方法来处理事件，子类可以按需求覆盖，由系统自动调用
- 只有继承自UIResponder的对象才能处理事件，我们称它们是响应者对象，接收并处理事件的对象。
![](/assets/屏幕快照 2016-11-29 10.28.16.png)

- 为什么说继承了UIResponder就能够处理事件?

 因为UIResponder内部提供了以下方法来处理事件


``` 
比如触摸事件会调用以下方法:
 - (void)touchesBegan:(NSSet *)touches withEvent:(UIEvent *)event;

 - (void)touchesMoved:(NSSet *)touches withEvent:(UIEvent *)event;

 - (void)touchesEnded:(NSSet *)touches withEvent:(UIEvent *)event;

 - (void)touchesCancelled:(NSSet *)touches withEvent:(UIEvent *)event;

 加速计事件会调用:

 - (void)motionBegan:(UIEventSubtype)motion withEvent:(UIEvent *)event;

 - (void)motionEnded:(UIEventSubtype)motion withEvent:(UIEvent *)event;

 - (void)motionCancelled:(UIEventSubtype)motion withEvent:(UIEvent *)event;

 远程控制事件会调用:

 - (void)remoteControlReceivedWithEvent:(UIEvent *)event;
```
![](/assets/屏幕快照 2016-12-01 13.44.51.png)
![](/assets/屏幕快照 2016-12-01 13.44.20.png)
```
事件响应
 用户点击屏幕后产生的一个触摸事件，经过一系列的传递过程后，会找到最合适的视图控件来处理这个事件,
 找到最合适的视图控件后,就会调用控件的touches方法来作具体的事件处理
 那这些touches方法的默认做法是将事件顺着响应者链条向上传递，将事件交给上一个响应者进行处理

 什么是响应者链条?
 是由多个响应者对象连接起来的链条.

 什么是响应者对象?
 继承了UIResponder对象我们称之为响应者对象,也就是能处理事件的对象

 事件传递的完整过程?
 在产生一个事件时,系统会将该事件加入到一个由UIApplication管理的事件队列中,
 UIApplication会从事件队列中取出最前面的事件,将它传递给先发送事件给应用程序的主窗口.
 主窗口会调用hitTest方法寻找最适合的视图控件,找到后就会调用视图控件的touches方法来做具体的事情.
 当调用touches方法,它的默认做法, 就会将事件顺着响应者链条往上传递，
 传递给上一个响应者,接着就会调用上一个响应者的touches方法

 如何去寻找上一个响应者?
 1.如果当前的View是控制器的View,那么控制器就是上一个响应者.
 2.如果当前的View不是控制器的View,那么它的父控件就是上一个响应者.
 3.在视图层次结构的最顶级视图，如果也不能处理收到的事件或消息，则其将事件或消息传递给window对象进行处理
 4.如果window对象也不处理，则其将事件或消息传递给UIApplication对象
 5.如果UIApplication也不能处理该事件或消息，则将其丢弃
```
