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
