## 镜像

- 阿里云 [http://mirrors.aliyun.com/pypi/simple/](http://mirrors.aliyun.com/pypi/simple/)
- 中国科技大学 [https://pypi.mirrors.ustc.edu.cn/simple/](https://pypi.mirrors.ustc.edu.cn/simple/)
- 豆瓣(douban) [http://pypi.douban.com/simple/](http://pypi.douban.com/simple/)
- 清华大学 [https://pypi.tuna.tsinghua.edu.cn/simple/](https://pypi.tuna.tsinghua.edu.cn/simple/)
- 中国科学技术大学 [http://pypi.mirrors.ustc.edu.cn/simple/](http://pypi.mirrors.ustc.edu.cn/simple/)
## Mac 配置

~/.config/pip/pip.conf

```conf
[global]
# index-url=https://pypi.tuna.tsinghua.edu.cn/simple
index-url=http://mirrors.aliyun.com/pypi/simple/
trusted-host=mirrors.aliyun.com
```
## Windows 配置

%APPDATA%\\pip\\pip.ini

```ini
[global]
index-url=
#...
```
## Linux 配置

$HOME/.config/pip/pip.conf

```conf
[global]
index-url=
```
