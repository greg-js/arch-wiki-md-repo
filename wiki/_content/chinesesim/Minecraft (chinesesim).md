Minecraft 是一个关于击毁和放置方块的游戏。游戏一开始玩家的主要目的是搭建各种结构使自己免遭夜晚出没的怪物的攻击并生存下来，但随着游戏的进行，玩家们可以合作创造出一些不可思议的、富有想象力的东西。

## Contents

*   [1 客户端](#.E5.AE.A2.E6.88.B7.E7.AB.AF)
    *   [1.1 安装](#.E5.AE.89.E8.A3.85)
    *   [1.2 局域网防火墙配置](#.E5.B1.80.E5.9F.9F.E7.BD.91.E9.98.B2.E7.81.AB.E5.A2.99.E9.85.8D.E7.BD.AE)
*   [2 服务器](#.E6.9C.8D.E5.8A.A1.E5.99.A8)
    *   [2.1 安装](#.E5.AE.89.E8.A3.85_2)
    *   [2.2 设置](#.E8.AE.BE.E7.BD.AE)
        *   [2.2.1 介绍](#.E4.BB.8B.E7.BB.8D)
        *   [2.2.2 启动服务器](#.E5.90.AF.E5.8A.A8.E6.9C.8D.E5.8A.A1.E5.99.A8)
        *   [2.2.3 服务器管理脚本](#.E6.9C.8D.E5.8A.A1.E5.99.A8.E7.AE.A1.E7.90.86.E8.84.9A.E6.9C.AC)
        *   [2.2.4 调整](#.E8.B0.83.E6.95.B4)
    *   [2.3 可替代服务器](#.E5.8F.AF.E6.9B.BF.E4.BB.A3.E6.9C.8D.E5.8A.A1.E5.99.A8)
        *   [2.3.1 Spigot ( 区别于 Craftbukkit)](#Spigot_.28_.E5.8C.BA.E5.88.AB.E4.BA.8E_Craftbukkit.29)
        *   [2.3.2 Cuberite](#Cuberite)
    *   [2.4 额外说明](#.E9.A2.9D.E5.A4.96.E8.AF.B4.E6.98.8E)
*   [3 Minecraft mod 启动器](#Minecraft_mod_.E5.90.AF.E5.8A.A8.E5.99.A8)
*   [4 其它程序和编辑器](#.E5.85.B6.E5.AE.83.E7.A8.8B.E5.BA.8F.E5.92.8C.E7.BC.96.E8.BE.91.E5.99.A8)
*   [5 故障排除](#.E6.95.85.E9.9A.9C.E6.8E.92.E9.99.A4)
    *   [5.1 Minecraft 服务器运行在 ARM 设备](#Minecraft_.E6.9C.8D.E5.8A.A1.E5.99.A8.E8.BF.90.E8.A1.8C.E5.9C.A8_ARM_.E8.AE.BE.E5.A4.87)
    *   [5.2 Minecraft 客户端和 Wayland 支持](#Minecraft_.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.92.8C_Wayland_.E6.94.AF.E6.8C.81)
    *   [5.3 Minecraft 客户端或服务器无法启动](#Minecraft_.E5.AE.A2.E6.88.B7.E7.AB.AF.E6.88.96.E6.9C.8D.E5.8A.A1.E5.99.A8.E6.97.A0.E6.B3.95.E5.90.AF.E5.8A.A8)
*   [6 参见](#.E5.8F.82.E8.A7.81)

## 客户端

### 安装

Minecraft 客户端可以通过 [minecraft-launcher](https://aur.archlinux.org/packages/minecraft-launcher/) 包来安装。它提供了官方游戏启动器，一个用于启动它的脚本和一个特定的 `.desktop` 文件。

或者，它也可以通过 [minecraft](https://aur.archlinux.org/packages/minecraft/) 包来安装.

### 局域网防火墙配置

在局域网内开放一个 Minecraft 世界你需要在 [firewall](/index.php/Firewall "Firewall") 中放行两个端口：

*   UDP 端口 `4445`。如果这个端口是关闭状态，当你保存退出世界时游戏会宕机；
*   当你将 Minecraft 开放到局域网后，它会自己随机选择一个 TCP 端口来开放。如果此端口被关闭，其他玩家将不能加入你的世界。

## 服务器

### 安装

Minecraft 服务器可以通过 [minecraft-server](https://aur.archlinux.org/packages/minecraft-server/) 包来安装。它附带一个 [systemd](/index.php/Systemd "Systemd") unit 文件，并包含一个小巧的控制脚本。

另请参阅 [#可替代服务器](#.E5.8F.AF.E6.9B.BF.E4.BB.A3.E6.9C.8D.E5.8A.A1.E5.99.A8) 以了解其他可替代服务器。

### 设置

#### 介绍

在安装过程中，`minecraft` 用户及组被引入。出于安全考虑，我们推荐并创建一个 Minecraft 特殊用户，通过在一个无特殊权限的用户下运行 Minecraft，当其他人攻破你的 Minecraft 服务器时，他们最多只能取得该用户的权限，从而保证了其他用户以及服务器的安全。 不过你需要安全地将你的用户添加到 `minecraft` 组，并给予该组 `/srv/minecraft` (默认) 目录的写入权限以允许其修改 Minecraft 服务器的设置。同时确保所有在 `/srv/minecraft` 目录下的文件的所有者为 `minecraft` 用户，或者通过其他手段让该用户拥有前面所提的目录下所有文件的读写权限。如果服务器无法访问某些文件同时没有足够的权限将该错误消息写入日志，服务器将会出错。

该软件包提供了一个 systemd 服务和一个计时器用于自动备份。默认情况下，备份位于服务器根目录下的 `backup` 文件夹。尽管为了保持硬盘空间不被占用过多，保险起见 10 个最近的备份是必要的 (可以通过修改 `KEEP_BACKUPS` 来控制备份数量)。相关的 systemd 文件分别为 `minecraftd-backup.timer` 和 `minecraftd-backup.service`。我们可以根据自己喜好非常愉快地来 [调整](/index.php/Edit "Edit")，例如：自定义备份时间间隔。

#### 启动服务器

你可以通过 systemd 来启动服务器，或者直接从命令行。无论哪种方式，服务器都是通过一个封装在 `minecraft` 用户下发起的 [GNU Screen](/index.php/GNU_Screen "GNU Screen") 会话的形式来运行的。通过 systemd 你可以 [start](/index.php/Start "Start") 和 enable 其包含的 `minecraftd.service` 服务。或者，从命令行启动：

```
# minecraftd start

```

**注意:** 如果你是第一次启动服务器，`/srv/minecraft/eula.txt` 目录下会生成一个 [EULA](https://en.wikipedia.org/wiki/EULA "wikipedia:EULA") 文件。你需要去编辑这个文件，来表明你同意合同中的条款以运行服务器。

#### 服务器管理脚本

为了方便的控制服务器，你或许会用到 `minecraftd` 提供的一些脚本。它可以执行一些基本的命令，比如 `start`，`stop`，`restart` 还可以将会话附加到 `console` 上。此外，它也可以通过 `status` 显示状态信息，使用 `backup` 来备份服务器世界的目录，通过 `restore` 来从备份中恢复世界的数据或者在服务器控制台中运行 `command *do-something*` 这条命令。

**注意:** 关于服务器看着他 (可以通过 `minecraftd console` 来访问)，请记住你可以通过 `ctrl+a` `d` 来退出任何 GNU Screen 会话。

#### 调整

通过编辑 `/etc/conf.d/minecraft` 来做一些小的调整 (比如：最大内存，线程数之类的)。

举个例子，许多高级用户倾向于启用 `IDLE_SERVER` 通过设置其为 `true`。这会启用管理脚本，当没有玩家在线超过 `IDLE_IF_TIME` (默认 20 分钟) 后挂起服务器。当服务器挂起时 `idle_server` 会通过 [ncat(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ncat.1) (也称之为 netcat 或者 simply nc for short) 监听 Minecraft 的端口，同时当监测到一个接入的连接时立刻启动服务器。虽然在挂起后一次加入会有明显的延迟，但它显著地降低了 CPU 和内存的使用量，从而使得资源分配更加合理减少系统功耗。

### 可替代服务器

#### Spigot ( 区别于 Craftbukkit)

[Spigot](https://www.spigotmc.org/) (也就是我们国内玩家常说的水龙头服) 是在世界上使用最广泛的 **改装版** Minecraft 服务器，因此 [AUR](/index.php/AUR "AUR") 中有一个 [spigot](https://aur.archlinux.org/packages/spigot/) 包。这个 spigot 的 PKGBUILD 建立在 [minecraft-server](https://aur.archlinux.org/packages/minecraft-server/) 包之上。这意味着，spigot 服务器也提供自己的 systemd unit 文件，spigot 脚本和相应的脚本配置文件。二进制文件叫做 `spigot`，有着与 `minecraftd` 相同的命令，其配置文件位于 `/etc/conf.d/spigot` 下。

确保你阅读了 [#设置](#.E8.AE.BE.E7.BD.AE) 部分，并且将 `minecraftd` 替换为 `spigot` 无论你在哪使用时。

它和 [Bukkit](http://bukkit.org/) (也就是我们国内玩家常说的水桶服) 有些故事，而且自 Bukkit 陨落以来越来越受欢迎。

#### Cuberite

[Cuberite](https://cuberite.org/) 是一个高性能且定制度极高的 Minecraft 服务器，由 C++ 和 Lua 编写而成。它有着比 vanilla Minecraft 服务器更好的性能，不过令人遗憾的是它与最新的 Minecraft 客户端不完全兼容 (某些功能缺失或无法正常工作)。

Cuberite minecraft 服务器可以通过 [cuberite](https://aur.archlinux.org/packages/cuberite/) 包来安装，默认情况下还提供了一个在 `8080` 端口的简易 web 界面，大多数服务器操作都可以在其中轻松完成。cuberite 的 PKGBUILD 同样建立在 [minecraft-server](https://aur.archlinux.org/packages/minecraft-server/) 包之上。这意味着 cuberite 服务器也提供自己的 systemd unit 文件，cuberite 脚本和相应的脚本配置文件。二进制文件叫做 `cuberite`，有着与 `minecraftd` 相同的命令，其配置文件位于 `/etc/conf.d/cuberite` 下。

确保你阅读了 [#设置](#.E8.AE.BE.E7.BD.AE) 部分，并且将 `minecraftd` 替换为 `cuberite` 无论你在哪使用时。

### 额外说明

*   有几个 server wrapper 可用，它们提供从自动备份到并行管理数十个服务器的一切东西，阅读 [Server Wrappers](http://www.minecraftwiki.net/wiki/Programs_and_editors#Server_Wrappers) 以获得更多信息。然而 AUR 所提供的管理脚本应该能够满足你的绝大多数需求。
*   你也许想要一个 [systemd timer](/index.php/Systemd/Timers "Systemd/Timers")，比如 [mapper](http://www.minecraftwiki.net/wiki/Programs_and_editors#Mappers) 可以在你的世界周期性地生成地图。
*   务必定期备份，比如，使用提供地管理脚本 (参见 [#介绍](#.E4.BB.8B.E7.BB.8D)) 或者 [rsync](/index.php/Rsync "Rsync")。

## Minecraft mod 启动器

你可以从许多不同的启动器启动 Minecraft，这些启动器通常包含一系列的 mod 包以提高游戏的可玩性并添加 [mods](http://minecraft.gamepedia.com/Mods)。

*   **Feed The Beast** — 起源于 Minecraft 中的挑战地图，由大量科技 mod 组成并逐渐演变为一个 mod 启动器。

	[https://www.feed-the-beast.com/](https://www.feed-the-beast.com/) || [feedthebeast](https://aur.archlinux.org/packages/feedthebeast/)

*   **MultiMC** — 用于管理可分离包关联的沙盒环境。

	[https://multimc.org/](https://multimc.org/) || [multimc5](https://aur.archlinux.org/packages/multimc5/) and [multimc-git](https://aur.archlinux.org/packages/multimc-git/)

*   **Technic Launcher** — 从流行程度排名发掘 mod 的 Modpack 安装程序。

	[http://www.technicpack.net/](http://www.technicpack.net/) || [minecraft-technic-launcher](https://aur.archlinux.org/packages/minecraft-technic-launcher/)

## 其它程序和编辑器

有几个 [程序和编辑器](http://www.minecraftwiki.net/wiki/Programs_and_editors) 可以让你的 Minecraft 之旅更加轻松。其中最常见的是地图生成器。使用其中之一可以加载的 Minecraft 文件并渲染其位 2D 图像，展现给你一个自上而下的世界地图。

*   AMIDST (出色的 Minecraft 接口和数据/结构追踪) ([amidst](https://aur.archlinux.org/packages/amidst/)) 是一个有助于在 Minecraft 世界中寻找建筑，生物群系和玩家的程序。它可以绘制世界的生物群落并通过给出一个随机种子标注哪里可能是个有意思的地方，或者从现有世界读取随机种子 (这种情况下，它可以显示这个世界的玩家)。该项目有很多分支，其中最引人注目的是 “Amidst Exporter” ([amidstexporter](https://aur.archlinux.org/packages/amidstexporter/)) 它包含一个用于计算 1.8+ 世界海洋纪念碑位置的补丁。

*   Mapcrafter ([mapcrafter-git](https://aur.archlinux.org/packages/mapcrafter-git/)) 是一个用 C++ 编写的高性能 Minecraft 地图渲染器，它将世界渲染为具有 3D 等距透视的地图。你可以在任何浏览器中查看这些地图，因此可以轻松地在一台服务器上部署它们。Mapcrafter 有一个简单的配置文件格式来指定要渲染的世界，不同的渲染模式，如白天/黑夜/洞穴，也可以从不同角度渲染世界。

*   Minutor ([minutor-git](https://aur.archlinux.org/packages/minutor-git/)) 是一个轻量级的 Minecraft 地图生成器。有一个简单的基于 GTK+ 的界面，用于查看你的世界。可以使用多种渲染模式，以及自定义着色模式和切割 z-levels 的功能。

## 故障排除

### Minecraft 服务器运行在 ARM 设备

Minecraft 服务器应该在具有最新 [Java](/index.php/Java "Java") 的 [ARM](https://archlinuxarm.org/) 设备上运行时没有任何问题，比如 [jre10-openjdk-headless](https://www.archlinux.org/packages/?name=jre10-openjdk-headless)。但是，如果遇到任何问题，尝试切换为 [jdk-arm](https://aur.archlinux.org/packages/jdk-arm/)。还可以考虑使用 [#Cuberite](#Cuberite) 服务器作为替代方案。

### Minecraft 客户端和 Wayland 支持

Waycraft 和其他窗口管理器目前不支持 Minecraft，因为 Minecraft 具有 [xorg-xrandr](https://www.archlinux.org/packages/?name=xorg-xrandr) 的先决条件，应该使用xorg打开。

### Minecraft 客户端或服务器无法启动

这可能是 [Java](/index.php/Java "Java") 版本的问题。Java 8 保证在所有情况下都能正常运行。

Minecraft 服务器和实际游戏都可以与最新版本的 [Java](/index.php/Java "Java") 完美搭配，比如 [jre10-openjdk](https://www.archlinux.org/packages/?name=jre10-openjdk)，但是 Minecraft 游戏启动器 (以及所有其它的 mod) 可能只适用于 [Java](/index.php/Java "Java") 8。

## 参见

*   [Minecraft 官方网站](https://www.minecraft.net/)
*   [Minecraft 社区链接](https://www.minecraft.net/community)
*   [Minecraft 客户端与服务器下载链接](https://minecraft.net/download)
*   [Crafting Recipes](http://www.minecraftwiki.net/wiki/Crafting)
*   [方块与物品数据](http://www.minecraftwiki.net/wiki/Data_values)
*   [Reddit Minecraft 社区](http://www.reddit.com/r/minecraft)
*   [Minecraft Skins](http://www.minecraftskins.net)