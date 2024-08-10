### Miniconda 安装

```shell
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh
```

取消自动激活 base 环境

```shell
conda config --set auto_activate_base false
```

或者直接修改`~/.condarc`

修改环境存储路径`envs_dirs`

```shell
# ~/.condarc
envs_dirs:
  - /data/<username>
auto_activate_base: false
```

换源`channels`

```shell
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
```

```shell
# ~/.condarc
channels:
  - channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
```



