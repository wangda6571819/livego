# livego

原地址:
https://github.com/gwuhaolin/livego
https://github.com/zhangjunfang/livego


直播服务器
简单高效的直播服务器：
- 安装和使用非常简单；
- 纯 Golang 编写，性能高，跨平台；
- 支持常用的传输协议、文件格式、编码格式；

#### 支持的传输协议
- [x] RTMP  适合延迟比较小3-4s
- [x] AMF
- [x] HLS   延迟一般在10s
- [x] HTTP-FLV 延迟一般在10s

#### 支持的容器格式
- [x] FLV  支持flash格式
- [x] TS

#### 支持的编码格式
- [x] H264
- [x] AAC
- [x] MP3

#### 从源码编译
1. 下载源码 `git clone https://github.com/wangda6571819/livego.git`
2. 在 livego 目录上执行  go mod init github.com/wangda6571819/livego 生成 go.mod 文件
3. 执行 go get 下载依赖库文件
4. 执行 go build
5. 执行 go run livego.go 

控制台上打印出:
2021/01/18 16:19:01 livego.go:118: start livego, version master

2021/01/18 16:19:01 liveconfig.go:35: starting load configure file(livego.cfg)......

2021/01/18 16:19:01 liveconfig.go:42: loadconfig: 

{ 
    "server": [ 
	{ 
	"appname":"live", 
	"liveon":"on", 
	"hlson":"on" 
	} 
	] 
} 

2021/01/18 16:19:01 liveconfig.go:49: get config json data:{[{live on on []}]} 
2021/01/18 16:19:01 livego.go:87: HTTP-FLV listen On :7001 
2021/01/18 16:19:01 livego.go:105: HTTP-Operation listen On :8090 
2021/01/18 16:19:01 livego.go:43: HLS listen On :7002 
2021/01/18 16:19:01 livego.go:62: hls server enable.... 
2021/01/18 16:19:01 livego.go:70: RTMP Listen On :1935 

表示服务开启

## 使用
2. 启动服务：执行 `livego` 二进制文件启动 livego 服务；
3. 上行推流：通过 `RTMP` 协议把视频流推送到 `rtmp://localhost:1935/live/movie`，例如使用 `ffmpeg -re -i demo.flv -c copy -f flv rtmp://localhost:1935/live/movie` 推送；
4. 下行播放：支持以下三种播放协议，播放地址如下：
    - `RTMP`:`rtmp://localhost:1935/live/movie`
    - `FLV`:`http://127.0.0.1:7001/live/movie.flv`
    - `HLS`:`http://127.0.0.1:7002/live/movie.m3u8`
