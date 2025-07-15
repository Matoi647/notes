### Docker 安装

``` shell
sudo apt install docker.io
sudo systemctl enable --now docker
```

### 常用命令

``` shell
docker save -o <container_name>.tar.gz <container_name>
```

``` shell
docker cp [OPTIONS] <source_path> <container_id>:<destination_path>
docker cp [OPTIONS] <container_id>:<source_path> <destination_path>
```

### 查看 Docker 磁盘占用情况

``` shell
docker system df -v
```

### Docker 缓存

尽量使用 `--no-cache` 构建！

如果不使用 `--no-cache`，假设构建过程中 Ctrl C 中断，则会留下大量缓存层，且无法清理（缓存计数未释放）

``` shell
# docker build --no-cache
docker compose build --no-cache
```

查看缓存层具体信息

``` shell
docker system df -v

Build cache usage: 163.7GB

CACHE ID       CACHE TYPE     SIZE      CREATED        LAST USED      USAGE     SHARED
o0l0o427an62   regular        0B        4 months ago   4 months ago   1         true
kx0j0zue5jhm   regular        0B        2 months ago   2 months ago   1         false
ru4a3ehp4jg7   regular        0B        2 months ago   2 months ago   1         false
```


``` shell
docker buildx du
# 其中带星号的是可以删除的
9zukmi0lckgpsfc6wnir8s7k7*                      true            334.1kB         23 hours ago
z53yd1sls62sfitoh6dw39gjn                       true            333.8kB         24 hours ago
yjhq6d6kd1op3tvsns1uq2v0u*                      true            0B              24 hours ago
st9b39ltfc97mf31ml9wu1329                       true            0B              23 hours ago
```

``` shell
docker buildx du --verbose | grep -C 15 "o0l0o427an6" --color=auto

ID:             y0t5zyabdhrnfyjqs0gcf55bs
Parent:         o0l0o427an62m8q13zezxg9f3
Created at:     2025-05-01 10:56:44.885833845 +0000 UTC
Mutable:        false
Reclaimable:    true
Shared:         true
Size:           0B
Description:    pulled from docker.io/nvidia/cuda:11.8.0-runtime-ubuntu22.04@sha256:eaaccb3528ceca110601131434ab467e41d694a41e8c9bf280fb27ac18fcb29b
Usage count:    1
Last used:      2 months ago
Type:           regular
```

```
ID:             缓存层ID
Parent:         依赖的父缓存层
Created at:     2025-05-01 10:56:44.885833845 +0000 UTC
Mutable:        false
Reclaimable:    true
Shared:         true
Size:           0B
Description:    构建过程的Docker命令
Usage count:    引用计数，如果不为0则无法删除
Last used:      2 months ago
Type:           regular
```

删除缓存层

``` shell
docker buildx prune --filter "id=o0l0o427an6"

# 删除失败，因为Usage count不为0
```
