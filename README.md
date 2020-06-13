# docker_images

Personal docker images.

## Images

|Ubuntu<br>Release|Software|Tag|
|:---------------:|:------:|:-:|
|Focal|ROS 2|[`:ros2-devel-focal`](./ros2/focal/Dockerfile)|

## ADE setup

1. Install [ADE](https://ade-cli.readthedocs.io/en/latest/)
   ```shell
   $ pip3 install -e git+https://gitlab.com/ApexAI/ade-cli#egg=ade_cli
   ```
1. Create `ade-home`
   ```shell
   $ cd ~
   $ mkdir ade-home
   $ cd ade-home
   $ touch .adehome
   ```
1. Copy `.bashrc`/`.bash_aliases`/other config files as needed
