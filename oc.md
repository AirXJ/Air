getter、setter方法统称访问器(accessor)方法
@synthesize 生成的实例变量不会以下划线开头，并且这些实例变量是私有的，子类不能访问
static 自动初始化为0，只要分配好内存就一直存在，除非对象销毁。