
######  什么是JSON
- JSON是一种轻量级的数据格式，一般用于数据交互;服务器返回给客户端的数据，一般都是JSON格式或者XML格式（文件下载除外）[^json->oc反序列化]
        

>JSON的格式很像OC中的字典和数组
 [^iOS标准JSON格式key必须是双引号]
 
### NSJSONSerialization序列化工具(性能最好)
[^类方法名是data或者JSONObject、With组合]

![](/assets/屏幕快照 2017-01-11 11.24.46.png)
### JSON->OC 反序列化
```
        /*
         第一个参数:JSON的二进制数据
         第二个参数:
         第三个参数:错误信息
         */
        /* 位移枚举第一个值不是0，默认可以是kNilOption提高效率，除非第三种情况。
         NSJSONReadingMutableContainers = (1UL << 0), 可变字典和数组
         NSJSONReadingMutableLeaves = (1UL << 1),      内部所有的字符串都是可变的 ios7之后又问题  一般不用
         NSJSONReadingAllowFragments = (1UL << 2)   既不是字典也不是数组,则必须使用该枚举值
         */
        NSString *strM = @"\"wendingding\"";
        //        NSDictionary *dict = [NSJSONSerialization JSONObjectWithData:data options:kNilOptions error:nil];
        id obj = [NSJSONSerialization JSONObjectWithData:[strM dataUsingEncoding:NSUTF8StringEncoding] options:NSJSONReadingAllowFragments error:nil];
```

### OC->JSON 序列化[^单单字符串不能序列化]
|注意|并不是所有的OC对象都能序列化为JSON|
|:--|------------------------------|
||最外层必须是 NSArray or NSDictionary|
 ||所有的元素必须是 NSString, NSNumber, NSArray, NSDictionary, or NSNull|
| |字典中所有的key都必须是 NSStrings类型的|
||NSNumbers必须是正式的NSNumber而且不能是无穷大|
```         
 BOOL isValid = [NSJSONSerialization isValidJSONObject:strM];
 /*
     第一个参数:要转换的OC对象
     第二个参数:选项NSJSONWritingPrettyPrinted 排版 美观
     */
 NSData *data = [NSJSONSerialization dataWithJSONObject:strM options:NSJSONWritingPrettyPrinted error:nil];
``` 

