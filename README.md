# Video-Download
Video Download using Annie

## 使用 annie 下载 B 站视频
当我们浏览 B 站或其他视频站点的时候，遇到了好的视频，就想下载下来永久收藏，或者我们即将去没有网络的偏远山区，想提前把视频下载到笔记本电脑上，那么我们该如何下载呢？  

恰好有这样一个工具，就是 annie，我们可以使用 annie 来下载，annie 是用 Go 语言构建的 CLI Tool（命令行工具），快速，简单的视频下载器，支持的平台很多，包括 MacOS、 Windows、 Linux 等，安装和使用是非常简单的，支持的网站也多，目前支持以下网站： 
<img src="https://github.com/cn666278/Video-Download/blob/main/website1.png" width="80%">  
<img src="https://github.com/cn666278/Video-Download/blob/main/website2.png" width="80%">  
接下来让我们先从 annie 开始吧 💪  
[Annie下载](https://blog.csdn.net/qq_41780295/article/details/119795152)  
annie 只是负责下载视频，而且是把一个完整的视频分成很多小视频下载，下载后的视频，我们还需要利用 FFmpeg 进行合并，接下来我们认识一下 FFmpeg。  

FFmpeg 是领先的多媒体框架，能够解码、编码、转码、混合、解密、流媒体、过滤和播放人类和机器创造的几乎所有东西。它支持最晦涩的古老格式，直到最尖端的格式；无论它们是由某个标准委员会、社区还是公司设计的；它还具有高度的便携性。

FFmpeg 可以在 Linux、Mac OS X、Microsoft Windows、BSDs、Solaris 等各种构建环境、机器架构和配置下编译、运行。

它包含了 libavcodec、libavutil、libavformat、libavfilter、libavdevice、libswscale 和 libswresample，可以被应用程序使用。还有 ffmpeg、ffplay 和 ffprobe，可以被终端用户用于转码和播放。

上面的内容是官方的介绍，说的直白一点：FFmpeg 可以进行音频、视频处理，也就是视频剪辑，音视和视频合并等。
只需要执行下面的命令确认一下即可：👇
```
whereis ffmpeg
ffmpeg -version
```
出现 ffmpeg: /usr/bin/ffmpeg......，以及 ffmpeg version 4.2.4......，说明本实验环境已经内置了 ffmpeg，且无需配置环境变量。

万事俱备只欠东风，有了 annie 和 FFmpeg，下一步就可以下载我们喜欢的视频 ~ 😬  

首先，配置 PATH 环境变量

同学们可以利用你们之前所学习的 Linux 知识，把 annie 的路径配置到 PATH 中，我们这里只是临时设置设置 annie 到 PATH 中（当前终端有效，新打开的终端还需要重新设置）。

输入下面的命令，设置临时环境变量：
```
export PATH=$PATH:/home/project
```
输入下面的命令，检测环境变量是否配置成功：
```
annie -v
```
如能出现： lux：version 字样，说明环境变量配置成功。

配置 annie 到 PATH。然后，下载 B 站视频

按下面的步骤依次操作：

打开一个自己感兴趣的视频网址，例如：
https://www.bilibili.com/video/BV1gK4y1u7UM?t=32.2

### 复制视频地址
在视频上点击右键，然后点击 “ 复制视频地址 ”。

用 annie 查看视频信息
在终端中输入下面的命令开始查看，地址就是上一步所复制的视频地址： 👇
```
annie -i https://www.bilibili.com/video/BV1gK4y1u7UM?t=32.2
```

视频信息如下图所示：
```
Site:      哔哩哔哩 bilibili.com
 Title:     走进蓝桥杯大赛国赛一等奖遍地的广东工业大学
 Type:      video
 Streams:   # All available quality
     [80-7]  -------------------
     Quality:         高清 1080P avc1.640032
     Size:            34.84 MiB (36536170 Bytes)
     # download with: lux -f 80-7 ...

     [80-12]  -------------------
     Quality:         高清 1080P hev1.1.6.L120.90
     Size:            27.98 MiB (29334283 Bytes)
     # download with: lux -f 80-12 ...

     [64-7]  -------------------
     Quality:         高清 720P avc1.640028
     Size:            24.79 MiB (25990532 Bytes)
     # download with: lux -f 64-7 ...

     [64-12]  -------------------
     Quality:         高清 720P hev1.1.6.L120.90
     Size:            22.64 MiB (23736482 Bytes)
     # download with: lux -f 64-12 ...

     [32-12]  -------------------
     Quality:         清晰 480P hev1.1.6.L120.90
     Size:            15.65 MiB (16407372 Bytes)
     # download with: lux -f 32-12 ...

     [32-7]  -------------------
     Quality:         清晰 480P avc1.64001F
     Size:            13.73 MiB (14396899 Bytes)
     # download with: lux -f 32-7 ...
```

可以看到有 1080P ，以及 720P..... ，可以输入不同的命令，选择下载不同的清晰度视频。

### 下载视频
清晰度越高，文件越大，同学们根据自己的实际情况选择，本实验下载 1080P 的，输入下面的命令开始下载 1080P 的视频：
```
annie -f 80-7 https://www.bilibili.com/video/BV1gK4y1u7UM?t=32.2
```


### 下载过程

下载过程中有 2 个文件，分别是音频文件（上图中 m4a 文件）和视频文件（上图中 mp4 文件），全部下载完毕后，会自动使用 ffmpeg 进行文件合并。


### 下载完毕

下载完毕后的最终格式是 mp4，大部分播放器都支持的格式。其中 Merging video...... 是 ffmpeg 进行音频和视频的合并操作。

本实验环境下不能进行视频的观看，同学们掌握了操作步骤后，可以右键下载到本机上，也可以在自己的电脑中再操作一次，下载完使用播放器查看下载的 mp4 视频。至此，使用 annie 下载视频就结束了，挺简单的吧，赶紧去下载自己感兴趣的视频吧~ 😄
