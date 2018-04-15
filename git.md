#git 进阶

## git 内部数据
###一. 综述
    本节首先介绍 git 内部使用的数据结构，然后介绍这些数据结构的存储空间，最后介绍一些 git 命令，并使用这些命令，探索 git 数据的生成和存储。

###二. git 数据结构
1. git 对象
    - 分类
        * blob
        * tree
        * commit
        * tag
    - object id
2. 引用

###三. git 存储空间
1. object store
2. index
3. 引用存储

###四. git 数据存储初探
1. find .git/
2. git add, find .git/objects
3. git cat-file -p
4. git ls-files -s
5. git write-tree
6. git commit-tree
7. git ls-files -s


## index 和文件存储
###一. 总述
    本节首先介绍一些与 index 相关的概念，然后介绍一些有关 index 的命令，最后介绍 git 文件存储的细节

###二. git 项目的文件存储区
1. repository (object store)
2. index
3. working directory

###三. git 项目文件分类
1. untracked
    - staged
    - unstaged
2. ignored
3. tracked
    - staged
    - unstaged
    - deleted
    - untouched

###四. 改变 index 的命令
1. 三个方向
    - 从 working directory 到　index
    - 从 repostitory 到 index
    - 直接改变 index
2. 从 working directory 到 index
    - 增加、修改: git add
    - 修改: git commit <file>, git commit -a
    - 删除: git rm
    - git mv = mv, git rm, git add
3. 从 repostiroty 到 index, 从 index 到　working directory
    - git checkout
    - git reset
4. 直接改变 index: git rm --cached


###五. 查看 index 的命令
1. git status
2. git ls-files -s
3. git diff
4. git diff --cache

###六. git 文件存储
图

## branch 和引用
1. 引用的名字
    - 名字解析规则
    - 全名引用 (P90, Branch or Tag?)
    - git rev-parse
    - 分级命名惯用法 (P91 top)
    - 通配符 git show-branch 'big/\*'
    - git check-ref-format
2. git branch <branch-name> [starting-commit]


## git diff
1. 三个文件存储空间之间的比较
    - working directory VS index
    - working directory VS repository
    - index VS repository
    - repository VS repository
2. git diff 与 git log 的 commit range 的区别
3. git diff <path-or-file>
4. pickaxe -- git diff -S


## merge
1. git log --graph
   git log --merge --left-right -p
2. conflict and index
3. merge strategy


## alter commit
1. 修改 commit history
    - git reset
2. 增加新的 commit
    - get cherry-pick
    - git revert
3. get reset 和 git checkout 的区别
4. get rebase
    - git rebase -i
5. git merge, git cherry-pick, git rebase 的区别
    - git merge: 合而为一
    - git cherry-pick: 在自己的分支上生长
    - git rebase: 嫁接到别的分支上


## stash and reflog
1. git stash
2. git relog
    - qualified name: HEAD@{1}
    - git reflog expire
3. git gc


## git remote
###一. repository type
1. bare
2. development(nonbare)
###二. git clone
1. development mode
    - remote local topic branch -> remote-tracking branch
    - remote tags -> tags
    - remote objects -> objects
    - remote repository named as 'origin' by default
    - config fetch refspec for origin remote
2. bare mode: --bare
###三. git remote
1. git remote, .git/config, git config
###四. branch type
1. remote branch
2. local branch
    - remote-tracking branch: refs/remotes
    - local-tracking branch: refs/heads
    - topic branch(development branch): refs/heads
###五. 引用其它 repository
1. remote url
2. refspec
    - refspec: 'source:dest'
    - fetch spec
    - push spec
3. example
4. git pull, git fetch, git push
###六. remote development cycle
例子
###七. remote configuration
1. git remote
    - git remote add
    - git remote update
    - git remote show
    - git remote rm
    - git remote prune
    - git remote update --prune *remote-name*
    - git branch -r -d origin/dev
2. git config
    - git config remote.<remote-name>.url ''
    - git config remote.<remote-name>.push '+refs/heads/\*:refs/heads/\*'
3. manual editing config file
###八. working with tracking branches
1. creating tracking branches
    - git checkout -b <local-tracking-branch> --track <remote-tracking-branch>: local can be different with remote branch name
    - git checkout --track <remote-tracking-branch>: local name matching remote branch name
    - git checkout <local-tracking-branch>: local name matching unique remote branch name
    - git branch --track <local-branch> <remote-branch>: create branch without checking out
    - git branch --set-upstream <local-branch> <remote-branch>: setting upstream for existed local-branch
###九. adding and deleting remote branches
1. git push <remote> <source>
2. git push <remote> <source>:<dest>
    - git push upstream new_dev:new_dev
    - git push upstream new_dev:refs/heads/new_dev
3. git push <remote> :<dest>
