### 安装

``` shell
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.4/install.sh | bash
nvm install 22
npm install -g @openai/codex

curl -fsSL https://github.com/SaladDay/cc-switch-cli/releases/latest/download/install.sh | bash
```

### Codex 沙箱中无法使用 GPU
https://github.com/openai/codex/issues/3141#issuecomment-3646668952

``` shell
codex --yolo
```
