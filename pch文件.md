><hr>
>pch文件名跟工程名字一样，但要提前编译，prefix[^提前准备]
<hr>
pch原理:pch里面的内容被项目中的所有文件共有.
<hr>
- pch作用:
 - 1.存放一些公用的宏
 
 如何设置[^这里Precompile Prefix Header是YES，路径名是工程路径，不是整个工程文件夹GameLive/GameLive/...，第二层就可以]
![](/assets/pch文件文件路径设置生效.png)