Related articles

*   [Silent boot](/index.php/Silent_boot "Silent boot")

[Plymouth](http://www.freedesktop.org/wiki/Software/Plymouth) is a project from Fedora and now listed among the [freedesktop.org's official resources](https://www.freedesktop.org/wiki/Software/#graphicsdriverswindowsystemsandsupportinglibraries) providing a flicker-free graphical boot process. It relies on [kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting") (KMS) to set the native resolution of the display as early as possible, then provides an eye-candy splash screen leading all the way up to the login manager.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Preparation](#Preparation)
*   [2 Installation](#Installation)
    *   [2.1 The plymouth hook](#The_plymouth_hook)
    *   [2.2 Alternative plymouth hook (systemd)](#Alternative_plymouth_hook_(systemd))
    *   [2.3 The kernel command line](#The_kernel_command_line)
*   [3 Configuration](#Configuration)
    *   [3.1 Smooth transition](#Smooth_transition)
    *   [3.2 Show Delay](#Show_Delay)
    *   [3.3 Changing the Theme](#Changing_the_Theme)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Show kernel messages](#Show_kernel_messages)
    *   [4.2 Adding Arch Logo to spinner and BGRT themes](#Adding_Arch_Logo_to_spinner_and_BGRT_themes)
    *   [4.3 Replacing the Arch Logo and creating custom themes](#Replacing_the_Arch_Logo_and_creating_custom_themes)
*   [5 See also](#See_also)

## Preparation

*Plymouth* primarily uses [KMS](/index.php/KMS "KMS") (Kernel Mode Setting) to display graphics. In EFI/UEFI systems, *plymouth* can utilize the EFI framebuffer. If you can't use KMS in e.g. because you are using a proprietary driver, or if you don't want to use EFI framebuffer, consider using [Uvesafb](/index.php/Uvesafb "Uvesafb") as it works with widescreen resolutions.

If you have neither KMS nor a framebuffer, *Plymouth* will fall back to text-mode.

## Installation

Plymouth is available from the [AUR](/index.php/AUR "AUR"): the stable package is [plymouth](https://aur.archlinux.org/packages/plymouth/) and the development version is [plymouth-git](https://aur.archlinux.org/packages/plymouth-git/).

If you also use [GDM](/index.php/GDM "GDM"), you should install the [gdm-plymouth](https://aur.archlinux.org/packages/gdm-plymouth/), which compiles gdm with plymouth support.

### The plymouth hook

Add `plymouth` to the `HOOKS` array in [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf"). It **must** be added **after** `base` and `udev` for it to work:

 `/etc/mkinitcpio.conf`  `HOOKS=(base udev plymouth [...])` 
**Warning:**

*   If you use [hard drive encryption](/index.php/System_Encryption_with_LUKS_for_dm-crypt "System Encryption with LUKS for dm-crypt") with the `encrypt` hook, you **must** replace the `encrypt` hook with `plymouth-encrypt` and add it after the `plymouth` hook in order to get to the TTY password prompts.
*   Using `PARTUUID` or `PARTLABEL` in `cryptdevice=` parameter does **not** work with `plymouth-encrypt` hook.
*   For a [ZFS encrypted root](/index.php/Installing_Arch_Linux_on_ZFS#Native_encryption "Installing Arch Linux on ZFS"), you **must** install [plymouth-zfs](https://aur.archlinux.org/packages/plymouth-zfs/) and replace `zfs` hook with `plymouth-zfs`

After adding the `plymouth-encrypt` hook, if input goes to the background in plaintext instead of into the password prompt you need to add your (kernel) graphics driver to your initramfs. For example, if using intel:

 `/etc/mkinitcpio.conf`  `MODULES=(i915 [...])` 

This might also be a step needed for some themes to work.

### Alternative plymouth hook (systemd)

If your [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf") includes the `systemd` hook, then replace `plymouth` with `sd-plymouth`. Additionally, if using hard drive encryption, use `sd-encrypt` instead of `encrypt` or `plymouth-encrypt`:

 `/etc/mkinitcpio.conf`  `HOOKS=(base systemd sd-plymouth [...] sd-encrypt [...])` 

### The kernel command line

You now need to set the `quiet splash loglevel=3 rd.udev.log_priority=3 vt.global_cursor_default=0` [kernel parameters](/index.php/Kernel_parameters "Kernel parameters"). See [Silent boot](/index.php/Silent_boot "Silent boot") for other parameters to limit the output to the console.

Rebuild your initrd image (see [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") article for details), for example:

```
# mkinitcpio -p linux

```

## Configuration

### Smooth transition

To enable *smooth transition* (if supported) you have to:

1.  [Disable](/index.php/Disable "Disable") your [display manager](/index.php/Display_manager "Display manager") unit, e.g. `gdm.service`
2.  [Enable](/index.php/Enable "Enable") the respective DM-plymouth unit (GDM, LXDM, SLiM, LightDM, SDDM units provided), e.g. `gdm-plymouth.service`

### Show Delay

Plymouth has a configuration option to delay the splash screen:

 `/etc/plymouth/plymouthd.conf` 
```
[Daemon]
Theme=spinner
ShowDelay=5
```

On systems that boot quickly, you may only see a flicker of your splash theme before your DM or login prompt is ready. You can set `ShowDelay` to an interval (in seconds) longer than your boot time to prevent this flicker and only show a blank screen. The default is 5 seconds, but you may wish to change this to a lower value to see your splash earlier during boot.

### Changing the Theme

Plymouth comes with a selection of themes:

1.  **Fade-in**: "Simple theme that fades in and out with shimmering stars"
2.  **Glow**: "Corporate theme with pie chart boot progress followed by a glowing emerging logo"
3.  **Script**: "Script example plugin" (Despite the description seems to be a quite nice Arch logo theme)
4.  **Solar**: "Space theme with violent flaring blue star"
5.  **Spinner**: "Simple theme with a loading spinner"
6.  **Spinfinity**: "Simple theme that shows a rotating infinity sign in the center of the screen"
7.  *(**Text**: "Text mode theme with tricolor progress bar")*
8.  *(**Details**: "Verbose fallback theme")*

Development version of Plymouth ([plymouth-git](https://aur.archlinux.org/packages/plymouth-git/)) also comes with the **BGRT** theme, which is a variation of Spinner that keeps the OEM logo if available.

In addition you can install other themes from [AUR](/index.php/AUR "AUR"), just have a look at the "Required by"-Array on [plymouth](https://aur.archlinux.org/packages/plymouth/).

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

By default, the **spinner** theme is selected. The theme can be changed by editing `/etc/plymouth/plymouthd.conf`, for example:

 `/etc/plymouth/plymouthd.conf` 
```
[Daemon]
Theme=spinner
ShowDelay=5
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

Every time a theme is changed, the kernel image must be rebuilt:

```
# plymouth-set-default-theme -R <theme>

```

Reboot to apply the changes.

## Tips and tricks

#### Show kernel messages

During boot you can switch to kernel messages by pressing "Home" (or "Escape") key.

### Adding Arch Logo to spinner and BGRT themes

To add Arch Logo to *spinner* and *BGRT* themes copy Arch logo to spinner theme directory with name `watermark.png`:

```
# cp /usr/share/plymouth/arch-logo.png /usr/share/plymouth/themes/spinner/watermark.png

```

### Replacing the Arch Logo and creating custom themes

The following themes use the Arch Linux logo supplied by Plymouth in `/usr/share/plymouth/arch-logo.png`: fade-in, script, solar, spinfinity. If you want to use another logo, you can take one of them or one of the plymouth themes in [AUR](/index.php/AUR "AUR"), edit the file `*.plymouth` (and maybe `*.script`, too) and replace this image with one of your choice. You should create a package from your newly created theme, because changes in `/usr/share/plymouth` may not be persistent across package upgrades.

After installing and selecting your theme, you should rebuild the initrd image to use the new splash.

## See also

*   [Original Spec](http://fedoraproject.org/wiki/Releases/FeatureBetterStartup)
*   [Related forum thread](https://bbs.archlinux.org/viewtopic.php?id=81406)