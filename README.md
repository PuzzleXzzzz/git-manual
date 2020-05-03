
# Git常用命令参考手册 ![](https://img.shields.io/github/license/xjh22222228/git-manual)  [git-repo](https://github.com/xjh22222228/git-manual)


基本涵盖了在开发中用到的git命令，能满足日常需求。

<center>
<img src="https://xiejiahe.gitee.io/public/tomato-work/project-9.png" />
</center>


---
# 目录
- [配置](#配置)
- [生成SSH_Key](#生成SSH_Key)
- [初始化本地仓库](#初始化本地仓库)
- [文件状态](#文件状态)
- [日志](#日志)
- [克隆](#克隆)
- [查看分支](#查看分支)
- [切换分支](#切换分支)
- [创建分支](#创建分支)
- [删除分支](#删除分支)
- [重命名分支](#重命名分支)
- [代码合并](#代码合并)
- [暂存](#暂存)
- [删除](#删除)
- [提交](#提交)
- [推送](#推送)
- [提交](#提交)
- [拉取最新内容](#拉取最新内容)
- [查看文件的改动](#查看文件的改动)
- [回滚版本](#回滚版本)
- [撤销](#撤销)
- [标签](#标签)
- [Git Flow](#GitFlow)
- [子模块](#子模块)
- [帮助](#帮助)
- [其他](#其他)

## 配置
```bash
# 查看配置列表
git config -l

# 查看已设置的用户名
git config --global --get user.name

# 设置用户名
git config --global user.name "xiejiahe"

# 查看已设置的邮箱
git config --global --get user.email

# 设置邮箱
git config --global user.email "example@example.com"
```



## 生成SSH_Key
```bash
# 1、粘贴以下命令，替换为您的GitHub电子邮件地址
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"

# 2、当提示“输入要在其中保存密钥的文件”时，按Enter。接受默认文件位置。
> Enter a file in which to save the key (/Users/you/.ssh/id_rsa): [Press enter]

# 3、在提示符下，键入一个安全密码。
> Enter passphrase (empty for no passphrase): [Type a passphrase]
> Enter same passphrase again: [Type passphrase again]
```

最后需要将生成的 SSH Key 添加到 `ssh config` 中
```bash
# 1、编辑
vim ~/.ssh/config

# 2、粘贴下面到 config 文件中
Host *
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_rsa
```






## 初始化仓库
`git init` 创建一个空的Git仓库或重新初始化一个现有的仓库
```bash
# 会在当前目录生成.git
git init

# 以安静模式创建，只会打印错误或警告信息
git init -q

# 创建一个裸仓库, 我们一般不会用到这个命令
git init --bare
```

## 文件状态
```bash
# 完整查看文件状态
git status

# 以短格式给出输出
git status -s

# 忽略子模块
git status --ignore-submodules
```

## 日志
```bash
# 查看完整历史提交记录
git log

# 查看前N次提交记录 commit message
git log -2

# 查看前N次提交记录，包括diff
git log -p -2

# 搜索关键词
git log -S 你好

# 列出提交者贡献数量, 只会打印作者和贡献数量
git shortlog -sn

# 以提交贡献数量排序并打印出message
git shortlog -n

# 采用邮箱格式化的方式进行查看贡献度
git shortlog -e
```


## 克隆
```bash
# https 协议
git clone https://github.com/xjh22222228/git-manual.git

# SSH协议
git clone git@github.com:xjh22222228/git-manual.git

# 克隆某个分支， -b 指定分支名字
git clone -b master https://github.com/xjh22222228/git-manual.git

# 递归克隆，如果项目包含子模块就非常有用
git clone --recursive git@github.com:xjh22222228/git-manual.git

# 克隆深度为1, 不会把历史的记录也克隆，这样可以节省克隆时间
git clone --depth=1 https://github.com/xjh22222228/git-manual.git
```



----


## 查看分支
```bash
# 查看所有分支
git branch --all

# 查看本地分支
git branch

# 查看远端分支
git branch -r
```

## 切换分支
```bash
# 2种方法，切换到master分支
git checkout master
git switch master

# 切换上一个分支
git checkout -
```

## 创建分支
```bash
# 创建develop分支
git branch develop

# 创建develop分支并切换
git checkout -b develop

# 切换远端分支
git checkout -t origin/dev
```


## 删除分支
```bash
# 删除本地分支
git branch -d <branchName>

# 删除远程分支
git branch -d -r origin/<branchName>
git push origin :<branchName>
```

## 重命名分支
```bash
# 重命名当前分支
git branch -m <branchName>
```


----


## 代码合并
```bash
# 两步法, 将 feature/v1.0.0 分支代码合并到 develop
git checkout develop
git merge feature/v1.0.0

# 或者一步法
git merge feature/v1.0.0 develop
```



## 暂存
```bash
# 暂存所有
git add -A

# 暂存某个文件
git add ./README.md

# 添加当前目录所有改动文件
git add .

# 暂存一系列文件
git add 1.txt 2.txt ...
```

## 删除
git add 的反向操作
```bash
# 删除1.txt 文件
git rm 1.txt
```

## 提交
```bash
# -m 提交的信息
git commit -m "changes log"

# 提交显示diff变化
git commit -v
```

## 推送
```bash
# 推送内容到主分支
git push -u origin master

# 本地分支推送到远程， 本地分支:远程分支
git push origin <branchName>:<branchName>

# 简写，默认推送当前分支
git push

# 强制推送, -f 是 --force 缩写
git push -f
```

----


## 拉取最新内容
```bash
# 推荐，因为不会做自动合并
git fetch origin master

# 相当于git fetch 然后 git merge
git pull

# 后面的意思是： 远程分支名:本地分支名
git pull origin master:master

# 如果是要与本地当前分支合并，则冒号后面的<本地分支名>可以不写
git pull origin master
```




----

## 查看文件的改动
```bash
# 查看所有文件改动
git diff

# 查看具体文件的改动
git diff README.md

# 查看某个版本的改动, 后面那一窜是commitId， git log后就能看到
git diff d68a1ef2407283516e8e4cb675b434505e39dc54

# 查看某个文件的历史修改记录
git log README.md
git show d68a1ef2407283516e8e4cb675b434505e39dc54 README.md
```


----

## 回滚版本
```bash
# 回滚上一个版本
git reset --hard HEAD^

# 回滚上两个版本
git reset --hard HEAD^^

# 回退到指定版本，git log 就能看到commit id了
git reset --hard 'commit id'

# 回滚版本是不保存在 git log，如果想查看使用
git reflog
```

----

## 撤销
```bash
# 撤销当前目录下所有文件的改动
git checkout -- .

# 撤销指定文件修改
git checkout -- README.md

# 暂存区回到工作区, 指定 ./README.md 文件从暂存区回到工作区
git reset HEAD ./README.md

# 撤销commit, 回到工作区, 一般commit id 是前一个
git reset <commit_id>

# 撤销commit, 并且把修改同时撤销
git reset --hard <commit_id>
```



## 标签
```bash
# 列出本地所有标签
git tag

# 列出远程所有标签
git ls-remote --tags origin

# 按照特定模式查找标签, `*` 模板搜索
git tag -l "v1.0.0*"

# 创建带有附注标签
git tag -a v1.1.0 -m "标签描述"

# 创建轻量标签, 不需要带任何参数
git tag v1.1.0

# 后期打标签, 假设之前忘记打标签了，可以通过git log查看commit id
git log
git tag -a v1.1.0 <commit_id>

# 推送到远程，默认只是本地创建
git push origin v1.1.0

# 一次性推送所有标签到远程
git push origin --tags

# 删除标签, 你需要再次运行 git push origin v1.1.0 才能删除远程标签
git tag -d v1.1.0

# 删除远程标签
git push origin --delete v1.1.0

# 检查标签
git checkout v1.1.0

# 查看本地某个标签详细信息
git show v1.1.0
```


## Git Flow
Git Flow 不是内置命令，需要单独安装

**初始化** 每个仓库都必须初始化一次
```bash
# 通常直接回车以完成默认设置
git flow init
```

**功能**
```bash
# 开启新的功能
git flow feature start v1.1.0

# 推送到远程, 在团队协作中这一步少不了
git flow feature publish v1.1.0

# 完成功能, 会将当前分支合并到 develop 然后删除分支，回到 develop
git flow feature finish v1.1.0
```

**打补丁**
hotfix是针对 `master` 进行打补丁的
```bash
# 开启新的 hotfix
git flow hotfix start v1.1.0_hotifx

# 推送到远程
git flow hotfix publish v1.1.0_hotifx

# 完成新的hotfix, 将当前分支合并到 master 和 develop，然后删除分支，回到 develop
git flow hotfix finish v1.1.0_hotifx
```

**发布**
```bash
# 开启新的 release
git flow release start v1.1.0

# 推送到远程
git flow release publish v1.1.0

# 完成, 将当前分支合并到 master 和 develop，删除当前分支然后回到 develop
git flow release finish v1.1.0
```

#### Git flow schema

![](media/git-flow.png)



---

## 子模块
具体使用还可以看这里 [git submodule子模块使用教程](https://www.xiejiahe.com/blog/detail/5dbceefc0bb52b1c88c30853)
```bash
# 添加子模块
git submodule add https://github.com/xjh22222228/git-manual.git

# 更新，有2种方法
# 一步到位
git submodule update --remote
# 或者进入到子模块项目再拉取
git pull

# 修复子模块分支指向 detached head
git submodule foreach -q --recursive 'git checkout $(git config -f $toplevel/.gitmodules submodule.$name.branch || echo master)'

# 删除子模块 common 为子模块名称，一般删除需要三部
git submodule deinit <common>
#清除子模块缓存
git rm --cached common
# 提交代码并推送
git commit -am "Remove a submodule" && git push
```



## 帮助
```bash
# 详细打印所有git命令
git help

# 打印所有git命令, 此命令不会有详细信息，更清晰一些
git help -a

# 列出所有可配置的变量
git help -c
```



## 其他
```bash
# 查看远程仓库地址
git remote -v

# 记住提交账号密码
git config --global credential.helper store

# 清除git已保存的用户名和密码
# windows
git credential-manager uninstall
# mac linux
git config --global credential.helper ""
# 或者
git config --global --unset credential.helper

# 清除本地git缓存
git rm -r --cached .
```




## License
MIT
