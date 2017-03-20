
MAC上GitHub工具下载（https://mac.github.com/index.html）


MAC上使用Git（http://git-scm.com）
工作区：本地文件夹目录，如learngit
缓存区：stage，如文件被添加的地方git add…
版本库：HEAD，如文件被提交的地方git commit…

一、安装和使用
1 安装
方法1
安装homebrew，然后通过homebrew安装Git，具体方法查阅homebrew的文档（http://brew.sh）

方法2
直接从AppStore安装Xcode，Xcode集成了Git，不过默认没有安装，需要运行Xcode，选择菜单“Xcode-Preferences-Downloads-Command line Tools-Install”

3 使用
3-1 创建版本库（版本库又名仓库，英文名repository，可以简单理解成一个目录，这个目录里面的所有文件都可以被Git管理起来，每个文件的修改，删除，Git都能跟踪，以便任何时刻都可以追踪历史，或者在将来某个时刻可以还原）
3-1-1 创建空目录：mkdir learngit
3-1-2 打开空目录：cd learngit
3-1-3 查看空目录路径（输出：/Users/zhangshaoyu/learngit）：pwd
3-1-4 添加Git管理（输出：Initialized empty Git repository in /Users/zhangshaoyu/learngit/.git/）：git init

注意：已创建的版本库中会出现一个.git目录，这个目录是Git用来跟踪管理版本库的，切忌手动修改，避免把Git仓库破坏了。

3-2 把文件添加到版本库
3-2-1 在版本库目录里创建新文件（如readme.txt，并编辑一些内容）
3-2-2 将新文件添加到版本库：git add readme.txt
3-2-3 将新文件提交到Git：git commit -m “add readme.txt”
3-2-4 查看Git状态（是否有变更信息需要提交）：git status
3-2-5 查看文件修改后的信息：git diff readme.txt

注意：每一次文件有修改时必须执行“git add 文件名称”与“git commit …”语句，其中“-m “add readme.txt””表示提交变更时的备注信息。

3 其他命令
3-1 查看版本提交历史记录：git log
3-2 版本回滚：git reset —hard HEAD^（说明：^表示上一个版本，^^表示上上一个版本，HEAD~19表示上19个版本）
3-3 版本回滚动后返回到指定版本：git reset —hard 9a8c613（说明：hard后接前几位的版本号，通常是前7位）
3-4 查看文件内容：cat readme.txt
3-5 查看版本提交历史命令：git reflog
3-5 文件修改后撤消（未添加前，即未git add …）：git checkout — readme.txt
3-6 文件修改后且已添加（未提交，即未git commit …）：git reset HEAD readme.txt，然后再执行：git checkout — readme.txt
3-7 下载更新内容：git checkout master（即导出最新的分支master内容）


4 删除文件
4-1 版本库删除：git rm license.txt，git commit -m “remove license.txt”
4-2 工作区删除：rm license.txt（属于误删除，因为版本库还存在，此时需要先从版本库恢复到工作区，即git checkout — license.txt，然后再从版本库删除，即4-1的操作）


二、远程仓库GitHub
1 创建SSH Key
1-1 创建命令：ssh-keygen -t rsa -C "zhangsy757@163.com"
1-2 设置存储密钥对的文件名称：learngitRSA
1-3 设置密码对密码：123456

注意：密钥对文件存储位置为当前命令行打开的目录，结果为在该目录下生成密钥对文件，learngitRSA，learngitRSA.pub。应该把密钥对文件保存在用户主目录里的.ssh目录中，否则无效。

2 登录GitHub
2-1 设置公钥信息：setting-SSH Keys-Add SSH key-title（自定义标题），key（复制learngitRSA.pub文件内容）
2-2 高置本地仓库公钥信息：
2-2-1 查看公钥是否有效：ssh -T git@github.com
2-2-2 添加公钥：ssh-agent，ssh-add ~/.ssh/learngitRSA，输入公钥密码


三、添加远程库
1 创建远程仓库
1-1 登录GitHub
1-2 右上角+-New repository-repository name（自定义名称），其他默认-确定

2 关联本地版本库与远程版本库
2-1 关联：git remote add origin git@github.com:potato512/learngit.git
2-2 本地库内容推送到远程库：git push -u origin master

注意：第一次推送时，由于远程库是空的，所以带上“-u”，“origin master”表示当前分支所有内容。

3 下载远程版本库
3-1 设置下载文件夹目录，即使用git下载命令前先进入下载存档文件夹的目录
3-2 从远程库下载：git clone git@github.com:potato512/DemoImagePhoto.git
3-3 GigHub上创建仓库：登录GitHub-右上角+-New repository-Repository name（自定义名称），选中Initialize this repository with a README（即创建readme文档）


四、分支管理
1 分支管理
1-1 创建分支dev：git checkout -b dev（表示创建并切换到分支dev，即git branch dev，git checkout dev）
1-2 查看分支：git branch
1-3 切换分支内容：git checkout dev
1-4 修改分支内容后提交更新代码（git add 文件名，git commit -m 备注，git push origin dev）
1-5 切换主分支内容：git checkout master
1-6 合并分支（如果还在分支dev上则无法合并，也无法删除）：git merge dev，或git merge --no-ff -m "merge with no-ff" dev
1-7 删除分支：git branch -d dev，或没有合并时的强行删除git branch -D dev


五、解决冲突
1 同一个文件存在冲突时，即出现形如“<<<<<<< ======= >>>>>>>”的文本信息，修改后，再进行更新操作（git add 文件名，git commit -m 备注）


六、远程仓库信息处理
1 查看远程仓库信息：git remote（origin为远程仓库名称），或git remote -v（显示更详细信息）
2 推送分支：git push origin master（master为主分支，也可以为其他子分支）
3 下载克隆远程仓库内容：git clone git@github.com:potato512/learngit.git
4 设置标签：git tag v1.0，或git tag v1.0 6224937（6224937为某个提交id号的版本），或git tag -a v1.0 -m “version 1.0 released” 6224937（6224937为某个提交id号的版本，-a为指定标签名，-m为指定说明文字）
5 查看标签：git tag
6 查看标签信息：git show v1.0
7 下载分支版本：git checkout -b dev origin/dev（创建本地和远程仓库分支对应的分支）
8 下载更新信息：git pull（必须保证本地仓库分支与远程仓库分支关联，若不一致，则建立关联：git branch —set-upstream dev origin/dev）


七、标签管理
1 创建带有说明的标签：git tag -a v1.0 -m “version 1.0 released” 6224937（6224937为某个提交id号的版本，-a为指定标签名，-m为指定说明文字）
2 查看标签信息：git show v1.0
3 创建带有-s私钥签名的标签：git tag -s v1.0 -m “signed version 1.0 released” 6224937
4 删除标签：git tag -d v1.0（只是删除本地仓库的标签），或git push origin:refs/tags/v1.0（删除远程仓库标签）
5 推送标签到远程仓库：git push origin v1.0，或git push origin —tags（一次性推送全部尚未推送到远程的本地标签）


八、使用GitHub
1 把别人的项目克隆到自己帐号下：点击Fork-然后下载到本地仓库就可以进行修改等操作（如果想修改他人项目的bug，或新增功能，可以在GitHub上发起一个pull request）

2 配置
2-1 忽略特殊文件：创建.gitignore文件（要忽略的内容），然后提交到版本仓库
要忽略的内容
# Windows:
Thumbs.db
ehthumbs.db
Desktop.ini

# Python:
*.py[cod]
*.so
*.egg
*.egg-info
dist
build

# My configurations:
db.ini
deploy_key_rsa

2-2 配置别名
2-2-1 git config —global alias.st status（表示 git status 的简写为 git st）

2-3 搭建Git服务器
前提条件：运行linux的机器（Ubuntu，或Debian），sudo权限帐号
2-3-1 安装git：sudo apt-get install git
2-3-2 创建git用户：adduser git
2-3-3 创建证书登录：收集所有需要登录的用户的公钥（即id_rsa.pub文件），把所有公钥导入到home/git/.ssh/authorized_keys文件里（一行一个）
2-3-4 初始化git仓库：sudo git init —bare sample.git（注意先选定文件夹目录）
2-3-5 把owner改为git：sudo chown -R git:git sample.git
2-3-6 禁用shell登录：通过编辑/etc/passwd文件完成，将 git:x:1001:1001:,,,:/home/git:/bin/bash 改为 git:x:1001:1001:,,,:/home/git:/user/bin/git-shell
2-3-7 克隆远程仓库：git clone git@server:/srv/sample.git

2-4 其他
2-4-1 管理公钥：Gitosis
2-4-2 管理权限：Gitolite






