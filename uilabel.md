** `通过字体计算frame`**
```
//计算单行label
NSDictionary *attributes = @{NSFontAttributeName:[UIFont systemFontOfSize:17]};
CGSize size = [self.name.text sizeWithAttributes:attributes];
```

```
//计算多行label高度
CGFloat textH= [self.textContent.text boundingRectWithSize:CGSizeMake(textW, MAXFLOAT) options:NSStringDrawingUsesLineFragmentOrigin attributes:attributes2 context:nil].size.height;
```
![](assets/UILable属性描述.png)

