1.配置:
    name:git config --global user.name "wzk"
    email:git config --global user.email "332684470@qq.com"
2.使用git:
    git status:
        查看当前仓库状态
    git init:(现实开发可能不这么做)
        初始化仓库
3.git中文件的状态:
    分为两种 未跟踪 和 已跟踪(又分为暂存 未修改 已修改)
    暂存:文件修改已保存,但是尚未提交
    未修改:磁盘中文件和git库中文件相同,没有修改
    已修改:磁盘中文件已经修改,和git仓库中文件不同

刚刚添加到项目的文件处于未跟踪状态:
    未跟踪--->暂存
        git add filename 将文件切换到暂存状态
        git add * 将所有已修改(未跟踪)的文件暂存
    暂存--->未修改
        git commit -m "xxxxx" 将暂存的文件存储到仓库中
        git commit -a -m "xxxxx" 提交所有已修改的文件(未跟踪的)
    未修改--->修改
        修改代码后,文件会变为修改状态
4.常用命令
-重置文件:
    git restore filename 恢复文件
    git restore --stage filename 把文件从暂存状态取消
-删除文件:
    git rm filename 删除文件
    git rm filename -f 强制删除
-移动文件:
    git mv from to 移动文件 重命名文件


5.分支
    git存储文件时,每一次提交代码,都会创建一个与之对应的节点,
    通过一个个的节点来记录代码状态,节点会构成一个树状结构,
    树状结构意味着存在分支,默认情况下仓库只有一个分支名为master,
    在使用git时,可以创建多个分支,分支与分支之间相互独立,
    在一个分支上修改代码不会影响其他分支
    分支操作:
    git branch 查看当前分支
    git branch branchname 创建新的分支
    git branch -d branchname 删除分支
    git switch branchname 切换分支
    git switch -c branchname 创建并切换分支 
    git merge branchname 合并分支

6.变基
    在开发中除了通过merge来合并分支,还可以使用变基来完成分支的合并  变基rebase
    通过merge合并分支时,在提交记录中会将所有的分支创建和分支合并的全过程全部显示出来,
    这样当项目比较复杂,开发比较波折时,需要反复的创建 合并 删除分支,这样会使我们代码的记录极为混乱
    变基原理:
        1.当发起变基时,git会首先找到两条分支最近的共同祖先
        2.对比当前分支相对于祖先的历史提交,并且将他们提取出来存储到一个临时文件中
        3.将当前部分指向目标基底
        4.以当前基底开始,重新执行历史操作 
    变基和merge对于合并分支来说最终的结果是一样的,但是变基会使得代码的提交记录更整洁更清晰
    但是如果代码已经提交到远程仓库,尽量不使用变基

7.远程仓库
    实际开中需要一个远程的git仓库,本质上与本地仓库无区别,不同点在于远程的仓库可以被多人同时访问,协同开发
    通常由公司搭建,内部使用,或是购买公共的私有git服务器
    学习阶段使用公共的git库:GitHub Gitee

    1.…or create a new repository on the command line
    echo "# xxxxxx" >> README.md
    git init
    git add README.md
    git commit -m "first commit"
    git branch -M main
    git remote add origin https://github.com/332684470/xxxxxx
    git push -u origin main

    2.…or push an existing repository from the command line     本地库上传
    git remote add origin https://github.com/332684470/xxxxxx
   #git remote add remotename url
    git branch -M main
   #修改分支的名字为main
    git push -u origin main
   #将代码上传至服务器

8.远程仓库的操作
    git remote                   #列出当前关联的远程库
    git add 远程库名 url          #关联远程库
    git remote remove 远程库名    #删除远程库
    git push -u 远程库名 分支名    #向远程库推送代码,并和当前分支关联
    git push 远程库名 本地分支:远程分支
    git clone url                 #从远程库下载代码
    git push                      #如果本地库的版本低于远程库,push默认无法推送
    git fetch                     #要想推送成功,必须确保本地库和远程库版本一致,
                                    fetch会从远程库下载所有代码,但不会将代码和当
                                    前分支自动合并,故fetch拉取代码之后需要手动合并
    git pull                      #从服务器上拉取代码且自动合并(有冲突也需要手动处理)
***推送代码之前一定先从远程库中拉取最新代码