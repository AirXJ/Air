### SVN介绍
- 1.将服务器的已有的内容下载到本地svn checkout 服务器地址 —username=mgr —password=mgr

- 2.touch main.m :创建main.msvn add main.m : 将main.m添加到svn的管理之下 svn commit -m "初始化项" main.m : 将main.m上传到服务器

- 3.查看文件状态:svn status ?AMD都是需要svn commit -m "注释"

- 4.公司常用的命令svn update : 更新svn commit -m "注释" :将本地的代码提交到服务器

### 在xcode中使用svn的注意点
- 1.如果使 到静态库需要特别注意,必须使 命令 将静态库添加到svn的管理之 下
- 2.如果使 到了storyboard也需要特别注意如果能使 xib,尽量使 xib 如果在项 当中使 到了storyboard,尽量保证只有 个 在操作storyboard
- 3.公司开发技巧(避免冲突)
－ 尽量写一些代码就提交到服务器,时时跟服务器的代码保持同步 
－ 尽量提前半小时提交代码,5.00
![](/assets/屏幕快照 2017-01-10 15.14.42.png)
```
? : 不在svn的管理之下
A : 该文件在已经添加到svn的管理之下,但是该文件在本地,并没有提交到服务器
M : 该文件在本地已经被修改,但是没有传到服务器
D : 该文件在本地已经删除,但是服务器依然有该文件,删除操作没有更新到服务器
```