---
layout: post
title: 从零开始搭建golang开发环境
tags: [devops,golang]
comments: true
---
# 1.安装golang
升级参考：[链接](https://zhuanlan.zhihu.com/p/453462046)

如果之前安装过go ，否则不用执行 
~~~
sudo rm -rf /usr/local/go
sudo apt-get remove golang
sudo apt-get remove golang-go
sudo apt-get autoremove
~~~

开始安装
~~~
# 版本可以换成想要的版本
mkdir ~/go && cd ~/go
# 下载golang安装包
wget https://studygolang.com/dl/golang/go1.16.12.linux-amd64.tar.gz
# 解压/usr/local目录下
tar -C /usr/local -zxvf go1.16.12.linux-amd64.tar.gz
~~~
配置环境变量
~~~
sudo vim /etc/profile
# 添加以下两行 GOROOT# go的安装目录
export GOROOT=/usr/local/go 
export PATH=$PATH:$GOROOT/bin
export GOPATH=/data/go
# 保存后source
go version
~~~
# 2.新建golang项目
~~~
mkdir -p $GOPATH/src
cd $GOPATH/src
mkdir go-project
cd go-project
#建main.go即可
go mod init
~~~
在go run main.go的时候需要拉取依赖包，进行如下配置
1. go env -w GOPRIVATE="git-core.megvii-inc.com" (设置私有仓库不走代理)
2. 为了更好更快的拉共有库的包, 需要设置代理: go env -w GOPROXY=https://goproxy.io 或者 go env -w GOPROXY=https://goproxy.cn,direct
3. git config --global url.ssh://git@git-core.megvii-inc.com/.insteadOf https://git-core.megvii-inc.com/ (访问git的方式由https转为ssh. 避免访问私有库时输入密码, 以本地公钥替代)


