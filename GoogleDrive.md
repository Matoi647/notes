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

### Google Drive 文件访问过多限制

https://zhuanlan.zhihu.com/p/678366332

https://bytesbin.com/how-to-download-a-large-file-from-google-drive-quickly/

``` shell
Failed to retrieve file url:

	Too many users have viewed or downloaded this file recently. Please
	try accessing the file again later. If the file you are trying to
	access is particularly large or is shared with many people, it may
	take up to 24 hours to be able to view or download the file. If you
	still can't access a file after 24 hours, contact your domain
	administrator.

You may still be able to access the file from the browser:

	https://drive.google.com/uc?id=14D3fFtaPX4GBe9dSJLKAIvUYlgK7fUxS

but Gdown can't. Please check connections and permissions.
unzip:  cannot find or open test_data.zip, test_data.zip.zip or test_data.zip.ZIP.
rm: cannot remove 'test_data.zip': No such file or directory
```
