[Fbsplash](http://fbsplash.berlios.de) (前身为 gensplash) 使用framebuffer layer为linux系统提供开关机splash.

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
    *   [1.1 Fbsplash](#Fbsplash)
    *   [1.2 附加包](#.E9.99.84.E5.8A.A0.E5.8C.85)
    *   [1.3 主题](#.E4.B8.BB.E9.A2.98)
    *   [1.4 Suspend to Disk](#Suspend_to_Disk)
*   [2 Configuration](#Configuration)
    *   [2.1 Kernel Command Line](#Kernel_Command_Line)
    *   [2.2 Configuration Files](#Configuration_Files)
*   [3 Starting Fbsplash early in the initcpio](#Starting_Fbsplash_early_in_the_initcpio)
*   [4 Console backgrounds](#Console_backgrounds)
*   [5 Links](#Links)

## 安装

### Fbsplash

从 [AUR](/index.php/AUR "AUR") [fbsplash](https://aur.archlinux.org/packages/fbsplash/) 下载安装编译。

### 附加包

fbsplash包只提供了最基本的功能,为了更好的支持, 应该安装 [fbsplash-extras](https://aur.archlinux.org/packages.php?ID=38775) 。

### 主题

安装Fbsplash主题。 [从AUR搜索 'fbsplash-theme'](https://aur.archlinux.org/packages.php?O=0&K=fbsplash-theme&do_Search=Go) 或 [GNOME-Look.org](http://gnome-look.org) 和 [KDE-Look.org](http://kde-look.org)。

**注意:** Fbsplash包默认不含主题文件。

### Suspend to Disk

If you want suspend to disk with Fbsplash, install the [uswsusp-fbsplash package](https://aur.archlinux.org/packages.php?ID=16233) from the AUR. For more info have a look at [Pm-utils#Using_another_sleep_backend_.28like_uswsusp.29](/index.php/Pm-utils#Using_another_sleep_backend_.28like_uswsusp.29 "Pm-utils") or [Suspend_to_Disk#Uswsusp_method (hibernate-script)](/index.php/Suspend_to_Disk#Uswsusp_method_.28hibernate-script.29 "Suspend to Disk"). Additionally there is limited support for using a Fbsplash theme in the [tuxonice-userui package](https://aur.archlinux.org/packages.php?ID=24613) for those using a kernel with the TuxOnIce patch.

## Configuration

### Kernel Command Line

You now need to set `quiet splash` as you kernel command line parameters in your bootloader. The following is an example for [GRUB](/index.php/GRUB "GRUB") (see the [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy"), [LILO](/index.php/LILO "LILO") or [Syslinux](/index.php/Syslinux "Syslinux") articles accordingly):

Edit the file `/etc/default/grub` and append your kernel options to the line `GRUB_CMDLINE_LINUX_DEFAULT=""`:

 `/etc/default/grub`  `GRUB_CMDLINE_LINUX_DEFAULT="ro quiet loglevel=3 logo.nologo vga=790 console=tty1 splash=silent,fadein,fadeout,theme:arch-banner-icons"` 

Re-generate `grub.cfg` with:

 `# grub-mkconfig -o /boot/grub/grub.cfg` 

The parameter `loglevel=3` prevents kernel messages from garbling the splash even with funny hardware (as recent initscripts do not set this by default any more). `quiet` is needed additionally for silencing initcpio messages. `logo.nologo` removes the boot logo (not needed with [linux-fbcondecor](https://aur.archlinux.org/packages/linux-fbcondecor/) since it does not have one anyway). `console=tty1` redirects system messages to tty1 and `splash=silent,fadein,fadeout,theme:arch-banner-icons` creates a silent, splash-only boot with fading in/out _arch-banner-icons_ theme.

### Configuration Files

Put one or more of the themes you installed into `/etc/conf.d/splash`. You can also specify screen resolutions to save some initcpio space:

 `/etc/conf.d/splash` 

```
SPLASH_THEMES="
    arch-black
    arch-banner-icons/1280x1024.cfg
    arch-banner-noicons/1280x1024.cfg"
```

**Note:** The theme **arch-banner-icons** contains mainly symlinks to **arch-banner-noicons**. So if one of them is included in total, not much space will be saved by limiting the resolutions.

## Starting Fbsplash early in the initcpio

If **uresume** and/or **encrypt** HOOKS are used, add **fbsplash** _after_ them in `/etc/[mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf")`, e.g.:

 `/etc/mkinitcpio.conf`  `HOOKS="base udev autodetect [...] keymap encrypt uresume fbsplash"` 

Rebuild your initcpio via mkinitcpio. See the [Mkinitcpio article](/index.php/Mkinitcpio#Creating_the_image "Mkinitcpio") for more info.

**Tip:** For a quick resume, it is recommended to put **uswsusp** _before_ **fbsplash** or even drop `fadein`, if using a Fbcondecor kernel.

If you have trouble getting fbsplash to work and your machine uses KMS (Kernel Mode Setting), try [adding the appropriate driver to mkinitcpio.conf](/index.php/Intel#KMS_.28Kernel_Mode_Setting.29 "Intel").

## Console backgrounds

If you have a kernel that supports Fbcondecor (eg. [linux-fbcondecor](https://aur.archlinux.org/packages/linux-fbcondecor/)), you can get nice graphical console backgrounds beside the splash screen. Just search the AUR for [fbsplash-theme](https://aur.archlinux.org/packages.php?O=0&K=fbsplash-theme&do_Search=Go).

After installing your patched kernel and fbsplash, add `fbcondecor` to your `DAEMONS` array in `/etc/[rc.conf](/index.php/Rc.conf "Rc.conf")`:

 `/etc/rc.conf`  `DAEMONS=(... fbcondecor ...)` 

There is also a configuration file `/etc/conf.d/fbcondecor` to set up the virtual terminals to be used.

You may even boot up with a nice console background and the plain Arch Linux boot messages instead of a splash screen. Just change your kernel command line to use the verbose mode:

```
quiet console=tty1 splash=verbose,theme:arch-banner-icons

```

## Links

*   [http://fbsplash.alanhaggai.org](http://fbsplash.alanhaggai.org)
*   [http://dev.gentoo.org/~spock/projects/fbcondecor/](http://dev.gentoo.org/~spock/projects/fbcondecor/)