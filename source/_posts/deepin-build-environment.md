---
title: deepin开发环境搭建
date: 2019-10-09 16:51:01
tags: deepin
toc: true
categories: 
  - linux
---
## (一) 配置node、npm
配置node、npm
访问 [官网](https://nodejs.org/en/) 下载对应的文件
解压,然后给node-v8.9.0-linux-x64文件夹改名（改不改名无所谓，路径对了就行）
```bash
tar -xvf node-v8.9.0-linux-x64.tar
mv node-v8.9.0-linux-x64 nodejs
```
<!--more-->
node和npm链接到/usr/local/bin下，可以执行
```bash
ln -s /usr/local/nodejs/bin/node /usr/local/bin/node
ln -s /usr/local/nodejs/bin/npm /usr/local/bin/npm
```
注意：要根据自己的路径进行设置，不要照搬。
OK！大功告成！现在可以在任何目录下执行node和npm命令了！
```bash
node -v
npm -v
```

## (二)sdkman配置Java、maven
这是[sdkman官网](sdkman官网),安装sdkman
```bash
curl -s "https://get.sdkman.io" | bash
source "$HOME/.sdkman/bin/sdkman-init.sh"
// 查看Java可用版本并安装
sdk list java
sdk install java 8.0.222-amzn

//查看maven并安装
```bash
sdk list maven
sdk install maven 3.5.4
```
## (三)docker
{% post_link docker-install-centos %}结合{% post_link docker-install-ubuntu %}
搞定docker环境

注意：使用深度终端管理远程服务器的时候，服务器中应安装rz,sz命令，上传下载才不会报错
```bash
yum install lrzsz
```

