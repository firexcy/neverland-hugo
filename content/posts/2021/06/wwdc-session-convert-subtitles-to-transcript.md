---
title: "从无文字版 WWDC 视频的字幕转制文字版"
date: "2021-06-13"
categories: 
---

大多数 WWDC 视频都配有文字版，在视频页面点击「Transcript」即可看到，还可以下载 TXT 格式版本。但也有少量视频（例如 [Design for Safari 15](https://developer.apple.com/videos/play/wwdc2021/10029/)）没有文字版，给检索和浏览造成不便。实际上，这类视频也有自动转写的字幕，只要下载后简单处理即可当作文字版浏览。

以上述 [Design for Safari 15](https://developer.apple.com/videos/play/wwdc2021/10029/) 讲座为例。

首先，用抓包工具（例如 Surge 或 Proxyman）抓取 WWDC 视频的域名 devstreaming-cdn.apple.com，并开始播放视频。

请求中，形如

```
https://devstreaming-cdn.apple.com/videos/wwdc/2021/10029/4/8B75DA3D-09DF-40FD-AC0E-FB6A7EECE3F1/subtitles/eng/prog_index.m3u8 
```

的即是获取字幕片段播放列表的请求，其内容为：

```
EXTM3U
#EXT-X-TARGETDURATION:7.0
#EXT-X-VERSION:3
#EXT-X-MEDIA-SEQUENCE:0
#EXT-X-PLAYLIST-TYPE:VOD
#EXTINF:6.006
sequence_0.webvtt
#EXTINF:6.006
sequence_1.webvtt
[...]
#EXTINF:6.006
sequence_334.webvtt
#EXTINF:0.3
sequence_335.webvtt
#EXT-X-ENDLIST
```

显然，这表明该视频的字幕共有从 `sequence_0.webvtt` 到 `sequence_335.webvtt` 共 336 个片段。

这样，在终端通过 `wget` 配合简单的循环即可批量下载：

```
counter=0
while [[ $counter -le 335 ]]
do
  wget "https://devstreaming-cdn.apple.com/videos/wwdc/2021/10029/4/8B75DA3D-09DF-40FD-AC0E-FB6A7EECE3F1/subtitles/eng/sequence_$counter.webvtt"
  ((counter++))
done
```

然后再通过一个循环将这些分段字幕合并为一个完整字幕：

```
counter=0
while [[ $counter -le 335 ]]                                                                  130
do
  cat "sequence_$counter.webvtt" >> full.webvtt
  ((counter++))
done
```

不过，`webvtt` 格式的字幕文件里有时间轴、格式信息和很多空行，并不方便阅读：

```
WEBVTT

00:19:58.498 --> 00:20:01.735 line:-2 align:center
Next, let’s talk about several
of the amazing new features

00:20:01.768 --> 00:20:03.904 align:center line:-1
of macOS, iOS, and iPadOS

00:20:03.937 --> 00:20:06.306 line:-1 align:center
and how they’ll impact the web.

00:20:06.340 --> 00:20:10.043 line:-2 align:center
Often, the very first experience
people will have of your website
```

解决方法也很简单，用随便一个支持正则表达式的文本编辑器搜索相关 pattern 批量删除即可。例如 Vim 中可以：

```
:g/WEBVTT/d
:g/-->/d
:g/\v^$/d
```

最后，由于是自动生成的字幕，会有不少同一句话出现两次的情况，这也可以通过正则表达式批量清理：

```
:g/\n^(.*)$\n\1/d
```
