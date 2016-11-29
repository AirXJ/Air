```
1.事件是怎么样产生与传递的?
  每产生一个事件，就会产生一个UIEvent对象，UIEvent还提供了相应的方法可以获得在某个view上面的触摸对象(UITouch).
  UIApplication->window->寻找处理事件最合适的view.
当发生一个触摸事件后,系统会将该事件加入到一个由UIApplication管理的事件队列中.
UIApplication会从事件队列中取出最前面的事件，并将事件分发下去以便处理，通常，先发送事件给应用程序的主窗口（keyWindow)。
  主窗口会在视图层次结构中找到一个最合适的视图来处理触摸事件,这是整个事件处理过程的第一步。
    找到合适的视图控件后，就会调用视图控件的touches方法来作具体的事件处理
触摸事件的传递是从父控件传递到子控件的.
如果一个父控件不能接收事件,那么它里面的了子控件也不能够接收事件.

1.如何寻找最合适的View?
 主窗口会在视图层次结构中找到一个最合适的视图来处理触摸事件.
 那如何找到最合适的View呢?
 1.先判断自己是否能够接收触摸事件,如果能再继续往下判断,
 2.再判断触摸的当前点在不在自己的身上.
 3.如果在自己身上,它会从后往前遍历子控件,遍历出每一个子控件后,重复前面的两个步骤.
 4.如果没有符合条件的子控件,那么它自己就是最适合的View.
```

* UIView不能接收触摸事件的三种情况：
  * 如果一个父控件不能接收事件,那么它里面的了子控件也不能够接收事件,判断坐标位置必须用自己的坐标系:[self convertPoint:point toView:chileV]
    * 隐藏：如果把父控件隐藏，那么子控件也会隐藏，隐藏的控件不能接受事件
    * 不允许交互：userInteractionEnabled = NO
    * 透明度：如果设置一个控件的透明度&lt;0.01，会直接影响子控件的透明度。alpha：0.0~0.01为透明。



```
 注意:UIImageView的userInteractionEnabled默认就是NO，
        因此UIImageView以及它的子控件默认是不能接收触摸事件的
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

