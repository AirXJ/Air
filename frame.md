# 给模型类增加frame属性

* 添加所有子控件的frame
* 添加cell的高度\(cellHeight\)属性

```
//模型层
@property (nonatomic,strong)NSString *text;
@property (nonatomic,strong)NSString *picture;
//...等属性
/** 头像frame */
@property (nonatomic,assign)CGRect iconPicFrame;
//...等frame
/** cell高度*/
@property (nonatomic,assign)CGFloat cellHeight;
```

* 利用懒加载重写属性cellHeight的get方法
  ```
  if (_cellHeight == 0) {
      .....
  }
  return _cellHeight;
  ```


# 在控制器中

* 实现一个返回cell高度的代理方法，开始的时候有多少个cell模型就调用多少次该方法，然后拿一个cell就调一次，顺序是cellForRowAtIndexPath、
set数据模型、heightForRowAtIndexPath，执行布满一个屏幕的cell的次数，然后调用一个屏幕的cell个数的layoutsubviews方法。所以你在这个方法里调cellForRowAtIndexPath肯定崩。
  * 在这个方法中返回indexpath位置对应cell的高度
    \`\`\`
  * \(CGFloat\)tableView:\(UITableView _\)tableView heightForRowAtIndexPath:\(NSIndexPath _\)indexPath{
    XMGStatus \*status = self.statuses\[indexPath.row\];
    return status.cellHeight;
    }
    \`\`\` 

* 给cell传递模型数据


```
- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath {
 XMGStatusTableViewCell *cell = [XMGStatusTableViewCell initWithTableView:tableView];
 cell.status = self.statuses[indexPath.row];
 return cell;
}
```

# 新建一个继承自UITableViewCell的子类，比如XMGStatusCell

* 在initWithStyle:reuseIdentifier:方法中
  * 添加子控件
  * 设置子控件的初始化属性\(比如文字颜色、字体\)

* 需要提供一个模型数据属性，重写模型数据的set方法

* 重写layoutSubviews方法，一定要加上\[super layoutSubviews\];
  - 将数据层定义的frame赋给cell层的子控件的frame属性


