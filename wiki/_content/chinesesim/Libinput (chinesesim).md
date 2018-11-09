Related articles

*   [Xorg](/index.php/Xorg "Xorg")
*   [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics")
*   [Wayland](/index.php/Wayland "Wayland")

来自[libinput](https://freedesktop.org/wiki/Software/libinput/) wiki 项目

	libinput 是一个函数库，在Wayland上用来接收设备的输入，在X.Org上提供h输入设备的驱动。它提供对设备事件的检测和接收。对输入设备信号进行处理。它提供了一些列的函数供用户使用。

## 安装

在Wayland上使用libinput不需要安装。[libinput](https://www.archlinux.org/packages/?name=libinput)包是所有Wayland图形环境的依赖包并且已经安装，也不需要额外的驱动。

如果想要在[Xorg](/index.php/Xorg "Xorg")上[安装libinput](/index.php/%E5%AE%89%E8%A3%85 "安装")，使用[xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput)包。此包允许libinput在X上作为驱动使用。此驱动会代替evdev和synaptics运行。 [[1]](https://freedesktop.org/wiki/Software/libinput/)

你可能也要安装[xorg-xinput](https://www.archlinux.org/packages/?name=xorg-xinput)来更改runtime设置