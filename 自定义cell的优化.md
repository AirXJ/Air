# tableview性能优化-cell的循环利用
- `只要cellForRowIndexPath方法一调用,我们就要调用dequeueReusableCellWithIdentifier方法从缓存池取cell，不再需要你重复创建cell;而且注册cell的方式比自己创建cell效率要高。`
- `重用标志`用`static`关键字修饰可以提高运算效率
- `- (void)layoutSubviews` `- (CGFloat)tableView:(UITableView *)tableView heightForRowAtIndexPath:(NSIndexPath *)indexPath`如果frame计算写在这两个方法中，影响性能非常严重，我们把计算的方法放到模型数组中，只需要计算一次。
- heightForRowAtIndexPath这个方法会调用所有的cell个数次数，直到计算出滚动条的长度，然后才开始调用cellForRowAtIndexPath方法，我们 只要设置了估算高度，就只会调用铺满一个屏幕的cell，不会再加载所有cell了。




```obj
//注册方法别写在cellForRowIndexPath方法里，一般在ViewDidLoad里
[self.tableView registerClass:[UITableViewCell class] forCellReuseIdentifier:ID];

static ID = @"indentifier";
UITableViewCell *cell = [tableView dequeueReusableCellWithIdentifier:ID];

```

