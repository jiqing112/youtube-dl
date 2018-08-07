默认主机环境为全局代理或者机身在墙外了

```
-F 获取视频链接的播放源，youtube是音视频分离的，所以通过-F参数可以看到很多
-f <序列号> 下在指定序列号的音频或视频,如何需要音视频合成，“视频序列号+音频序列号“
```

以Youtube这个视频“[Something Just Like This “](https://www.youtube.com/watch?v=anXh6C5bNQw)为例，执行命令获取下载源：

![](https://www.linuxprobe.com/wp-content/uploads/2018/07/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE_4.png)

在给定的输出结果中可以看到下载源，带有“audio only”字样的行是纯音频，带有"video only"字样的行是纯视频，视频行也有详细的参数代表着视频的质量，一般来说分辨率越大的视频质量越高。

最前面的format code代表着下载序列号。

比如要下载序列号为“248”的视频：

```
youtube-dl -f 248 https://www.youtube.com/watch?v=anXh6C5bNQw
```

这样下载下来的是纯视频，没有声音的。youtube-dl可以调用ffmpeg，将下载的音视频合成。

比如同时下载视频“248”和音频“251”并合成。**下载视频的序列号得放到下载音频前面。**

```
youtube-dl -f 248+251 https://www.youtube.com/watch?v=anXh6C5bNQw
```

如果没有安装ffmpeng，转换会报错。

CentOS6和7安装方法是不一样的，下面分别说明：

安装前都需要先安装epel扩展源

```
yum -y install epel-release
```

CentOS 6比较简单，安装yum源之后直接安装即可：

```
su -c 'yum localinstall --nogpgcheck https://download1.rpmfusion.org/free/el/rpmfusion-free-release-6.noarch.rpm https://download1.rpmfusion.org/nonfree/el/rpmfusion-nonfree-release-6.noarch.rpm'

yum -y install ffmpeg ffmpeg-devel
```

而CentOS 7需额外安装扩展源：

```
su -c 'yum localinstall --nogpgcheck https://download1.rpmfusion.org/free/el/rpmfusion-free-release-7.noarch.rpm https://download1.rpmfusion.org/nonfree/el/rpmfusion-nonfree-release-7.noarch.rpm'

rpm --import http://li.nux.ro/download/nux/RPM-GPG-KEY-nux.ro
rpm -Uvh http://li.nux.ro/download/nux/dextop/el7/x86_64/nux-dextop-release-0-1.el7.nux.noarch.rpm

yum -y install ffmpeg ffmpeg-devel
```