> 同时使用 SSH 和 HTTPS

```shell
# 测试是否可用
ssh -T -p 443 git@ssh.github.com
```

> 配置 SSH 连接

```config
Host github.com
	Hostname ssh.github.com
	Port 443
	User ?(git)
```

```shell
# 测试 ssh
ssh -T git@github.com
```