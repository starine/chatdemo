# 1. Chat Demo

- [1. Chat Demo](#1-chat-demo)
  - [1.1. 环境准备](#11-环境准备)
    - [1.1.1. 安装Golang](#111-安装golang)
    - [1.1.2. 代理设置](#112-代理设置)
    - [1.1.3. 安装VSCODE](#113-安装vscode)
  - [1.2. 启动服务](#12-启动服务)
  - [1.3. 测试](#13-测试)

> 这是一个简单的websocket协议demo。

## 1.1. 环境准备

### 1.1.1. 安装Golang

打开 https://golang.google.cn/dl/ ，下载对应的安装包。

**在Mac下可以在终端执行**:

>brew install golang

### 1.1.2. 代理设置

打开你的终端并执行

```cmd
go env -w GO111MODULE=on
go env -w GOPROXY=https://goproxy.cn,direct
```

> https://goproxy.cn/

### 1.1.3. 安装VSCODE

从 https://code.visualstudio.com/ 下载`Visual Studio Code`。

安装完vscode之后，就可以打开本demo项目了，它会提示你安装一些`扩展和Golang的环境工具`，确认安装即可。

## 1.2. 启动服务

> go run main.go chat

```shell
$ go run main.go chat
INFO[0000] started                                       id=demo listen=":8000" module=Server
```

## 1.3. 测试服务端

打开两个websocket测试界面（ http://coolaf.com/tool/chattest ）, 并分别输入指定URL：

```html
ws://localhost:8000?user=userA
ws://localhost:8000?user=userB
```
测试是否可以连接服务端和发消息。

服务端信息如下：
```shell
$ go run main.go chat
INFO[0000] started                                       id=demo listen=":8000" module=Server
INFO[0008] user userA in from [::1]:58475                id=demo listen=":8000" module=Server
INFO[0013] user userB in from [::1]:58570                id=demo listen=":8000" module=Server
INFO[0035] {true 0 1 true [158 255 186 220] 16}         
INFO[0035] recv message hello i am userA from userA     
INFO[0035] send to userB : hello i am userA -- FROM userA 
INFO[0052] {true 0 1 true [187 15 45 19] 23}            
INFO[0052] recv message 你好， 我是用户B from userB            
INFO[0052] send to userA : 你好， 我是用户B -- FROM userB   
```
### <span id="head8"> 测试服务端：</span>
https://user-images.githubusercontent.com/42311991/184083831-9f666a28-c1a4-4406-8dc4-b13b9c85423c.mp4

## 1.3. 测试客户端
启动服务端：
```shell
$ go run main.go chat               
INFO[0000] started                                       id=demo listen=":8000" module=Server
INFO[0010] user userA in from 127.0.0.1:56201            id=demo listen=":8000" module=Server
INFO[0018] user userB in from 127.0.0.1:56330            id=demo listen=":8000" module=Server
INFO[0060] wirte a pong...                              
INFO[0068] wirte a pong...  
```

打开两个终端分别启用两个客户端，可以看到其中控制台输出的消息如下：

```shell
$ go run main.go client --user=userA
INFO[0000] connect to ws://127.0.0.1:8000?user=userA    
INFO[0000] readloop started                             
INFO[0000] heartbeatloop started                        
INFO[0050] ping...                                      
INFO[0050] recv a pong...   
```

```shell
$ go run main.go client --user=userB
INFO[0000] connect to ws://127.0.0.1:8000?user=userB    
INFO[0000] readloop started                             
INFO[0000] heartbeatloop started                        
INFO[0050] ping...                                      
INFO[0050] recv a pong...                 
```
### <span id="head8"> 测试客户端：</span>
https://user-images.githubusercontent.com/42311991/184084367-fb27fa81-4d85-421d-8764-5fe98ad2b390.mp4
