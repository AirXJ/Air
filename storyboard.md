# 对比自定义等高cell，需要几个额外的步骤\(iOS8开始才支持\)

* 添加子控件和contentView之间的间距约束，storyboard的label约束右边可以不约束，xib不会出错。

* 设置tableViewCell的真实行高和估算行高，这2句叫做`self-sizing技术，自动计算行高(iOS8 以后)`

  ```
  // 告诉tableView所有cell的真实高度是根据设置的约束自动计算的
  self.tableView.rowHeight = UITableViewAutomaticDimension;
  self.tableView.estimatedRowHeight = 44;
  ```

* 将storyboard中的约束连线，在自定义cell类的模型数据的set方法中修改约束为0


# iOS8之前

* 添加各种约束，但是最后底部控件到底部的那条约束千万别添加进去
* 模型类里添加cellHeight属性，在自定义cell类的模型的set方法中给模型类的cellHeight属性
  ```
  [self layoutIfNeeded];
  if (!self.status.picture) {
  _status.cellHeight = CGRectGetMaxY(self.textContent.frame)+10;
  }else{
  _status.cellHeight = CGRectGetMaxY(self.picView.frame)+10;
  }
  ```


```
- (CGFloat)tableView:(UITableView *)tableView heightForRowAtIndexPath:(NSIndexPath *)indexPath{
 XMGStatus *status = self.statuses[indexPath.row];
 return status.cellHeight;
}

```

```
//从xib或storyboard加载控件，只调用一次
- (void)awakeFromNib{
    [super awakeFromNib];
    //手动设置label的最大宽度属性(让label能够计算出自己最真实的尺寸)
    self.textContent.preferredMaxLayoutWidth = [UIScreen mainScreen].bounds.size.width- 20.0;
}
```

* 调用estimatedHeightForRowAtIndexPath方法，或者使用self.tableView.estimatedRowHeight = ??，这样会快速加载提高性能;

