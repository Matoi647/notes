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

### USD材质丢失

https://docs.omniverse.nvidia.com/extensions/latest/ext_usd-paths.html

1. 右击usd文件 -> Collect Assets

2. 左上角Windows -> Utilities -> USD Paths -> Search修改路径 -> Preview -> Apply
