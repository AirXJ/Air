>按钮的图片状态区别，纯色一般是setbackgroundimage景图片，可以拉伸；setimage是内容图片大小不能随意拉伸.
[^设置按钮的类型职能在初始化的时候设置]

- 设置按钮的类型只能在初始化的时候设置
![](/assets/屏幕快照 2017-01-08 15.18.06.png)
- 监听按钮点击事件［故事板按住control点击鼠标连接到控制器或者uiview］
UIControlEventTouchDown touchbegin
UIControlEventTouchUpInside touchend

>@interface UIControl : UIView
@property(nonatomic,getter=isEnabled) BOOL enabled;   没有输入内容登陆按钮不可点击，在这个状态下的按钮内容枚举UIControlStateDisabled;通常是自定义按钮的时候设置这个属性@property(nonatomic,getter=isSelected) BOOL selected; 

```obj
 [button addTarget:self action:@selector(demo:) forControlEvents:UIControlEventTouchUpInside];

```


### 新建自定义按钮,继承重写方法

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
     //子控件的布局imageView、titleLabel是系统定义的，不是自定义的
    self.imageView.frame = CGRectMake(imageX, imageY, imageW, imageH);
    
    self.titleLabel.frame = CGRectMake(labelX, labelY, labelW, labelH);
}

//取消按钮高亮状态下做的事,让按钮马上高亮
-(void)setHighlighted:(BOOL)highlighted {
    
}

```