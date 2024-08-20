### Oh-My-Zsh 安装

https://www.haoyep.com/posts/zsh-config-oh-my-zsh/

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

### 安装 power10k

``` shell
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```

或者使用 power10k 国内镜像
``` shell
git clone --depth=1 https://gitee.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```

然后在`~/.zshrc`中添加一行`ZSH_THEME="powerlevel10k/powerlevel10k"` （默认是robbyrussell）

最后`source ~/.zshrc`

### 安装插件

语法高亮 zsh-syntax-highlighting

``` shell
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

命令提示 zsh-autosuggestions
``` shell
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

编辑`~/.zshrc`，添加插件
``` shell
plugins=(git zsh-syntax-highlighting zsh-autosuggestions)
```

### 修改 power10k 显示

输入 `p10k configure` 逐步选择
``` shell
p10k configure
```

或者直接编辑 `~/.p10k.zsh`

https://github.com/romkatv/powerlevel10k/blob/master/README.md

取消显示用户名和右边的三条横线：修改`POWERLEVEL9K_RIGHT_PROMPT_ELEMENTS`，注释掉`context`和`background_jobs`

``` shell
typeset -g POWERLEVEL9K_RIGHT_PROMPT_ELEMENTS=(
    ...
    # background_jobs         # presence of background jobs
    # context                 # user@hostname
    ...
)
```

最后`source ~/.zshrc`
