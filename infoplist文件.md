常见属性
Localiztion native development region(CFBundleDevelopmentRegion)-本地化相关

Bundle display name(CFBundleDisplayName)-程序安装后显示的名称,限制在10－12个字符，如果超出，将被显示缩写名称

Icon file(CFBundleIconFile)-app图标名称,一般为Icon.png

Bundle version(CFBundleShortVersionString)-应用程序的版本号，每次往App Store上发布一个新版本时，需要增加这个版本号

Main storyboard file base name(NSMainStoryboardFile)-主storyboard文件的名称

Bundle identifier(CFBundleIdentifier)-项目的唯一标识，部署到真机时用到

02-项目中常见的文件(info.plist)
Supporting file一般都是放些资源文件,像一些plist这些等.
xcode5当中也有info.plist,只不过它的名字很长.是工程的名称.
在xcode5当中,会自动生成一个pch文件,在Xcode6当中不会帮我们生成PCH文件.
info.plist当中保存着整个应用当中基本的配置.它是一个字典.查看它的类型.
这个当中,主要掌握三个Key,
Bundle Name:应用程序的名称.
Bundle version string,short:应用程序的版本.在开发当中都是迭代开发.苹果要求下一次提交的版本必须得要比上一次提交的版本要高.
Bundle Version:应用程序编译的版本.
Bundle identifier:应用程序标识符.保证应用程序的唯一性,
如果两个应用同一个标识符, 那么之前的那个应用会被干掉.
作用:上传到AppStore的时候必须得要有标识符.
当做推送的时候也必须得要Bundle identifier.
Targets对应者info.plist.文件.