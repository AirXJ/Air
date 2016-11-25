方法执行顺序 heightForRowAtIndexPath/estimatedHeightForRowAtIndexPath、cellForRowAtIndexPath(、set模型数据、layout[self layoutIfNeeded手动调用];、heightForRowAtIndexPath、layout[自动布局自动调用]

### - tableview的属性

```
// 设置tableView每一行cell的高度
    self.tableView.rowHeight = 100;
    
    // 设置tableView每一组的头部高度
    self.tableView.sectionHeaderHeight = 80;
    // 设置tableView每一组的尾部高度
//    self.tableView.sectionFooterHeight = 80;
    
    // 设置分割线的颜色
//    self.tableView.separatorColor = [UIColor redColor];
    
    // 设置分割线的样式
    self.tableView.separatorStyle = UITableViewCellSeparatorStyleNone;
    
    // 设置表头控件
    self.tableView.tableHeaderView = [[UISwitch alloc] init];
    // 设置表尾控件
    self.tableView.tableFooterView = [[UISwitch alloc] init];
```


###  代理方法 

```
 /** 

 * 取消选中了某一行cell就会调用这个方法

 */

- (void)tableView:(UITableView *)tableView didDeselectRowAtIndexPath:(NSIndexPath *)indexPath

{

// NSLog(@"取消选中了:%ld",indexPath.row);

}
```