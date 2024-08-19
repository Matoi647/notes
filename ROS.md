### Docker 安装 ROS

https://blog.csdn.net/zysss_/article/details/134125740

```shell
docker pull osrf/ros:humble-desktop-full
```

``` shell
docker run -it  \
    --env="DISPLAY" \
    --env="QT_X11_NO_MITSHM=1" \
    --volume="/tmp/.X11-unix:/tmp/.X11-unix:rw" \
    osrf/ros:noetic-desktop-full \
```

```shell
docker exec -it <container_name> /bin/bash
```

```shell
# setup.bash或者setup.zsh
echo "source /opt/ros/humble/setup.bash" >> ~/.bashrc
soruce ~/.bashrc
```

