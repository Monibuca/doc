# JESSICA 插件

通过 Websocket 传输音视频数据，使用 Jessibuca 播放器进行播放。

## 插件地址

https://github.com/Monibuca/plugin-jessica

## 插件引入

```go
import _ "m7s.live/plugin/jessica/v4"
```

## 配置

可配置 WS 协议和 WSS 协议监听地址端口

```yaml
jessica:
  http:
    listenaddr: :8080 # 网关地址，用于访问API
    listenaddrtls: "" # 用于HTTPS方式访问API的端口配置
    certfile: ""
    keyfile: ""
    cors: true # 是否自动添加cors头
    username: "" # 用户名和密码，用于API访问时的基本身份认证
    password: ""
<!--@include: @/block/config/config.subscribe.md-->
```

## 协议说明

该插件提供 websocket 格式的协议供 jessibuca 播放器播放。

### WS-RAW

- 地址格式：ws://[HOST]/jessica/[streamPath]

- 该协议传输的是私有格式，第一个字节代表音视频，1 为音频，2 为视频，后面跟 4 个字节的时间戳，然后接上字节流（RTMP 的 VideoTag 或 AudioTag）

### WS-FLV

- 地址格式：ws://[HOST]/jessica/[streamPath].flv
- 该协议传输的 flv 格式的文件流

## Raw-H26x

- 地址格式：`<http|ws>://[HOST]/jessica/[streamPath].<h264|h265>`
- 该协议传输裸流格式的 H264 或 H265 数据