### Docker 安装

https://docs.docker.com/engine/install/ubuntu/

``` shell
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update

sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

### 配置镜像

https://toolshu.com/docker-mirror

https://github.com/dongyubin/DockerHub

https://blog.csdn.net/weixin_48953586/article/details/145503572

```
sudo mkdir -p /etc/docker
sudo nano /etc/docker/daemon.json
```

`/etc/docker/daemon.json`如下：

```
{
  "registry-mirrors": [
    "https://docker.1ms.run",
    "https://docker.m.daocloud.io",
    "https://docker-0.unsee.tech"
  ]
}
```

```
sudo systemctl daemon-reload  
sudo systemctl restart docker
```

### Docker添加用户组

```
sudo usermod -aG docker $USER
# 重启之后生效
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


``` shell
#!/bin/bash

docker buildx du | grep hours | awk 'NR>1 {print $1}' | while read -r ID; do
    CLEANED_ID="${ID%"*"}"
    echo "Cleaning: $CLEANED_ID"
    docker buildx prune -f --filter "id=$CLEANED_ID"
    sleep 0.1
done
echo "Docker clean finished"
```

``` python
import subprocess
from graphviz import Digraph
import os

# Usage: python3 docker-clean.py
# put the generated docker_layer_tree file into https://www.devtoolsdaily.com/graphviz
# clean cache layer from children to parent (according to the graph shown by the website)

def main():
    result = subprocess.run(
        ['docker', 'buildx', 'du', '--verbose'],
        capture_output=True, text=True
    )
    
    if result.returncode != 0:
        print("Failed to run docker buildx du")
        print(result.stderr)
        return
    
    output = result.stdout

    layers = {}
    current_id = None
    
    for line in output.split('\n'):
        line = line.strip()
        if line.startswith('ID:'):
            current_id = line.split(':', 1)[1].strip()
            layers[current_id] = {'parent': None, 'children': []}
        elif line.startswith('Parent:') and current_id:
            parent = line.split(':', 1)[1].strip()
            layers[current_id]['parent'] = parent if parent != '<empty>' else None
    
    for layer_id, info in layers.items():
        parent_id = info['parent']
        if parent_id and parent_id in layers:
            layers[parent_id]['children'].append(layer_id)
    
    dot = Digraph(comment='Docker cahce layer graph', 
                  format='png',
                  graph_attr={'rankdir': 'TB', 'splines': 'ortho'},
                  node_attr={'shape': 'box', 'style': 'rounded,filled', 'fillcolor': '#E6F3FF'})
    
    for layer_id in layers:
        if layers[layer_id]['parent'] is None or layers[layer_id]['parent'] not in layers:
            dot.node(layer_id[:8], layer_id[:8], fillcolor='#FFD6A0')
        else:
            dot.node(layer_id[:8], layer_id[:8])
    
    for layer_id, info in layers.items():
        for child_id in info['children']:
            dot.edge(layer_id[:8], child_id[:8])
    
    # dot.render('docker_layer_tree', view=True)
    # print(f"Generated graph: {os.path.abspath('docker_layer_tree.png')}")


    print("Docker cache layer tree (top-down):")
    for layer_id, info in layers.items():
        if not info['parent'] or info['parent'] not in layers:
            print_tree(layer_id, layers)

def print_tree(layer_id, layers, depth=0, prefix=''):
    print(f"{prefix}{layer_id[:12]}")

    children = layers[layer_id]['children']
    for i, child_id in enumerate(children):
        is_last = (i == len(children) - 1)
        new_prefix = prefix + ("│   " if not is_last else "    ")
        connector = "└── " if is_last else "├── "
        print(f"{prefix}{connector}{child_id[:12]}")
        
        if layers[child_id]['children']:
            sub_prefix = prefix + ("    " if is_last else "│   ")
            print_tree(child_id, layers, depth+1, sub_prefix)

if __name__ == "__main__":
    main()
```
