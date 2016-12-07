####  模型只保存最重要的数据,导致模型的属性和字典不能一一对应
- KVC根据字典会有问题，模型中不一定有属性，所以现在绕开字典，根据模型到字典中去对应的值就可以了。通过runtime拿到类对象的属性列表，因为属性最后会变成ivar成员变量，所以我们要拿ivar。
- 通过rumtime来获取类的成员变量，第一步导入头文件objc／message。然后要获取这个Ivar数组必须用copy防止修改，因为它是类的所以是类开头class_copyivar之类的方法。
- Ivar:成员变量数组，在runtime头文件里 ;看了下头文件应该是一种数据结构(暂时没学会c++看不懂),不单单是存放变量，里面还有成员变量的类型之类的其它东西，要获取它的名字应该有专门的方法，可能是get打头的方法通过ivar[index]元素作为参数。


```
#import "NSObject+Model.h"
#import <objc/message.h>

@implementation NSObject (Model)

/*
 int a = 2;
 int b = 3;
 int c = 4;
 int arr[] = {a,b,c};
 int *p = arr;
 p[0];
 NSLog(@"%d %d",p[0],p[1]);

 */

// 获取类里面所有方法
// class_copyMethodList(<#__unsafe_unretained Class cls#>, <#unsigned int *outCount#>)// 本质:创建谁的对象


// 获取类里面属性
//  class_copyPropertyList(<#__unsafe_unretained Class cls#>, <#unsigned int *outCount#>)

// Property:属性
+ (instancetype)modelWithDict:(NSDictionary *)dict
{
    id objc = [[self alloc] init];
    
    // runtime:根据模型中属性,去字典中取出对应的value给模型属性赋值
    // 1.获取模型中所有成员变量 key
    // 获取哪个类的成员变量
    // count:成员变量个数
    unsigned int count = 0;
    // 获取成员变量数组
    Ivar *ivarList = class_copyIvarList(self, &count);
    
    // 遍历所有成员变量
    for (int i = 0; i < count; i++) {
        // 获取成员变量
        Ivar ivar = ivarList[i];
        
        // 获取成员变量名字
        NSString *ivarName = [NSString stringWithUTF8String:ivar_getName(ivar)];
        // 获取成员变量类型
        NSString *ivarType = [NSString stringWithUTF8String:ivar_getTypeEncoding(ivar)];
        // @\"User\" -> User
        ivarType = [ivarType stringByReplacingOccurrencesOfString:@"\"" withString:@""];
        ivarType = [ivarType stringByReplacingOccurrencesOfString:@"@" withString:@""];
        // 获取key
        NSString *key = [ivarName substringFromIndex:1];
        
        // 去字典中查找对应value
        // key:user  value:NSDictionary
        
        id value = dict[key];
        
        // 二级转换:判断下value是否是字典,如果是,字典转换层对应的模型
        // 并且是自定义对象才需要转换
        if ([value isKindOfClass:[NSDictionary class]] && ![ivarType hasPrefix:@"NS"]) {
            // 字典转换成模型 userDict => User模型
            // 转换成哪个模型

            // 获取类
            Class modelClass = NSClassFromString(ivarType);
            
            value = [modelClass modelWithDict:value];
        }
        
        // 给模型中属性赋值
        if (value) {
            [objc setValue:value forKey:key];
        }
    }
        
    return objc;
}
```