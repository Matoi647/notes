### WSL 磁盘管理

https://learn.microsoft.com/zh-cn/windows/wsl/disk-space

https://blog.csdn.net/hzgaoshichao/article/details/125530763

```shell
wsl --shutdown
cd E:\wsl\Ubuntu	# ext4.vhdx所在文件夹
diskpart
```

```shell
DISKPART> select vdisk file="E:\wsl\Ubuntu\ext4.vhdx"
DISKPART> compact vdisk
DISKPART> detach vdisk
DISKPART> exit
```

### WSL 配置

https://learn.microsoft.com/zh-cn/windows/wsl/wsl-config

`wsl.conf` `.wslconfig` `systemd`


### WSL 更改位置/镜像导出备份

https://zhuanlan.zhihu.com/p/20680293901

```
wsl --export Ubuntu-22.04 D:\wsl\image\wsl_ubuntu_2204.tar
wsl --unregister Ubuntu-22.04
wsl --import Ubuntu-22.04 D:\wsl\Ubuntu2204 D:\wsl\image\wsl_ubuntu_2204.tar
```


### 更改WSL用户

WSL export->unregister-import 之后，用户会从原来变为root

```
sudo nano /etc/wsl.conf
```

修改`/etc/wsl.conf`，添加以下内容：

```
[user]
default = <USERNAME>
```
