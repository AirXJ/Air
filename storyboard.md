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

- heightForRowAtIndexPath这个方法会调用所有的cell个数次数，直到计算出滚动条的长度，然后才开始调用cellForRowAtIndexPath方法，我们只要调用estimatedHeightForRowAtIndexPath方法，就只会调用铺满一个屏幕的cell，不会再加载所有cell了，系统会帮助我们估算出滚动条的大小,会执将heightForRowAtIndexPath替换成estimatedHeightForRowAtIndexPath，提高了性能。