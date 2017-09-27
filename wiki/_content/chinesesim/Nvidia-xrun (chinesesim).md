**翻译状态：** 本文是英文页面 [Nvidia-xrun](/index.php/Nvidia-xrun "Nvidia-xrun") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-09-19，点击[这里](https://wiki.archlinux.org/index.php?title=Nvidia-xrun&diff=0&oldid=490779)可以查看翻译后英文页面的改动。

[nvidia-xrun](https://github.com/Witko/nvidia-xrun)是一个实用的独立显卡与独立的NVIDIA图形完全性能。[bumblebee](/index.php/Bumblebee "Bumblebee")目前的状态提供了非常糟糕的表现，nvidia-xrun这个解决方案提供了一个更复杂的程序，拥有更好的GPU利用效率。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 设置nvidia的bus id](#.E8.AE.BE.E7.BD.AEnvidia.E7.9A.84bus_id)
    *   [2.2 自动y运行窗口管理器](#.E8.87.AA.E5.8A.A8y.E8.BF.90.E8.A1.8C.E7.AA.97.E5.8F.A3.E7.AE.A1.E7.90.86.E5.99.A8)
    *   [2.3 使用bbswitch在管理nvidia显卡](#.E4.BD.BF.E7.94.A8bbswitch.E5.9C.A8.E7.AE.A1.E7.90.86nvidia.E6.98.BE.E5.8D.A1)
*   [3 使用](#.E4.BD.BF.E7.94.A8)
*   [4 问题](#.E9.97.AE.E9.A2.98)

## 安装

安装：

*   [nvidia](https://www.archlinux.org/packages/?name=nvidia)
*   [bbswitch](https://www.archlinux.org/packages/?name=bbswitch)
*   [nvidia-xrun](https://aur.archlinux.org/packages/nvidia-xrun/) 或者 [nvidia-xrun-git](https://aur.archlinux.org/packages/nvidia-xrun-git/)
*   一个 [窗口管理器](/index.php/Window_manager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Window manager (简体中文)"), 例如 [openbox](https://www.archlinux.org/packages/?name=openbox) 可选，仅用来运行需要使用nvidia的程序，因为直接使用nvidia-xrun运行一些程序（如steam）表现较差，使用一些像Openbox窗口管理器会好一些。

## 配置

### 设置nvidia的bus id

如果安装nvidia-xrun完毕后，`/etc/X11/nvidia-xorg.conf.d/30-nvidia.conf`文件中已经设置好bus id，可直接跳过本步。 如果你从[nvidia-xrun github repo]下载安装的nvidia-xrun，你应该需要进行手动设置bus id。

获取ID：一般的设备的总线ID是1:0:0，为了确保正确，使用一下命令获取ID:

```
 lspci | grep NVIDIA

```

在输出内容中第行首即可看到ID。

新增文件`/etc/X11/nvidia-xorg.conf.d/30-nvidia.conf` ，添加类似如下内容：

 `/etc/X11/nvidia-xorg.conf.d/30-nvidia.conf` 
```
Section "Device"
    Identifier "nvidia"
    Driver "nvidia"
    BusID "PCI:1:0:0"
EndSection
```

同样的，如果遇到问题你可以调整一些NVIDIA设置：

 `/etc/X11/nvidia-xorg.conf.d/30-nvidia.conf` 
```
Section "Screen"
    Identifier "nvidia"
    Device "nvidia"
    #  Option "AllowEmptyInitialConfiguration" "Yes"
    #  Option "UseDisplayDevice" "none"
EndSection
```

### 自动y运行窗口管理器

编辑~/.nvidia-xinitrc，例如使用openbox，在其中添加：

```
 openbox-session

```

在tty登录后，通过以下命令启动openbox桌面环境，在openbox中运行程序即可使用NVIDIA渲染：

```
 nvidia-xrun

```

### 使用bbswitch在管理nvidia显卡

平时使用bbswitch关闭nvidia显卡，在需要使用nvidia运行程序时，运行`nvidia-xrun`就会唤醒nvidia显卡，并自动打开设定好的窗口管理器。

*   在启动时载入bbswitch模块

```
 # echo 'bbswitch ' > /etc/modules-load.d/bbswitch

```

*   关闭nvidia显卡的选项

```
 # echo 'options bbswitch load_state=0' > /etc/modprobe.d/bbswitch.conf 

```

*   将nvidia相关模块加入黑名单

```
 $ lsmod | grep nvidia | cut -d ' ' -f 1 > /tmp/nvidia
 $ lsmod | grep  nouveau | cut -d ' ' -f 1 > > /tmp/nvidia
 $ sort -n /tmp/nvidia | uniq >  /tmp/nvidia.conf#去重
 $ sed -i 's/^\w*$/blacklist &/g' /tmp/nvidia.conf  #添加blacklist
 # cp /tmp/nvidia.conf /etc/modprobe.d/nvidia.conf  #移动

```

重启系统即可。 查看状态：

```
 cat /proc/acpi/bbswitch  

```

开关显卡可以使用bbswitch相关命令

```
 # tee /proc/acpi/bbswitch <<<OFF
 # tee /proc/acpi/bbswitch <<<ON

```

更多bbswitch信息查看 [Bumblebee-Project/bbswitch](https://github.com/Bumblebee-Project/bbswitch)

## 使用

1.  切换到tty
2.  登录
3.  运行`nvidia-xrun [app]`

## 问题

直接使用nvidia-xrun运行steam表现较差，使用一些像Openbox窗口管理器会更好。