 null_resettable:必须要处理为空情况,重写get方法,这个关键字只能在括号里写
 null_resettable作用:get方法不能返回nil,set可以传入为空
 _Null_unspecified:不确定是否为空
 关键字注意点
 在NS_ASSUME_NONNULL_BEGIN和NS_ASSUME_NONNULL_END之间默认是nonnull
 关键字不能用于基本数据类型(int,float),nil只用于对象


在属性的括号里敲n有提示
 nonnull 语法2 * 关键字 变量名
 @property (nonatomic, strong/*,nullable*/) NSString * _Nonnull name;

 nonnull 语法3 这个写法不推荐，不能上架
 @property (nonatomic, strong) NSString * __nonnull name;
