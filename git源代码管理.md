![](/assets/屏幕快照 2017-01-15 21.08.58.png)
[^个人理解:commit提交到本地分支(.git目录内),push上传共享版本库，add添加到暂缓区但是xcode不需要add,直接commit，pull下载共享版本库到本地版本库]
[^.git隐藏文件,隐藏文件，我可以命令行打开它，用open .gitconfig,我已经将git全局设置好了，打开全局配置文件就能看到设置了，git lg别名]
### 一.命令行的演示 
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
- git reset --hard 版本号(哈希值一般前5位，前5位一样被雷劈)


#####9.给log起别名[^了解]
- git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"

### 二.共享版本库[^多人开发，本地的代码库共享，需要共享版本库] 
- git服务器的搭建非常繁琐(linux)，那本很厚的git书介绍怎么搭建
- 可以把代码托管到(Github/OSChina)  
- 一个文件夹 
- 一个U盘 小码哥资料里有或者https://my.oschina.net/leeming/blog/85029

#### 例子演示
#####1.一个文件夹作为共享版本库[^先cd进入到某个文件夹，在那个路径里设置共享版本库, 共享版本库没有.git]
- git init --bare

#####2.将共享版本库的所有内容下载到本地，命令行要cd到本地代码仓库
- git clone 共享版本库地址
- git push 从共享版本库下载
- git pull 从共享版本库上传
- git add . 添加某个文件夹下的所有内容
#####3.删除忽略文件，在本地代码仓库里创建.gitignore文件，它跟.git文件夹平行
- touch .gitignore —> Github ->搜索".gitignore" -> 选择*最多的->找到 Object-C文件,文件内容全部复制下来https://github.com/github/gitignore/blob/master/Objective-C.gitignore

##### 3.5在`本地版本库`用xcode初始化项目

##### 4.版本回退
- git reset --hard HEAD^ :回到上一个版本(张三)，所有人都要同步操作回退到上一个版本
- git push -f :强制上传到共享版本库
- git reset —hard HEAD^ :然后经理那边回到上一个版本(经理)
[^静态库不识别，cd到静态库目录再git add .,文件量少可以右击菜单栏add]

#### 三.版本备份(了解)

#####1.1.0版本开发完毕,将1.0版本上传到AppStore,对1.0版本进行备份(打上标签)
- git tag -a weibo1.0 -m "这是1.0版本"  :weibo1.0标签名
- git tag 查看版本

#####2.需要将打上标签名的代码push到共享版本库
- git push origin weibo1.0
 
#####3.开始2.0版本的开发

#####4.发现1.0版本有bug,在经理的文件夹下面创建一个文件夹, 于修复bug,将共享版本库所有内容clone,下面可能需要cd到本地代码仓库
 - git clone
 
#####5.将当前的代码转为1.0标签,创建分支,并切换到该分支[^这一步要在代码仓库中执行]
 - git checkout weibo1.0 : 转为1.0标签
 - git checkout -b weibo1.1fixbug : 创建分支,并切换到该分支
                   
#####6.在分支中修复bug,上传到AppStore,将修复好的版本,在当前分支打上tag,并上传到共享版本库[^分支名和前面的tag值和这次的tag都不能重复]
- git tag -a weibo1.1 -m "这是修复了1.0bug的1.1版本"
- git push origin weibo1.1

#####7.跟当前正在开发的2.0版本进行合并
 source Control - > pull ->weibo1.1fixbug
 
#####8.删除分支步骤[^一步不能错]
- git branch :查看当前在哪个分支，不知道分支全路径
- git branch -r :查看本地版本库的分支,路径全，不能知道当前在哪个分支
- git checkout master 切换分支,不用全路径
- git branch -d weibo1.1fixbug : 删除本地分支
- git branch -r -d origin/weibo1.1fixbug :删除本地版本库分支(全路径) 
- git push origin —delete weibo1.1fixbug :删除共享版本库分支

####四.新人代码仓库:专门给新人的版本库
- 创建一个文件夹作为共享版本库
- git init --bare
- 项目经理项目的代码仓库push代码 source control -> configuration -> 添加共享版本库地址

####  五.Github上托管代码
#####1.使用HTTPS认证

#####2.使用SSHKeys认证
- 公钥 : 存在github上用来解密
- 私钥 : 存在本地的一个.ssh文件夹下用来加密
git.oschina.net

魏俊杰QQ:1846903862 

https://github.com/CoderJJWei/JJKit.git   
      