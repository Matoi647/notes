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