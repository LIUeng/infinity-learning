## 生成 SSH 凭证

```shell
# ed_25519
ssh-keygen -t ed25519 -C "注释"
# 复制
pbcopy < ~/.ssh/?.pub
# 添加 host
ssh-add --apple-use-keychain ~/.ssh/?_ed25519
# 测试
ssh -T git@gitee.com
```
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

## FAQ

> `通过 git+ssh 进行 npm install 的时候注意区分使用哪个 git config 配置`

可以使用环境变量形式安装 GIT_SSH_COMMAND='ssh -i ~/.ssh/?.rsa' npm install

> ssh 不起作用时，需要重新添加配置

```shell
eval "$(ssh-agent -s)"

ssh-add 重新添加秘钥
```