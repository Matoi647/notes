https://developer.nvidia.com/cuda-downloads

### conda 安装 CUDA

https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#conda-installation

### `nvcc -V` 和 `nvidia-smi` 的区别

https://stackoverflow.com/questions/53422407/different-cuda-versions-shown-by-nvcc-and-nvidia-smi

`nvidia-smi` 显示的是当前驱动版本、当前驱动支持的最高 CUDA 版本 ？

`nvcc -V` 显示的是当前安装的 CUDA 版本

### python 查看当前 torch 使用的 CUDA 版本

```
import torch
print(torch.version.cuda)
```
