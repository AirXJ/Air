\#第四天

\#\#\#0 补充（static）

```
static关键字会在声明变量的时候分配内存，在程序运行期间只分配一次内存。之后再访问时，实际都是在访问原先分配的内存

如果使用static来修饰局部变量，那么局部变量在代码块结束后将不会回收，下次使用保持上次使用后的值。

如果使用static来修饰全局变量，那么表示该全局变量只在本文件中有效，外界无法使用extern来引用。static变量的作用域被限制在定义变量的当前文件中，其它文件是不能访问的。
```

\#\#\#\#1.NSURLConnection使用

* 1.1 NSURLConnection同步请求（GET）

（1）步骤

```
    01 设置请求路径

    02 创建请求对象（默认是GET请求，且已经默认包含了请求头）

    03 使用NSURLSession sendsync方法发送网络请求

    04 接收到服务器的响应后，解析响应体
```

（2）相关代码

\`\`\`objc

//1.确定请求路径

```
NSURL \*url = \[NSURL URLWithString:@"http://120.25.226.186:32812/login?username=520it&pwd=520it&type=XML"\];
```

//    NSURL \*url = \[NSURL URLWithString:@"[http://120.25.226.186:32812/video?type=XML"\](http://120.25.226.186:32812/video?type=XML"\)\];

```
//2.创建一个请求对象

NSURLRequest \*request = \[NSURLRequest requestWithURL:url\];



//3.把请求发送给服务器

//sendSynchronousRequest  阻塞式的方法，会卡住线程



NSHTTPURLResponse \*response = nil;

NSError \*error = nil;



/\*

 第一个参数：请求对象

 第二个参数：响应头信息，当该方法执行完毕之后，该参数被赋值

 第三个参数：错误信息，如果请求失败，则error有值

 \*/

 //该方法是阻塞式的，会卡住线程

NSData \*data = \[NSURLConnection sendSynchronousRequest:request returningResponse:&response error:&error\];



//4.解析服务器返回的数据

NSString \*str = \[\[NSString alloc\]initWithData:data encoding:NSUTF8StringEncoding\];
```

\`\`\`

* 1.2 NSURLConnection异步请求（GET-SendAsync）

（1）相关说明

```
01 该方法不会卡住当前线程，网络请求任务是异步执行的
```

（2）相关代码

\`\`\`objc

//1.确定请求路径

```
NSURL \*url = \[NSURL URLWithString:@"http://120.25.226.186:32812/login?username=520it&pwd=520it"\];



//2.创建一个请求对象

NSURLRequest \*request = \[NSURLRequest requestWithURL:url\];



//3.把请求发送给服务器,发送一个异步请求

/\*

 第一个参数：请求对象

 第二个参数：回调方法在哪个线程中执行，如果是主队列则block在主线程中执行，非主队列则在子线程中执行

 第三个参数：completionHandlerBlock块：接受到响应的时候执行该block中的代码

    response：响应头信息

    data：响应体

    connectionError：错误信息，如果请求失败，那么该参数有值

 \*/

\[NSURLConnection sendAsynchronousRequest:request queue:\[\[NSOperationQueue alloc\]init\] completionHandler:^\(NSURLResponse \* \_\_nullable response, NSData \* \_\_nullable data, NSError \* \_\_nullable connectionError\) {



    //4.解析服务器返回的数据

    NSString \*str = \[\[NSString alloc\]initWithData:data encoding:NSUTF8StringEncoding\];

    //转换并打印响应头信息

    NSHTTPURLResponse \*r = \(NSHTTPURLResponse \*\)response;

    NSLog\(@"--%zd---%@--",r.statusCode,r.allHeaderFields\);

}\];
```

\`\`\`

* 1.3 NSURLConnection异步请求（GET-代理）

（1）步骤

```
01 确定请求路径

02 创建请求对象

03 创建NSURLConnection对象并设置代理

04 遵守NSURLConnectionDataDelegate协议，并实现相应的代理方法

05 在代理方法中监听网络请求的响应
```

（2）设置代理的几种方法

\`\`\`objc

/\*

```
 设置代理的第一种方式：自动发送网络请求

 \[\[NSURLConnection alloc\]initWithRequest:request delegate:self\];

 \*/



/\*

 设置代理的第二种方式：

 第一个参数：请求对象

 第二个参数：谁成为NSURLConnetion对象的代理

 第三个参数：是否马上发送网络请求，如果该值为YES则立刻发送，如果为NO则不会发送网路请求

 NSURLConnection \*conn = \[\[NSURLConnection alloc\]initWithRequest:request delegate:self startImmediately:NO\];



 //调用该方法控制网络请求的发送

 \[conn start\];

 \*/



//设置代理的第三种方式：使用类方法设置代理，会自动发送网络请求

NSURLConnection \*conn = \[NSURLConnection connectionWithRequest:request delegate:self\];

//取消网络请求

//\[conn cancel\];
```

\`\`\`

（3）相关的代理方法

\`\`\`objc

/\*

1.当接收到服务器响应的时候调用

第一个参数connection：监听的是哪个NSURLConnection对象

第二个参数response：接收到的服务器返回的响应头信息

\*/

* \(void\)connection:\(nonnull NSURLConnection \*\)connection didReceiveResponse:\(nonnull NSURLResponse \*\)response

/\*

2.当接收到数据的时候调用，该方法会被调用多次

第一个参数connection：监听的是哪个NSURLConnection对象

第二个参数data：本次接收到的服务端返回的二进制数据（可能是片段）

\*/

* \(void\)connection:\(nonnull NSURLConnection \*\)connection didReceiveData:\(nonnull NSData \*\)data

/\*

3.当服务端返回的数据接收完毕之后会调用

通常在该方法中解析服务器返回的数据

\*/

-\(void\)connectionDidFinishLoading:\(nonnull NSURLConnection \*\)connection

/\*4.当请求错误的时候调用（比如请求超时）

第一个参数connection：NSURLConnection对象

第二个参数：网络请求的错误信息，如果请求失败，则error有值

\*/

* \(void\)connection:\(nonnull NSURLConnection \*\)connection didFailWithError:\(nonnull NSError \*\)error

\`\`\`

（4）其它知识点

\`\`\`objc

```
01 关于消息弹窗第三方框架的使用

    SVProgressHUD

02 字符串截取相关方法

- \(NSRange\)rangeOfString:\(NSString \*\)searchString;

- \(NSString \*\)substringWithRange:\(NSRange\)range;
```

\`\`\`

* 1.4 NSURLConnection发送POST请求

（1）发送POST请求步骤

```
a.确定URL路径

b.创建请求对象（可变对象）

c.修改请求对象的方法为POST，设置请求体（Data）

d.发送一个异步请求

e.补充：设置请求超时，处理错误信息，设置请求头（如获取客户端的版本等等,请求头是可设置可不设置的）
```

（2）相关代码

\`\`\`objc

//1.确定请求路径

```
NSURL \*url = \[NSURL URLWithString:@"http://120.25.226.186:32812/login"\];



//2.创建请求对象

NSMutableURLRequest \*request = \[NSMutableURLRequest requestWithURL:url\];



//2.1更改请求方法

request.HTTPMethod = @"POST";



//2.2设置请求体

request.HTTPBody = \[@"username=520it&pwd=520it" dataUsingEncoding:NSUTF8StringEncoding\];



//2.3请求超时

request.timeoutInterval = 5;



//2.4设置请求头

\[request setValue:@"ios 9.0" forHTTPHeaderField:@"User-Agent"\];





//3.发送请求

\[NSURLConnection sendAsynchronousRequest:request queue:\[NSOperationQueue mainQueue\] completionHandler:^\(NSURLResponse \* \_\_nullable response, NSData \* \_\_nullable data, NSError \* \_\_nullable connectionError\) {



    //4.解析服务器返回的数据

    if \(connectionError\) {

        NSLog\(@"--请求失败-"\);

    }else

    {

        NSLog\(@"%@",\[\[NSString alloc\]initWithData:data encoding:NSUTF8StringEncoding\]\);

    }



}\];
```

\`\`\`

* 1.5 URL中文转码问题

\`\`\`objc

//1.确定请求路径

```
NSString \*urlStr = @"http://120.25.226.186:32812/login2?username=小码哥&pwd=520it";

NSLog\(@"%@",urlStr\);

//中文转码操作

urlStr =  \[urlStr stringByAddingPercentEscapesUsingEncoding:NSUTF8StringEncoding\];

NSLog\(@"%@",urlStr\);



NSURL \*url = \[NSURL URLWithString:urlStr\];
```

\`\`\`

\#\#\# 2.0 JSON解析

* 2.1 JSON简单介绍

```
001 问：什么是JSON

    答：

    （1）JSON是一种轻量级的数据格式，一般用于数据交互

    （2）服务器返回给客户端的数据，一般都是JSON格式或者XML格式（文件下载除外）

002 相关说明

    （1）JSON的格式很像OC中的字典和数组

    （2）标准JSON格式key必须是双引号

003 JSON解析方案

    a.第三方框架  JSONKit\SBJSON\TouchJSON

    b.苹果原生（NSJSONSerialization）
```

* 2.2  JSON解析相关代码

（1）json数据-&gt;OC对象

\`\`\`objc

//把json数据转换为OC对象

-\(void\)jsonToOC

{

```
//1. 确定url路径

NSURL \*url = \[NSURL URLWithString:@"http://120.25.226.186:32812/login?username=33&pwd=33&type=JSON"\];



//2.创建一个请求对象

NSURLRequest \*request = \[NSURLRequest requestWithURL:url\];



//3.使用NSURLSession发送一个异步请求

\[NSURLConnection sendAsynchronousRequest:request queue:\[NSOperationQueue mainQueue\] completionHandler:^\(NSURLResponse \* \_Nullable response, NSData \* \_Nullable data, NSError \* \_Nullable connectionError\) {



    //4.当接收到服务器响应的数据后，解析数据\(JSON---&gt;OC\)



    /\*

     第一个参数：要解析的JSON数据，是NSData类型也就是二进制数据

     第二个参数: 解析JSON的可选配置参数

     NSJSONReadingMutableContainers 解析出来的字典和数组是可变的

     NSJSONReadingMutableLeaves 解析出来的对象中的字符串是可变的  iOS7以后有问题

     NSJSONReadingAllowFragments 被解析的JSON数据如果既不是字典也不是数组, 那么就必须使用这个

     \*/

    NSDictionary \*dict = \[NSJSONSerialization JSONObjectWithData:data options:kNilOptions error:nil\];

    NSLog\(@"%@",dict\);



}\];
```

}

\`\`\`

（2）OC对象-&gt;JSON对象

\`\`\`objc

//1.要转换成JSON数据的OC对象\*这里是一个字典

```
NSDictionary \*dictM = @{

                        @"name":@"wendingding",

                        @"age":@100,

                        @"height":@1.72

                        };

//2.OC-&gt;JSON

/\*

 注意：可以通过+ \(BOOL\)isValidJSONObject:\(id\)obj;方法判断当前OC对象能否转换为JSON数据

 具体限制：

     1.obj 是NSArray 或 NSDictionay 以及他们派生出来的子类

     2.obj 包含的所有对象是NSString,NSNumber,NSArray,NSDictionary 或NSNull

     3.字典中所有的key必须是NSString类型的

     4.NSNumber的对象不能是NaN或无穷大

 \*/

/\*

 第一个参数：要转换成JSON数据的OC对象，这里为一个字典

 第二个参数：NSJSONWritingPrettyPrinted对转换之后的JSON对象进行排版，无意义

 \*/

NSData \*data = \[NSJSONSerialization dataWithJSONObject:dictM options:NSJSONWritingPrettyPrinted error:nil\];



//3.打印查看Data是否有值

/\*

 第一个参数：要转换为STring的二进制数据

 第二个参数：编码方式，通常采用NSUTF8StringEncoding

 \*/

NSString \*strM = \[\[NSString alloc\]initWithData:data encoding:NSUTF8StringEncoding\];

NSLog\(@"%@",strM\);
```

\`\`\`

（3）OC对象和JSON数据格式之间的一一对应关系

\`\`\`objc

//OC对象和JSON数据之间的一一对应关系

-\(void\)oCWithJSON

{

```
//JSON的各种数据格式

//NSString \*test = @"\"wendingding\"";

//NSString \*test = @"true";

NSString \*test = @"{\"name\":\"wendingding\"}";



//把JSON数据-&gt;OC对象,以便查看他们之间的一一对应关系

//注意点：如何被解析的JSON数据如果既不是字典也不是数组（比如是NSString）, 那么就必须使用这NSJSONReadingAllowFragments

id obj = \[NSJSONSerialization JSONObjectWithData:\[test dataUsingEncoding:NSUTF8StringEncoding\] options:NSJSONReadingAllowFragments error:nil\];



NSLog\(@"%@", \[obj class\]\);





/\* JSON数据格式和OC对象的一一对应关系

     {} -&gt; 字典

     \[\] -&gt; 数组

     "" -&gt; 字符串

     10/10.1 -&gt; NSNumber

     true/false -&gt; NSNumber

     null -&gt; NSNull

 \*/
```

}

}

\`\`\`

（4）如何查看复杂的JSON数据

\`\`\`objc

方法一：

```
在线格式化http://tool.oschina.net/codeformat/json
```

方法二：

```
把解析后的数据写plist文件，通过plist文件可以直观的查看JSON的层次结构。

\[dictM writeToFile:@"/Users/文顶顶/Desktop/videos.plist" atomically:YES\];
```

\`\`\`

（5）视频的简单播放

\`\`\`objc

```
//0.需要导入系统框架

\#import &lt;MediaPlayer/MediaPlayer.h&gt;



//1.拿到该cell对应的数据字典

XMGVideo \*video = self.videos\[indexPath.row\];



NSString \*videoStr = \[@"http://120.25.226.186:32812" stringByAppendingPathComponent:video.url\];



//2.创建一个视频播放器

MPMoviePlayerViewController \*vc = \[\[MPMoviePlayerViewController alloc\]initWithContentURL:\[NSURL URLWithString:videoStr\]\];

//3.present播放控制器



\[self presentViewController:vc animated:YES completion:nil\];
```

\`\`\`

* 2.3 字典转模型框架

（1）相关框架

```
 a.Mantle 需要继承自MTModel

 b.JSONModel 需要继承自JSONModel

 c.MJExtension 不需要继承，无代码侵入性
```

（2）自己设计和选择框架时需要注意的问题

```
a.侵入性

b.易用性，是否容易上手

c.扩展性，很容易给这个框架增加新的功能
```

（3）MJExtension框架的简单使用

\`\`\`objc

//1.把字典数组转换为模型数组

```
//使用MJExtension框架进行字典转模型

    self.videos = \[XMGVideo objectArrayWithKeyValuesArray:videoArray\];
```

//2.重命名模型属性的名称

//第一种重命名属性名称的方法，有一定的代码侵入性

//设置字典中的id被模型中的ID替换

+\(NSDictionary \*\)replacedKeyFromPropertyName

{

```
return @{

         @"ID":@"id"

         };
```

}

//第二种重命名属性名称的方法，代码侵入性为零

```
\[XMGVideo setupReplacedKeyFromPropertyName:^NSDictionary \*{

    return @{

             @"ID":@"id"

             };

}\];
```

//3.MJExtension框架内部实现原理-运行时

\`\`\`

\#\#\# 3.0 XML解析

* 3.1 XML简单介绍

（1） XML：可扩展标记语言

```
    a.语法

    b.XML文档的三部分（声明、元素和属性）

    c.其它注意点（注意不能交叉包含、空行换行、XML文档只能有一个根元素等）
```

（2） XML解析

```
    a.XML解析的两种方式

        001 SAX:从根元素开始，按顺序一个元素一个元素的往下解析，可用于解析大、小文件

        002 DOM:一次性将整个XML文档加载到内存中，适合较小的文件

    b.解析XML的工具

        001 苹果原生NSXMLParser:使用SAX方式解析，使用简单

        002 第三方框架

            libxml2:纯C语言的，默认包含在iOS SDK中，同时支持DOM和SAX的方式解析

            GDataXML:采用DOM方式解析，该框架由Goole开发，是基于xml2的
```

* 3.2 XML解析

（1）使用NSXMLParser解析XML步骤和代理方法

\`\`\`objc

//解析步骤：

//4.1 创建一个解析器

NSXMLParser \*parser = \[\[NSXMLParser alloc\]initWithData:data\];

//4.2 设置代理

parser.delegate = self;

//4.3 开始解析

\[parser parse\];

---

//1.开始解析XML文档

-\(void\)parserDidStartDocument:\(nonnull NSXMLParser \*\)parser

//2.开始解析XML中某个元素的时候调用，比如&lt;video&gt;

-\(void\)parser:\(nonnull NSXMLParser \*\)parser didStartElement:\(nonnull NSString \*\)elementName namespaceURI:\(nullable NSString \*\)namespaceURI qualifiedName:\(nullable NSString \*\)qName attributes:\(nonnull NSDictionary&lt;NSString \*,NSString \*&gt; \*\)attributeDict

{

```
if \(\[elementName isEqualToString:@"videos"\]\) {

    return;

}

//字典转模型

XMGVideo \*video = \[XMGVideo objectWithKeyValues:attributeDict\];

\[self.videos addObject:video\];
```

}

//3.当某个元素解析完成之后调用，比如&lt;/video&gt;

-\(void\)parser:\(nonnull NSXMLParser \*\)parser didEndElement:\(nonnull NSString \*\)elementName namespaceURI:\(nullable NSString \*\)namespaceURI qualifiedName:\(nullable NSString \*\)qName

//4.XML文档解析结束

-\(void\)parserDidEndDocument:\(nonnull NSXMLParser \*\)parser

\`\`\`

（2）使用GDataParser解析XML的步骤和方法

\`\`\`objc

//4.0 配置环境

// 001 先导入框架，然后按照框架使用注释配置环境

// 002 GDataXML框架是MRC的，所以还需要告诉编译器以MRC的方式处理GDataXML的代码

//4.1 加载XML文档（使用的是DOM的方式一口气把整个XML文档都吞下）

```
GDataXMLDocument \*doc = \[\[GDataXMLDocument alloc\]initWithData:data options:kNilOptions error:nil\];
```

//4.2 获取XML文档的根元素，根据根元素取出XML中的每个子元素

NSArray \* elements = \[doc.rootElement elementsForName:@"video"\];

//4.3 取出每个子元素的属性并转换为模型

for \(GDataXMLElement \*ele in elements\) {

```
XMGVideo \*video = \[\[XMGVideo alloc\]init\];

video.name = \[ele attributeForName:@"name"\].stringValue;

video.length = \[ele attributeForName:@"length"\].stringValue.integerValue;

video.url = \[ele attributeForName:@"url"\].stringValue;

video.image = \[ele attributeForName:@"image"\].stringValue;

video.ID = \[ele attributeForName:@"id"\].stringValue;



//4.4 把转换好的模型添加到tableView的数据源self.videos数组中

\[self.videos addObject:video\];
```

}

\`\`\`

* 3.3 多值参数和中文输出问题

（1）多值参数如何设置请求路径

\`\`\`objc

//多值参数

/\*

如果一个参数对应着多个值，那么直接按照"参数=值&参数=值"的方式拼接

\*/

-\(void\)test

{

```
//1.确定URL

NSURL \*url = \[NSURL URLWithString:@"http://120.25.226.186:32812/weather?place=Beijing&place=Guangzhou"\];

//2.创建请求对象

NSURLRequest \*request = \[NSURLRequest requestWithURL:url\];



//3.发送请求

\[NSURLConnection sendAsynchronousRequest:request queue:\[NSOperationQueue mainQueue\] completionHandler:^\(NSURLResponse \* \_Nullable response, NSData \* \_Nullable data, NSError \* \_Nullable connectionError\) {



    //4.解析

    NSLog\(@"%@",\[NSJSONSerialization JSONObjectWithData:data options:kNilOptions error:nil\]\);

}\];
```

}

\`\`\`

（2）如何解决字典和数组中输出乱码的问题

\`\`\`objc

答：给字典和数组添加一个分类，重写descriptionWithLocale方法，在该方法中拼接元素格式化输出。

-\(nonnull NSString \*\)descriptionWithLocale:\(nullable id\)locale

\`\`\`

\#\#\# 4.0 文件下载

* 4.1 小文件下载

（1）第一种方式（NSData）

\`\`\`objc

//使用NSDta直接加载网络上的url资源（不考虑线程）

-\(void\)dataDownload

{

```
//1.确定资源路径

NSURL \*url = \[NSURL URLWithString:@"http://120.25.226.186:32812/resources/images/minion\_01.png"\];



//2.根据URL加载对应的资源

NSData \*data = \[NSData dataWithContentsOfURL:url\];



//3.转换并显示数据

UIImage \*image = \[UIImage imageWithData:data\];

self.imageView.image = image;
```

}

\`\`\`

（2）第二种方式（NSURLConnection-sendAsync）

\`\`\`objc

//使用NSURLConnection发送异步请求下载文件资源

-\(void\)connectDownload

{

```
//1.确定请求路径

NSURL \*url = \[NSURL URLWithString:@"http://120.25.226.186:32812/resources/images/minion\_01.png"\];



//2.创建请求对象

NSURLRequest \*request = \[NSURLRequest requestWithURL:url\];



//3.使用NSURLConnection发送一个异步请求

\[NSURLConnection sendAsynchronousRequest:request queue:\[NSOperationQueue mainQueue\] completionHandler:^\(NSURLResponse \* \_Nullable response, NSData \* \_Nullable data, NSError \* \_Nullable connectionError\) {

    //4.拿到并处理数据

    UIImage \*image = \[UIImage imageWithData:data\];

    self.imageView.image = image;



}\];
```

}

\`\`\`

（3）第三种方式（NSURLConnection-delegate）

\`\`\`objc

//使用NSURLConnection设置代理发送异步请求的方式下载文件

-\(void\)connectionDelegateDownload

{

```
//1.确定请求路径

NSURL \*url = \[NSURL URLWithString:@"http://120.25.226.186:32812/resources/videos/minion\_01.mp4"\];



//2.创建请求对象

NSURLRequest \*request = \[NSURLRequest requestWithURL:url\];



//3.使用NSURLConnection设置代理并发送异步请求

\[NSURLConnection connectionWithRequest:request delegate:self\];
```

}

\#pragma mark--NSURLConnectionDataDelegate

//当接收到服务器响应的时候调用，该方法只会调用一次

-\(void\)connection:\(NSURLConnection \*\)connection didReceiveResponse:\(NSURLResponse \*\)response

{

```
//创建一个容器，用来接收服务器返回的数据

self.fileData = \[NSMutableData data\];



//获得当前要下载文件的总大小（通过响应头得到）

NSHTTPURLResponse \*res = \(NSHTTPURLResponse \*\)response;

self.totalLength = res.expectedContentLength;

NSLog\(@"%zd",self.totalLength\);



//拿到服务器端推荐的文件名称

self.fileName = res.suggestedFilename;
```

}

//当接收到服务器返回的数据时会调用

//该方法可能会被调用多次

-\(void\)connection:\(NSURLConnection \*\)connection didReceiveData:\(NSData \*\)data

{

//    NSLog\(@"%s",\_\_func\_\_\);

```
//拼接每次下载的数据

\[self.fileData appendData:data\];



//计算当前下载进度并刷新UI显示

self.currentLength = self.fileData.length;



NSLog\(@"%f",1.0\* self.currentLength/self.totalLength\);

self.progressView.progress = 1.0\* self.currentLength/self.totalLength;
```

}

//当网络请求结束之后调用

-\(void\)connectionDidFinishLoading:\(NSURLConnection \*\)connection

{

```
//文件下载完毕把接受到的文件数据写入到沙盒中保存



//1.确定要保存文件的全路径

//caches文件夹路径

NSString \*caches = \[NSSearchPathForDirectoriesInDomains\(NSCachesDirectory, NSUserDomainMask, YES\) lastObject\];



NSString \*fullPath = \[caches stringByAppendingPathComponent:self.fileName\];



//2.写数据到文件中

\[self.fileData writeToFile:fullPath atomically:YES\];



NSLog\(@"%@",fullPath\);
```

}

//当请求失败的时候调用该方法

-\(void\)connection:\(NSURLConnection \*\)connection didFailWithError:\(NSError \*\)error

{

```
NSLog\(@"%s",\_\_func\_\_\);
```

}

\`\`\`



