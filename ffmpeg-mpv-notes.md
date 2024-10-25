## 关于 FFMPEG 和 MPV 的笔记

### 抽取视频流导出为 H264 裸数据

```
ffmpeg -i 源视频 -an -codec:v copy -bsf:v h264_mp4toannexb 输出1.h264
```

- -an Skip inclusion of audio streams
- -codec:v Select an encoder for video streams
- copy Indicate that the stream is not to be re-encoded
- -bsf:v Set a bitstream filter for video streams
- h264_mp4toannexb

### 提取一个视频的音频文件

```
ffmpeg -i 源视频 -vn -codec:a copy 输出2.m4a
```

- -vn Skip inclusion of video streams
- -codec:a Select an encoder for audio streams
- copy Indicate that the syream is not to be re-encoded

### 将音频和 H264 裸数据整合到一起

```
ffmpeg -ss 00:05 -i 音频.m4a -i 视频裸数据.h264 -codec:a copy -bsf:a
```

- aac_adtstoasc -codec:v copy -f mp4 输出视频.mp4

### MPV 播放 .m3u8

```
mpv 文件名.m3u8 --demuxer-lavf-o=protocol_whitelist=[file,http,https,tls,rtp,tcp,udp,crypto,httpproxy,data]
```
