* ## **`cell.contentview是cell里所有控件的父视图`**

- cell的循环重用，分为3种
  - 故事板、xib注册 
  - 代码注册 
  - 自己new

## cell的一些属性
`优先级是backgroudview高`
![](/assets/cell背景色设置.png)
cell.selectionstyle = UITableViewCellSelectionStyleNone;

- xib创建和注册cell
```
[[NSBundle mainBundle] loadNibName:NSStringFromClass([cell类 class]) owner:nil options:nil] lastObject]
```

```
UINib *nib = [UINib nibWithNibName:NSStringFromClass([cell类 class]) bundle:nil];
[self.tableView registerNib:nib forCellReuseIdentifier:@"A"]
```