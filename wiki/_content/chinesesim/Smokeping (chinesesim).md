**翻译状态：** 本文是英文页面 [Smokeping](/index.php/Smokeping "Smokeping") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-04-07，点击[这里](https://wiki.archlinux.org/index.php?title=Smokeping&diff=0&oldid=473199)可以查看翻译后英文页面的改动。

[Smokeping](http://oss.oetiker.ch/smokeping/index.en.html)允许你监测多台服务器。 Smokeping使用RRDtool来存储数据，另外，其可基于RRDtool输出生成相应的统计图表。 Smokeping由两个部分组成。一个运行在后台、定期收集数据的服务。一个以图表形式展示数据的Web界面。

这个wiki页面包括安装smokeping后台服务和Web界面的基本步骤。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
    *   [1.1 可选的安装](#.E5.8F.AF.E9.80.89.E7.9A.84.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 编辑配置文件](#.E7.BC.96.E8.BE.91.E9.85.8D.E7.BD.AE.E6.96.87.E4.BB.B6)
        *   [2.1.1 有关smokeping配置文件语法的注意事项](#.E6.9C.89.E5.85.B3smokeping.E9.85.8D.E7.BD.AE.E6.96.87.E4.BB.B6.E8.AF.AD.E6.B3.95.E7.9A.84.E6.B3.A8.E6.84.8F.E4.BA.8B.E9.A1.B9)
    *   [2.2 安装系统中的其他部分](#.E5.AE.89.E8.A3.85.E7.B3.BB.E7.BB.9F.E4.B8.AD.E7.9A.84.E5.85.B6.E4.BB.96.E9.83.A8.E5.88.86)
    *   [2.3 启动服务](#.E5.90.AF.E5.8A.A8.E6.9C.8D.E5.8A.A1)

## 安装

这一节包括使用[smokeping](https://www.archlinux.org/packages/?name=smokeping)包安装[Smokeping](http://oss.oetiker.ch/smokeping/index.en.html)。 FastCGI的安装步骤可以参见[Apache and FastCGI](/index.php/Apache_and_FastCGI "Apache and FastCGI")。

smokeping软件包包括两个部分：

*   smokeping的后台服务和在`/etc/smokeping/`的配置文件。这个后台服务执行监测任务。
*   在`/srv/http/smokeping`的“htdocs”。这些文件被Web界面所使用。

除了安装[smokeping](https://www.archlinux.org/packages/?name=smokeping)包之外，您还需要：

*   一个smokeping监测的工具。[fping](https://www.archlinux.org/packages/?name=fping) 是默认ping探针的最简洁方法。
*   [apache](https://www.archlinux.org/packages/?name=apache) 和[mod_fcgid](https://www.archlinux.org/packages/?name=mod_fcgid) 被用于Web界面。
*   一个图像缓存目录，其可被FastCGI脚本写入，例如：`/srv/smokeping/imgcache`
*   一个数据存储目录，其可被smokeping后台服务写入，同时可被FastCGI脚本读取，例如：`/srv/smokeping/data`
*   确保主配置文件可被smokeping后台服务读取。

### 可选的安装

如果你想使用其他探针，例如DNS、http探针，你需要安装如下所示的其他软件包。 这些探针的配置并不包括在这个wiki页面中。

| 探针 | 所需软件包 |
| Curl | [curl](https://www.archlinux.org/packages/?name=curl) |
| DNS | [bind-tools](https://www.archlinux.org/packages/?name=bind-tools) (被用于Dig) |
| EchoPing | [echoping](https://www.archlinux.org/packages/?name=echoping) |
| SSH | [openssh](https://www.archlinux.org/packages/?name=openssh) |
| TelnetIOSPing | [perl-net-telnet](https://www.archlinux.org/packages/?name=perl-net-telnet) |
| AnotherDNS | [perl-net-dns](https://www.archlinux.org/packages/?name=perl-net-dns) |
| LDAP | [perl-ldap](https://www.archlinux.org/packages/?name=perl-ldap) |
| LDAP (tls) | [perl-io-socket-ssl](https://www.archlinux.org/packages/?name=perl-io-socket-ssl) |
| Authen | [perl-authen-radius](https://www.archlinux.org/packages/?name=perl-authen-radius) |

## 配置

Smokeping需要你编辑许多文件。 未编辑的文件的扩展名为`.dist`。将在`/etc/smokeping`目录中以`.dist`结尾的文件去除`.dist`后缀。 *find* 可以完成这件任务，同时打印出所有被重命名与需要编辑的文件。

```
# cd /etc/smokeping
# find . -name '*.dist' -print -execdir sh -c 'mv {} $(basename {} .dist)' \;
# mv /srv/http/smokeping/smokeping.fcgi.dist /srv/http/smokeping/smokeping.fcgi

```

### 编辑配置文件

下一步，编辑 `/etc/smokeping/config` 文件。这个文件是smokeping的主配置文件。 下面将用一个完整的配置文件例子简要介绍各节的功用。

`/etc/smokeping/config` 中 *General* 节是最容易被编辑的。 根据你个人信息个性化上述的配置文件。相应的条目均有注释。

注意：如果你没有安装`sendmail`的软件（例如：postfix 或 sendmail），使用一些别的东西代替，例如`/bin/false`。 你编辑的文件必须存在，否则smokeping将会报错。

*Alerts* 节。这个最小化的配置文件例子中并不需要 *Alerts* 节，所以你可以将其注释或删除。

*Database* 节不需要做任何改动。

*Presentation* 节中，模板文件的路径需要更新。

*Probes* 节规定哪些探针被激活。默认情况下，仅 *FPing* 探针被激活。这一节不需要做任何更改。

*Slaves* 节。这个最小化的配置文件例子中并不需要 *Slaves* 节，所以你可以将其注释或删除。注意：如果你在*Slaves*节中使用`smokeping_secrets`设置，你必须确保那个文件不能被其他用户访问，否则smokeping将会报错。`chmod 600 /etc/smokeping/smokeping_secrets`

*Targets* 节指定哪些主机将被探测（在这个例子中为ping的目标）。像如下的例子，根据你想要搜集统计数据的主机，个性化 *Targets* 节。

你可以在这个网址 [http://oss.oetiker.ch/smokeping/doc/smokeping_examples.en.html](http://oss.oetiker.ch/smokeping/doc/smokeping_examples.en.html) 了解更多关于Smokeping 配置文件的知识。

 `/etc/smokeping/config` 
```
*** General ***

owner     = Your Name Here                            # 你的名字
contact   = your.email@host.bla                       # 你的电子邮件地址
mailhost  = your.smtp.server.bla                      # 你的邮件服务器
sendmail  = /bin/false                                # sendmail程序路径
imgcache  = /srv/smokeping/imgcache                   # filesystem directory where we store files
imgurl    = imgcache                                  # URL directory to find them
datadir   = /srv/smokeping/data                       # daemon 与 webapp 共享的数据目录
piddir    = /var/run                                  # filesystem directory to store PID file
cgiurl    = http://localhost/smokeping/smokeping.fcgi  #  外部URL
smokemail = /etc/smokeping/smokemail   
tmail     = /etc/smokeping/tmail
syslogfacility = local0
# each probe is now run in its own process
# disable this to revert to the old behaviour
# concurrentprobes = no

*** Database ***

step     = 300
pings    = 20

# consfn mrhb steps total

AVERAGE  0.5   1  1008
AVERAGE  0.5  12  4320
    MIN  0.5  12  4320
    MAX  0.5  12  4320
AVERAGE  0.5 144   720
    MAX  0.5 144   720
    MIN  0.5 144   720

*** Presentation ***

template = /etc/smokeping/basepage.html

+ charts

menu = Charts
title = The most interesting destinations
++ stddev
sorter = StdDev(entries=>4)
title = Top Standard Deviation
menu = Std Deviation
format = Standard Deviation %f

++ max
sorter = Max(entries=>5)
title = Top Max Roundtrip Time
menu = by Max
format = Max Roundtrip Time %f seconds

++ loss
sorter = Loss(entries=>5)
title = Top Packet Loss
menu = Loss
format = Packets Lost %f

++ median
sorter = Median(entries=>5)
title = Top Median Roundtrip Time
menu = by Median
format = Median RTT %f seconds

+ overview 

width = 600
height = 50
range = 10h

+ detail

width = 600
height = 200
unison_tolerance = 2

"Last 3 Hours"    3h
"Last 30 Hours"   30h
"Last 10 Days"    10d
"Last 400 Days"   400d

*** Probes ***

+ FPing

binary = /usr/sbin/fping

*** Targets ***

probe = FPing

menu = Top
title = Network Latency Grapher
remark = Welcome to the SmokePing website of Arch User. \
         Here you will learn all about the latency of our network.

+ targets
menu = Targets

++ ArchLinux

menu = Arch Linux
title = Arch Linux Website
host = 66.211.214.131

++ GoogleDNS

menu = Google DNS
title = Google DNS server
host = 8.8.8.8

++ MultiHost

menu = Multihost example
title = Arch Wiki and Google DNS
host = /targets/ArchLinux /targets/GoogleDNS

```

#### 有关smokeping配置文件语法的注意事项

每一个 **+** 号定义了一个有着层次等级的节。在节名称中不允许含有空格。英文句号 **.** 和正斜杠 **/** 同样应当尽量避免出现在节名称中。这是因为存储在数据目录下的RRD文件有着和节名称一样的文件名。

在*Targets* 节，你可以用真实的主机名或其他节名称的路径来定义`host`，从而生成含有多个主机结果的图表，具体情况可以参考上面例子中的`MultiHost`。

### 安装系统中的其他部分

创建配置文件提到的额外目录：

```
# mkdir -p /srv/smokeping/data
# mkdir -p /srv/smokeping/imgcache
# chown -R smokeping:smokeping /srv/smokeping
# chown -R http:http /srv/smokeping/imgcache
# chmod a+rx /srv/smokeping
# chmod -R a+rx /srv/smokeping/data

```

由于smokeping配置文件同时被smokeping服务和FastCGI脚本读取，所以它应当具有可读取权限：

```
# chmod a+rx /etc/smokeping
# chmod a+r /etc/smokeping/config

```

### 启动服务

启动 [Start](/index.php/Start "Start") `smokeping.service`服务，并且确认它正在运行。

```
# systemctl start smokeping.service
# systemctl enable smokeping.service

```