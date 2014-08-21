Git command

* 配置
  * /etc/gitconfig，针对所有用户，命令选项`--system`
  * ~/.gitconfig，针对当前用户，命令选项`--global`
  * .git/config，针对当前项目
  * `git config --global user.name` "user"
  * `git config --global user.email` "email"
  * `git config --global core.editor` vim
  * `git config --global merge.tool` vimdiff
  * `git config --global color.ui` true
  * `git config --global commit.template` $HOME/.gitmessage.txt
  * `git config --global core.pager` ''
  * 自动完成, Git源代码,进入contrib/completion目录,会看到一个 git-completion.bash 文件
    1. cp git-completion.bash  /.git-completion.bash
    2. .bashrc 中添加 ￼source ~/.git-completion.bash
  * git命令可以取别名, 如下:
    * `git config --global alias.co checkout`
    * `git config --global alias.br branch`
    * `git config --global alias.ci commit`
    * `git config --global alias.st status`
  * 利用git命令取创建新命令
    * `git config --global alias.unstage 'reset HEAD --'`, `git unstage $file` 等价于 `git reset HEAD` $file
    * `git config --global alias.last 'log -1 HEAD'`, `git last` 等价于查看最后一次提交信息
  
 
* 查看配置信息
  * `git config --list`
 
* 帮助
  * `git help`
  * `git --help`
  * `man git`
  
* 初始化
  * `git init`
 
* 添加文件
  * `git add` *.c
  * `git add` readme
 
* 克隆
  * `git clone` $url
  * `git clone` $url $local_dir
 
* 查看状态
  * `git status`
 
* 添加忽略文件
  * `#`：注释
  * `*.[oa]`：忽略.o和.a结尾的文件:
  * `*~ `：忽略~结尾的文件:
  * `*.a`：忽略.a结尾的文件
  * `!lib.a`：但lib.a除外
  * `/TODO`：忽略根目录下TODO文件
  * `build/`：忽略build/整个目录
  * `doc/*.txt`：忽略doc/下的所有.txt结尾的文件，但不包括其子目录的

* 比较差异
  * `git diff` 查看未缓存的文件更新了哪些
  * `git diff --cached` 或者 `git diff --staged` 已缓存的和上次提交时快照的差异
 
* 提交
  * `git commit`
  * `git commit -m "commit logs"`
 
* 删除
  * `git rm` $filename
  * `git rm --cahed` $filename
  * `git rm` log/\*.log
 
* 移动
  * `git mv` $file_from $file to
   
* 日志
  * `git log`
  * `git log -p -2`
  * `git log --stat`
  * `git log --pretty=online`
  * `git log --pretty=format:`"%h - %an, %ar : %s"
  * `git log --pretty=format:`"%h %s" `--graph`
  * `git log --since`=2.weeks
    * `-(n)` 仅显示最近的 n 条提交    * `--since`, `--after` 仅显示指定时间之后的提交    * `--until`, `--before` 仅显示指定时间之前的提交    * `--author` 仅显示指定作者相关的提交    * `--committer` 仅显示指定提交者相关的提交。
    * `-p` 按补丁格式显示每个更新之间的差异。    * `--stat` 显示每次更新的文件修改统计信息。    * `--shortstat` 只显示 --stat 中最后的行数修改添加移除统计。    * `--name-only` 仅在提交信息后显示已修改的文件清单。    * `--name-status` 显示新增、修改、删除的文件清单。    * `--abbrev-commit` 仅显示 SHA-1 的前几个字符,而非所有的 40 个字符。    * `--relative-date` 使用较短的相对时间显示(比如,“2 weeks ago”)。    * `--graph` 显示 ASCII 图形表示的分支合并历史。    * `--pretty` 使用其他格式显示历史提交信息。可用的选项包括: 
      * `online`
      * `short`
      * `full`
      * `fuller`
      * `format`:
        * `%H` 提交对象(commit)的完整哈希字串 %h 提交对象的简短哈希字串        * `%T` 树对象(tree)的完整哈希字串        * `%t` 树对象的简短哈希字串        * `%P` 父对象(parent)的完整哈希字串 %p 父对象的简短哈希字串        * `%an` 作者(author)的名字        * `%ae` 作者的电子邮件地址        * `%ad` 作者修订日期(可以用 -date= 选项定制格式) %ar 作者修订日期,按多久以前的方式显示        * `%cn` 提交者(committer)的名字        * `%ce` 提交者的电子邮件地址        * `%cd` 提交日期        * `%cr` 提交日期,按多久以前的方式显示 %s 提交说明

* 重新提交
  * `git commit --amend`

* 取消当前修改
  * `git checkout` $filename

* 查看远程库
  * `git remote`
  * `git remote -v`
  * `git remote add` [shortname] $url
  * `git remote show` [remote-name]

* 从远程库抓取数据
  * `git fetch` [remote-name] 

* 推送
  * `git push` [remote-name] [branch-name]

* 远程库删除和重命名
  * `git remote rm` $remote-name 
  * `git remote reanme` $name_from $name_to

* 标签
  * `git tag`
  * `git tag -l ` "$keyword"
  * `git tag -a ` [tag_name] `-m` 'description'
  * `git show ` [tag_name]
  * `git tag -s` [tag_name] `-m` 'description'
  * `git tag` [tag_name]
  * `git tag -v` [tag_name]
  * `git push origin` [tag_name]
  * `git push origin --tags`
  
* 分支
  * `git branch`
  * `git branch` [branch_name]
  * `git checkout` [branch_name]
  * `git checkout -b` [branch_name]
  * `git merga` [branch_name]
  * `git branch -d` [branch_name]
  * `git branch -v`
  * `git branch --merged`
  * `git branch --no-merged`
  * `git fetch origin` 抓取远程分支，只得到指针，并不可编辑
  * `git checkout -b` [branch_name] origin/[branch_name] 从远程分化出新分支，并切换到新分支
  * `git checkout --track` origin/[branch_name] 跟踪分支
  * `git checkout -b sf` origin/[branch_name] 自动推送和抓取分支
  * `git push` origin:[branch_name] 删除远程分支

* 衍合 **永远不要衍合那些已经推送到公共仓库的更新**
  * `git rebase` [branch_name]
  * `git rebase` [master] [branch_name1] [branch_name2] 会将后面2个分支衍合到master，并删除后2个分支

* ￼

 
 
 