#### 分布式工作流程（Git中每个开发者扮演节点和集线器角色）

- 集中式工作流：一个中心集线器（仓库），接受代码，开发者作为节点（仓库消费者）与其进行同步
- 集成管理者工作流：
  - 项目维护者推送到主仓库。
  - 贡献者克隆此仓库，做出修改。
  - 贡献者将数据推送到自己的公开仓库。
  - 贡献者给维护者发送邮件，请求拉取自己的更新。
  - 维护者在自己本地的仓库中，将贡献者的仓库加为远程仓库并合并修改。
  - 维护者将合并后的修改推送到主仓库
- 司令官与副官工作流：
  - 普通开发者在自己的特性分支上工作，并根据 `master` 分支进行变基。 这里是司令官的 `master` 分支。
  - 副官将普通开发者的特性分支合并到自己的 `master` 分支中。
  - 司令官将所有副官的 `master` 分支并入自己的 `master` 分支中。
  - 司令官将集成后的 `master` 分支推送到参考仓库中，以便所有其他开发者以此为基础进行变基。

#### 维护项目

- 在特性分支上面工作

- 应用来自邮件的补丁

  - 检查补丁是否可应用：`git apply --check {补丁路径}`

  - 应用补丁：`git apply {补丁路径}`、`git am {补丁路径}`

  - 应用补丁报错三种应对方式：
    - 解决错误后执行：`git am --resolved`
    - ` 跳过该错误：`git am --skip
    -  重置并且停止应用补丁：`git am --abort`

- 确定引入了哪些东西

  - 比较分支间差异：`git log contrib --not master`

  - 手工的方式找出公共祖先 ：`git merge-base contrib master`

  - 分支最新提交与两分支共同祖先比较：`git diff master...contrib`

- 将贡献的工作整合进来
  - 合并工作流：反复的直接将工作合并进入master分支
  - 大项目合并工作流： ：`master`、`next`，用于新工作的 `pu`（proposed updates）和用于维护性向后移植工作（maintenance backports）的 `maint` 分支 

- 变基与拣选工作流：
  - 挑拣：`git cherry-pick e43a6fd3e94888d76779ad79fb568ed180e5fcdf`

- Rerere：
  -  配置选项：`git config --global rerere.enabled true`