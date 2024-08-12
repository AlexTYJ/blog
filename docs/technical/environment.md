# vscode中常用虚拟环境建立指令

- 查看目前已有的虚拟环境：

``` bash
conda env list
```

- 删除环境

``` bash
conda env remove --name your_env_name
```

- 创建虚拟环境

```bash
conda create --name your_env_name python=3.8
```

- 清华源

```bash
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple package_name
```