Java Archive 打包压缩程序文件
## 优点

- Security
- Decreased download time
- Compression
- Packaging for extensions
- Package Sealing
- Package Versioning
- Portability
## 使用

```sh
jar
```
### 常见命令

#### jar cf  jar-file input-files(s)

- c - 创建输出文件
- f - 输出文件（stdout）
- v - verbose output on stdout
- 0(zero) - 不压缩
- M - 不生成 manifest 文件
- m 生成 manifest 文件
- C - 改变文件夹输出地址
#### jar tf jar-file

- t - 以 table 方式显示文件相关的信息
- f - 指定文件显示信息
#### jar xf jar-file \[archived-file(s)\]

提取内容

- x - 提取文件
- f - 指定提取文件
#### jar uf jar-file input-files(s)

更新文件

- u - update existing JAR file
- f - update is specified
## 运行

```sh
java -jar jar-file
```

## Manifest

META-INF/MANIFEST.MF

```mf
Manifest-Version: 1.0
Created-By: 1.7.0_06(Oracle Corporation)
Main-Class: MyPackage.MyClass
Class-Path: MyUtils.jar
```
### jar cfm jar-file manifest-addition input-files(s)

- m - 指定相应的文件更新 manifest 内容
### 指定入口

```sh
jar cfe app.jar MyApp MyApp.class
jar cfe Main.jar foo.Main foo/Main.class
```

- e - 指定入口文件
### Classpath

在 JAR 文件中引用其他文件类

```sh
jar cfm MyJar.jar Manifest.txt MyPackage/*.class
```
### 配置包信息

- Name
- Specification-Title
- Specification-Version
- Specification-Vendor
- Implementation-Title
- Implementation-Version
- Implementation-Vendor
### Sealing Packages

包中定义的所有类必须归档到同一个JAR文件中

```mf
Name: myCompany/firstPackage/
Sealed: true

Name: myCompany/secondPackage/
Sealed: true
```
## 签名验证

```mf
Name: test/images/ImageOne.gif
SHA1-Digest: kdHbE7kL9ZHLgK7akHttYV4XIa0=

Name: test/images/ImageTwo.gif
SHA1-Digest: mF0D5zpk68R4oaxEqoS9Q7nhm60=
```
### 签名

```sh
jarsigner jar-file alias
```

- alias 私钥
- -keystore url -> 指定密钥地址
- -sigfile file -> Specifies the base name for the .SF and .DSA files
- -signedjar file -> 指定文件签名文件不覆盖原始文件
- -tsa url -> Time Stamping Authority (TSA) identified by the URL
- -tsacert alias -> 生成使用公钥验证的时间戳
- -altsigner class -> |Indicates that an alternative signing mechanism be used to time stamp the signature. The fully-qualified class name identifies the class used.
- -altsingerpath classpathlist -> Provides the path to the class identified by the altsigner option and any JAR files that the class depends on.
## 验证

```sh
jarsigner -verify jar-file
```
## JAR APIs

- java.util.jar
- java.net.JarURLConnection
- java.net.URLClassLoader

```sh
java JarRunner http://www.example.com/TargetApp.jar
```