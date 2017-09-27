**警告:** goagent已经停止维护，本页面内容失效，请使用其他代理方法，参考[General recommendations (简体中文)](/index.php/General_recommendations_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "General recommendations (简体中文)")一文中的[中国大陆用户的推荐解决方案-代理](/index.php/General_recommendations_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E4.BB.A3.E7.90.86 "General recommendations (简体中文)")，选择其他工具。

GoAgent 是使用 [Python](/index.php/Python "Python") 和 Google App Engine SDK 编写的免费代理软件，利用 Google App Engine 充当代理服务器。

GoAgent 的运行原理于其他代理工具基本相同，其借由 Google App Engine 的服务器作为中传，将数据数据包后传送至 Google 服务器，再由 Google 服务器转发至目的服务器，接收数据时方法也类似。相对其他代理工具而言 GoAgent 要稳定许多。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 服务器端](#.E6.9C.8D.E5.8A.A1.E5.99.A8.E7.AB.AF)
    *   [2.2 客户端](#.E5.AE.A2.E6.88.B7.E7.AB.AF)
        *   [2.2.1 Chrome/Chromium](#Chrome.2FChromium)
        *   [2.2.2 亚全局](#.E4.BA.9A.E5.85.A8.E5.B1.80)
*   [3 运行](#.E8.BF.90.E8.A1.8C)
    *   [3.1 以 daemon 形式运行 (推荐)](#.E4.BB.A5_daemon_.E5.BD.A2.E5.BC.8F.E8.BF.90.E8.A1.8C_.28.E6.8E.A8.E8.8D.90.29)
        *   [3.1.1 屏蔽日志输出](#.E5.B1.8F.E8.94.BD.E6.97.A5.E5.BF.97.E8.BE.93.E5.87.BA)
        *   [3.1.2 日志输出至TTY](#.E6.97.A5.E5.BF.97.E8.BE.93.E5.87.BA.E8.87.B3TTY)
    *   [3.2 手动运行(不推荐+不支持)](#.E6.89.8B.E5.8A.A8.E8.BF.90.E8.A1.8C.28.E4.B8.8D.E6.8E.A8.E8.8D.90.2B.E4.B8.8D.E6.94.AF.E6.8C.81.29)
*   [4 疑难解答](#.E7.96.91.E9.9A.BE.E8.A7.A3.E7.AD.94)
    *   [4.1 Firefox 31.0 及以上版本提示安全连接失败：证书包含未知的关键扩展。](#Firefox_31.0_.E5.8F.8A.E4.BB.A5.E4.B8.8A.E7.89.88.E6.9C.AC.E6.8F.90.E7.A4.BA.E5.AE.89.E5.85.A8.E8.BF.9E.E6.8E.A5.E5.A4.B1.E8.B4.A5.EF.BC.9A.E8.AF.81.E4.B9.A6.E5.8C.85.E5.90.AB.E6.9C.AA.E7.9F.A5.E7.9A.84.E5.85.B3.E9.94.AE.E6.89.A9.E5.B1.95.E3.80.82)
        *   [4.1.1 解决方法 1 （推荐）](#.E8.A7.A3.E5.86.B3.E6.96.B9.E6.B3.95_1_.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89)
            *   [4.1.1.1 重新生成新的 GoAgent 证书](#.E9.87.8D.E6.96.B0.E7.94.9F.E6.88.90.E6.96.B0.E7.9A.84_GoAgent_.E8.AF.81.E4.B9.A6)
            *   [4.1.1.2 在 Firefox 中导入新证书](#.E5.9C.A8_Firefox_.E4.B8.AD.E5.AF.BC.E5.85.A5.E6.96.B0.E8.AF.81.E4.B9.A6)
        *   [4.1.2 解决方法 2](#.E8.A7.A3.E5.86.B3.E6.96.B9.E6.B3.95_2)
*   [5 参阅](#.E5.8F.82.E9.98.85)

## 安装

[官方软件源](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)")已收录 [goagent](https://www.archlinux.org/packages/?name=goagent)，直接用 [pacman](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)") 安装即可.

## 配置

### 服务器端

申请 Google Appengine 并创建 appid 。具体教程可参考[此](http://www.douban.com/note/262773856/)。

**注意:** appid请勿包含android/ios等关键词，否则有可能被某些网站识别为移动设备用户。

上传(使用root用户，否则会出现权限不够的问题）：

 `# python2 /usr/share/goagent/server/uploader.py` 
**注意:** 原来的uploader.zip在新版本已经不存在了，代替它的是uploader.py。如出现不能上传的情况可以去github上git下来用里面的那个uploader.py试试

**注意:** 无效的 hosts 可能会导致上传失败，可尝试清空 `/etc/resolv.conf` 再上传。 将来的版本更新可能会要求重新上传。请参看[官方的更新历史](https://code.google.com/p/goagent/#更新历史_2013)，带有[是]标记的则需要重新上传。此外是否需要重新上传是相对于前一版的，若您之前版本与当前版本之间某一版或多版带有[是]仍然需要重新上传

**提示：** 首次上传后，可以再任意修改 Appid，无需再重新上传，不过最好重启以生效

执行时会要求您再输入 appid ，请保持与 `proxy.ini` 中已有的一致；接着还要输入 Google 邮箱及密码。

**注意:** 若您的 Google 账户有开通两步验证功能，则密码应为16位的应用程序专用密码。

至此，代理服务器 127.0.0.1:8087 已搭建完毕。现在以 [Chrome/Chromium](/index.php/Chromium_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Chromium (简体中文)") 为例，示范使用代理服务器的方法。

**注意:** 若浏览器类软件要通过 GoAgent 代理访问 Internet，可能均需要导入证书

### 客户端

**提示：** goagent 3.1.2-2 引入了用户配置文件(goagent.user.ini), 配置方法有所变动. 如果您是从旧版本升级, 可以在按照如下方法配置后放心删除以前的 /etc/goagent.pacsave. 此次变动之后, 您将不再需要在每次升级后合并该配置文件.

打开 `/etc/goagent` (默认情况下该文件为空), 增加类似下面的段落:

```
[gae]
appid = your_appid
password = yourpassword

```

修改 `your_appid` 为您所申请的 appid。如果您申请了多个 appid 用于负载均衡, 用竖线 | 分隔多个id (不含空格). 如果您使用的服务端没有配置密码, 可以省略掉 `password =` 开头的一整行.

goagent 3.1.5-1 新增 dnsproxy 功能, 基本配置依然是修改 `/etc/goagent` 文件, 加入类似以下内容:

```
[dns]
enable = 1
listen = 127.0.0.1:5353

```

如果希望 DNS 服务跑在 53 端口, 需要使用 root 用户运行服务. 新增 `/etc/systemd/system/goagent.service.d/use_root.conf` 文件, 加入以下内容即可:

```
[Service]
User=root

```

#### Chrome/Chromium

请安装 [SwitchySharp 插件](https://chrome.google.com/webstore/detail/proxy-switchysharp/dpplabbmogkhghncfbfdeeokoefdjegm)，接着导入[该设置](https://goagent.googlecode.com/files/SwitchyOptions.bak)。可参考[该扩展提供的图解流程](https://code.google.com/p/switchysharp/wiki/SwitchySharp_GFW_List_2)。

打开设置－管理证书－授权中心－Authorities，导入 `/usr/share/goagent/local/CA.crt`，弹出窗口的三条选项均勾选。

**注意:** 如果第一次安装 GoAgent 尝试到此步骤时发现该文件不存在，请先启动一次 GoAgent 后再重新尝试。

#### 亚全局

在 Unix 和 GNU/Linux 中，大多 HTTP 应用程序均支持调用环境变量 `http_proxy` 和 `https_proxy` 进行代理，就像 lynx、 [wget](/index.php/Wget "Wget") 和 curl，甚至也包括了 [Chromium (简体中文)](/index.php/Chromium_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Chromium (简体中文)") 和 [git (简体中文)](/index.php/Git_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Git (简体中文)")。此外该环境变量的大小写其实并没有统一标准，有个别程序就只支持全大写的环境变量。所以为方便起见，直接在 `~/.bash_profile` 或 `~/.zshenv` 添加以下即可：

```
export http_proxy=[http://127.0.0.1:8087/](http://127.0.0.1:8087/)
export https_proxy=$http_proxy
export HTTP_PROXY=$http_proxy
export HTTPS_PROXY=$HTTP_PROXY

```

**注意:** 虽然 Chrome 浏览器也可以通过其环境变量进行全局代理从而不再需要 Proxy Extension，但不建议这么做，因为会导致访问国内网站的速度下降，甚至个别网站就拒绝境外代理访问，例如收录了大量版权视频的网站。

再执行以下命令，以导入证书进 Arch Linux。至此，就可以实现 Arch Linux 亚全局代理：

```
# ln -s /usr/share/goagent/local/CA.crt /etc/ca-certificates/trust-source/anchors/GoAgent.crt
# trust extract-compat

```

2014-12-11 官方发布新闻[证书导入采用新方法](https://www.archlinux.org/news/ca-certificates-update/)。若在此之前导入过证书，请进行清理：

```
# rm -fr /usr/share/ca-certificates/goagent
# rm -fr /etc/ca-certificates/conf.d

```

## 运行

### 以 daemon 形式运行 (推荐)

```
# systemctl start goagent

```

若想开机自启动，执行：

```
# systemctl enable goagent

```

**提示：** 可通过`# journalctl -u goagent`来查询日志

#### 屏蔽日志输出

如果不想让 GoAgent 的输出信息进入日志，可以通过屏蔽 goagent.service 里的对应行解决，方法如下：

1\. 创建目录 `/etc/systemd/system/goagent.service.d`

2\. 创建文件 `/etc/systemd/system/goagent.service.d/nostdout.conf`, 写入如下内容:

```
[Service]
StandardOutput=null

```

#### 日志输出至TTY

如果不想让 GoAgent 的输出信息进入日志，但是又想得到 GoAgent 的运行情况，可以通过修改 goagent.service 里的对应行解决，方法如下：

1\. 创建目录 `/etc/systemd/system/goagent.service.d`

2\. 创建文件 `/etc/systemd/system/goagent.service.d/totty.conf`, 写入如下内容:

```
[Service]
StandardOutput=tty
StandardError=tty
TTYPath=/dev/ttyX #X为数字，ttyX不能正在被使用，推荐为1-12之间的整数，用Ctrl+Alt+FX切换至
#TTYVTDisallocate=yes #若需要在启动前清理所在TTY的虚拟终端，取消本行前的注释

```

3.运行：

```
# systemctl daemon-reload && systemctl restart goagent

```

### 手动运行(不推荐+不支持)

由于不明原因，总有个别用户无法成功以 daemon 形式运行GoAgent，可改试手动运行：

```
$ sudo -u nobody python2 /usr/share/goagent/local/goagent

```

若是在更新后发生问题，可尝试清空`/usr/share/goagent/local/certs`目录，甚至卸载并手动删除`/etc/`和`/usr/share/`下的有关文件，然后重新安装和配置。

## 疑难解答

### Firefox 31.0 及以上版本提示安全连接失败：证书包含未知的关键扩展。

从 Firefox 31.0 开始默认使用新的 mozilla::pkix 为证书验证库。GoAgent 证书已被证实和此证书验证机制不兼容。新证书认证会导致提示“安全连接失败：证书包含未知的关键扩展。 （错误码： sec_error_unknown_critical_extension）”。解决的方法有两种，推荐使用解决方法 1 。

#### 解决方法 1 （推荐）

##### 重新生成新的 GoAgent 证书

取得 Root 权限并执行以下命令：

```
 # rm /usr/share/goagent/local/CA.crt
 # rm -rf /usr/share/goagent/local/certs
 # systemctl restart goagent

```

##### 在 Firefox 中导入新证书

在 Firefox 中点击右上角的菜单按钮（三道杠），在弹出的菜单中点击“首选项”（齿轮图标），打开首选项页面，点击"高级"-"证书"-"查看证书“，弹出一个新窗口，点击”证书机构“，在列表中找到"GoAgent CA"项并选中该项，点击"删除或不信任"，即完成删除原来的证书。点击"导入"，弹出文件选择窗口，进入目录 /usr/share/goagent/local/ ，选择文件 CA.crt 并点击打开，即完成导入新证书。点击确定关闭弹出窗口，重新启动 Firefox 即可。

#### 解决方法 2

在 Firefox 的地址栏上输入 about:config ，在输入框中输入 security.use_mozillapkix_verification ，在下面的列表中找到该项并双击修改为 false 。

## 参阅

*   [GoAgent 在 Google Code 的主页](https://code.google.com/p/goagent/)
*   [GoAgent 在 GitHub 的主页](https://github.com/goagent/goagent)
*   两位开发者的 Twitter 帐号：[@hewigovens](https://twitter.com/hewigovens),[@phuslu](https://twitter.com/phuslu)
*   [讨论亚全局代理的 Email List](https://groups.google.com/forum/#!topic/archlinux-cn/_PPW2dZHltE)