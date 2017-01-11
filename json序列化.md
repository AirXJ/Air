
######  什么是JSON
- JSON是一种轻量级的数据格式，一般用于数据交互;服务器返回给客户端的数据，一般都是JSON格式或者XML格式（文件下载除外）[^json->oc反序列化]
        

>JSON的格式很像OC中的字典和数组
 [^iOS标准JSON格式key必须是双引号]
 
### NSJSONSerialization序列化工具(性能最好)
[^类方法名是data或者JSONObject、With组合]

![](/assets/屏幕快照 2017-01-11 11.24.46.png)


### OC->JSON 序列化
>注意:并不是所有的OC对象都能转换为JSON
     - 最外层必须是 NSArray or NSDictionary
     - 所有的元素必须是 NSString, NSNumber, NSArray, NSDictionary, or NSNull
     - 字典中所有的key都必须是 NSStrings类型的
     - NSNumbers必须是正式的NSNumber而且不能是无穷大
```         
 BOOL isValid = [NSJSONSerialization isValidJSONObject:strM];
``` 

