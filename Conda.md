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

### Condacolab

https://github.com/conda-incubator/condacolab/tree/0.1.x

``` shell
!pip install -q condacolab
import condacolab
condacolab.install()
condacolab.check()
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
