**翻译状态：** 本文是英文页面 [ClamAV](/index.php/ClamAV "ClamAV") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2014-03-22，点击[这里](https://wiki.archlinux.org/index.php?title=ClamAV&diff=0&oldid=304307)可以查看翻译后英文页面的改动。

[Clam AntiVirus](http://www.clamav.net) 是一款 UNIX 下开源的 (GPL) 反病毒工具包，专为邮件网关上的电子邮件扫描而设计。该工具包提供了包含灵活且可伸缩的监控程序、命令行扫描程序以及用于自动更新数据库的高级工具在内的大量实用程序。该工具包的核心在于可用于各类场合的反病毒引擎共享库。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 启动守护进程](#.E5.90.AF.E5.8A.A8.E5.AE.88.E6.8A.A4.E8.BF.9B.E7.A8.8B)
*   [3 更新病毒库](#.E6.9B.B4.E6.96.B0.E7.97.85.E6.AF.92.E5.BA.93)
*   [4 扫描病毒](#.E6.89.AB.E6.8F.8F.E7.97.85.E6.AF.92)
*   [5 疑难解答](#.E7.96.91.E9.9A.BE.E8.A7.A3.E7.AD.94)
    *   [5.1 Error: Clamd was NOT notified](#Error:_Clamd_was_NOT_notified)
    *   [5.2 Error: Can't create temporary directory](#Error:_Can.27t_create_temporary_directory)

## 安装

ClamAV 可通过 [clamav](https://www.archlinux.org/packages/?name=clamav) 包进行[安装](/index.php/Pacman "Pacman")，在[官方源](/index.php/Official_repositories "Official repositories")中可以找到.

## 启动守护进程

服务名是 `clamd.service`. 关于启动服务和设置自动启动的详细信息，请阅读 [Daemons](/index.php/Daemons "Daemons")。

## 更新病毒库

通过下列命令更新病毒库:

```
# freshclam

```

病毒库保存在下列文件中：

```
/var/lib/clamav/daily.cvd
/var/lib/clamav/main.cvd

```

## 扫描病毒

`clamscan` 可用以扫描文件, 用户目录亦或是整个系统：

```
$ clamscan myfile
$ clamscan -r -i /home
$ clamscan -r -i --exclude-dir='^/sys|^/proc|^/dev|^/lib|^/bin|^/sbin' /

```

*   如果希望 `clamscan` 删除感染的文件，请使用 `--remove` 参数。
*   使用 `-l _path/to/file_` 参数可以将 `clamscan` 的日志写入 log 文件。

## 疑难解答

### Error: Clamd was NOT notified

如果你在运行 freshclam 命令之后出现下列信息：

```
WARNING: Clamd was NOT notified: Cannot connect to clamd through 
/var/lib/clamav/clamd.sock connect(): No such file or directory

```

为 clamav 添加一个 sock 文件：

```
# touch /var/lib/clamav/clamd.sock
# chown clamav:clamav /var/lib/clamav/clamd.sock

```

然后， 编辑 `/etc/clamav/clamd.conf` – 去掉该行注释:

```
LocalSocket /var/lib/clamav/clamd.sock

```

保存并重启守护进程`systemctl restart clamd`

当启动守护进程时出现下列错误信息：

```
LibClamAV Error: cli_loaddb(): No supported database files found
in /var/lib/clamav ERROR: Not supported data format

```

以 root 身份运行 freshclam：

```
# freshclam -v

```

### Error: Can't create temporary directory

如果提示如下错误并给出 UID 和 GID 的提示，

```
# can't create temporary directory

```

请修改权限：

```
# chown UID:GID /var/lib/clamav & chmod 755 /var/lib/clamav

```