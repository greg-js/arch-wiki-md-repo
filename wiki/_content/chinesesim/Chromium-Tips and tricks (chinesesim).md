相关文章

*   [Chromium (简体中文)](/index.php/Chromium_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Chromium (简体中文)")
*   [Firefox Tweaks](/index.php/Firefox_Tweaks "Firefox Tweaks")

**翻译状态：** 本文是英文页面 [Chromium_Tips_and_Tweaks](/index.php/Chromium_Tips_and_Tweaks "Chromium Tips and Tweaks") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2012-10-07，点击[这里](https://wiki.archlinux.org/index.php?title=Chromium_Tips_and_Tweaks&diff=0&oldid=226108)可以查看翻译后英文页面的改动。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 浏览体验](#浏览体验)
    *   [1.1 chrome://xxx](#chrome://xxx)
    *   [1.2 下载标签图标错误](#下载标签图标错误)
    *   [1.3 鼠标的滚动速度](#鼠标的滚动速度)
    *   [1.4 搜索引擎](#搜索引擎)
    *   [1.5 Tmpfs](#Tmpfs)
        *   [1.5.1 tmpfs 作为缓存](#tmpfs_作为缓存)
        *   [1.5.2 tmpfs 保存配置](#tmpfs_保存配置)
*   [2 安全](#安全)
    *   [2.1 沙箱中运行](#沙箱中运行)
    *   [2.2 用户终端信息](#用户终端信息)

## 浏览体验

### chrome://xxx

在地址栏中输入 "chrome://xxx" 可以修改一些选项。完整的列表位于**chrome://chrome-urls**，其中包括:

*   chrome://flags - 启用实验功能，例如 WebGL 和 GPU 网页渲染等
*   chrome://gpu-internals - GPU 选项的状态
*   chrome://sandbox - 沙箱状态
*   chrome://version - 显示版本和启动 `/usr/bin/chromium` 时使用的开关
*   chrome://plugins - 查看、启用和禁用当前使用的插件。

[这里](http://peter.sh/experiments/chromium-command-line-switches/)包含一个不停更新的 chromium 开关列表。

### 下载标签图标错误

如果 Chromium 下载标签页显示的图标不正确，一直是破损文档的形式，可能是因为没有安装软件包 [gnome-icon-theme](https://www.archlinux.org/packages/?name=gnome-icon-theme)。[安装](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)")这个软件包应该能修复这个错误。

### 鼠标的滚动速度

使用`--scroll-pixels=` 选项设置鼠标滚动速度，例如：

```
$ chromium --scroll-pixels=200

```

### 搜索引擎

在 wiki.archlinux.org 和 wikipedia.org 上直接搜索可以更快找到需要的内容。先执行一次搜索，然后到 Options>Preferences>Basics 并点击默认搜索中的 "管理"。“编辑” Wikipedia 项，将关键字改为 "w"。这样要从 Wikipedia 搜索 "Arch Linux"，只需在地址栏输入 "w arch linux"。

Google search 已经有了写死的 **?** 关键字，所以不需要手动创建。

### Tmpfs

#### tmpfs 作为缓存

**注意:** Chromium 将缓存目录和配置目录**分开存放**。

要减少 Chromium 的缓存写入磁盘操作，可以用`--disk-cache-dir=/foo/bar` 将缓存定义到其它地方：

```
$ chromium --disk-cache-dir=/tmp/cache

```

或者编辑`/etc/fstab`，添加：

```
 tmpfs     /home/<user>/.cache/chromium tmpfs mode=1777,noatime 0 0

```

Cache 应该都是临时保存，重启后会丢失。

#### tmpfs 保存配置

将浏览器配置放到 [tmpfs](https://en.wikipedia.org/wiki/Tmpfs "wikipedia:Tmpfs") 文件系统如 `/tmp` 或 `/dev/shm` 可以提高程序的响应速度，因为全部内容都保存在内存。

为了简化使用，可以使用动态脚本进行管理，可以从 AUR 获得[profile-sync-daemon](https://www.archlinux.org/packages/?name=profile-sync-daemon),更多信息请参考 [Profile-sync-daemon](/index.php/Profile-sync-daemon "Profile-sync-daemon")。

## 安全

### 沙箱中运行

在沙箱中运行 chromium 可以提高安全性：

```
$ chromium --enable-seccomp-sandbox

```

### 用户终端信息

Chromium 默认会给出非常详细的用户终端信息，可以从 EFF 的 [Panopticlick](https://panopticlick.eff.org/) 测试看出。这会导致外界可以比较精确得辨别用户 — 而非稳定版本更是如此。

要提高安全性，可以通过下面选项修改为任意值：`--user-agent="[string]"`。

例如 Chrome Linux x64 版本可以使用：

```
--user-agent="Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/535.7 (KHTML, like Gecko) Chrome/16.0.912.75 Safari/535.7"

```