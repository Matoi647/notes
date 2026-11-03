### 安装

``` shell
# 1. codex-cli
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.4/install.sh | bash
nvm install 22
npm install -g @openai/codex

# 2. cc-switch-cli
curl -fsSL htts://github.com/SaladDay/cc-switch-cli/releases/latest/download/install.sh | bash

# 3. codex-provider-sync
npm install -g @dailin521/codex-provider-sync
```

### Codex 沙箱中无法使用 GPU
https://github.com/openai/codex/issues/3141#issuecomment-3646668952

``` shell
codex --yolo
```

### Codex 切换账号/中转站并迁移对话历史

1. cc-siwtch-cli 切换账号

2. `codex-provider sync`

3. `codex app-server daemon stop`

必须要停止 codex 的 daemon 进程，否则会出现以下报错：

```
Failed to resume session from /home/lbyang/.codex/sessions/2026/11/03/rollout-2026-11-03T10-18-20-01a19f33-362c-7840-8fe9-b6347f5416fd.jsonl: thread/resume failed during TUI bootstrap: thread/resume failed: This chat uses openai, but your current provider is custom. Switch to openai to continue. (code -32600), data: {"type":"modelProviderMismatch","modelProvider":"openai","currentModelProvider":"custom"}
```
