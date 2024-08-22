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
import os
os.environ["HF_ENDPOINT"] = "https://hf-mirror.com"
os.environ["HF_HOME"] = "./cache/hf"
os.environ['TORCH_HOME']='./cache/torch'
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
