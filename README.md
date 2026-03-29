<p align="center">
    <img src="https://image.biliup.me/2024-06-26/1719388842-365149-logo.png" width="400" alt="logo">
</p>

# 🎬 fork-biliup - B站直播录制与上传工具

![Python](https://img.shields.io/badge/Python-3.8+-blue?logo=python)
![License](https://img.shields.io/badge/License-MIT-green)

## 📖 项目简介

fork-biliup是B站直播录制与自动上传工具,支持多平台直播录制(B站、斗鱼、虎牙、Twitch、YouTube等),自动选择上传线路,支持弹幕录制和WebUI管理。

## 📦 项目来源

- **原项目**: [biliup/biliup](https://github.com/biliup/biliup)
- **原作者**: ForgQi
- **开源协议**: MIT License
- **Fork时间**: 2024年

## 🔧 二次开发内容

本项目为原项目的学习研究版本,未进行实质性修改,主要用于:
- 学习直播流媒体的录制原理
- 研究多平台直播源的解析方法
- 了解自动上传技术的实现

## 系统架构 | System Architecture

```mermaid
graph TB
    subgraph Input["📥 输入层"]
        A[直播平台URL] --> B[配置文件]
        C[WebUI界面] --> B
        D[命令行参数] --> B
    end
    
    subgraph Core["⚙️ 核心引擎"]
        B --> E[平台识别模块]
        E --> F{平台类型}
        F -->|B站| G[Bilibili处理器]
        F -->|斗鱼| H[Douyu处理器]
        F -->|虎牙| I[Huya处理器]
        F -->|Twitch| J[Twitch处理器]
        F -->|YouTube| K[YouTube处理器]
        G --> L[流媒体下载器]
        H --> L
        I --> L
        J --> L
        K --> L
    end
    
    subgraph Download["⬇️ 下载模块"]
        L --> M[Stream-gears]
        L --> N[Streamlink]
        L --> O[yt-dlp]
        L --> P[ykdl]
        M --> Q[防花屏处理]
        N --> Q
        O --> Q
        P --> Q
    end
    
    subgraph Upload["⬆️ 上传模块"]
        Q --> R[自动选择线路]
        R --> S[并发上传控制]
        S --> T[哔哩哔哩投稿]
    end
    
    subgraph Extra["🎯 扩展功能"]
        U[弹幕录制] --> V[外挂播放器]
        W[WebUI管理] --> X[远程控制]
        Y[Docker部署] --> Z[容器化运行]
    end
    
    style A fill:#e1f5ff
    style C fill:#e1f5ff
    style T fill:#c8e6c9
    style Q fill:#fff9c4
```

## 数据流转流程 | Data Flow

```mermaid
sequenceDiagram
    participant U as 用户
    participant W as WebUI/CLI
    participant C as 配置管理
    participant P as 平台处理器
    participant D as 下载器
    participant S as 存储系统
    participant B as B站API
    
    U->>W: 添加直播链接
    W->>C: 保存配置
    C->>P: 识别平台类型
    P->>P: 获取直播流地址
    P->>D: 启动下载任务
    D->>S: 保存视频文件
    D->>D: 防花屏处理
    D->>S: 保存弹幕文件
    
    loop 定时检测
        P->>P: 检测直播状态
        P->>D: 直播开始/结束
    end
    
    D->>B: 自动上传到B站
    B->>U: 上传完成通知
```

<div align="center">

[![python](https://img.shields.io/badge/python-3.7%2B-blue)](http://www.python.org/download)
[![PyPI](https://img.shields.io/pypi/v/biliup)](https://pypi.org/project/biliup)
[![PyPI - Downloads](https://img.shields.io/pypi/dm/biliup)](https://pypi.org/project/biliup)
[![license](https://img.shields.io/github/license/biliup/biliup)](https://github.com/biliup/biliup/blob/master/LICENSE)
[![Telegram](https://img.shields.io/badge/Telegram-Group-blue.svg?logo=telegram)](https://t.me/+IkpIABHqy6U0ZTQ5)


[![issues](https://img.shields.io/github/issues/biliup/biliup?label=Github%20issues)](https://github.com/biliup/biliup/issues)
[![STARS](https://img.shields.io/github/stars/biliup/biliup)](https://github.com/biliup/biliup/stargazers)
[![forks](https://img.shields.io/github/forks/biliup/biliup)](https://github.com/biliup/biliup/network)

</div>




  <p align="center">
    录制各大主流直播平台并上传至哔哩哔哩弹幕网<br />
  自动选择上传线路，保证上传稳定性，可手动调整并发<br />
    支持录制哔哩哔哩、斗鱼、虎牙、Twitch直播弹幕用于外挂播放器<br />
 防止录制花屏（使用默认的stream-gears下载器就会有这个功能），解决网络、PK导致的花屏。


<br />
    <a href="https://biliup.github.io/biliup/docs/guide/changelog"><strong>更新日志 »</strong></a>
    <br />
    <br />
    <a href="https://github.com/biliup/biliup/wiki/%E5%AE%89%E8%A3%85-%E8%BF%90%E8%A1%8C-%E6%9B%B4%E6%96%B0-%E5%8D%B8%E8%BD%BD">简易教程</a>
    ·
    <a href="https://biliup.me/">交流社区</a>
    ·
    <a href="https://github.com/biliup/biliup-app">投稿工具</a>
  </p>
</div>





<p align="center">
  <b>社区教程</b>: <a href="https://www.bilibili.com/opus/908292536945082370">图文教程</a> by <a href="https://github.com/ikun1993">@ikun1993</a>编写。
</p>


## Quick Start
### Windows
下载 exe: [Release](https://github.com/biliup/biliup/releases/latest)

### Linux or macOS
0. python`version >= 3.8`
1. `pip3 install biliup`
2. `biliup start`
3. 启动时访问 `http://your-ip:19159` 使用webUI，

### Docker
```sh
docker run -d \
  --name biliup \
  --restart unless-stopped \
  -p 0.0.0.0:19159:19159 \
  -v /path/to/save_folder:/opt \
  ghcr.io/biliup/caution:latest \
  --password password123
```
#### docker-compose.yml [点我](https://github.com/biliup/biliup/blob/master/docker-compose.yml) 
* 用户名为`biliup`
* 暴露在公网中也许会产生风险，所以设置密码是很有必要的。
* 以上示例根据需求进行修改，只作为参考。

* * * * * * * * *


![](.github/resource/light.png)
![](.github/resource/dark.png)

## How to Contribute

1. nodejs `version >= 18`
2. `npm i`
3. `npm run dev`
4. `python3 -m biliup`
5. 访问`http://localhost:3000`

## 支持

| 直播平台 | 支持类型      | 链接示例 | 特殊注释 |
| :------:| :--------------: | --------- | ------ |
| 虎牙 | 直播 | `https://www.huya.com/123456` | 可录制弹幕 |
| 斗鱼 | 直播 | `https://www.douyu.com/123456` | 可录制弹幕 |
| YY语音 | 直播 | `https://www.yy.com/123456` |
| 哔哩哔哩 | 直播 | `https://live.bilibili.com/123456` | 特殊分区hls流需要单独配置/可录制弹幕 |
| acfun | 直播 | `https://live.acfun.cn/live/123456` |
| afreecaTV | 直播 | `https://play.afreecatv.com/biliup123/123456` | 录制部分直播时需要登陆 |
| bigo | 直播 | `https://www.bigo.tv/123456` |
| 抖音 | 直播 | 直播:`https://live.douyin.com/123456(直播间数字号)`<br>直播:`https://live.douyin.com/tiktok(抖音号)`<br>主页:`https://www.douyin.com/user/456789(抖音号)` | 使用主页链接或被风控需配置cookies |
| 快手 | 直播 | `https://live.kuaishou.com/u/biliup123` | 监控开播需使用中国大陆IPv4家宽，<br>且24小时内单直播间最多120次请求 |
| 网易CC | 直播 | `https://cc.163.com/123456` |
| flextv | 直播 | `https://www.flextv.co.kr/channels/123456/live` |
| 映客 | 直播 | `https://www.inke.cn/liveroom/index.html?uid=123456` |
| 猫耳FM | 直播 | `https://fm.missevan.com/live/123456` | 猫耳为纯音频流 |
| nico | 直播 | `https://live.nicovideo.jp/watch/lv123456` | 可配置登录信息 |
| twitch | 直播<br>回放 | 直播:`https://www.twitch.tv/biliup123`<br>回放:`https://www.twitch.tv/biliup123/videos?filter=archives&sort=time`  | 可配置登录信息/尽量录制回放/可录制弹幕 |
| youtube | 直播<br>回放 | 直播:`https://www.youtube.com/watch?v=biliup123(单场)`<br>直播:`https://www.youtube.com/@biliup123/live(最远的预约)`<br>回放:`https://www.youtube.com/@biliup123/videos` | 可配置登录信息/尽量录制回放/可配置回放下载日期 |
* 理论上streamlink与yt-dlp支持的都可以下载，但不保证可以正常使用，详见:[streamlink支持列表](https://streamlink.github.io/plugins.html)，[yt-dlp支持列表](https://github.com/yt-dlp/yt-dlp/tree/master/yt_dlp/extractor).


## Credits
* Thanks `ykdl, youtube-dl, streamlink` provides downloader.
* Thanks `THMonster/danmaku`.


## 捐赠
* 爱发电 :`https://afdian.net/a/biliup`


## Stars
[![Star History Chart](https://api.star-history.com/svg?repos=biliup/biliup&type=Date)](https://star-history.com/#biliup/biliup&Date)
