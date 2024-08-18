### 下载 GoogleDrive 文件

https://blog.csdn.net/lzq6261/article/details/130032780

``` shell
pip install gdown
```

点击 GoogleDrive 文件右侧 -> 共享 -> 复制链接，提取链接中的 id

``` shell
gdown https://drive.google.com/uc?id=<链接中的id>
```

例如: 

复制的链接：https://drive.google.com/file/d/1ftesnmlh7NU3m5MuXGQ6OCJkylTsBOjU/view?usp=share_link

提取的 id：1ftesnmlh7NU3m5MuXGQ6OCJkylTsBOjU

则下载命令为：

``` shell
gdown https://drive.google.com/uc?id=1ftesnmlh7NU3m5MuXGQ6OCJkylTsBOjU
```

也可以断点续传:

``` shell
gdown -c https://drive.google.com/uc?id=1ftesnmlh7NU3m5MuXGQ6OCJkylTsBOjU
```
