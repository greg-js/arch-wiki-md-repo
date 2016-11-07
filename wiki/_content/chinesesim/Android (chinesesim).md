**翻译状态：** 本文是英文页面 [Android](/index.php/Android "Android") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-09-26，点击[这里](https://wiki.archlinux.org/index.php?title=Android&diff=0&oldid=451481)可以查看翻译后英文页面的改动。

## Contents

*   [1 浏览安卓设备](#.E6.B5.8F.E8.A7.88.E5.AE.89.E5.8D.93.E8.AE.BE.E5.A4.87)
*   [2 安卓开发](#.E5.AE.89.E5.8D.93.E5.BC.80.E5.8F.91)
    *   [2.1 安卓 SDK 核心组件](#.E5.AE.89.E5.8D.93_SDK_.E6.A0.B8.E5.BF.83.E7.BB.84.E4.BB.B6)
    *   [2.2 获取 Android SDK 特定平台 API](#.E8.8E.B7.E5.8F.96_Android_SDK_.E7.89.B9.E5.AE.9A.E5.B9.B3.E5.8F.B0_API)
    *   [2.3 开发环境](#.E5.BC.80.E5.8F.91.E7.8E.AF.E5.A2.83)
        *   [2.3.1 Android Studio](#Android_Studio)
        *   [2.3.2 Eclipse](#Eclipse)
        *   [2.3.3 Netbeans](#Netbeans)
    *   [2.4 安卓调试桥 (ADB)](#.E5.AE.89.E5.8D.93.E8.B0.83.E8.AF.95.E6.A1.A5_.28ADB.29)
        *   [2.4.1 连接设备](#.E8.BF.9E.E6.8E.A5.E8.AE.BE.E5.A4.87)
        *   [2.4.2 手动查找设备 ID](#.E6.89.8B.E5.8A.A8.E6.9F.A5.E6.89.BE.E8.AE.BE.E5.A4.87_ID)
        *   [2.4.3 添加 udev 规则](#.E6.B7.BB.E5.8A.A0_udev_.E8.A7.84.E5.88.99)
        *   [2.4.4 配置 adb](#.E9.85.8D.E7.BD.AE_adb)
        *   [2.4.5 检测设备](#.E6.A3.80.E6.B5.8B.E8.AE.BE.E5.A4.87)
        *   [2.4.6 使用方法](#.E4.BD.BF.E7.94.A8.E6.96.B9.E6.B3.95)
        *   [2.4.7 注意事项和疑难杂症](#.E6.B3.A8.E6.84.8F.E4.BA.8B.E9.A1.B9.E5.92.8C.E7.96.91.E9.9A.BE.E6.9D.82.E7.97.87)
    *   [2.5 NVIDIA Tegra 平台专用工具](#NVIDIA_Tegra_.E5.B9.B3.E5.8F.B0.E4.B8.93.E7.94.A8.E5.B7.A5.E5.85.B7)
*   [3 构建 Android](#.E6.9E.84.E5.BB.BA_Android)
    *   [3.1 OS 位数](#OS_.E4.BD.8D.E6.95.B0)
    *   [3.2 需要的软件包](#.E9.9C.80.E8.A6.81.E7.9A.84.E8.BD.AF.E4.BB.B6.E5.8C.85)
    *   [3.3 Java Development Kit](#Java_Development_Kit)
    *   [3.4 配置构建环境](#.E9.85.8D.E7.BD.AE.E6.9E.84.E5.BB.BA.E7.8E.AF.E5.A2.83)
    *   [3.5 下载源代码](#.E4.B8.8B.E8.BD.BD.E6.BA.90.E4.BB.A3.E7.A0.81)
    *   [3.6 开始构建](#.E5.BC.80.E5.A7.8B.E6.9E.84.E5.BB.BA)
    *   [3.7 测试镜像](#.E6.B5.8B.E8.AF.95.E9.95.9C.E5.83.8F)
    *   [3.8 创建可烧录镜像](#.E5.88.9B.E5.BB.BA.E5.8F.AF.E7.83.A7.E5.BD.95.E9.95.9C.E5.83.8F)
*   [4 恢复 Android](#.E6.81.A2.E5.A4.8D_Android)
    *   [4.1 Fastboot](#Fastboot)
    *   [4.2 Samsung](#Samsung)
        *   [4.2.1 Heimdall](#Heimdall)
        *   [4.2.2 Odin (Virtualbox)](#Odin_.28Virtualbox.29)
*   [5 其它连接方法](#.E5.85.B6.E5.AE.83.E8.BF.9E.E6.8E.A5.E6.96.B9.E6.B3.95)
    *   [5.1 adb-sync](#adb-sync)
    *   [5.2 AirDroid](#AirDroid)
    *   [5.3 AndroidScreencast](#AndroidScreencast)
    *   [5.4 FTP](#FTP)
    *   [5.5 KDE Connect](#KDE_Connect)
    *   [5.6 SSH 服务器](#SSH_.E6.9C.8D.E5.8A.A1.E5.99.A8)
    *   [5.7 Samba](#Samba)
*   [6 技巧和提示](#.E6.8A.80.E5.B7.A7.E5.92.8C.E6.8F.90.E7.A4.BA)
    *   [6.1 调试时出现 "Source not found"](#.E8.B0.83.E8.AF.95.E6.97.B6.E5.87.BA.E7.8E.B0_.22Source_not_found.22)
    *   [6.2 在 sd 卡上安装 Linux 发行版](#.E5.9C.A8_sd_.E5.8D.A1.E4.B8.8A.E5.AE.89.E8.A3.85_Linux_.E5.8F.91.E8.A1.8C.E7.89.88)
*   [7 疑难杂症](#.E7.96.91.E9.9A.BE.E6.9D.82.E7.97.87)
    *   [7.1 Android Studio: Android Virtual Devices show 'failed to load'.](#Android_Studio:_Android_Virtual_Devices_show_.27failed_to_load.27.)
    *   [7.2 aapt: No such file or directory](#aapt:_No_such_file_or_directory)
    *   [7.3 ValueError: unsupported pickle protocol](#ValueError:_unsupported_pickle_protocol)

## 浏览安卓设备

有多种方法浏览安卓设备：

*   [MTP](/index.php/MTP "MTP") 协议可以用USB传输文件。
*   [其它连接方法](#.E5.85.B6.E5.AE.83.E8.BF.9E.E6.8E.A5.E6.96.B9.E6.B3.95) (比如 FTP, SSH)。

更高阶的用法，开发、刷机和恢复等：

*   [ADB 工具包](#.E5.AE.89.E5.8D.93.E8.B0.83.E8.AF.95.E6.A1.A5_.28ADB.29) 广泛用于开发。
*   [恢复 Android](#.E6.81.A2.E5.A4.8D_Android) 用于刷机和恢复安卓固件（包括 fastboot）。

## 安卓开发

在Archlinux中开发安卓程序，需如下三步：

1.  安装 Android SDK 核心组件，
2.  安装一个或数个 Android SDK 特定平台软件包，
3.  安装一个兼容 Android SDK 的 IDE

### 安卓 SDK 核心组件

**注意:** 如果运行 64 位操作系统，你需要启用[multilib](/index.php/Multilib "Multilib")软件源以避免安装时出现"error: target not found: lib32-zlib"报错信息。

**注意:** 如果你想要安装 [#Android Studio](#Android_Studio) 且使用其来管理你的SDK安装，你不需要安装以下软件包。

在开发安卓程序之前，需要安装安卓 SDK。它由下列三组软件包组成，均可从 [AUR](/index.php/Arch_User_Repository_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch User Repository (简体中文)") 安装：

1.  [android-sdk](https://aur.archlinux.org/packages/android-sdk/)
2.  [android-sdk-platform-tools](https://aur.archlinux.org/packages/android-sdk-platform-tools/)
3.  [android-sdk-build-tools](https://aur.archlinux.org/packages/android-sdk-build-tools/)

对于旧设备的支持， [android-support](https://aur.archlinux.org/packages/android-support/) 软件包是必需的。 软件包会安装到`/opt/android-sdk`。 这个目录需要 root 权限，所以你需要以 root 用户运行 sdk manager，否则你将无法修改这个目录中的内容。 如果打算以一般用户权限来访问，需要创建 android sdk 用户组（名称任意）：

```
# groupadd sdkusers

```

然后将用户添加到这个组中：

```
# gpasswd -a <user> sdkusers

```

修改目录所属的用户组：

```
# chown -R :sdkusers /opt/android-sdk/

```

修改目录的权限，使得刚加入组中的用户也能在目录中写入：

```
# chmod -R g+w /opt/android-sdk/

```

重新登录或者以 <user> 登录终端的用户组变为新建的组：

```
$ newgrp sdkusers

```

**注意:** 除了上述 [AUR](/index.php/AUR "AUR") 全局安装的方式，还可以参考[上游说明](https://developer.android.com/sdk/index.html)将 SDK 安装到用户 home 目录。你也可以使用[AUR](/index.php/AUR "AUR")中的 android-*-dummy 软件包来解决系统依赖。

### 获取 Android SDK 特定平台 API

从[AUR](/index.php/Arch_User_Repository_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch User Repository (简体中文)")安装所需的 Android SDK 特定平台软件包：

*   [android-platform-21](https://aur.archlinux.org/packages/android-platform-21/)
*   [android-platform-20](https://aur.archlinux.org/packages/android-platform-20/)
*   [android-platform-19](https://aur.archlinux.org/packages/android-platform-19/)
*   [android-platform-18](https://aur.archlinux.org/packages/android-platform-18/)
*   [android-platform-17](https://aur.archlinux.org/packages/android-platform-17/)
*   [android-platform-16](https://aur.archlinux.org/packages/android-platform-16/)
*   [android-platform-15](https://aur.archlinux.org/packages/android-platform-15/)
*   [android-platform-14](https://aur.archlinux.org/packages/android-platform-14/)

### 开发环境

如下所述，基于 IntelliJ IDEA 的 Android Studio 是新的官方开发环境，也可以使用 [Eclipse](/index.php/Eclipse "Eclipse") + 官方不再支持的 ADT 插件，或者结合 NBAndroid 插件使用 [Netbeans](/index.php/Netbeans "Netbeans") 进行开发。

#### Android Studio

[Android Studio](http://developer.android.com/sdk/installing/studio.html) 是基于 [IntelliJ Idea](https://www.jetbrains.com/idea/) 的 Android 开发环境。它替代了原来的 [Eclipse Android Developer Tools](https://developer.android.com/tools/help/adt.html) 插件，为开发和调试提供了集成环境。

你可以通过 [AUR](/index.php/AUR "AUR") 中的 [android-studio](https://aur.archlinux.org/packages/android-studio/) 软件包下载并安装。若提示缺少 SDK，参考上节获取 Android SDK 特定平台 API。

**注意:** 如果使用了除i3wm之外的平铺窗口管理器，可能需要按 [这里](https://code.google.com/p/android/issues/detail?id=57675) 描述的修复方法进行处理。

**注意:** 确保[配置了 Java 环境](/index.php/Java#Change_default_Java_environment "Java") 已正确配置，否则无法启动 android-studio。

**注意:** 如 [这个](https://youtrack.jetbrains.com/issue/IDEA-57233#comment=27-876236) 页面所述，安装 [infinality-bundle](/index.php/Infinality#Installation "Infinality") 并使用 AUR 中 infinality 打完补丁的 openJDK7 （[jdk7-openjdk-infinality](https://aur.archlinux.org/packages/jdk7-openjdk-infinality/)）或者 openJDK 8 （[jdk8-openjdk-infinality](https://aur.archlinux.org/packages/jdk8-openjdk-infinality/)）能修复 Android Studio 中糟糕的字体渲染问题，也可以使用 [Infinality 非官方软件库](/index.php/Unofficial_user_repositories#infinality-bundle "Unofficial user repositories") 中打完补丁的 OpenJDK8。

**注意:** 在 `~/.AndroidStudio1.2/studio64.vmoptions` 文件中添加 `-Dhidpi=true` 能修复 HiDPI 缩放情况下文本超出控件边界的问题。

一般会在 Android Studio 图形界面下编译应用，如果需要通过命令行编译应用 （使用诸如 `./gradlew assembleDebug`），需要在 `~/.bashrc` 中添加：

```
export ANDROID_HOME=/opt/android-sdk

```

#### Eclipse

**注意:** 自 2014-12-08 起，官方已经不再建议使用 ADT 插件，官方的开发环境是 Android Studio。

官方的但已经废弃的 [Eclipse ADT](http://developer.android.com/sdk/eclipse-adt.html) 插件可以通过 [eclipse-android](https://aur.archlinux.org/packages/eclipse-android/) 软件包安装。

**注意:**

*   如果你遇到了不可解析的依赖的错误信息，手动安装 [Java](/index.php/Java "Java") 并重试。
*   另外，你也可以通过 eclipse 内置的 "add new software" 方法来安装 ADT（详见 ADT 网站的帮助）。
*   如果实在不行，你可以下载 Android SDK 并使用捆绑的 Eclipse，通常不再会有问题。
*   如果你需要安装不在 AUR 中的额外 SDK 组件，你必须先改变 /opt/android-sdk 中文件的所有者和权限，运行 `# chgrp -R users /opt/android-sdk ; chmod -R 0775 /opt/android-sdk` （详细信息可参见 [文件权限](/index.php/File_Permissions "File Permissions")）。

在下面设置中设置 Android SDK 路径：

```
Windows -> Preferences -> Android

```

**注意:** 如果 AUR 软件包升级之后插件无法在 Eclipse 中显示出来，eclipse 可能使用了过期缓存。执行一次 `sudo eclipse -clean`。如果还是不行，就删除 Eclipse 及其所有插件，删除 `/usr/share/eclipse` 再重装。

#### Netbeans

如果想用 Netbeans 作为 Android 开发的 IDE，需要下载 [NBAndroid](http://www.nbandroid.org)：

```
Tools -> Plugins -> Settings

```

添加如下 URL：[http://nbandroid.org/updates/updates.xml](http://nbandroid.org/updates/updates.xml)

然后到 **Available Plugins** 安装 IDE 版本对应的 **Android** 和 **Junit** 插件，安装后到：

```
Tools -> Options -> Miscellaneous -> Android

```

设置 SDK 安装路径（默认是 /opt/android-sdk）。这样就行了，现在你可以在 Netbeans 里面创建和开发新的 Android 项目。

### 安卓调试桥 (ADB)

**提示：** 有些设备需要先启用 MTP 才能使用 ADB，而另一些设备需要启用 PTP。

**提示：** 许多设备的 udev 规则被包含在 [libmtp](https://www.archlinux.org/packages/?name=libmtp)，所以如果你已经安装此软件包，以下步骤是不必要的。

#### 连接设备

要使用 安卓调试桥(ADB) 在 Arch 下连接真实设备，必须：

1.  安装 [android-tools](https://www.archlinux.org/packages/?name=android-tools)。除此之外，如果希望为设备在 `/dev/` 中建立正确的节点,需安装 [android-udev](https://www.archlinux.org/packages/?name=android-udev) 软件包。
2.  在手机或设备上启用 USB 调试：
3.  Jelly Bean （4.2）或更新版本：访问 `Settings（设置） --> About Phone（关于手机）`，不停点击 “Build Number（版本号）” （7次），直到弹出消息提示开启了开发者选项。然后访问 `Settings（设置） --> Developer（开发者选项） --> USB debugging（USB 调式）` 并启用它。
4.  旧版本： 通常能通过 `Settings（设置） --> Applications （应用程序）--> Development（开发者选项） --> USB debugging（USB调试）`。勾选后重启手机，确保 USB 调试已启用。
5.  将用户加入组 *adbusers*。
6.  gpasswd -a *username* adbusers

如果 [ADB 能识别你的设备](#.E6.A3.80.E6.B5.8B.E8.AE.BE.E5.A4.87) (在IDE中可以看见和访问）就行了，否则见下面的内容。

#### 手动查找设备 ID

每一个手机供应商都提供了 usb 厂商ID和产品ID，比如 HTC Evo 为：

```
vendor id: 0bb4
product id: 0c8d

```

连接设备并执行：

```
$ lsusb

```

应该会出现类似的结果：

```
Bus 002 Device 006: ID 0bb4:0c8d High Tech Computer Corp.

```

#### 添加 udev 规则

使用 [Android developer](http://source.android.com/source/initializing.html#configuring-usb-access) 的规则，或者下面的模板，并用你的 [VENDOR ID] 和 [PRODUCT ID] 替换里面的值。 然后把这些规则复制到 `/etc/udev/rules.d/51-android.rules`：

 `/etc/udev/rules.d/51-android.rules` 
```
SUBSYSTEM=="usb", ATTR{idVendor}=="[VENDOR ID]", MODE="0666", GROUP="adbusers"
SUBSYSTEM=="usb",ATTR{idVendor}=="[VENDOR ID]",ATTR{idProduct}=="[PRODUCT ID]",SYMLINK+="android_adb"
SUBSYSTEM=="usb",ATTR{idVendor}=="[VENDOR ID]",ATTR{idProduct}=="[PRODUCT ID]",SYMLINK+="android_fastboot"
```

再加载刚定义的规则，运行：

```
# udevadm control --reload-rules

```

确保你是 `adbusers` [group](/index.php/Group "Group") 的成员，以访问 `adb` 设备。

#### 配置 adb

除了使用 udev 规则外，也可以创建/编辑 `~/.android/adb_usb.ini`，里面包含了一个 vendor ID 的列表。

```
$ cat ~/.android/adb_usb.ini 
0x27e8

```

#### 检测设备

配置了 udev 规则之后，拔掉设备然后重新连接，再运行：

```
$ adb devices

```

可以看到类似的结果：

```
List of devices attached 
HT07VHL00676    device

```

#### 使用方法

现在可以通过 adb 在设备和计算机间传输文件了。使用：

```
$ adb push *<what-to-copy>* *<where-to-place>*

```

向设备传送文件，使用：

```
$ adb pull *<what-to-pull>* *<where-to-place>*

```

从设备获取文件。

#### 注意事项和疑难杂症

*   **ADB** 也可以通过 [platform tools](#Android_SDK_platform_API)（通常位于 `/opt/android-sdk/platform-tools/`）， 所以可能没有必要安装 [android-tools](https://www.archlinux.org/packages/?name=android-tools)（位于 `/usr/bin/`）

如果列表为空（设备没有找到），可能是因为设备上没有启用 USB 调试。可以到 设置 => 应用程序 => 开发 (Settings => Applications => Development) 来启用 USB 调试。Android 4.2 (Jelly Bean) 隐藏了开发者选项菜单，到 设置 => 关于手机 (Settings => About phone)，然后点击 Build number （版本号） 7 次来启用它。

若仍有问题，比如 *adb* 显示 `???????? no permissions`，尝试以 root 权限重启 adb 服务。

```
# adb kill-server
# adb start-server

```

### NVIDIA Tegra 平台专用工具

如果应用程序的目标平台是 NVIDIA Tegra 平台，可以安装 NVIDIA 提供的工具、文档和示例。[NVIDIA 移动开发者](http://developer.nvidia.com/category/zone/mobile-development) 提供了两个工具：

1.  [Tegra 安卓开发包](http://developer.nvidia.com/tegra-resources) 提供了与[Eclipse ADT](http://developer.android.com/sdk/eclipse-adt.html)相关的工具（NVIDIA 调试管理器）及文档。
2.  [Tegra Toolkit](http://developer.nvidia.com/tegra-resources) 提供了工具(大部分是 CPU 和 GPU 优化相关)，示例和文档。

因为 NVIDIA 现在需要先注册登录才能下载，所以两者均无法再从 [AUR](/index.php/AUR "AUR") 获取。

## 构建 Android

请注意如下说明文档是基于[官方 AOSP 构建说明](http://source.android.com/source/building.html)的。其他基于 Android 的系统，如 CyanogenMod，通常需要额外的步骤。

### OS 位数

只有安卓 2.2.x (Froyo) 和更早的版本需要在 32 位系统中构建。而2.3.x (Gingerbread) 之后，则需要 64 位系统。

### 需要的软件包

编译任意版本的安卓系统，都需要安装下列软件包：

*   32位和64位系统：[gcc](https://www.archlinux.org/packages/?name=gcc) [git](https://www.archlinux.org/packages/?name=git) [gnupg](https://www.archlinux.org/packages/?name=gnupg) [flex](https://www.archlinux.org/packages/?name=flex) [bison](https://www.archlinux.org/packages/?name=bison) [gperf](https://www.archlinux.org/packages/?name=gperf) [sdl](https://www.archlinux.org/packages/?name=sdl) [wxgtk](https://www.archlinux.org/packages/?name=wxgtk) [squashfs-tools](https://www.archlinux.org/packages/?name=squashfs-tools) [curl](https://www.archlinux.org/packages/?name=curl) [ncurses](https://www.archlinux.org/packages/?name=ncurses) [zlib](https://www.archlinux.org/packages/?name=zlib) [schedtool](https://www.archlinux.org/packages/?name=schedtool) [perl-switch](https://www.archlinux.org/packages/?name=perl-switch) [zip](https://www.archlinux.org/packages/?name=zip) [unzip](https://www.archlinux.org/packages/?name=unzip) [libxslt](https://www.archlinux.org/packages/?name=libxslt) [python2-virtualenv](https://www.archlinux.org/packages/?name=python2-virtualenv) [bc](https://www.archlinux.org/packages/?name=bc)

*   仅64位系统：[gcc-multilib](https://www.archlinux.org/packages/?name=gcc-multilib) [lib32-zlib](https://www.archlinux.org/packages/?name=lib32-zlib) [lib32-ncurses](https://www.archlinux.org/packages/?name=lib32-ncurses) [lib32-readline](https://www.archlinux.org/packages/?name=lib32-readline)

*   AUR 软件包 32位和64位系统： [ncurses5-compat-libs](https://aur.archlinux.org/packages/ncurses5-compat-libs/)

*   AUR 软件包 仅64位系统： [lib32-ncurses5-compat-libs](https://aur.archlinux.org/packages/lib32-ncurses5-compat-libs/)

**注意:** [ncurses5-compat-libs](https://aur.archlinux.org/packages/ncurses5-compat-libs/) 和 [lib32-ncurses5-compat-libs](https://aur.archlinux.org/packages/lib32-ncurses5-compat-libs/) 的 PGP 签名可能会引起错误，可以通过手动导入以下签名解决：

$ gpg --recv-keys 702353E0F7E48EDB

要编译 Android 6+，你需要安装以下额外的软件包：

*   32位和64位系统： [rsync](https://www.archlinux.org/packages/?name=rsync)

**Note:** CyanogenMod 从13.0版本起使用了Maven构建工具，要编译 CyanogenMod，需要安装 [maven](https://www.archlinux.org/packages/?name=maven)软件包

### Java Development Kit

Android 7 (Nougat) 可以使用 [jdk8-openjdk](https://www.archlinux.org/packages/?name=jdk8-openjdk) 编译。[[1]](https://source.android.com/source/requirements.html)

*   Android 5 和 6 （Lollipop 和 Marshmallow）需要OpenJDK 7，可以通过 [jdk7-openjdk](https://www.archlinux.org/packages/?name=jdk7-openjdk) 软件包安装。

旧版本 [需要](http://source.android.com/source/initializing.html) **Oracle JDK** 才能编译，**不支持** OpenJDK。

*   Gingerbread 到 KitKat (2.3 - 4.4) 需要 Java 6，可以通过 [AUR](/index.php/AUR "AUR") 软件包 [jdk6](https://aur.archlinux.org/packages/jdk6/) 安装，详情参阅 [Java](/index.php/Java "Java")。
*   Cupcake 到 Froyo (1.5 - 2.2) 需要 Java 5，可以通过 [jdk7-openjdk](https://www.archlinux.org/packages/?name=jdk7-openjdk) 软件包安装。。

。

### 配置构建环境

安装 [repo](https://www.archlinux.org/packages/?name=repo) 软件包，然后：

```
$ mkdir ~/bin
$ export PATH=~/bin:$PATH
$ curl [https://storage.googleapis.com/git-repo-downloads/repo](https://storage.googleapis.com/git-repo-downloads/repo) > ~/bin/repo
$ chmod a+x ~/bin/repo

```

创建一个用于构建的目录：

```
$ mkdir ~/android
$ cd ~/android

```

需要把默认的 python 从 3.X 版切换到 2.X 版：

```
$ virtualenv2 venv # 创建一个包含 Virtualenv 的目录 venv

```

{{注意|编译时可能报缺少 python 模块，可以通过链接 /usr/lib/python2.7/* 到 ~/android/venv/python2.7/ 来解决，实际路径按照虚拟环境的路径确定。

激活 Virtualenv，使得 $PATH 指向 Python 2。

**Note:** 虚拟环境仅在当前终端有效。

```
$ source venv/bin/activate

```

### 下载源代码

克隆整个代码库。你 **仅** 需在初次构建安卓或者切换分支时执行这一步。

*   `repo` 有一个 `-j` 选项，用法与 `make` 的相似。它决定了下载的线程数，你可以根据下载带宽进行调整。

*   你需要通过 `-b` 选项指定要检出的**分支**（安卓版本）。若不指定，会检出所谓的**master 分支**。

```
$ repo init -u [https://android.googlesource.com/platform/manifest](https://android.googlesource.com/platform/manifest) -b master
$ repo sync -j4

```

**注意:** 为尽一步减少下载时间，可以像下面使用repo 命令的 -c 开关：
```
$ repo sync -j8 -c

```
`-c` 开关仅同步在 manifest 中指定的分支，它的内容由 `-b` 开关中指定的分支或者使用版本库维护者设置的默认分支来决定，。

静候多时。未编译的源代码加上这些代码的 `.repo`、`.git` 目录，大小会超过 10 GB。

**注意:** 若之后要更新本地的安卓代码，只要进入编译目录，载入 Virtualenv，然后重新同步：
```
$ repo sync

```

### 开始构建

AOSP 中需执行下列命令：

```
$ source build/envsetup.sh
$ lunch full-eng
$ make -j4

```

如果不添加任何参数运行 **lunch**，则会被询问想要创建什么样的 build。使用 -j 参e数加一个数字进行并行构建，数值介于CPU核数或线程数的 1 至 2 倍。

编译很耗时。

**注意:** 确保你有足够的内存，推荐 4GB 以上的内存。Android 会大量使用 /tmp 目录。默认情况下，/tmp 目录所挂载的分区大小是内存的一半，分区满时编译会失败。

*   另外，你也可以不使用 [fstab](/index.php/Fstab "Fstab") 里的 tmpfs 。

**注意:** 根据 [Android Building and Running guide](https://source.android.com/source/building-running.html#build-the-code)：

"GNU make 使用 -jN 参数处理并行任务，编译时通常会使用界于 1 到 2 倍计算机硬件的线程数。例如，在 dual-E5520 机器上 （2 个 CPU, 每个 CPU 4核，每个核双线程），使用界于 make -j16 到 make -j32 的命令进行编译会最快。"

### 测试镜像

完成之后，运行并测试最终的映像。

```
$ emulator

```

### 创建可烧录镜像

通过下列命令创建可烧录的镜像：

```
make -j8 updatepackage

```

它会在 **out/target/product/hammerhead** （其中的 hammerhead 是设备名）生成一个可烧录的文件.

## 恢复 Android

某些情况下，Android 设备刷了某些定制 ROM 后想刷回官方的 Android 固件，可以访问 [XDA 论坛](http://forum.xda-developers.com/) 获取刷机的帮助。

### Fastboot

[official repositories](/index.php/Official_repositories "Official repositories") 中的 [android-tools](https://www.archlinux.org/packages/?name=android-tools) 软件包提供了 Fastboot（以及[ADB](#Connecting_to_a_real_device_-_Android_Debug_Bridge_.28ADB.29)）。

**注意:** 通过 `fastboot` 重置固件是十分需要技巧的。你可以浏览 [XDA developers forums](http://www.xda-developers.com/) 以获取官方固件,通常是一个 `*.zip` 文件，但其中包含着固件文件和 `flash-all.sh` 脚本。例如，[Google Nexus](https://developers.google.com/android/nexus/images) 附件包括 `flash-all.sh` 脚本.另一个例子， OnePlus One - [XDA thread](http://forum.xda-developers.com/oneplus-one/general/guide-return-opo-to-100-stock-t2826541)，其中你可以找到包含着 `flash-all.sh` 脚本的固件。

### Samsung

Samsung 设备不支持通过 **Fastboot' *工具烧录。可选择的工具只有* Heimdall** 和 **Odin** （通过使用 Windows 和 VirtualBox）。

#### Heimdall

[Heimdall](http://glassechidna.com.au/heimdall/) 是一个跨平台用于在三星移动设备上烧录固件（也称作ROMS）的开源工具，它也是以[Odina](http://odindownload.com/) 的备选方案为人而知。 它可以通过 [heimdall](https://www.archlinux.org/packages/?name=heimdall) 或 [heimdall-git](https://aur.archlinux.org/packages/heimdall-git/) 软件包被安装。

烧路说明位于 Heimdall 的 [GitHub page](https://github.com/Benjamin-Dobell/Heimdall/tree/master/Linux) 或 [XDA forums](http://forum.xda-developers.com/showthread.php?t=1922461)。

#### Odin (Virtualbox)

[Heimdall](http://glassechidna.com.au/heimdall/) 是一个跨平台用于在三星移动设备上烧录固件（也称作ROMS）的开源工具，它也是以[Odina](http://odindownload.com/) 的备选方案为人而知。 它可以通过 [heimdall](https://www.archlinux.org/packages/?name=heimdall) 或 [heimdall-git](https://aur.archlinux.org/packages/heimdall-git/) 软件包被安装。

烧路说明位于 Heimdall 的 [GitHub page](https://github.com/Benjamin-Dobell/Heimdall/tree/master/Linux) 或 [XDA forums](http://forum.xda-developers.com/showthread.php?t=1922461)。

Arch Linux 相关步骤：

1.  一同安装 [VirtualBox](/index.php/VirtualBox "VirtualBox") 和它的 [extension pack](/index.php/VirtualBox#Extension_pack "VirtualBox") 和 [guest additions](/index.php/VirtualBox#Guest_additions_disc "VirtualBox").
2.  使用 VirtualBox 在虚拟硬盘中安装你偏好的且与 Odin 适配的 Windows 操作系统（安装了 VirtualBox guest additions的）。
3.  打开 VirtualBox 中 Windows 操作系统的设置，跳转至**USB**，然后勾选（或者确保它是被勾选的）**Enable USB 2.0 (EHCI) Controller**。
4.  在 VirtualBox 中运行 Windows 操作系统，点击菜单栏中的**Device** ---> **USB Devices**，然后点击你已通过USB连接到电脑的 Samsung 移动设备。

Windows 相关链接：

*   Samsung 驱动可以从 [here](http://androidxda.com/download-samsung-usb-drivers) 下载。
*   Odin can 可以从 [here](https://www.androidfilehost.com/?fid=23501681358557126) 下载。
*   Samsung 安卓固件可以从 [here](http://www.sammobile.com/firmwares/) 下载。

如果你想确保一切都正常工作且准备就绪：

1.  切换你的设备至下载模式,连接到你的 Linux 机器。
2.  在虚拟机工具栏中， 选择 `devices` --> `USB` --> `...Samsung...` 设备。
3.  打开 Odin.名为**Message**的对话框，将打印类似于。

```
<ID:0/003> Added!!

```

的信息 这意味着你的设备对于 Odin 是可见的，且是准备就绪烧录的。

{{注意|不存在关于重置 Samsung 移动设备固件的通用说明。你必须通过 [Google](https://www.google.com) 和 [XDA developers forums](http://www.xda-developers.com) 来找到特定设备的烧录说明。例如， 这个[帖子](http://goo.gl/cZLyF8) 是关于Samsung Galaxy S4 设备的。

## 其它连接方法

### adb-sync

[adb-sync](https://github.com/google/adb-sync) （可通过 [adb-sync-git](https://aur.archlinux.org/packages/adb-sync-git/) 安装）是一个使用 ADB 协议，用于在 PC 和安卓设备间同步文件的工具。

### AirDroid

[AirDroid](http://goo.gl/EZQ9GQ) 可以通过网页浏览器访问设备。

### AndroidScreencast

[AndroidScreencast](http://xsavikx.github.io/AndroidScreencast) 是被开发用于从 PC 显示和控制你的安卓设备（使用ADB）。

### FTP

在 Arch 上建立 FTP 服务器并通过手机访问，或者在手机上运行 FTP 服务并在 Arch 上连接。 参阅 [List of applications/Internet#FTP](/index.php/List_of_applications/Internet#FTP "List of applications/Internet")。Android 上有许多 FTP 客户端/服务端应用。

### KDE Connect

[kdeconnect](https://www.archlinux.org/packages/?name=kdeconnect) 集成了你的安卓设备和 KDE 桌面，它的功能包括同步通知，同步剪贴板，多媒体控制，和文件/URL共享。

### SSH 服务器

Android 上有很多 SSH 服务器（应用），可以通过 `scp` 命令传输文件，参见 [SSH](/index.php/SSH "SSH").

### Samba

See [Samba](/index.php/Samba "Samba").

## 技巧和提示

### 调试时出现 "Source not found"

一般这时调试器正在单步进入（Step into） Java 代码。而 Android SDK 并不提供 Java 源代码，所以导致了错误。最好的解决方法是设置单步过滤器，不要跳转到（jump into） Java 源代码。单步过滤器默认没有启动，通过如下方式设置：

```
Window -> Preferences -> Java -> Debug -> Step Filtering

```

可以全选，此外还可以酌情添加 android.* 软件包。以下的论坛贴有更详细信息：

[http://www.eclipsezone.com/eclipse/forums/t83338.rhtml](http://www.eclipsezone.com/eclipse/forums/t83338.rhtml)

### 在 sd 卡上安装 Linux 发行版

可以参照这篇 [贴子](http://forum.xda-developers.com/showthread.php?t=631389) 安装 Debian，[archlinuxarm.org上](http://archlinuxarm.org/forum/viewtopic.php?f=27&t=1361&start=40)有在 chroot 环境下安装（与 Android 并存）的详细介绍。

## 疑难杂症

### Android Studio: Android Virtual Devices show 'failed to load'.

确保你已经设置了 [#Android Studio](#Android_Studio) 中说明的 `ANDROID_HOME` 环境变量。

### aapt: No such file or directory

安装工具包含 32 位程序，需要 32 位的库。如果是手动安装 SDK，还需要安装 multilib/[lib32-libstdc++5](https://www.archlinux.org/packages/?name=lib32-libstdc%2B%2B5) 和 multilib/[lib32-zlib](https://www.archlinux.org/packages/?name=lib32-zlib)。

### ValueError: unsupported pickle protocol

一种修复方法：

```
rm ~/.repopickle_.gitconfig

```

如果不起效，试试这样：

```
rm `find /path/to/android-root -name .repopickle_config`

```