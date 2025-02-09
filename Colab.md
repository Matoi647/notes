### Colab 更改 CUDA 版本

https://medium.com/@ajithkumarv/how-to-modify-cuda-gcc-python-versions-in-colab-584ed4113157

``` shell
!wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/cuda-ubuntu2204.pin
!sudo mv cuda-ubuntu2204.pin /etc/apt/preferences.d/cuda-repository-pin-600
!wget https://developer.download.nvidia.com/compute/cuda/11.8.0/local_installers/cuda-repo-ubuntu2204-11-8-local_11.8.0-520.61.05-1_amd64.deb
!sudo dpkg -i cuda-repo-ubuntu2204-11-8-local_11.8.0-520.61.05-1_amd64.deb
!sudo cp /var/cuda-repo-ubuntu2204-11-8-local/cuda-*-keyring.gpg /usr/share/keyrings/
!sudo apt-get update
!sudo apt-get -y install cuda-11-8

!export CUDA_HOME=/usr/local/cuda-11.8 && \
export PATH=/usr/local/cuda-11.8/bin:$PATH && \
export LD_LIBRARY_PATH=/usr/local/cuda-11.8/lib64:$LD_LIBRARY_PATH && \
nvcc --version
```

在 Colab 中使用环境变量

``` shell
import os

cuda_version = "11.8"

os.environ["CUDA_HOME"] = f"/usr/local/cuda-{cuda_version}"
os.environ["PATH"] = f"/usr/local/cuda-{cuda_version}/bin:" + os.environ["PATH"]
os.environ["LD_LIBRARY_PATH"] = f"/usr/local/cuda-{cuda_version}/lib64:" + os.environ.get("LD_LIBRARY_PATH", "")

!nvcc --version
```
