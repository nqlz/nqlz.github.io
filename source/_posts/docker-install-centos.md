---
title: centos安装docker
date: 2019-09-26 09:20:09
tags: docker环境搭建
toc: true
categories: 
  - docker
---
## (一)、替换yum源
鉴于国内网络问题，强烈建议使用国内源，官方源请在注释中查看。
```bash
curl -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
yum clean all
yum makecache
```
<!--more-->
## (二)、安装
1、用yum 安装docker
安装必要依赖
```shell
sudo yum install -y yum-utils \
device-mapper-persistent-data \
lvm2
```
更新 yum 软件源缓存，并安装 docker-ce。
```shell
$ sudo yum makecache fast
$ sudo yum install docker-ce
```
如果需要最新版本的 Docker CE 请使用以下命令：
```shell
sudo yum-config-manager --enable docker-ce-edge
```
2、使用脚本自动安装
在测试或开发环境中 Docker 官方为了简化安装流程，提供了一套便捷的安装脚本，CentOS 系统上可以使用这套脚本安装：
```shell
$ curl -fsSL get.docker.com -o get-docker.sh
$ sudo sh get-docker.sh --mirror Aliyun
```
执行这个命令后，脚本就会自动的将一切准备工作做好，并且把 Docker CE 的 Edge 版本安装在系统中。

## （三）、配置
 1、配置镜像加速器
 鉴于国内网络问题，配置国内镜像加速器
 对于使用 systemd 的系统，请在 /etc/docker/daemon.json 中写入如下内容（如果文件不存在请新建该文件）
```json
 {
     "registry-mirrors": ["https://registry.docker-cn.com"],
     "exec-opts": ["native.cgroupdriver=systemd"]
 }
``` 
注意，一定要保证该文件符合 json 规范，否则 Docker 将不能启动。
之后重新启动服务。
```shell
sudo systemctl daemon-reload
sudo systemctl restart docker
```
2、建立 docker 用户组
默认情况下，docker 命令会使用 Unix Socket与 Docker 引擎通讯。而只有 root 用户和 docker 组的用户才可以访问 Docker 引擎的 Unix socket。出于安全考虑，一般 Linux 系统上不会直接使用 root 用户。因此，更好地做法是将需要使用 docker 的用户加入 docker 用户组。
建立 docker 组：
```shell
sudo groupadd docker
```
将当前用户加入 docker 组：
```shell
sudo usermod -aG docker $USER
```

## （四）、安装docker-compose
在 Linux 上的也安装十分简单，从 官方 GitHub Release处直接下载编译好的二进制文件即可。例如，在 Linux 64 位系统上直接下载对应的二进制包。
```shell
 sudo curl -L https://github.com/docker/compose/releases/download/1.25.1/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
 sudo chmod +x /usr/local/bin/docker-compose
```
如果以上方法不能docker-compose安装不成功，则用以下方法
点  [github这里](https://github.com/docker/compose/releases)  打开官网，网页拉到最下面,Assets下载对应平台的文件
以Linux为例，下载：[docker-compose-Linux-x86_64](https://github.com/docker/compose/releases/download/1.25.0-rc2/docker-compose-Linux-x86_64)
然后将文件上传到 /usr/local/bin/ 文件夹下，然后将其重命名为docker-compose，修改此文件的权限，增加可执行：chmod +x /usr/local/bin/docker-compose
然后再运行 
```bash
[root@nqlz ~]# docker-compose version
docker-compose version 1.25.0-rc2, build 661ac20e
docker-py version: 4.0.1
CPython version: 3.7.4
OpenSSL version: OpenSSL 1.1.0k  28 May 2019
```
问题解决。
ubuntu上安装移步{% post_link docker-install-ubuntu %}。
