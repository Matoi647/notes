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

https://learn.microsoft.com/en-us/windows/wsl/wsl-config#configuration-settings-for-wslconfig

https://learn.microsoft.com/zh-cn/windows/wsl/wsl-config

`wsl.conf` `.wslconfig` `systemd`

### WSL 代理

WSL 默认使用NAT网络模式，无法和Windows共用代理，需要手动设置代理
（注意：Clash要设置允许局域网）

```
export WIN_IP=$(cat /etc/resolv.conf | grep nameserver | awk '{print $2}')
export HTTP_PROXY="http://$WIN_IP:7897"
export HTTPS_PROXY="https://$WIN_IP:7897"
export ALL_PROXY="http://$WIN_IP:7897"
export http_proxy="http://$WIN_IP:7897"
export https_proxy="https://$WIN_IP:7897"
export all_proxy="http://$WIN_IP:7897"

# export NO_PROXY="localhost,127.0.0.1,::1"
```

WSL使用镜像网络：https://learn.microsoft.com/en-us/windows/wsl/networking

仅支持Windows11 22H2及更高版本

### WSL ping 不通 Windows主机

https://blog.csdn.net/Cypher_X/article/details/123011200

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
