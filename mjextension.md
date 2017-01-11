###  可以将plist转换成模型数组
**在NSObject+MJKeyValue.h文件里搜plist或者file每个版本方法名都不一样**
[^多数方法都在NSObject+MJKeyValue.h这个分类里]
###### json反序列化面向模型开发
```
//替换
    [XMGVideo mj_setupReplacedKeyFromPropertyName:^NSDictionary *{
        return @{
                 @"ID":@"id"
                 };
    }];
    //字典转模型
    self.videos = [XMGVideo mj_objectArrayWithKeyValuesArray:dictM[@"videos"]];
```

### 如何学习第三方框架
![](/assets/Snip20170111_3.png)