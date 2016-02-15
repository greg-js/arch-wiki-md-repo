[Plymouth](http://www.freedesktop.org/wiki/Software/Plymouth) is a project from Fedora providing a flicker-free graphical boot process. It relies on [kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting") (KMS) to set the native resolution of the display as early as possible, then provides an eye-candy splash screen leading all the way up to the login manager.

## Contents

*   [1 Preparation](#Preparation)
*   [2 Installation](#Installation)
    *   [2.1 The plymouth hook](#The_plymouth_hook)
    *   [2.2 The kernel command line](#The_kernel_command_line)
*   [3 Configuration](#Configuration)
    *   [3.1 Smooth transition](#Smooth_transition)
    *   [3.2 Show Delay](#Show_Delay)
    *   [3.3 Changing the Theme](#Changing_the_Theme)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Replacing the Arch Logo and creating custom themes](#Replacing_the_Arch_Logo_and_creating_custom_themes)
*   [5 See also](#See_also)

## Preparation

**Warning:** Plymouth is currently under heavy development and may contain serious bugs.

Plymouth primarily uses [KMS](/index.php/KMS "KMS") (Kernel Mode Setting) to display graphics. If you can't use KMS (e.g. because you are using a proprietary driver) you will need to use [framebuffer](/index.php/Framebuffer#Framebuffer_Resolution "Framebuffer") instead. In EFI/UEFI systems, plymouth can utilize the EFI framebuffer, otherwise Uvesafb is recommended as it can function with widescreen resolutions.

If you have neither KMS nor a framebuffer, Plymouth will fall back to text-mode.

## Installation

Plymouth is available from the [AUR](/index.php/AUR "AUR"): the stable package is [plymouth](https://aur.archlinux.org/packages/plymouth/) and the development version is [plymouth-git](https://aur.archlinux.org/packages/plymouth-git/).

If you also use [KDM](/index.php/KDM "KDM"), you need to install the [kdebase-workspace-plymouth](https://aur.archlinux.org/packages/kdebase-workspace-plymouth/), otherwise kdm may not start correctly.

If you also use [GDM](/index.php/GDM "GDM"), you should install the [gdm-plymouth](https://aur.archlinux.org/packages/gdm-plymouth/), which compiles gdm with plymouth support.

Both packages are also available in the unofficial [nullptr_t](/index.php/Unofficial_user_repositories#nullptr_t "Unofficial user repositories") repository.

### The plymouth hook

Add `plymouth` to the HOOKS array in [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf"). It **must** be added **after** `base` and `udev` for it to work:

 `/etc/mkinitcpio.conf`  `HOOKS="base udev plymouth [...] "` 
**Warning:** If you use [hard drive encryption](/index.php/System_Encryption_with_LUKS_for_dm-crypt "System Encryption with LUKS for dm-crypt") with the `encrypt` hook, you **must** replace the `encrypt` hook with `plymouth-encrypt` in order to get to the TTY password prompts.

For early KMS start (if you are using the open drivers) add the module [radeon](/index.php/Radeon "Radeon") (for radeon cards), [i915](/index.php/I915 "I915") (for intel cards) or [nouveau](/index.php/Nouveau "Nouveau") (for nvidia cards) to the MODULES line in `/etc/mkinitcpio.conf`:

 `/etc/mkinitcpio.conf` 

```
MODULES="i915"
**or**
MODULES="radeon"
**or**
MODULES="nouveau"
```

### The kernel command line

You now need to set `quiet splash` as your kernel command line parameter in your bootloader. See [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters") for more info.

Rebuild your initrd image (see [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") article for details), for example:

```
# mkinitcpio -p linux

```

## Configuration

### Smooth transition

**Warning:** Plymouth version 0.9.2-5 has been reported to cause issues when starting [LightDM](/index.php/LightDM "LightDM"). The issue is known on upstream and you should use light display managers like [SLiM](/index.php/SLiM "SLiM") or [SDDM](/index.php/SDDM "SDDM") for now.

For _smooth transition_ to [display manager](/index.php/Display_manager "Display manager") you have to:

1.  Disable your Display Manager Unit, e.g. `systemctl disable gdm.service`
2.  Enable the respective DM-plymouth Unit (GDM, KDM, LXDM, SLiM units provided), e.g. `systemctl enable gdm-plymouth.service`

### Show Delay

As of version 0.9.0 plymouth has a new configuration option available in /etc/plymouth/plymouthd.conf

 `/etc/plymouth/plymouthd.conf` 

```
[Daemon]
Theme=spinner
ShowDelay=5
```

On systems that boot quickly, you may only see a flicker of your splash theme before your DM or login prompt is ready. You can set ShowDelay to an interval (in seconds) longer than your boot time to prevent this flicker and only show a blank screen. The default is 5 seconds, but you may wish to change this to a lower value to see your splash earlier during boot.

### Changing the Theme

Plymouth comes with a selection of themes:

1.  **Fade-in**: "Simple theme that fades in and out with shimmering stars"
2.  **Glow**: "Corporate theme with pie chart boot progress followed by a glowing emerging logo"
3.  **Script**: "Script example plugin" (Despite the description seems to be a quite nice Arch logo theme)
4.  **Solar**: "Space theme with violent flaring blue star"
5.  **Spinner**: "Simple theme with a loading spinner"
6.  **Spinfinity**: "Simple theme that shows a rotating infinity sign in the center of the screen"
7.  _(**Text**: "Text mode theme with tricolor progress bar")_
8.  _(**Details**: "Verbose fallback theme")_

In addition you can install other themes from [AUR](/index.php/AUR "AUR"), just have a look at the "Required by"-Array on [plymouth](https://aur.archlinux.org/packages/plymouth/).

By default, **spinner** theme is selected. You can change the theme by editing `/etc/plymouth/plymouthd.conf`, for example:

 `/etc/plymouth/plymouthd.conf` 

```
[Daemon]
Theme=spinner
ShowDelay=5
```

You will also need to rebuild your initrd image every time you change your theme.

All currently installed themes can be listed by using this command:

```
$ plymouth-set-default-theme -l

```

or:

 `$ ls /usr/share/plymouth/themes` 

```
details  glow    solar       spinner  tribar
fade-in  script  spinfinity  text

```

Themes can be previewed without rebuilding, press `Ctrl+Alt+F2` to change to console, log in as root and type:

```
# plymouthd
# plymouth --show-splash

```

To quit the preview, press `Ctrl+Alt+F2` again and type:

```
# plymouth --quit

```

every time a theme is changed, the kernel image must be rebuilt with:

```
# mkinitcpio -p <name of your kernel preset; e.g. linux>

```

To change theme and rebuild initrd image:

```
# plymouth-set-default-theme -R <theme>

```

Reboot to apply the changes.

## Tips and tricks

During boot you can switch to kernel messages by pressing "Home" (or "Escape") key.

### Replacing the Arch Logo and creating custom themes

The following themes use the Arch Linux logo supplied by Plymouth in `/usr/share/plymouth/arch-logo.png`: fade-in, script, solar, spinfinity. If you want to use another logo, you can take one of them or one of the plymouth themes in [AUR](/index.php/AUR "AUR"), edit the file `*.plymouth` (and maybe `*.script`, too) and replace this image with one of your choice. You should create a package from your newly created theme, because changes in `/usr/share/plymouth` may not be persistent across package upgrades.

After installing and selecting your theme, you should rebuild the initrd image to use the new splash.

## See also

*   [Original Spec](http://fedoraproject.org/wiki/Releases/FeatureBetterStartup)
*   [Related forum thread](https://bbs.archlinux.org/viewtopic.php?id=81406)