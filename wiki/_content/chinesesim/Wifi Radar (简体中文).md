## Contents

*   [1 介绍](#.E4.BB.8B.E7.BB.8D)
*   [2 安装](#.E5.AE.89.E8.A3.85)
*   [3 配置](#.E9.85.8D.E7.BD.AE)
*   [4 小技巧](#.E5.B0.8F.E6.8A.80.E5.B7.A7)
*   [5 附加资料](#.E9.99.84.E5.8A.A0.E8.B5.84.E6.96.99)

## 介绍

[Wifi雷达（Wifi Radar）](http://wifi-radar.systemimager.org/)是一个小巧的GUI程序，你可以用它很容易的切换无线网络连接。

## 安装

要安装Wifi雷达，只需执行：

```
# pacman -S wifi-radar

```

## 配置

```
# visudo

```

增加下面一行：

```
你的用户名     ALL=(ALL) NOPASSWD: /usr/sbin/wifi-radar

```

按 ESC, 接着冒号 (:), 然后按 x, 然后按 ENTER 保存并退出。

增加 _wifi-radar_ 到 /etc/rc.conf 中的DAEMONS组。

从你的程序菜单运行wifi-radar。如果你想查看可用的网络连接，执行_sudo wifi-radar_。

## 小技巧

1.  你可能需要编辑 /etc/conf.d/wifi-radar，设置适合你的特殊网络接口。

1.  有的用户可能要设置‘Ifup required’为开启，以便wifi-radar能正常工作。

## 附加资料

[Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration") - 无线网络安装wiki。