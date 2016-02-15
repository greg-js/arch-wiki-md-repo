[Fbsplash](http://sourceforge.net/projects/fbsplash.berlios/) (formerly gensplash) is a userspace implementation of a splash screen for Linux systems. It provides a graphical environment during system boot using the Linux framebuffer layer. Fbsplash has not been actively updated in the recent years and may not be working correctly on a recent Arch setup using [systemd](/index.php/Systemd "Systemd"). If you want a fancy splash screen during boot, you might want to try [Plymouth](/index.php/Plymouth "Plymouth") instead.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Fbsplash](#Fbsplash)
    *   [1.2 Scripts](#Scripts)
    *   [1.3 Themes](#Themes)
    *   [1.4 Suspend to Disk](#Suspend_to_Disk)
*   [2 Configuration](#Configuration)
    *   [2.1 Kernel Command Line](#Kernel_Command_Line)
    *   [2.2 Configuration Files](#Configuration_Files)
*   [3 Starting Fbsplash early in the initcpio](#Starting_Fbsplash_early_in_the_initcpio)
*   [4 Console backgrounds](#Console_backgrounds)
*   [5 Links](#Links)

## Installation

### Fbsplash

[Install](/index.php/Install "Install") the [fbsplash](https://aur.archlinux.org/packages/fbsplash/) package. For console backgrounds (discussed later in this article) you should install a kernel patched with fbcondecor such as [linux-fbcondecor](https://aur.archlinux.org/packages/linux-fbcondecor/).

### Scripts

The fbsplash package provides the scripts for basic functionality. If you want more bells and whistles, like smooth progress, filesystem-check progress messages, support for boot-services/'daemons'-icons and theme hook scripts, you may also install the [fbsplash-extras](https://aur.archlinux.org/packages/fbsplash-extras/) package.

### Themes

Themes can be found by searching the AUR for [fbsplash-theme](https://aur.archlinux.org/packages.php?O=0&K=fbsplash-theme&do_Search=Go), in [GNOME-Look.org](http://gnome-look.org) or in [KDE-Look.org](http://kde-look.org).

**Note:** The package fbsplash does not contain a default theme.

### Suspend to Disk

If you want suspend to disk with [Uswsusp](/index.php/Uswsusp "Uswsusp") using Fbsplash, [install](/index.php/Install "Install") the [uswsusp-fbsplash](https://aur.archlinux.org/packages/uswsusp-fbsplash/) package. Additionally there is limited support for using Fbsplash in the [tuxonice-userui](https://aur.archlinux.org/packages/tuxonice-userui/) package for those using a kernel with the [TuxOnIce](/index.php/TuxOnIce "TuxOnIce") patch.

## Configuration

### Kernel Command Line

You now need to set something like `quiet loglevel=3 logo.nologo gfxpayload=keep console=tty1 splash=silent,fadein,fadeout,theme:arch-banner-icons` as your kernel command line parameters in your bootloader. See [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters") for more info.

The parameter `loglevel=3` prevents kernel messages from garbling the splash even with funny hardware (as recent initscripts do not set this by default any more). `quiet` is needed additionally for silencing initcpio messages. `logo.nologo` removes the boot logo (not needed with [linux-fbcondecor](https://aur.archlinux.org/packages.php?ID=50924) since it does not have one anyway). `console=tty1` redirects system messages to tty1 and `splash=silent,fadein,fadeout,theme:arch-banner-icons` creates a silent, splash-only boot with fading in/out _arch-banner-icons_ theme.

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

If **uresume** and/or **encrypt** HOOKS are used, add **fbsplash** _after_ them in [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf"), e.g.:

 `/etc/mkinitcpio.conf`  `HOOKS="base udev autodetect [...] keymap encrypt uresume fbsplash"` 

Rebuild your initcpio via mkinitcpio. See [mkinitcpio#Image creation and activation](/index.php/Mkinitcpio#Image_creation_and_activation "Mkinitcpio") for more info.

**Tip:** For a quick resume, it is recommended to put **uswsusp** _before_ **fbsplash** or even drop `fadein`, if using a Fbcondecor kernel.

If you have trouble getting fbsplash to work and your machine uses KMS (Kernel Mode Setting), try [adding the appropriate driver to mkinitcpio.conf](/index.php/Intel#KMS_.28Kernel_Mode_Setting.29 "Intel").

## Console backgrounds

If you have a kernel that supports Fbcondecor (eg. [linux-fbcondecor](https://aur.archlinux.org/packages/linux-fbcondecor/)), you can get nice graphical console backgrounds beside the splash screen.

Currently(2015) the [fbsplash](https://aur.archlinux.org/packages/fbsplash/) package provides a deprecated daemon script to set up console backgrounds. However, the programs that actually handle console backgrounds are still working fine! Just look for /usr/bin/splash_manager or /usr/bin/fbcondecor_ctl and set up console backgrounds manually, or use them as a basis to [write](/index.php/Systemd#Writing_unit_files "Systemd") your own systemd unit.

Even if you have no interest in a splash screen, you will still need splash themes for your console background. Either get an existing one from the AUR [fbsplash-theme](https://aur.archlinux.org/packages.php?O=0&K=fbsplash-theme&do_Search=Go) or create one yourself in `/etc/splash/`. The only parameter in the theme .cfg file needed to enable console backgrounds is `pic`.

You may even boot up with a nice console background and the plain Arch Linux boot messages instead of a splash screen. Just change your kernel command line to use the verbose mode:

```
quiet console=tty1 splash=verbose,theme:arch-banner-icons

```

## Links

*   [http://fbsplash.alanhaggai.org](http://fbsplash.alanhaggai.org) 
*   [http://dev.gentoo.org/~spock/projects/fbcondecor/](http://dev.gentoo.org/~spock/projects/fbcondecor/) 
*   [http://www.mepiscommunity.org/fbcondecor](http://www.mepiscommunity.org/fbcondecor)