https://developer.nvidia.com/cuda-downloads

### conda 安装 CUDA

https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#conda-installation

```
conda install cuda -c nvidia
```

安装指定版本

```
conda install cuda -c nvidia/label/cuda-11.8.0
pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
# pip3 install torch==2.0 --index-url https://download.pytorch.org/whl/cu118
# pip3 install torch==2.0 -f https://mirrors.aliyun.com/pytorch-wheels/cu118
```



### `nvcc -V` 和 `nvidia-smi` 的区别

https://stackoverflow.com/questions/53422407/different-cuda-versions-shown-by-nvcc-and-nvidia-smi

`nvidia-smi` 显示的是当前驱动版本、当前驱动支持的最高 CUDA 版本 ？

`nvcc -V` 显示的是当前安装的 CUDA 版本


### 实时查看显存占用

`pip install nvitop`

### 显存未释放

`ps aux | grep python` 查看进程的启动命令

### python 查看当前 torch 使用的 CUDA 版本

```
import torch
print(torch.version.cuda)
```

如果是通过 `conda install cuda -c nvidia/label/cuda-11.8.0 -y` 安装的 CUDA，则会改变整个 conda 环境中的 CUDA 路径，以上命令与 `nvcc -V` 显示的 CUDA 版本相同

如果是通过 `pip install torch==2.3.1` 安装的 CUDA，则会根据 torch 的 requirements.txt 安装对应版本的 CUDA (nvidia-cuda-runtime-cu12==12.1.105)，而 `nvcc -V` 仍然显示 conda 环境之外的 CUDA 版本
