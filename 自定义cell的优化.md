# tableview性能优化-cell的循环利用
- `只要cellForRowIndexPath方法一调用,我们就要调用dequeueReusableCellWithIdentifier方法从缓存池取cell，不再需要你重复创建cell;而且注册cell的方式比自己创建cell效率要高。`
- `重用标志`用`static`关键字修饰可以提高方法运行效率


```obj
//注册方法别写在cellForRowIndexPath方法里，一般在ViewDidLoad里
[self.tableView registerClass:[UITableViewCell class] forCellReuseIdentifier:ID];

static ID = @"indentifier";
UITableViewCell *cell = [tableView dequeueReusableCellWithIdentifier:ID];

```