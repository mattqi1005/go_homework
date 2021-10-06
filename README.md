# go_homework
[go 9.25课后作业.md](https://github.com/mattqi1005/go_homework/files/7295322/go.9.25.md)
️ go 9.25课后作业
内容：编写一个 HTTP 服务器，大家视个人不同情况决定完成到哪个环节，但尽量把1都做完



##### 1.接收客户端 request，并将 request 中带的 header 写入 response header

a.搭建go linux环境（CentOS7）

​	下载go安装包

```sh
wget https://studygolang.com/dl/golang/go1.17.1.linux-amd64.tar.gz
```

​	解压至/opt目录下

```sh 
 tar -xvf go1.17.1.linux-amd64.tar.gz -C /opt/
```

​	配置go环境变量

​		`GOROOT`=/opt/go

​		`GOPATH`=/root/goprojects/

```go
export GOROOT=/opt/go
export PATH=$PATH:$GOROOT/bin
export GOPATH=$HOME/goprojects/
```

b.clone httpserver项目

```sh
[root@node1 ~]# mkdir -p $GOPATH/src/github.com/cncamp
[root@node1 ~]# yum install -y git
[root@node1 ~]# cd $GOPATH/src/github.com/cncamp
[root@node1 cncamp]# git git clone https://github.com/cncamp/golang.git
```

b.设置go mod

```sh
[root@node1 cncamp]# cd golang
[root@node1 golang]# mv go.mod go.mod.bak
[root@node1 golang]# mv go.sum go.sum.bak
[root@node1 golang]# go mod init
go: creating new go.mod: module github.com/cncamp/golang
go: to add module requirements and sums:
        go mod tidy
[root@node1 golang]# cat go.mod
module github.com/cncamp/golang

go 1.17
[root@node1 golang]# go mod tidy
go: finding module for package github.com/golang/glog
github.com/cncamp/golang/httpserver imports github.com/golang/glog: module github.com/golang/glog: Get "https://proxy.golang.org/github.com/golang/glog/@v/list": dial tcp 142.251.43.17:443: connect: connection refused
[root@node1 golang]# go env |grep -i goproxy
GOPROXY="https://proxy.golang.org,direct"
[root@node1 golang]# export GOPROXY="https://goproxy.cn,direct"
[root@node1 golang]# go env |grep -i goproxy
GOPROXY="https://goproxy.cn,direct"
[root@node1 golang]# go mod tidy
go: finding module for package github.com/golang/glog
go: downloading github.com/golang/glog v1.0.0
go: found github.com/golang/glog in github.com/golang/glog v1.0.0
[root@node1 golang]#
[root@node1 golang]# cat go.mod
module github.com/cncamp/golang

go 1.17

require github.com/golang/glog v1.0.0
```

c.go build httpserver 项目

```sh 
[root@node1 golang]# cd httpserver/
[root@node1 httpserver]# go build main.go
[root@node1 httpserver]# ./main
ERROR: logging before flag.Parse: I1007 06:11:53.918633   68667 main.go:17] Starting http server...
entering root handler
entering root handler
```

d.运行./main并检查httpserver

![go-1.png](https://i.loli.net/2021/10/06/kWdTb63P9Xlht8J.png)2.读取当前系统的环境变量中的 VERSION 配置，并写入 response header



3.Server 端记录访问日志包括客户端 IP，HTTP 返回码，输出到 server 端的标准输出



##### 4.当访问 localhost/healthz 时，应返回200

![go-2.png](https://i.loli.net/2021/10/06/gbeUh6pNQwcmFEM.png)




