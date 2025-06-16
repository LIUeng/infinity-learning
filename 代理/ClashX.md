## 配置白名单

跳过代理

> 在配置文件夹创建 proxyIgnoreList.plist 文件

```plist
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<array>
    <string>127.0.0.1</string>
    <string>localhost</string>
    <string>*.local</string>
    <string>*.superboss.cc</string>
    <string>*.raycloud.com</string>
    <string>*.kuaidizs.cn</string>
    <string>*.js.org</string>
    <string>0.0.0.0</string>
</array>
</plist>

```