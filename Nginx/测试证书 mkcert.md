[mkcert](https://github.com/FiloSottile/mkcert)
## 生成证书

```shell
mkcert -key-file cert.key -cert-file cert.crt 域名
```

- 支持通配符 \*.example.com
## 根证书

查看位置

```shell
mkcert -CAROOT
```

证书可以手动添加到系统中