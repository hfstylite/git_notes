#### 获取仓库

- Git初始化文件：`git init`
- Git克隆项目：`git clone {项目url}`
- 添加指定文件的追踪：`git add {文件}`或`git add .`

#### 记录每次更新到仓库

- 状态简揽：`git status -s`
- 忽略文件：`.gitignore`文件里面添加需要忽略的文件
  - 文件 `.gitignore` 的格式规范如下：
    - 所有空行或者以 `＃` 开头的行都会被 Git 忽略。
    - 可以使用标准的 glob 模式匹配。
    - 匹配模式可以以（`/`）开头防止递归。
    - 匹配模式可以以（`/`）结尾指定目录。
    - 要忽略指定模式以外的文件或目录，可以在模式前加上惊叹号（`!`）取反。
- 查看尚未暂存文件更新了哪些部分：`git diff`
- 查看已暂存将添加至下次提交内容：`git diff --cached`或`git diff --staged`

- 移除文件：
  - 删除文件及记录：
    - 第一种：手动删除然后记录这次操作`rm {文件}` `git rm {文件}`
    - 第二种：强制删除加上 `-f`
  - 文件暂存区移除磁盘保留：`git rm --cached {文件}`
- 移动/重命名文件：`git mv {文件1} {文件2}`

#### 查看提交历史

- 查看所有提交：`git log`

- 查看最近两次提交：`git log -2`

- `git log`常用选项：

  | `-p`              | 按补丁格式显示每个更新之间的差异。                           |
  | ----------------- | ------------------------------------------------------------ |
  | `--stat`          | 显示每次更新的文件修改统计信息。                             |
  | `--shortstat`     | 只显示 --stat 中最后的行数修改添加移除统计。                 |
  | `--name-only`     | 仅在提交信息后显示已修改的文件清单。                         |
  | `--name-status`   | 显示新增、修改、删除的文件清单。                             |
  | `--abbrev-commit` | 仅显示 SHA-1 的前几个字符，而非所有的 40 个字符。            |
  | `--relative-date` | 使用较短的相对时间显示（比如，“2 weeks ago”）。              |
  | `--graph`         | 显示 ASCII 图形表示的分支合并历史。                          |
  | `--pretty`        | 使用其他格式显示历史提交信息。可用的选项包括 oneline，short，full，fuller 和 format（后跟指定格式）。 |

- 限制`git log`输出选项：

  | 选项                  | 说明                               |
  | :-------------------- | :--------------------------------- |
  | `-(n)`                | 仅显示最近的 n 条提交              |
  | `--since`, `--after`  | 仅显示指定时间之后的提交。         |
  | `--until`, `--before` | 仅显示指定时间之前的提交。         |
  | `--author`            | 仅显示指定作者相关的提交。         |
  | `--committer`         | 仅显示指定提交者相关的提交。       |
  | `--grep`              | 仅显示含指定关键字的提交           |
  | `-S`                  | 仅显示添加或移除了某个关键字的提交 |

#### 撤销操作

- 取消暂存文件：`git reset {文件}`
- 撤销对文件的修改：`git checkout -- {文件}`

#### 远程仓库的使用

- 克隆远程仓库：`git clone {仓库url}`
- 远程库的简写与URL：`git remote -v`
- 添加远程仓库：`git remote add <shortname> <url> `
- 从远程仓库抓取与拉取：
  - 抓取：`git fetch [remote-name]`
  - 拉取：`git pull`
- 推送到远程仓库：`git push [remote-name] [branch-name]`
- 查看某个远程仓库：`git remote show [remote-name]`
- 远程仓库的移除与重命名：
  - 重命名：`git remote rename [旧名] [新名]`
  - 移除：`git remote rm {远程分支}`

#### 打标签

- 查看标签：`git tag` 或 `git tag -l 'v1.8.8*'`

- 轻量标签： 一个轻量标签很像一个不会改变的分支——它只是一个特定提交的引用 

  - 创建标签：`git tag v1.4-lw`
  - 查看标签：`git show v1.4-lw`

- 附注标签： 附注标签是存储在 Git 数据库中的一个完整对象 

  - 创建标签：`git tag -a v1.4 -m "my version 1.4"`
  - 查看标签：`git show v1.4`

- 后期打标签：`git tag -a {标签名} {提交哈希值}`

- 共享标签：

  - 共享一个：`git push origin [tagname]` 

  - 共享全部：`git push origin --tags`

- 删除标签：

  - 删除本地标签`git tag -d <tagname>`
  - 删除远程标签：`git push <remote> :refs/tags/<tagname>`

- 检出标签：`git checkout <tagname>`