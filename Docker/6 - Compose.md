## 定义

Docker Compose 设置和共享多容器应用
## 用法

创建 compose.yaml

```yaml
services
	app1:
	app2:
```
## 运行

```sh
docker compose up -d
```
## 查看日志

```sh
docker compose logs -f app1
```
## 停止

```sh
# --volumes
docker compose down
```