![](/assets/屏幕快照 2017-01-15 21.08.58.png)
[^.git隐藏文件]
#### 一.命令行的演示 
#####1.初始化一个代码仓库
 - git init
 
#####2.如果使用GIT,必须给GIT配置用户名和邮箱。给当前的git仓库配置用户名和邮箱
- git config user.name "XMG"
- git config user.email "XMG@163.com"
给git配置全局的用户和邮箱
- git config --global user.name "XMG"
- git config --global user.email "XMG@163.com"

#####3.初始化项
 - touch main.m : 创建了main.m
 - git add main.m : 将main.m添加到暂缓区
 - git commit -m "初始化项" : 将在暂缓区的所有内容提交到本地版本库, 清空暂缓区
 - git add . : 将在工作区所有不在暂缓区的所有内容添加到暂缓区注意: 添加的文件或者是修改的文件都要通过add命令将该文件添加到暂缓区
 
#####4.查看文件状态
- git status

 红色 : 该文件被添加或者被修改,但是没有添加到git的暂缓区

 绿色 : 该文件在暂缓区,但是没有提交到本地版本库


##### 5.给命令行起别名
- git config alias.st "status"
- git config alias.ci "commit -m"
- git config --global alias.st "status"
 
#####6.删除文件
- git rm person.m : 将person.m删除

#####7.查看版本信息
- git log - > 版本号是由sha1算法生成的40位哈希值 [^只能看到3个版本,当前，前一个，初始版本]
- git reflog : 可以查看所有版本回退的操作

#####8.版本回退[^结合git reflog方便使用]
- git reset --hard HEAD : 没有提交版本,回到当前版本
- git reset --hard HEAD^ : 回到上一个版本 
- git reset --hard HEAD^^ : 回到上上个版本                   
- git reset --hard HEAD~100 :回到前100个版本
- git reset --hard 版本号(哈希值一般前5位，前4位一样被雷劈)
[^第四个第五个随便用哪个]

#####9.给log起别名[^了解]
- git config --global alias.lg "log --color --graph -- pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit" 

#### 二.共享版本库 
- git服务器的搭建 常繁琐(linux) 
- 可以把代码托管到(Github/OSChina)  
- 个 件夹 
- 个U盘

#####1.一个文件夹作为共享版本库
- git init —bare

#####2.将共享版本库的所有内容下载到本地 
- git clone 共享版本库地址
#####3.删除忽略文件
- touch .gitignore —> Github ->搜索".gitignore" -> 选择*最多的->找到 Object-C,复制下来
#####4.版本回退
- git reset --hard HEAD^ :回到上一个版本(张三)
- git push -f :强制上传到共享版本库
- git reset —hard HEAD^ :回到上一个版本(经理)


#### 三.版本备份(了解)

#####1.1.0版本开发完毕,将1.0版本上传到AppStore,对1.0版本进行备份(打上标签)git tag -a weibo1.0 -m "这是1.0版本"git tag

#####2.需要将标签push到共享版本库
 - git push origin weibo1.0
 
#####3.开始2.0版本的开发

#####4.发现1.0版本有bug,在经理的文件夹下面创建一个文件夹, 于修复bug,将共享版本库所有内容clone
 - git clone
 
#####5.将当前的代码转为1.0标签,创建分支,并切换到该分支
 - git checkout weibo1.0 : 转为1.0标签
 - git checkout -b weibo1.1fixbug : 创建分支,并切换到该分支
                   
#####6.在分支中修复bug,上传到AppStore,将修复好的版本,打上tag,并上传到共享版本库
- git tag -a weibo1.1 -m "这是修复了1.0bug的1.1版本"
- git push origin weibo1.1

#####7.跟当前正在开发的2.0版本进行合并
 source Control - > pull ->weibo1.1fixbug
 
#####8.删除分支
- git branch :查看当前在哪个分支
- git branch -r :查看本地版本库的分支
- git branch -d weibo1.1fixbug : 删除本地分支
- git branch -r -d origin/weibo1.1fixbug :删除本地版本库分支 
- git push origin —delete weibo1.1fixbug

####四.新人代码仓库
- 创建一个文件夹作为共享版本库 
- 项目经理项目的代码仓库push代码 source control -> configuration -> 添加共享版本库地址

####  五.Github上托管代码
#####1.使用HTTPS认证

#####2.使用SSHKeys认证
- 公钥 : 存在github上用来解密
- 私钥 : 存在本地的一个.ssh文件夹下用来加密
git.oschina.net

魏俊杰QQ:1846903862 

https://github.com/CoderJJWei/JJKit.git   
      