### Miniconda 安装

```shell
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh
```

### Colab 安装 Miniconda
``` shell
!wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
!bash Miniconda3-latest-Linux-x86_64.sh -b -f -p /usr/local
```

### ` Do you wish the installer to initialize Anaconda3 by running conda init?[yes/no]`

https://cloud.tencent.com/developer/article/2062844

如果选择yes，则会更新~/.bashrc，自动激活conda base环境

如果选择no，则需要手动修改~/.bashrc，否则conda无法使用

```
echo 'export PATH="~/miniconda3/bin:$PATH"' >> ~/.bashrc
```

### Condacolab

https://github.com/conda-incubator/condacolab/tree/0.1.x

``` shell
!pip install -q condacolab
import condacolab
condacolab.install()
condacolab.check()
!which python
```


### `.condarc`设置

```shell
# ~/.condarc
auto_activate_base: false
envs_dirs:
  - /path/to/conda/envs
pkgs_dirs:
  - /path/to/conda/pkgs
channels:
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
  - defaults

```

### Conda清理空间

```shell
conda clean --packages  # 清除没有用到的包
conda clean --tarballs  # 清除*.tar
```
