# tableview性能优化-cell的循环利用
- `只要cellForRowIndexPath方法一调用,我们就要调用从缓存池里取cell复用cell的方法，不再需要你重复创建cell;而且注册cell的方式比自己创建cell效率要高。`

```
[self.tableView registerClass:[UITableViewCell class] forCellReuseIdentifier:ID];

static ID = @"indentifier";
UITableViewCell *cell = [tableView dequeueReusableCellWithIdentifier:ID];

```