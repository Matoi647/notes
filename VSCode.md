### Debug 配置

`launch.json`

#### 调试 python 程序

`justMyCode: false` 调试外部库

``` json
{
    "name": "llava-dpo-debug",
    "type": "debugpy",
    "request": "launch",
    "program": "/home/lbyang/workspace/llm-robot/openvla/trl/examples/scripts/dpo_visual.py",
    "console": "integratedTerminal",
    "args": [
        "--dataset_name", "/home/lbyang/workspace/llm-robot/openvla/trl/mytest/data/rlaif-v_formatted",
        "--model_name_or_path", "/home/lbyang/workspace/llm-robot/openvla/llava-1.5-7b-hf",
        ...
    ],
    "justMyCode": false
}
```

#### torchrun 调试

`cwd` 指定调试工作目录

`module` 指定 torchrun 入口

`args` 需要填写 torchrun 的参数和 python 文件的参数

``` json
{
    "name": "openvla-sft-debug",
    "type": "debugpy",
    "request": "launch",
    "console": "integratedTerminal",
    "module": "torch.distributed.run",
    "env": {
        "CUDA_VISIBLE_DEVICES": "1",
    },
    "cwd": "/home/lbyang/workspace/llm-robot/openvla",
    "args": [
        "--standalone",
        "--nnodes", "1",
        "--nproc_per_node", "1",
        "./vla-scripts/finetune.py", 
        "--vla_path", "./openvla-7b",
        ...
    ],
    "justMyCode": false
}, 
```


