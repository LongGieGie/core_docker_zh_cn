### 1、安装docker
参考docker官网安装
### 2、安装和执行
**注意：docker build时如果遇到网络问题，请自行使用第三方docker镜像源或者使用TUN模式的VPN进行路由层面的代理**
[Overview - CORE Documentation (coreemu.github.io)](https://coreemu.github.io/core/install.html#dockerfile-based-install)
根据中国大陆网络环境定制了`Dockerfile_core903_emane151.ubuntu`，而非使用原本的`Dockerfile.ubuntu`
[LongGieGie/core_docker_zh_cn: 中国大陆环境下构建coreemu的docker镜像 (github.com)](https://github.com/LongGieGie/core_docker_zh_cn)
[sample-workload](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/sample-workload.html)
[GPU Enumeration](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/docker-specialized.html)
```shell
# build image
sudo docker build -t core -f Dockerfile_core903_emane151.ubuntu .
# start container  主机绝对路径:容器路径:rw
sudo docker run -itd --name core -e DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix:rw --privileged core
# start container with Nvidia Container Toolkit
sudo docker run -itd --name core -e DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix:rw --privileged --gpus all core
# launch core-daemon
sudo docker exec -it core core-daemon
# enable xhost access to the root user(允许本地root用户访问xserver，容器外部执行指令)
xhost +local:root
# launch core-gui
sudo docker exec -it core core-gui
```

