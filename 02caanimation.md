>作用在根层，和CALayer产生关联

06-CABasicAnimation基础核心动画 
	
	核心动画之作用在层上面.
	动画的本质是改图层的某一个属性.
	CABasicAnimation *anim = [CABasicAnimation animation];
	图层有那些属性,这里才能写那些属性.
	anim.keyPath = @"transform.scale";
	anim.toValue = @0.5;
	告诉动画完成的时候不要移除
	anim.removedOnCompletion = NO;
	保存动画最前面的效果.
	anim.fillMode = kCAFillModeForwards;
	把动画添加到层上面.
	[_redView.layer addAnimation:anim forKey:nil];

11.UIView与核心动画对比?

	1.UIView和核心动画区别?
	   核心动画只能添加到CALayer
	   核心动画一切都是假象，并不会改变真实的值。
	   
	2.什么时候使用UIView的动画?
	  如果需要与用户交互就使用UIView的动画.
	  不需要与用户交互可以使用核心动画
	 
    3.什么场景使用核心动画最多?
          在转场动画中，核心动画的类型比较多
	  根据一个路径做动画，只能用核心动画（帧动画）
	  动画组：同时做多个动画

