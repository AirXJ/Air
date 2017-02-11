### 4.第三方框架

（1）SDWebImage基本使用

```objc
    01 设置imageView的图片
    [cell.imageView sd_setImageWithURL:[NSURL URLWithString:app.icon] placeholderImage:[UIImage imageNamed:@"placehoder"]];

    02 设置图片并计算下载进度
       //下载并设置图片
    /*
     第一个参数：要下载图片的url地址
     第二个参数：设置该imageView的占位图片
     第三个参数：传一个枚举值，告诉程序你下载图片的策略是什么
     第一个block块：获取当前图片数据的下载进度
         receivedSize：已经下载完成的数据大小
         expectedSize：该文件的数据总大小
     第二个block块：当图片下载完成之后执行该block中的代码
         image:下载得到的图片数据
         error:下载出现的错误信息
         SDImageCacheType：图片的缓存策略（不缓存，内存缓存，沙盒缓存）
         imageURL：下载的图片的url地址
     */
    [cell.imageView sd_setImageWithURL:[NSURL URLWithString:app.icon] placeholderImage:[UIImage imageNamed:@"placehoder"] options:SDWebImageRetryFailed progress:^(NSInteger receivedSize, NSInteger expectedSize) {

        //计算当前图片的下载进度
        NSLog(@"%.2f",1.0 *receivedSize / expectedSize);

    } completed:^(UIImage *image, NSError *error, SDImageCacheType cacheType, NSURL *imageURL) {

    }];

    03 系统级内存警告如何处理（面试）
    //取消当前正在进行的所有下载操作
    [[SDWebImageManager sharedManager] cancelAll];

    //清除缓存数据(面试)
    //cleanDisk：删除过期的文件数据，计算当前未过期的已经下载的文件数据的大小，如果发现该数据大小大于我们设置的最大缓存数据大小，那么程序内部会按照按文件数据缓存的时间从远到近删除，知道小于最大缓存数据为止。

    //clearMemory:直接删除文件，重新创建新的文件夹
    //[[SDWebImageManager sharedManager].imageCache cleanDisk];
    [[SDWebImageManager sharedManager].imageCache clearMemory];

    04 SDWebImage默认的缓存时间是1周
    05 如何播放gif图片
    /*
    5-1 把用户传入的gif图片->NSData
    5-2 根据该Data创建一个图片数据源（NSData->CFImageSourceRef）
    5-3 计算该数据源中一共有多少帧，把每一帧数据取出来放到图片数组中
    5-4 根据得到的数组+计算的动画时间-》可动画的image
    [UIImage animatedImageWithImages:images duration:duration];
    */

    06 如何判断当前图片类型
    + (NSString *)sd_contentTypeForImageData:(NSData *)data;
```


***


####0.第三方框架SDWebImage

（1）SDWebImage基本使用
```objc
01 设置imageView的图片
[cell.imageView sd_setImageWithURL:[NSURL URLWithString:app.icon] placeholderImage:[UIImage imageNamed:@"placehoder"]];

02 设置图片并计算下载进度
//下载并设置图片
/*
第一个参数：要下载图片的url地址
第二个参数：设置该imageView的占位图片
第三个参数：传一个枚举值，告诉程序你下载图片的策略是什么
第一个block块：获取当前图片数据的下载进度
receivedSize：已经下载完成的数据大小
expectedSize：该文件的数据总大小
第二个block块：当图片下载完成之后执行该block中的代码
image:下载得到的图片数据
error:下载出现的错误信息
SDImageCacheType：图片的缓存策略（不缓存，内存缓存，沙盒缓存）
imageURL：下载的图片的url地址
*/
[cell.imageView sd_setImageWithURL:[NSURL URLWithString:app.icon] placeholderImage:[UIImage imageNamed:@"placehoder"] options:SDWebImageRetryFailed progress:^(NSInteger receivedSize, NSInteger expectedSize) {

//计算当前图片的下载进度
NSLog(@"%.2f",1.0 *receivedSize / expectedSize);

} completed:^(UIImage *image, NSError *error, SDImageCacheType cacheType, NSURL *imageURL) {

}];

03 系统级内存警告如何处理（面试）
//取消当前正在进行的所有下载操作
[[SDWebImageManager sharedManager] cancelAll];

//清除缓存数据(面试)
//cleanDisk：删除过期的文件数据，计算当前未过期的已经下载的文件数据的大小，如果发现该数据大小大于我们设置的最大缓存数据大小，那么程序内部会按照按文件数据缓存的时间从远到近删除，知道小于最大缓存数据为止。

//clearMemory:直接删除文件，重新创建新的文件夹
//[[SDWebImageManager sharedManager].imageCache cleanDisk];
[[SDWebImageManager sharedManager].imageCache clearMemory];

04 SDWebImage默认的缓存时间是1周
05 如何播放gif图片
/*
5-1 把用户传入的gif图片->NSData
5-2 根据该Data创建一个图片数据源（NSData->CFImageSourceRef）
5-3 计算该数据源中一共有多少帧，把每一帧数据取出来放到图片数组中
5-4 根据得到的数组+计算的动画时间-》可动画的image
[UIImage animatedImageWithImages:images duration:duration];
*/

06 如何判断当前图片类型，只判断图片二进制数据的第一个字节
+ (NSString *)sd_contentTypeForImageData:(NSData *)data;

07 内部如何进行缓存处理？使用了NSCache类，使用和NSDictionary类似
08 沙盒缓存图片的命名方式为对该图片的URL进行MD5加密 echo -n "url" |MD5
09 当接收到内存警告之后，内部会自动清理内存缓存
10 图片的下载顺序，默认是先进先出的

```
（2）SDWebImage内部结构
![](/assets/1.png)



---

