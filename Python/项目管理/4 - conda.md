[conda 文档](https://docs.conda.io/projects/conda/en/stable/user-guide/getting-started.html)

> 使用 environment.yml 文件管理项目

## 创建虚拟环境

- 首先创建 environment.yaml 文件

```yaml
name: 创建的环境名
channels:
	- defaults
dependencies:
# 可以已配置 python 版本
	- python=版本号
```

- 执行创建

```shell
# 创建虚拟环境
conda env create -f environment.yaml
# 更新
conda env update -f environment.yaml
```

- 删除环境

```shell
conda env remove --name 要删除的环境名
```
## 项目构建

[Conda-build](https://docs.conda.io/projects/conda-build/en/stable/)