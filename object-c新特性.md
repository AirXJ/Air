### Object-C常见关键字用法

```
null_resettable:必须要处理为空情况,重写get方法,这个关键字只能在括号里写
null_resettable作用:get方法不能返回nil,set可以传入为空
_Null_unspecified:不确定是否为空
关键字注意点
在NS_ASSUME_NONNULL_BEGIN和NS_ASSUME_NONNULL_END之间默认是nonnull
```

关键字不能用于基本数据类型\(int,float\),nil只用于对象

```
在属性的括号里敲n有提示
 nonnull 语法2 * 关键字 变量名
 @property (nonatomic, strong/*,nullable*/) NSString * _Nonnull name;
 nonnull 语法3 这个写法不推荐，不能上架
 @property (nonatomic, strong) NSString * __nonnull name;
```

## 泛型声明定义

```
//声明
@interface Person<ObjectType> : NSObject
//定义，如果没有定义泛型.默认就是id，就没法用点语法了。
 Person<iOS *> *p = [[Person alloc] init];
 p.language = ios;
```

### 泛型中用于父子类型的转换,注意单词拼写

```
__covariant:协变,子类转父类，记忆方法，正常，人都会做父亲
__contravariant:逆变,父类转子类,记忆方法，大逆不道
//都是用在父类里
@interface Person<__covariant ObjectType> : NSObject
 泛型注意点:在数组中,一般用可变数组添加方法,泛型才会生效,如果使用不可变数组,添加元素,泛型没有效果

```

### 关键字__kindof:相当于
表示当前类或者它的子类
其他知识扩展:id和instancetype的区别，编译时检查识别当前类的对象。id可以调用任何对象的方法，不能在编译时检测。










