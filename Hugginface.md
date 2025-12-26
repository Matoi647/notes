### Huggingface 下载

``` python
import os
os.environ["HF_ENDPOINT"] = "https://hf-mirror.com"
os.environ["HF_HOME"] = ".cache/hf"
# os.environ['TORCH_HOME']=".cache/torch"

from huggingface_hub import snapshot_download
from huggingface_hub import login
login(token="hf_****")

# download single file
hf_hub_download(
    repo_id="robotics-diffusion-transformer/maniskill-model", 
    filename="rdt/mp_rank_00_model_states.pt", 
    local_dir="./maniskill-model")

# download repository
snapshot_download(
    repo_id="robotics-diffusion-transformer/maniskill-model",
    local_dir="./maniskill-model")

# download with file pattern
snapshot_download(
    repo_id="robotics-diffusion-transformer/maniskill-model",
    allow_patterns="lang_embeds/*",
    local_dir="./maniskill-model")

# download dataset
snapshot_download(
    repo_id="google/fleurs", 
    repo_type="dataset", 
    local_dir="./fleurs")
```

### Huggingface 国内镜像

https://blog.csdn.net/qyhua/article/details/139505301

如果要访问：https://huggingface.co/THUDM/chatglm3-6b

改成：https://hf-mirror.com/THUDM/chatglm3-6b，即可访问

或者直接换源：

``` python
# export HF_ENDPOINT=https://hf-mirror.com
import os
os.environ["HF_ENDPOINT"] = "https://hf-mirror.com"
```

### Hugginface 模型下载

如果无法访问，可以直接wget每个文件，并将url改成国内镜像


### 修改模型默认存储路径

``` python
# export HF_ENDPOINT=https://hf-mirror.com
# export HF_HOME=.cache/hf
# export TORCH_HOME=.cache/torch
import os
os.environ["HF_ENDPOINT"] = "https://hf-mirror.com"
os.environ["HF_HOME"] = ".cache/hf"
os.environ['TORCH_HOME']=".cache/torch"
```

### Huggingface上传

1. 首先在huggingface网站上手动创建仓库

2. `huggingface-cli login`，输入huffingface token

3. 
``` python
from huggingface_hub import HfApi

api = HfApi()
api.upload_folder(
    folder_path="/path/to/local/space",
    repo_id="username/my-cool-space",
    repo_type="space",
)
```

### Llama3 转换为 Huggingface 格式

https://github.com/huggingface/transformers/pull/30334

https://github.com/meta-llama/llama-recipes?tab=readme-ov-file#model-conversion-to-hugging-face

``` shell
## Install Hugging Face Transformers from source
pip freeze | grep transformers ## verify it is version 4.31.0 or higher

git clone git@github.com:huggingface/transformers.git
cd transformers
pip install protobuf
python src/transformers/models/llama/convert_llama_weights_to_hf.py \
   --input_dir /path/to/downloaded/llama/weights --model_size 7B --output_dir /output/path
```
