参考网站
[Overview - CORE Documentation (coreemu.github.io)](https://coreemu.github.io/core/install.html#dockerfile-based-install)
[core/dockerfiles/Dockerfile.ubuntu](https://github.com/coreemu/core/blob/master/dockerfiles/Dockerfile.ubuntu)

根据中国大陆网络环境定制了 `Dockerfile_core.ubuntu-zh_cn`，而非使用原本的 `Dockerfile.ubuntu`

```shell
# build image
sudo docker build -t core -f Dockerfile_core.ubuntu-zh_cn .
sudo docker build -t core_torch -f Dockerfile_core_torch_cu118.ubuntu-zh_cn .
# start container
sudo docker run -itd --name core -e DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix:rw --privileged core
# or start container with Nvidia Container Toolkit
sudo docker run -itd --name core -e DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix:rw --privileged --gpus all core
# launch core-daemon
sudo docker exec -it core core-daemon
# enable xhost access to the root user(允许本地root用户访问xserver)
xhost +local:root
# launch core-gui
sudo docker exec -it core core-gui
```
