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
### UITableViewDataSource数据源
#####检索索引[^索引显示搜索符号]


```
//右边索引 表头数(如果不实现 就不显示右侧索引)
- (NSArray<NSString *> *)sectionIndexTitlesForTableView:(UITableView *)tableView{
    NSMutableArray *charArr = [NSMutableArray array];
    //和下面等价[charArr addObject:@"{search}"];
    [charArr addObject:UITableViewIndexSearch];
    
    char a[27];
    for(int i=0;i<26;i++)  //大写字母
    {
        a[i] = 'A'+ i;
        if (i == 25) {
            a[i+1] = '\0';
        }
    }
     
    NSString *str = [NSString stringWithCString:a encoding:NSUTF8StringEncoding];
    //改成26就是字母大写的
    for (int i = 0; i < 9; i++) {
        NSString *strA = [str substringWithRange:NSMakeRange(i, 1)];
        [charArr addObject:strA];
    }
    
    return charArr;
}

//点击右侧索引表项时调用
- (NSInteger)tableView:(UITableView *)tableView sectionForSectionIndexTitle:(NSString *)title atIndex:(NSInteger)index {
    NSString *key = [sectionTitleArray objectAtIndex:index];
    NSLog(@"sectionForSectionIndexTitle key=%@",key);
    if (key == UITableViewIndexSearch) {
        [listTableView setContentOffset:CGPointZero animated:NO];
        return NSNotFound;
         }
    return index;
}
```