## 描述

拉取最近一次的提交记录（减少内存占用）

```shell
git clone --depth=1 仓库地址
```
## 切换分支

- 因为值拉取了最近的一次提交记录，其他分支信息没有获取完整
### 方法1

```shell
# 1. 查看远程分支列表（确认目标分支是否存在）
git branch -r

# 2. 拉取远程分支的浅提交到本地
git fetch origin dev --depth=1

# 3. 创建并切换到本地分支，关联远程分支
git checkout -b dev origin/dev
```
### 方法2

```shell
# 1. 克隆仓库时拉取所有分支的浅提交
git clone --depth=1 --branch=dev --single-branch <仓库URL> .
# --branch=dev: 指定克隆某个分支（默认分支可省略）
# --single-branch: 仅克隆该分支（但后续可手动拉取其他分支）

# 2. 若需切换其他分支，重复以下操作：
git fetch origin other-branch --depth=1
git checkout -b other-branch origin/other-branch
```
### 方法3

```shell
# 解除浅克隆限制，拉取完整历史
git fetch --unshallow
# 或拉取所有分支的完整历史
git config remote.origin.fetch "+refs/heads/*:refs/remotes/origin/*"
git fetch
```