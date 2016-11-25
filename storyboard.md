# 对比自定义等高cell，需要几个额外的步骤(iOS8开始才支持)
- 添加子控件和contentView之间的间距约束
 

- 设置tableViewCell的真实行高河估算行高，`self-sizing技术，自动计算行高(iOS8 以后)`
```
// 告诉tableView所有cell的真实高度是根据设置的约束自动计算的
self.tableView.rowHeight = UITableViewAutomaticDimension;
self.tableView.estimatedRowHeight = 44;
```

- 将storyboard中的约束连线，在自定义cell类的模型数据的set方法中修改约束为0

# iOS8之前，将自定义cell的IBLayOut属性放到头文件中
- 添加各种约束，但是最后底部控件到底部的那条约束千万别添加进去
- 还要讲自定义cell的子控件放到头文件里去
![](/assets/ios8之前.png)