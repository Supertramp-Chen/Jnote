# 本地仓库


## git的6行配置




        git config --global user.name 你的英文名
        git config --global user.email 你的邮箱
        git config --global push.default simple
        git config --global core.quotepath false
        git config --global core.editor "code --wait"
        git config --global core.autocrlg input

        git config --global --list(把配置打出来)


    
    bash(整个的黑框框)命令行里有很多命令，git只是一个命令




## 版本控制、多版本切换


        给你的代码进行快照(复制)

        使得代码有版本 且可随时回到某个版本


        .git 目录用来容纳你的代码快照

            .git 目录就算本地仓库

            不会重复复制相同的文件（优化）
            支持多个分支
        

        


        git init 创建 .git目录

            创建一个空仓库





        git add 路径

            处理文件变化而不是文件

            选择需要提交的路径，绝对路径or相对
            
            哪些是可以提交的 但还没有提交

            删除也需要add到待提交区


        .gitignore

            选择哪些不需要提交

            .node_modules
            .DS_Strore
            .idea
            .vsCODE



        git status


        git commit -m "版本1"w

            复制了一份到 .git目录

            每一次提交都是一次复制的过程



        git commit -m 字符串

            提交并说明理由，字符串有空格需引号


        git commit -v

            可回顾之前的修改

        git log

            从最开始到当前version的log

        切换版本
        git reset --hard XXXXXX

            前6位

            确保代码处于要么忽略，要么commit
            否则会自动消失,不能处于没有确定的状态



        git reflog

            private log

            all things





    

## 两个文件同时开发

        git branck X

            从当前位置 当前文件开始 创造平行时间线X  ，分支

            把当前文件 虚拷贝一份
            使得能够基于两个文件同时开发

            主线 master
            支线 X

        git checkout X

            如有未提交的代码，只要和另一分支不冲突即不需要理会

            当前目录的内容变成本地仓库里 x 分支的最新内容

        取决于在哪个分支



        git branch

    

    两个分支合并

        git merge X

            首先到达要保留的分支
            git checkout master

        
        解决冲突

            搜索 4个以上的 =
            上下 
            选择要保留的行，其他删除


            会得到conflict提示
            git status -sb查看冲突文件

            git add 对应文件
            git status -sb 下一个冲突
            没有冲突
            git commit 


        删除无用分支

            git branch -d X




# 远程仓库


    ssh key

        解决身份问题

        使得GitHub知道这个电脑和账号属于你

        公钥(GitHub)
        私钥(你的电脑)

        公钥和私钥可相互解密，配对的关系

        上传代码用私钥加密，GitHub用公钥解密




        产生ssh key

        ssh-keygen -t rsa -b 4096 -C你的邮箱

        回车

        ssh-keygen -t rsa -b 4096 -C mforward@126.com


        得到公钥内容 copy至GitHub设置页面
        
        cat /c/Users/86183/.ssh/id_rsa.pub
        ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQDMbLkQzrlObZGtipIB02AYkztYw97WNbDB9jErguLIu8EEXMJNnAh8e/Waja06iU7Ep4TSp1eX/ROj8GRPucRJ5s60aDKImAlyO1gBBwU02SIRfeG7OTFzuR5G3fQJsLbHivwD+3xn3lfemqiX3e54Tk0OoBx61ly0gwAQWtDHzJFD6qWg3DHFF7p7NwGRRzVGa1R7e8UTq7hn9JTM16V5eIUZKn8KMSOfXKjIG3MAP+pjA0m33CGdvqsVdsDK/sCKgSu+lUQnDq8jbd31IeCkLSKeYYSj+kLmyfjVaMTAO/bVU2WNg8D8M3vf8hCe+8XVpY5Dtv/p/iy5YuUYdQWgTg6dURlvOAqK05JFibRVjNxGjbjZ4zshoPvSk+WkPcjGIDGrN8sQ+/kRd1UCgw7PO1IwMkHuuTw2fBHeDkVutJX4MiOKz2XKwvLMPIL2CaSwiqZ6SiERhC9dgeq0qeI+CnTvZdEcK2FvdJnxAn2xvTEKRjwhpE1lx1M5jviZfnl+u5/dVFJ8F6y3NNBdwqZufh9FyBIgt19vuEfXJ8JOqKZVtVMhZYEDZMeVCsmBg+Myo/DINqK9YCjl+skXtIzdlMCbHfCnI9McBAeLHfjUphtJBBVQv6iypXPveFYeTycuGz79UB1LHCbQetGaVWnvUjRIy4x2t7dJGL4tAyPBaw== mforward@126.com


        测试配对成功
        ssh -T git@github.com




## 上传代码(复制)

 
        新建GitHub Repo

        本地添加远程仓库地址

        git remote add origin git@

        origin为远程仓库默认name

        每次push是把本地仓库的一个分支push到远程仓库
      
        git push -u origin master

            推送本地master分支到远程origin的master分支

            -u origin master 是设置上游分支
            之后不需要设置，直接 git push


        上传其他分支

            git push origin X:X

                左X为源头，右X为目标

            or

            git push -u origin X



## 下载代码(复制)

        git clone git@

        整个仓库

        git pull (更新)

        git clone git@?/xxx.git

            以元素目录名

            cd XXX

        git clone git@?/XXX.git yyy

            改目录name为yyy

        git clone git@?/xxx.git .

            先创建一个目录再把代码导入

            使用当前目录容纳代码和.git

            空目录



    一个本地仓库上传到两个远程仓库

        git remote add origin git@
        git remote add origin2 git@
        
        git push -u origin master
        git push -u origin2 master


    一个仓库上传到GitHub和另外一个网站




# git高级操作


    bash alias 简化命令

        gst/ga/gc/gl/gp


        touch ~/.bashrc

            code ~/.bashrc
            .bashrc 命令行的配置文件
            echo 'alias ga="git add"' ?? ~/.bashrc
            echo 'alias gc="git commit"' ?? ~/.bashrc
            echo 'alias gl="git pull"' ?? ~/.bashrc
            echo 'alias gp="git push"' ?? ~/.bashrc
            echo 'alias gco="git checkout"' ?? ~/.bashrc
            echo 'alias gst="git status -sb"' ?? ~/.bashrc
            source ~/.bashrc



            vi ~/.bashrc
            alias ga="git add ."
            alias gc="git commit -v"
            alias gi="git init"
            alias gp="git push"
            alias gl="git pull"
            alias gst="git status -sb"
            alias glog="git log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit   -- | less"
            source ~/.bashrc



        美化历史命令

            git rebase -i XXXX

            XXX复制你要美化的所有提交的前一个

            pick —— squash(采用，但是合并到上一个提交)
                    rework(采用，但是改写 message)

            git rebase --abort(可以取消rebase)
            git rebase --continue(继续)




        临时隐藏代码——通灵术

            git stash
            
            git stash pop(召唤)

            

    echo "# NOTES" >> README.md
    git init
    git add README.md
    git commit -m "first commit"
    git branch -M main
    git remote add origin git@github.com:Supertramp-Chen/NOTES.git
    git push -u origin main





# GitHub搭建个人博客


    github 预览markdown

    markdown语法

        # 
        ## 
        ### 

        1. 
        2. 
        3. 

        * xxx
        * yyy

            var = 1

        or


        网站[我的网站](https://google.com)

        ![图片](1.png)

        
        vscode - ctrl+shift+p




    快速打开对应的仓库

        yarn global add git-open(快速打开对应的仓库)
            安装yarn
            先装node
            https://classic.yarnpkg.com/en/docs/install#windows-stable

        npm i -g git-open
        git open 仓库名(不写默认为origin)

        git remote -v
        git remote remove 



        本地仓库

            创建新的目录用vscode打开
            vscode终端运行git init
            

        远程仓库

            GitHub创建远程仓库
            终端配置 origin



## Hugo

    Go语言实现的第一个博客生成器
    最快的博客生成器

    JS实现的Hexo(难用)


    hugo_xxx_windows-64bit.zip
    hugo.exe —— D:\Software\hugo ——  path
    hugo version

    hugo官网看文档，弄除public

        hugo new site 仓库名字(Supertramp-Chen.github.io-creator)
        cd quickstart
        git init


        hugo new posts/XXXX.md(创建新文章)


        draft: true
        改为 draft: false


        hugo -D

        把public上传到GitHub

          

            新建.gitignore里写/pulic/ (当前仓库不要存储public，piblic自成一个仓库，外面的仓库不管public)

            cd public
            git init
            git add .
            git commit -v

            github中新建一个仓库用户名.github.io

            git remote add origin git@github.com:Forwardman555/forwardman555.github.io.git

            git branch -M "main"
            git push -u origin "main"


        github page


        切换主题

            目录在 -creator上

            hugo server -D(重新启动server)



    
    hugo new post/
    hugo
    cd pubilic/
    git push