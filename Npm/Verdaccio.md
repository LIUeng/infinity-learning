[搭建私有仓库](https://verdaccio.org/zh-CN/)
## Verdaccio

配置文件 

| 命令                 | 默认值                            | 范例             | 描述                                                                                                                                                     |
| ------------------ | ------------------------------ | -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| --listen \ **-l**  | http:localhost:4873            | 7000           | 定义 协议 + 域名 + 端口 ([格式](https://github.com/verdaccio/verdaccio/blob/08c36e688e8635733f92080eb3598239d43259cb/packages/node-api/src/cli-utils.ts#L7-L16)) |
| --config \ **-c**  | ~/.local/verdaccio/config.yaml | ~./config.yaml | 设置配置文件的位置                                                                                                                                              |
| --info \ **-i**    |                                |                | 打印本地环境信息                                                                                                                                               |
| --version \ **-v** |                                |                | 显示版本信息                                                                                                                                                 |
## Docker

```yml
version: '3.1'
services:
	nginx:
		build:
			context: ''
			dockerfile: nginx/Dockerfile
	ports:
		- '80:80'
	networks:
		- node-network
	container_name: 'nginx'
	depends_on:
		- verdaccio
	verdaccio:
		image: verdaccio/verdaccio
		container_name: 'verdaccio_relative_path_v5'
		networks:
			- node-network
		environment:
			- VERDACCIO_PORT=4873
			- DEBUG=verdaccio:*
		ports:
			- '4873:4873'
		volumes:
			- './storage:/verdaccio/storage'
			- './conf/v5:/verdaccio/conf'
networks:
	node-network:
		driver: bridge
```

### Nginx 配置

```conf
upstream verdaccio_relative_v5 {

server verdaccio_relative_path_v5:4873;
	keepalive 8;
}

server {
	listen 80 default_server;
	access_log /var/log/nginx/verdaccio.log;
	charset utf-8;

	location ~ ^/verdaccio/(.*)$ {
		proxy_set_header X-Real-IP $remote_addr;
		proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
		proxy_set_header Host $host;
		proxy_set_header X-NginX-Proxy true;
		proxy_pass http://verdaccio_relative_v5/$1;
		proxy_redirect off;
	}
}
```

> Dockerfile

```dockerfile
FROM nginx:1.21-alpine
COPY nginx/default.conf /etc/nginx/conf.d/default.conf
```
### 运行

```shell
docker compose up --build --force-recreate 
```