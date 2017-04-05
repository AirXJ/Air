
---

* 设置状态栏 [^启动状态栏设置]  
  ![](/assets/屏幕快照 2017-01-12 11.23.21.png)

* 添加.a静态库\(不开源\) ![](/assets/屏幕快照 2017-01-12 11.25.18.png)

类前缀

### tcp链接接收方缓冲区过小处理过程

在xcode菜单栏的product的scheme编辑里  
![](/assets/20161129204530782.png)

```
1.选择 Product –>Scheme–>Edit Scheme 
2.选择 Arguments 
3.在Environment Variables添加一个环境变量 OS_ACTIVITY_MODE 设置值为”disable” 
4.clean和build一下 
5.重新运行，发觉已经完全解决。
```



