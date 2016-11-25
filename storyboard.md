# 对比自定义等高cell，需要几个额外的步骤(iOS8开始才支持)
- 添加子控件和contentView之间的间距约束
 

- 设置tableViewCell的真实行高和估算行高，这2句叫做`self-sizing技术，自动计算行高(iOS8 以后)`
```
// 告诉tableView所有cell的真实高度是根据设置的约束自动计算的
self.tableView.rowHeight = UITableViewAutomaticDimension;
self.tableView.estimatedRowHeight = 44;
```

- 将storyboard中的约束连线，在自定义cell类的模型数据的set方法中修改约束为0

# iOS8之前，将自定义cell的IBLayOut属性放到头文件中
- 添加各种约束，但是最后底部控件到底部的那条约束千万别添加进去
- 还要将自定义cell的子控件放到头文件里去
- 
![](/assets/ios8之前.png)这个label不会布局，没有最大宽度属性，平时故事板上都自动带有，这里要手动填写；这里而且不会刷新布局，所以没法得到frame，所以要强制刷新，然后可以得到行高。
```
XMGStatusTableViewCell *cell;
- (CGFloat)tableView:(UITableView *)tableView heightForRowAtIndexPath:(NSIndexPath *)indexPath{
 NSLog(@"aaa----%zd",indexPath.row);
 static NSString *iDentifier = @"statuses";
 if (cell == nil) {
 cell = [self.tableView dequeueReusableCellWithIdentifier:iDentifier];
 }
 cell.status = self.statuses[indexPath.row];
 cell.textContent.preferredMaxLayoutWidth = [UIScreen mainScreen].bounds.size.width- 20.0;
 //要计算控件的frame必须刷新，不然就刷不出label
 [cell layoutIfNeeded];
 CGFloat cellHeight = 0;
 if (!cell.status.picture) {
 cellHeight = CGRectGetMaxY(cell.textContent.frame)+10;
 }else{
 cellHeight = CGRectGetMaxY(cell.picView.frame)+10;
 }
 return cellHeight;
}

```
- 调用estimatedHeightForRowAtIndexPath方法，或者使用self.tableView.estimatedRowHeight = ??，这样会快速加载提高性能;