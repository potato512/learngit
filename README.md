# Git分布式版本控制系统。

[Git](http://git-scm.com)
[Git图形界面工具](https://mac.github.com/index.html)

SVN集中式和Git分布式版本控制系统有什么区别呢？
* 集中式：
  * 1、必须联网，且带宽够大，速度够快；
  * 2、依赖控制系统的中央服务器，如果中央服务器出了问题，则没法干活；
* 分布式：
  * 1、没有中央服务器的概念，每台电脑都是一个完整的版本库，互相不依赖；
  * 2、提交时才需要联网处理修改的文件；

# Git工作原理
Git管理的是修改（如新增文件、新增字符、删除文件、删除字符、修改字符等），而不是文件。
* 1、概念
  * 工作区：个人电脑里的文件夹目录。
  * 版本库：工作区的隐藏目录.git。
  * 暂存区：版本库里的stage，或index。
  * 分支：版本库里自动创建的唯一一个master分支。branch。
  * HEAD：

* 2、操作命令执行
  * 步骤1 添加文件”git add”，即把工作区的文件添加到版本库中的暂存区；
  * 步骤2 提交文件”git commit”，即把版本库中暂存区的所有内容提交到当前分支；
  * 步骤3 删除文件”git rm”，即把版本库当前分支的文件删除；


# Git的安装
* 1、在Linux上安装Git：sudo apt-get install git
* 2、Mac OS X上安装Git:
   * 方法1 ：安装homebrew，然后通过homebrew安装Git，具体方法请参考homebrew的文档：http://brew.sh/。
~~~ javascript
// 安装  
brew install git  

// 检测git是否安装成功：  
git --version  

// 显示当前git的路径  
which git  
~~~

   * 方法2：安装Xcode，Xcode集成了Git，不过默认没有安装，你需要运行Xcode，选择菜单“Xcode”->“Preferences”，在弹出窗口中找到“Downloads”，选择“Command Line Tools”，点“Install”就可以完成安装了。

# Git的使用
[Git_Initialization初始化使用](https://github.com/potato512/learngit/Git_Initialization)







