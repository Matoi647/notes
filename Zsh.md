### Oh-My-Zsh 安装

https://ohmyz.sh/#install

https://github.com/ohmyzsh/ohmyzsh

首先安装 Zsh 和 git

``` shell
sudo apt-get install zsh
sudo apt-get install git
```

通过curl安装

``` shell
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

通过wget安装

``` shell
sh -c "$(wget https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"
```

### GitHub DNS 污染导致无法 git clone

``` shell
fatal: unable to access 'https://github.com/ohmyzsh/ohmyzsh.git/': gnutls_handshake() failed: The TLS connection was non-properly terminated.
```

更换 ohmyzsh 镜像

https://mirrors.tuna.tsinghua.edu.cn/help/ohmyzsh.git/

``` shell
git clone https://mirrors.tuna.tsinghua.edu.cn/git/ohmyzsh.git
cd ohmyzsh/tools
REMOTE=https://mirrors.tuna.tsinghua.edu.cn/git/ohmyzsh.git sh install.sh
git -C $ZSH remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/ohmyzsh.git
git -C $ZSH pull
```



