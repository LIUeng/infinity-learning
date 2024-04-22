## 问题

使用以下解决方案不灵活，每次需要手动切换

```sh
alias git_personal="(ssh-agent) && ssh-add ~/.ssh/personal"
alias git_work="(ssh-agent) && ssh-add ~/.ssh/work"
```
## 解决办法

### 在根目录下 .gitconfig 添加以下配置

```sh
[user]
# 全局信息

[github]
# github 相关的信息

[includeIf "gitdir:~/"]
path = ~/.gitconfig-personal

[includeIf "gitdir:~/Work/"]
path = ~/.gitconfig-work

[core]
excludesfile = ~/.gitignore
```

### 创建相关的文件

- .gitconfig-personal

```sh
[user]
name = x
email = y

[github]
user = x

[core]
sshCommand = ssh -i ~/.ssh/personal
```

- .gitconfig-work

```sh
[user]
name = x
email = y

[github]
user = x

[core]
sshCommand = ssh -i ~/.ssh/work
```
### 测试

```shell
git config --list | grep user
```