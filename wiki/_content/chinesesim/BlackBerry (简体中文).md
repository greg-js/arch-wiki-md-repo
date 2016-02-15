## Contents

*   [1 黑莓](#.E9.BB.91.E8.8E.93)
*   [2 通过barry同步手机](#.E9.80.9A.E8.BF.87barry.E5.90.8C.E6.AD.A5.E6.89.8B.E6.9C.BA)
    *   [2.1 安装如下包](#.E5.AE.89.E8.A3.85.E5.A6.82.E4.B8.8B.E5.8C.85)
    *   [2.2 创建同步配对](#.E5.88.9B.E5.BB.BA.E5.90.8C.E6.AD.A5.E9.85.8D.E5.AF.B9)

## 黑莓

黑莓是由加拿大RIM公开发的移动电子邮件和智能手机终端. 除提供典型的智能手机应用(地址簿, 日历, 待办事项等等, 当然还有必不可少的通话功能), 黑莓更为人称道的是其对电子邮件的完美支持. 它占据智能手机市场20.8%的份额, 仅次于诺基亚的塞班系统.

注1 诺基亚已与微软合作, 以Windows Phone 7为下一代手机系统. 虽然诺基亚仍在出产塞班手机, 但毫无疑问,塞班系统的时代已经结束了.

注2 黑莓的最大特色, Pushmail服务目前只在北美和欧洲地区支持. 中国移动正与黑莓合作, 试图在国内推行Pushmail服务. 但费用极为昂贵, 并不适合个人用户. 有兴趣的莓友可以尝试一些第三方软件, 如Berrymail和尚邮Shangmail.

## 通过barry同步手机

下面以Evolution与手机同步联系人和日历为例说明.理论上, 同样的步聚可适用其它的邮件和日历客户端, 包括kmail和Google日历.

### 安装如下包

`evolution` 可从extra仓库获得
`msynctool-stable` - 可从aur仓库获得 - [https://aur.archlinux.org/packages.php?ID=32917](https://aur.archlinux.org/packages.php?ID=32917)
`libopensync-plugin-evolution2-stable` -可从aur仓库获得 - [https://aur.archlinux.org/packages.php?ID=39025](https://aur.archlinux.org/packages.php?ID=39025)
`barry` - 可从aur仓库获得 - [https://aur.archlinux.org/packages.php?ID=20874](https://aur.archlinux.org/packages.php?ID=20874)

在编译barry时, PKGBUILD文件中必须加上对opensync插件的支持. 可按照如下方式修改PKGBUILD文件.

 `./configure --prefix=/usr --enable-gui --enable-opensync-plugin` 

目前barry opensync插件只兼容opensync-stable和msynctool-stable包.

### 创建同步配对

首先安装evolution, 此步略过.

创建名为evoberry的同步组

 `msynctool --addgroup evoberry` 

把evolution和barry加入同步组

```
msynctool --addmember evoberry evo2-sync
msynctool --addmember evoberry barry-sync
```

配置evolution

 `msynctool --configure evoberry 1` 

将evolution保存数据文件设为默认.

```
<config>
<address_path>file:///home/user/.evolution/addressbook/local/system</address_path>
<calender_path>file:///home/user/.evolution/calendar/local/system</calender_path>
<tasks_path>file:///home/user/.evolution/tasks/local/system</tasks_path>
</config>
```

配置barry

 `msynctool --configure evoberry 2` 

按如下示例文件配置, 并修改Device值为当机手机PIN码.

```
#
# This is the default configuration file for the barry-sync opensync plugin.
# Comments are preceded by a '#' mark at the beginning of a line.
# The config format is a set of lines of <keyword> <values>.
#
# Keywords available:
#
# DebugMode        - If present, verbose USB debug output will be enabled
#
# Device           - If present, it is followed by the following values:
#      PIN number    - PIN number of the device to sync with (in hex)
#      sync calendar - 1 to sync calendar, 0 to skip
#      sync contacts - 1 to sync contacts, 0 to skip
#
# Password secret  - If present, specifies the device's password in plaintext
#

#DebugMode

Device 00000000 1 1

#Password secret

===开始同步===
确认evolution已经关闭, 同时手机已与电脑相连, 现在只需要输入下述命令. 
 msynctool --sync evoberry
```