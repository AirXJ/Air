#4.如何监听UIView的触摸事件?
    	想要监听UIViiew的触摸事件,首先第一步要自定义UIView,
    	因为只有实现了UIResponder的事件方法才能够监听事件.
```
//当开始触摸屏幕的时候调用
-(void)touchesBegan:(NSSet<UITouch *> *)touches withEvent:(UIEvent *)event{
 NSLog(@"%s",__func__);
}

//触摸时开始移动时调用(移动时会持续调用)
//NSSet:无序
//NSArray:有序
-(void)touchesMoved:(NSSet<UITouch *> *)touches withEvent:(UIEvent *)event{
 //做UIView拖拽
 UITouch *touch = [touches anyObject];

 //求偏移量 = 手指当前点的X - 手指上一个点的X
 CGPoint curP = [touch locationInView:self];
 CGPoint preP = [touch previousLocationInView:self];

 NSLog(@"curP====%@",NSStringFromCGPoint(curP));
 NSLog(@"preP====%@",NSStringFromCGPoint(preP));

 CGFloat offsetX = curP.x - preP.x;
 CGFloat offsetY = curP.y - preP.y;

 //平移
 self.transform = CGAffineTransformTranslate(self.transform, offsetX, offsetY);
}

//当手指离开屏幕时调用
-(void)touchesEnded:(NSSet<UITouch *> *)touches withEvent:(UIEvent *)event{

 NSLog(@"%s",__func__);

}

//当发生系统事件时就会调用该方法(电话打入,自动关机)
-(void)touchesCancelled:(NSSet<UITouch *> *)touches withEvent:(UIEvent *)event{

 NSLog(@"%s",__func__);

}

```

1.ios当中常用的事件分为三种:

		触摸事件
		加速计事件
		远程控制事件
		
    2.什么是响应者对象?
    	继承了UIResponds的对象我们称它为响应者对象
    	UIApplication、UIViewController、UIView都继承自UIResponder
    	因此它们都是响应者对象，都能够接收并处理事件

    3.为什么说继承了UIResponder就能够处理事件?
    	因为UIResponder内部提供了以下方法来处理事件
    	
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