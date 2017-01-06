>UIApplication会从事件队列中取出最前面的事件，主窗口会调用UIView的hitTest和pointInside方法找到合适的事件响应者调用touch方法，然后形成响应者链条，通过[super touch]完成事件传递。
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


```
//作用:去寻找最适合的View
//什么时候调用:什么时候用调用:只要一个事件,传递给一个控件时, 就会调用这个控件的hitTest方法
//返回值:返回的是谁,谁就是最适合的View(就会调用最适合的View的touch方法)
-(UIView *)hitTest:(CGPoint)point withEvent:(UIEvent *)event{
 //1.判断自己能否接收事件
 if(self.userInteractionEnabled == NO || self.hidden == YES || self.alpha <= 0.01) {
     return nil;
 }

 //2.判断当前点在不在当前View.
 if (![self pointInside:point withEvent:event]) {
     return nil;
 }

 //3.从后往前遍历自己的子控件.让子控件重复前两步操作,(把事件传递给,让子控件调用hitTest)
 int count = (int)self.subviews.count;
 for (int i = count - 1; i >= 0; i--) {

 //取出每一个子控件
 UIView *chileV = self.subviews[i];
 //把当前的点转换成子控件从标系上的点.
 CGPoint childP = [self convertPoint:point toView:chileV];
 UIView *fitView = [chileV hitTest:childP withEvent:event];
 //判断有没有找到最适合的View
 if(fitView){
     return fitView;
  }
 }
 //4.没有找到比它自己更适合的View.那么它自己就是最适合的View
 return self;
}

//作用:判断当前点在不在方法调用者身上,(谁调用pointInside,这个View就是谁)
//什么时候调用:它是在hitTest方法当中调用的.
//注意:point点必须得要跟它方法调用者在同一个坐标系里面
-(BOOL)pointInside:(CGPoint)point withEvent:(UIEvent *)event{

 NSLog(@"%s",__func__);

 return [super pointInside:point withEvent:event];

}
```



