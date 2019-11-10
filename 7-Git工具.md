#### 选择修订版本

- 简短的SHA-1：`git log --abbrev-commit --pretty=oneline`

- 分支引用：

  - 探测分支指定的SHA-1：`git rev-parse {分支名}`

- 引用日志： 引用日志记录了最近几个月你的 HEAD 和分支引用所指向的历史 ， 值得注意的是，引用日志只存在于本地仓库，一个记录你在你自己的仓库里做过什么的日志 

  - 查看引用日志：`git reflog` 或者 `git log -g {分支名}`
  - 查看HEAD在指定次数值时的提交：`git show HEAD@{n}`
  - 查看指定分支指定时间的提交：`git show master@{yesterday}`

- 祖先引用：

  - 查看HEAD父提交：`git show HEAD^` 或 `git show HEAD~`
  - 查看多个父提交：该语法只适用于合并的提交，因为合并提交会有多个父提交
    - `git show HEAD^2`：查看第二父提交，第一父提交是你合并时所在分支，而第二父提交是你所合并的分支 
    - `git show HEAD~2`： 第一父提交的第一父提交 ，即祖父提交

- 提交区间：

  - 双点：

    - 说明： 选出在一个分支中而不在另一个分支中的提交 
    - 语法`git loog {分支名}..{分支名}`

  - 多点：

    - 说明： 哪些提交是被包含在某些分支中的一个，但是不在你当前的分支上 
    - 引用前加`^`或者`--not` ；

    ```
    git log refA..refB
    git log ^refA refB
    git log refB --not refA
    三者等价
    ```

  - 三点：

    - 说明： 选择出被两个引用中的一个包含但又不被两者同时包含的提交 
    - 例：`git log --left-right master...experiment`

#### 交互式暂存

- 进入交互式终端：`git add -i`或`git add --interactive`

#### 储藏与清理

- 储藏工作：
  - 储藏推送入栈：`git stash` 或 `git stash save`
  - 储藏列表：`git stash list`
  - 应用储藏：
    - 重新应用：`git stash apply` 或 `git stash apply {储藏名}`
    - 重新应用并且以前暂存的保留暂存：`git stash apply --index`
    - 重新应用并在栈中删除：`git stash pop`
  - 移除堆栈中储藏：`git stash drop {储藏名}`
- 创造性的储藏：
  - 不储藏`git add`已暂存的东西：`git stash --keep-index`
  -  储藏任何创建的未跟踪文件 ：`git stash  --include-untracked`或`git stash -u`
  - 储藏检查：`git stash --patch`
- 从储藏创建一个分支：
  - 储藏在储藏的分支上的应用出现冲突时，可以创建一个新分支测试应用储藏，然后删除储藏：`git stash branch`
- 清理工作目录：
  -  工作目录中移除未被追踪的文件 (无法找回)：`git clean`
  - 移除(移除每一样东西并存放在栈中)：`git stash --all`
  -  移除工作目录中所有未追踪的文件以及空的子目录 ：`git clean -f -d`
  - 移除演习：`git clean -d -n`
  - 移除忽略文件(.o文件)：`git clean -f -d -x`
  - 交互式运行clean：`git clean -x -i`