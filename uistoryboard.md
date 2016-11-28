``` 
//从StoryBaord当中加载控制器
    UIStoryboard *storyBoard = [UIStoryboard storyboardWithName:@"Main" bundle:nil];
    UIViewController *vc = [storyBoard instantiateInitialViewController];
```

//从xib或storyboard加载控件，只调用一次

- (void)awakeFromNib
