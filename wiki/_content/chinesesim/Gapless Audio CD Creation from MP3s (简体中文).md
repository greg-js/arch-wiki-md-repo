## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 将MP3解码](#.E5.B0.86MP3.E8.A7.A3.E7.A0.81)
*   [3 创建一个目录文件表格](#.E5.88.9B.E5.BB.BA.E4.B8.80.E4.B8.AA.E7.9B.AE.E5.BD.95.E6.96.87.E4.BB.B6.E8.A1.A8.E6.A0.BC)
*   [4 刻录](#.E5.88.BB.E5.BD.95)

## 安装

我们将要用到一些程序。

```
pacman -S lame cdrdao

```

把cdrdao配置成为我们的CD刻录机。打开 <tt>/etc/cdrdao.conf</tt> (以root用户),加入刻录设备，格式如下：

```
write_device: "/dev/hdc"

```

检查看看cdrdao是否有正确的组权限，否则可能不能正常工作。

```
ls -l /usr/bin/cdrdao

```

输出的信息与以下类似：

```
-rwxr-xr-x 1 root optical 569040 2006-10-27 05:56 /usr/bin/cdrdao

```

如果不是，你可能要改变cdrdao属主chown为以下组：

```
# chown root:optical /usr/bin/cdrdao

```

## 将MP3解码

首先将所有你要刻录到CD的歌曲复制到一个文件夹。最好将他们按音轨顺序重命名(比如01.mp3, 02.mp3,等等). 现在我们将把全部MP3解码为未压缩的wav文件。请记住整张专辑可能解码超过800MB的wav文件，需要花费些时间。

```
mkdir wav
for file in *.mp3 ; do
   lame --decode "$file" "wav/$file.wav"
done

```

## 创建一个目录文件表格

完成后，让我们创建一个目录文件表格来描述CD规划。

```
cd wav
{
  echo "CD_DA"
  for file in *.wav ; do
    echo "TRACK AUDIO"
    # echo "PREGAP 00:02:00"  # insert a 2-second silent gap before each track
    echo "FILE \"$file\" 0"
  done
} > toc

```

## 刻录

最后我们只要做的就是刻录了。

```
cdrdao write toc

```