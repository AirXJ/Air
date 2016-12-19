
UITouch

- 当用户一根手指触摸屏幕时，会创建一个与手指相关联的UITouch对象,默认一般情况就一个手指，如果想多个要设置。
![](/assets/屏幕快照 2016-12-19 14.47.19.png)
- 一根手指对应一个UITouch对象
- UITouch的作用
  - 保存跟手指有关的信息，比如触摸的位置、时间、阶段
  - 当手指移动时，系统会更新一个UITouch对象，使之能够一直保存该手指所在的触摸位置
  - 当手指离开屏幕时，系统会销毁相应的UITouch对象


#4.如何监听UIView的触摸事件?
    	想要监听UIView的触摸事件,首先第一步要自定义UIView,
    	因为只有实现了UIResponder的事件方法才能够监听事件.
        为什么说继承了UIResponder就能够处理事件? 
        因为UIResponder内部提供了以下方法来处理事件

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

   