相关文章

*   [Mirroring](/index.php/Mirroring "Mirroring")
*   [pacman](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)")
*   [reflector](/index.php/Reflector "Reflector")

本页面说明如何选择和配置镜像，以及列出可用的镜像。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 启用您喜爱的镜像](#启用您喜爱的镜像)
    *   [1.1 强制 pacman 刷新软件包列表](#强制_pacman_刷新软件包列表)
*   [2 镜像状态](#镜像状态)
*   [3 镜像排序](#镜像排序)
    *   [3.1 按速度排序](#按速度排序)
    *   [3.2 按速度和状态排序](#按速度和状态排序)
    *   [3.3 使用 Reflector](#使用_Reflector)
*   [4 官方镜像](#官方镜像)
    *   [4.1 支持 IPv6 的镜像](#支持_IPv6_的镜像)
*   [5 非官方镜像](#非官方镜像)
    *   [5.1 全球](#全球)
    *   [5.2 保加利亚](#保加利亚)
    *   [5.3 中国](#中国)
    *   [5.4 德国](#德国)
    *   [5.5 印度尼西亚](#印度尼西亚)
    *   [5.6 立陶宛](#立陶宛)
    *   [5.7 马来西亚](#马来西亚)
    *   [5.8 新西兰](#新西兰)
    *   [5.9 俄罗斯](#俄罗斯)
    *   [5.10 南非](#南非)
    *   [5.11 美国](#美国)
*   [6 参见](#参见)

## 启用您喜爱的镜像

想要启用镜像，打开 `/etc/pacman.d/mirrorlist` 并定位到你的地理区域。对您想使用的镜像取消注释。例如：

```
# Any
# Server = ftp://mirrors.kernel.org/archlinux/$repo/os/$arch
**Server = http://mirrors.kernel.org/archlinux/$repo/os/$arch**

```

参见 [#镜像状态](#镜像状态) 和 [#按速度排序](#按速度排序) 查看帮助选择镜像的工具。

**提示：**

*   取消5个你最喜欢的镜像的注释，把他们放在 mirrorlist 文件最上方。这样你就很容易找到它们并且如果第一个镜像出问题可以很容易切换。这也让合并 mirrorlist 更新更容易。
*   HTTP 镜像比 FTP 快，因为 HTTP 可以 [保持连接](https://en.wikipedia.org/wiki/HTTP_persistent_connection "wikipedia:HTTP persistent connection")，而使用 FTP 时 *pacman*每下载一个新软件包就需要重新建立连接。

也可以在 `/etc/pacman.conf` 中指定镜像。对于 *[core]* 仓库，默认设置是：

```
[core]
Include = /etc/pacman.d/mirrorlist

```

想要使用 *HostEurope* 镜像作为默认镜像，把它添加在 `Include` 行之前：

```
[core]
**Server = ftp://ftp.hosteurope.de/mirror/ftp.archlinux.org/core/os/$arch**
Include = /etc/pacman.d/mirrorlist

```

pacman 会首先尝试链接这个镜像。如果需要的话，可以继续修改*[testing]*, *[extra]*, 和 *[community]*部分。

**注意:** 如果镜像直接在 `pacman.conf` 中声明，记得在所有的仓库使用同样的镜像。否则不相容的包就可能被安装。如 *[core]* 中的 linux 和 *[extra]* 中的旧的内核模块不相容。

### 强制 pacman 刷新软件包列表

创建和编辑 `/etc/pacman.d/mirrorlist` 之后，使用下面命令刷新镜像：

```
# pacman -Syyu

```

传入两次`--refresh`或`-y`将强制更新所有软件包列表，即使系统认为它们已经是最新。**每次修改镜像之后都应该使用`pacman -Syyu`**。

## 镜像状态

可以通过访问如下网址检查镜像的状态：[https://www.archlinux.org/mirrors/status/](https://www.archlinux.org/mirrors/status/)

从[这里](https://www.archlinux.org/mirrorlist/)可以自动生成最新的镜像列表，安装[Reflector](/index.php/Reflector "Reflector")这个工具也可以自动检查和生成镜像列表。

## 镜像排序

### 按速度排序

更快的源可以显著的提升pacman的性能,和arch的整体操作体验。可以使用 `rankmirrors` 将镜像列表按速度排列。但是`rankmirrors`不能测试这些源的速度。

`cd`到`/etc/pacman.d/`目录:

 `# cd /etc/pacman.d` 

备份已经存在的`/etc/pacman.d/mirrorlist`:

 `# cp mirrorlist mirrorlist.backup` 

编辑`/etc/pacman.d/mirrorlist.backup`，取消要测速镜像前的注释。

让rankmirrors带上参数`-n`对这个备份文件`mirrorlist.backup`执行操作,然后把输出重定向以方便生成一个新的/etc/pacman.d/mirrorlist源列表:

 `# rankmirrors -n 6 mirrorlist.backup > mirrorlist` 
**注意:** **-n 6**:将生成6个最接近的源，运行`rankmirrors -h`可查看所有可用选项。

### 按速度和状态排序

仅是使用最快的镜像服务器并不是一件好事，因为它们可能是过时的。我们更推荐先[#按速度排序](#按速度排序)，然后在选出的镜像中按[#镜像状态](#镜像状态)排序。

只要简单地访问它们的[#镜像状态](#镜像状态)连接，然后将它们按照尽量新的顺序排序。将越新的镜像排到`/etc/pacman.d/mirrorlist`的越上面。如果镜像真的太过时了，别用它们（把它们注释掉，然后再[#按速度排序](#按速度排序)），重复这么做，排除过时的镜像。最后将有6个又快又新的镜像。

当出现镜像问题是，应该重复上面的步骤。或者一段时间就重复一次以保持`/etc/pacman.d/mirrorlist`最新，即使没有镜像问题。

### 使用 Reflector

[Reflector](/index.php/Reflector "Reflector")工具可以从[镜像状态](https://www.archlinux.org/mirrors/status/)页面自动获取最新的镜像列表，过滤掉未及时同步的镜像，然后按照速度排序覆盖`/etc/pacman.d/mirrorlist`。

## 官方镜像

官方镜像可以通过软件包 [pacman-mirrorlist](https://www.archlinux.org/packages/?name=pacman-mirrorlist) 获得。最新的镜像可以通过[Pacman 镜像列表生成器](https://www.archlinux.org/mirrorlist/)查询。

如果没有配置任何镜像，也没有安装 `pacman-mirrorlist`，请运行如下命令：

```
# wget -O /etc/pacman.d/mirrorlist https://www.archlinux.org/mirrorlist/all/

```

取消选中镜像前的注释然后：

```
# pacman -Syy
# pacman -S --force pacman-mirrorlist

```

如果要将自己的镜像加入官方列表，请提出申请并将其加入下面的 [#非官方镜像](#非官方镜像) 列表。

如果碰到 `$arch` 变量未定义的问题，请在 `/etc/pacman.conf` 中加入：

```
Architecture = auto

```

### 支持 IPv6 的镜像

[pacman 镜像列表生成工具](https://www.archlinux.org/mirrorlist/?country=all&protocol=http&ip_version=6) 可以用来查找当前的 IPv6 镜像。

## 非官方镜像

镜像**没有**加入`/etc/pacman.d/mirrorlist`.

### 全球

*   [http://sourceforge.net/projects/archlinux/files/](http://sourceforge.net/projects/archlinux/files/) - *Does not have recent ISO releases. Use it only if for getting older ISOs.*

### 保加利亚

*   [http://mirror.telepoint.bg/archlinux/](http://mirror.telepoint.bg/archlinux/)
*   [ftp://mirror.telepoint.bg/archlinux/](ftp://mirror.telepoint.bg/archlinux/)

### 中国

**电信**

*   [http://mirror.bit.edu.cn/archlinux/](http://mirror.bit.edu.cn/archlinux/) - *北京理工大学*
*   [http://mirrors.aliyun.com/archlinux/](http://mirrors.aliyun.com/archlinux/) - *阿里巴巴*
*   [http://mirrors.163.com/archlinux/](http://mirrors.163.com/archlinux/) - *网易*

**联通**

*   [http://mirrors.sohu.com/archlinux/](http://mirrors.sohu.com/archlinux/)
*   [http://mirrors.yun-idc.com/archlinux/](http://mirrors.yun-idc.com/archlinux/)

**教育网**

*   [http://mirror.hust.edu.cn/archlinux/](http://mirror.hust.edu.cn/archlinux/) - *华中科技大学*
*   [http://ftp.sjtu.edu.cn/archlinux/](http://ftp.sjtu.edu.cn/archlinux/) - *上海交通大学*
*   [http://mirrors.4.tuna.tsinghua.edu.cn/archlinux/](http://mirrors.4.tuna.tsinghua.edu.cn/archlinux/) *(ipv4 only)*
*   [http://mirrors.6.tuna.tsinghua.edu.cn/archlinux/](http://mirrors.6.tuna.tsinghua.edu.cn/archlinux/) *(ipv6 only)*
*   [http://mirror.lzu.edu.cn/archlinux/](http://mirror.lzu.edu.cn/archlinux/) - *兰州大学*
*   [https://mirrors.nju.edu.cn/archlinux/](https://mirrors.nju.edu.cn/archlinux/) - *南京大学*
*   [https://mirrors.dgut.edu.cn/archlinux/](https://mirrors.dgut.edu.cn/archlinux/) - *东莞理工学院*

### 德国

*   [http://ftp.uni-erlangen.de/mirrors/archlinux/](http://ftp.uni-erlangen.de/mirrors/archlinux/)
*   [ftp://ftp.uni-erlangen.de/mirrors/archlinux/](ftp://ftp.uni-erlangen.de/mirrors/archlinux/)
*   [http://ftp.u-tx.net/archlinux/](http://ftp.u-tx.net/archlinux/)
*   [ftp://ftp.u-tx.net/archlinux/](ftp://ftp.u-tx.net/archlinux/)

### 印度尼西亚

*   [http://mirror.kavalinux.com/archlinux/](http://mirror.kavalinux.com/archlinux/) - *only from Indonesia*
*   [http://kambing.ui.ac.id/archlinux/](http://kambing.ui.ac.id/archlinux/)
*   [http://repo.ukdw.ac.id/archlinux/](http://repo.ukdw.ac.id/archlinux/)

### 立陶宛

*   [http://edacval.homelinux.org/mirrors/archlinux/](http://edacval.homelinux.org/mirrors/archlinux/) - *Only from LT, without ISO*

### 马来西亚

*   [http://mirror.oscc.org.my/archlinux/](http://mirror.oscc.org.my/archlinux/)
*   [http://mirrors.inetutils.net/archlinux/](http://mirrors.inetutils.net/archlinux/) - *ISO and Core*

### 新西兰

*   [http://mirror.ihug.co.nz/archlinux/](http://mirror.ihug.co.nz/archlinux/)
*   [http://mirror.ece.auckland.ac.nz/archlinux/](http://mirror.ece.auckland.ac.nz/archlinux/) *NZ only*

### 俄罗斯

*   [http://hatred.homelinux.net/archlinux/](http://hatred.homelinux.net/archlinux/) - *Vladivostok, without iso, with <sub>[3SPY](http://hatred.homelinux.net/wiki/proekty:3spy:start)</sub> project repos and [**mingw32**](http://hatred.homelinux.net/archlinux/mingw32/os/i686) repo*

### 南非

*   [http://ftp.sun.ac.za/ftp/pub/mirrors/archlinux/](http://ftp.sun.ac.za/ftp/pub/mirrors/archlinux/) - *Stellenbosch University*
*   [ftp://ftp.sun.ac.za/pub/mirrors/archlinux/](ftp://ftp.sun.ac.za/pub/mirrors/archlinux/)
*   [http://ftp.leg.uct.ac.za/pub/linux/arch/](http://ftp.leg.uct.ac.za/pub/linux/arch/) - *University of Cape Town*
*   [ftp://ftp.leg.uct.ac.za/pub/linux/arch/](ftp://ftp.leg.uct.ac.za/pub/linux/arch/)

### 美国

*   [http://archlinux.linuxfreedom.com](http://archlinux.linuxfreedom.com) - *Contains numerous ISO images but does not contain the ISO dated 2011.08.19*
*   [http://mirror.pointysoftware.net/archlinux/](http://mirror.pointysoftware.net/archlinux/)

## 参见

*   [MirUp](http://wiki.gotux.net/code:bash:mirup) -- pacman mirrorlist downloader/checker