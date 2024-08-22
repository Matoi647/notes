### Huggingface 国内镜像

https://blog.csdn.net/qyhua/article/details/139505301

如果要访问：https://huggingface.co/THUDM/chatglm3-6b

改成：https://hf-mirror.com/THUDM/chatglm3-6b，即可访问

或者直接换源：

``` python
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
