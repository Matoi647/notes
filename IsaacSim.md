### IsaacSim安装

https://blog.csdn.net/weixin_61044335/article/details/137866781

### Omniverse Launcher下载IsaacSim速度过慢

https://blog.csdn.net/Vulcan_S/article/details/140004437

### 无法加载Asset

https://blog.csdn.net/Vulcan_S/article/details/142418933

### inotify 不足导致 `No space left on device`

``` shell
cat /proc/sys/fs/inotify/max_user_watches
sudo sysctl fs.inotify.max_user_watches=524288
```

### 设置 default prim

1. 找到root prim, unset default prim
2. 找到要设置的prim，左上角Edit->Unparent, 然后拖放到root prim同一层级
3. 选择要设置的prim, 右键set as default prim

### USD材质丢失

https://docs.omniverse.nvidia.com/extensions/latest/ext_usd-paths.html

1. 右击usd文件 -> Collect Assets

2. 左上角Windows -> Utilities -> USD Paths -> Search修改路径 -> Preview -> Apply


### X Error of failed request: GLXBadFBConfig

https://github.com/isaac-sim/IsaacLab/issues/2573

``` shell
2025-07-16 01:46:54 [0ms] [Warning] [omni.kit.app.plugin] No crash reporter present, dumps uploading isn't available.
X Error of failed request:  GLXBadFBConfig
  Major opcode of failed request:  148 (GLX)
  Minor opcode of failed request:  0 ()
  Serial number of failed request:  141
  Current serial number in output stream:  141
```

解决方法：`export DISPLAY=:0`
