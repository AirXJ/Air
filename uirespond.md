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

