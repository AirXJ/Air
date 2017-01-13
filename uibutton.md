- 设置按钮的类型只能在初始化的时候设置
![](/assets/屏幕快照 2017-01-08 15.18.06.png)
- 监听按钮点击事件

```obj
 [button addTarget:self action:@selector(demo:) forControlEvents:UIControlEventTouchUpInside];

```


- 新建自定义按钮,继承重写方法

```
//返回当前按钮当中ImageView的位置尺寸
//contentRect:当前按钮的位置尺寸
-(CGRect)imageRectForContentRect:(CGRect)contentRect {
    
    CGFloat w = 40;
    CGFloat h=  48;
    CGFloat x = (contentRect.size.width - w) * 0.5;
    CGFloat y = 20;
   
   return  CGRectMake(x, y, w, h);
}


//返回当前按钮当中Label的位置尺寸
//-(CGRect)titleRectForContentRect:(CGRect)contentRect {
//
//}

-(void)layoutSubviews{
    [super layoutSubviews];
}

//取消按钮高亮状态下做的事,让按钮马上高亮
-(void)setHighlighted:(BOOL)highlighted {
    
}

```