## Packages

有不少软件可以挂载FTP，你可以将FTP挂载到某个目录下，然后就像本地文件系统一样操作。

*   curlftpfs [推荐]
*   fuseftp
*   lufs [过时了]

这三个都是基于FUSE库。

### curlftpfs

安装

```
# pacman -S curlftpfs

```

有必要的话，加载fuse内核模块

```
# modprobe fuse

```

有必要的话，创建一个挂载点。

```
# mkdir /mnt/ftp
# curlftpfs ftp.yourserver.com /mnt/ftp/ -o user=username:password

```

如果你想让其他用户访问，用以下命令。

```
# curlftpfs ftp.yourserver.com /mnt/ftp/ -o user=username:password,allow_other

```

不要添加额外的空格或逗号，否则 _allow_other_ 参数可能无法被程序识别.

如果要使用FTP的 active mode 挂载，请添加 'ftp_port=-':

```
# curlftpfs ftp.yourserver.com /mnt/ftp/ -o user=username:password,allow_other,ftp_port=-

```

你也可以把这一行加入 /etc/fstab 来自动在开机时后挂载。

```
curlftpfs#USER:PASSWORD@ftp.domain.org /mnt/mydomainorg fuse auto,user,uid=1000,allow_other 0 0

```

译者注，似乎这样用也是可以到。

```
sudo curlftpfs -o rw,allow_other [ftp://username:password@ftp.yourserver.com](ftp://username:password@ftp.yourserver.com) /mnt/ftp

```

如果中文出现乱码，你可能需要指定编码：

```
sudo curlftpfs -o codepage=gbk -o rw,allow_other [ftp://username:password@ftp.yourserver.com](ftp://username:password@ftp.yourserver.com) /mnt/ftp

```