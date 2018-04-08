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
3. 从 repostiroty 到 index
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
