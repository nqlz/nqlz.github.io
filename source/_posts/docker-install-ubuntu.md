---
title: Ubuntu 安装 Docker
date: 2019-09-26 10:01:09
tags: docker环境搭建
toc: true
categories: 
  - docker
---
## 卸载旧版本
旧版本的 Docker 称为 docker 或者 docker-engine，使用以下命令卸载旧版本：
```bash
sudo apt-get remove docker \
docker-engine \
docker.io
```
<!--more-->
## （一）、使用APT安装时：
安装必要的一些系统工具
```bash
sudo apt-get update
sudo apt-get -y install apt-transport-https ca-certificates curl software-properties-common
```
安装 GPG 证书
```bash
curl -fsSL http://mirrors.aliyun.com/docker-ce/linux/ubuntu/gpg | sudo apt-key add -
```
写入软件源信息
```bash
sudo add-apt-repository "deb [arch=amd64] http://mirrors.aliyun.com/docker-ce/linux/ubuntu $(lsb_release -cs) stable"
```
更新并安装 Docker CE
```bash
sudo apt-get -y update
sudo apt-get -y install docker-ce
```
> 以上命令会添加稳定版本的 Docker CE APT 镜像源，如果需要最新或者测试版本的 Docker CE 请将 stable 改为 edge 或者 test。从 Docker 17.06 开始，edge test 版本的 APT 镜像源也会包含稳定版本的 Docker。

## (二)、使用脚本自动安装
在测试或开发环境中 Docker 官方为了简化安装流程，提供了一套便捷的安装脚本，Ubuntu 系统上可以使用这套脚本安装：
```bash
curl -fsSL get.docker.com -o get-docker.sh
# 可能会出现 404 错误，请移步下面的特别说明
sudo sh get-docker.sh --mirror Aliyun
```
执行这个命令后，脚本就会自动的将一切准备工作做好，并且把 Docker CE 的 Edge 版本安装在系统中。
如果已经使用了 Aliyun 脚本安装并成功的，卸载时请使用apt-get autoremove docker-ce命令
删除 /etc/apt/sources.list.d 目录下的 docker.list 文件
使用 AzureChinaCloud 镜像脚本重新安装，命令为：sudo sh get-docker.sh --mirror AzureChinaCloud

**启动 Docker CE**
```bash
sudo systemctl enable docker
sudo systemctl start docker
```
后续安装建立docker用户组以及安装docker-compose，可移步{% post_link docker-install-centos %}此篇目中有详细步骤。



