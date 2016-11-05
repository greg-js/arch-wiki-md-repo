## Contents

*   [1 GUI configuration tools](#GUI_configuration_tools)
*   [2 Visual configuration](#Visual_configuration)
    *   [2.1 Setting the framebuffer resolution](#Setting_the_framebuffer_resolution)
    *   [2.2 915resolution hack](#915resolution_hack)
    *   [2.3 Background image and bitmap fonts](#Background_image_and_bitmap_fonts)
    *   [2.4 Theme](#Theme)
    *   [2.5 Menu colors](#Menu_colors)
    *   [2.6 Hidden menu](#Hidden_menu)
    *   [2.7 Disable framebuffer](#Disable_framebuffer)
*   [3 Booting ISO9660 image file directly via GRUB](#Booting_ISO9660_image_file_directly_via_GRUB)
*   [4 Persistent block device naming](#Persistent_block_device_naming)
*   [5 Using labels](#Using_labels)
*   [6 Password protection of GRUB menu](#Password_protection_of_GRUB_menu)
    *   [6.1 Password protection of GRUB edit and console options only](#Password_protection_of_GRUB_edit_and_console_options_only)
*   [7 Hide GRUB unless the Shift key is held down](#Hide_GRUB_unless_the_Shift_key_is_held_down)
*   [8 Combining the use of UUIDs and basic scripting](#Combining_the_use_of_UUIDs_and_basic_scripting)
*   [9 Manually creating grub.cfg](#Manually_creating_grub.cfg)
*   [10 Multiple entries](#Multiple_entries)
    *   [10.1 Disable submenu](#Disable_submenu)
    *   [10.2 Recall previous entry](#Recall_previous_entry)
    *   [10.3 Changing the default menu entry](#Changing_the_default_menu_entry)
    *   [10.4 Boot non-default entry only once](#Boot_non-default_entry_only_once)
*   [11 Play a tune](#Play_a_tune)
*   [12 Manual configuration of core image for early boot](#Manual_configuration_of_core_image_for_early_boot)

## GUI configuration tools

Following package may be installed:

*   **grub-customizer** — GTK+ customizer for GRUB or BURG

	[https://launchpad.net/grub-customizer](https://launchpad.net/grub-customizer) || [grub-customizer](https://aur.archlinux.org/packages/grub-customizer/)

*   **grub2-editor** — KDE4 control module for configuring the GRUB bootloader

	[http://kde-apps.org/content/show.php?content=139643](http://kde-apps.org/content/show.php?content=139643) || [grub2-editor](https://aur.archlinux.org/packages/grub2-editor/)

*   **grub2-editor-frameworks** — Unofficial KF5 port of grub2-editor

	[https://github.com/maz-1/grub2-editor](https://github.com/maz-1/grub2-editor) || [grub2-editor-frameworks](https://aur.archlinux.org/packages/grub2-editor-frameworks/)

*   **startupmanager** — GUI app for changing the settings of GRUB Legacy, GRUB, Usplash and Splashy ([abandonned](https://launchpad.net/startup-manager/+announcement/8300))

	[http://sourceforge.net/projects/startup-manager/](http://sourceforge.net/projects/startup-manager/) || [startupmanager](https://aur.archlinux.org/packages/startupmanager/)

## Visual configuration

In GRUB it is possible, by default, to change the look of the menu. Make sure to initialize, if not done already, GRUB graphical terminal, gfxterm, with proper video mode, gfxmode, in GRUB. This can be seen in the section [GRUB#"No suitable mode found" error](/index.php/GRUB#.22No_suitable_mode_found.22_error "GRUB"). This video mode is passed by GRUB to the linux kernel via 'gfxpayload' so any visual configurations need this mode in order to be in effect.

### Setting the framebuffer resolution

GRUB can set the framebuffer for both GRUB itself and the kernel. The old `vga=` way is deprecated. The preferred method is editing `/etc/default/grub` as the following sample:

```
GRUB_GFXMODE=1024x768x32
GRUB_GFXPAYLOAD_LINUX=keep

```

Multiple resolutions can be specified, including the default `auto`, so it is recommended that you edit the line to resemble `GRUB_GFXMODE=<desired resolution>,<fallback such as 1024x768>,auto`. For more information, refer to [the GRUB gfxmode documentation](https://www.gnu.org/software/grub/manual/html_node/gfxmode.html#gfxmode). The [gfxpayload](https://www.gnu.org/software/grub/manual/html_node/gfxpayload.html#gfxpayload) property will make sure the kernel keeps the resolution.

**Note:**

*   Only the modes supported by the graphics card via [VESA BIOS Extensions](https://en.wikipedia.org/wiki/VESA_BIOS_Extensions "wikipedia:VESA BIOS Extensions") can be used. To view the list of supported modes, install [hwinfo](https://www.archlinux.org/packages/?name=hwinfo) and run `hwinfo --framebuffer` as root. Alternatively, enter the GRUB command line and run the command `videoinfo`.
*   [NVIDIA](/index.php/NVIDIA "NVIDIA") proprietary driver (tested with GeForce GTX 970, driver: nvidia 370) accepts `GRUB_GFXMODE` in format `*<width>*x*<height>*-*<depth>*` (e.g. `1920x1200-24`, but not `1920x1200x24`).
*   Make sure to run `grub-mkconfig -o /boot/grub/grub.cfg` after making changes.

If this method does not work for you, the deprecated `vga=` method will still work. Just add it next to the `"GRUB_CMDLINE_LINUX_DEFAULT="` line in `/etc/default/grub` for example: `"GRUB_CMDLINE_LINUX_DEFAULT="quiet splash vga=792"` will give you a `1024x768` resolution.

### 915resolution hack

Some times for Intel graphic adapters neither `# hwinfo --framebuffer` nor `videoinfo` will show you the desired resolution. In this case you can use `915resolution` hack. This hack will temporarily modify video BIOS and add needed resolution. See [915resolution's home page](http://915resolution.mango-lang.org/). The package can be found here: [915resolution](https://aur.archlinux.org/packages/915resolution/)

First you need to find a video mode which will be modified later. For that we need the GRUB command shell:

 `sh:grub> 915resolution -l` 
```
Intel 800/900 Series VBIOS Hack : version 0.5.3
[...]
**Mode 30** : 640x480, 8 bits/pixel
[...]

```

Next, we overwrite the `Mode 30` with `1440x900` resolution:

 `/etc/grub.d/00_header` 
```
[...]
**915resolution 30 1440 900  # Inserted line**
set gfxmode=${GRUB_GFXMODE}
[...]

```

Lastly we need to set `GRUB_GFXMODE` as described earlier, regenerate `grub.cfg` and reboot to test changes.

### Background image and bitmap fonts

GRUB comes with support for background images and bitmap fonts in `pf2` format. The unifont font is included in the [grub](https://www.archlinux.org/packages/?name=grub) package under the filename `unicode.pf2`, or, as only ASCII characters under the name `ascii.pf2`.

Image formats supported include tga, png and jpeg, providing the correct modules are loaded. The maximum supported resolution depends on your hardware.

Make sure you have set up the proper [framebuffer resolution](#Setting_the_framebuffer_resolution).

Edit `/etc/default/grub` like this:

```
GRUB_BACKGROUND="/boot/grub/myimage"
#GRUB_THEME="/path/to/gfxtheme"
GRUB_FONT="/path/to/font.pf2"

```

**Note:** If you have installed GRUB on a separate partition, `/boot/grub/myimage` automatically becomes `/grub/myimage` in `grub.cfg`.

[Re-generate](/index.php/GRUB#Generate_the_main_configuration_file "GRUB") `grub.cfg` to apply the changes. If adding the splash image was successful, the user will see `"Found background image..."` in the terminal as the command is executed. If this phrase is not seen, the image information was probably not incorporated into the `grub.cfg` file.

If the image is not displayed, check:

*   The path and the filename in `/etc/default/grub` are correct
*   The image is of the proper size and format (tga, png, 8-bit jpg)
*   The image was saved in the RGB mode, and is not indexed
*   The console mode is not enabled in `/etc/default/grub`
*   The command `grub-mkconfig` must be executed to place the background image information into the `/boot/grub/grub.cfg` file
*   The `grub-mkconfig` scripts won't quote the file name in `grub.cfg` so make sure it does not contain spaces

### Theme

Here is an example for configuring Starfield theme which was included in GRUB package.

Edit `/etc/default/grub`

```
GRUB_THEME="/usr/share/grub/themes/starfield/theme.txt"

```

[Re-generate](/index.php/GRUB#Generate_the_main_configuration_file "GRUB") `grub.cfg` to apply the changes. If configuring the theme was successful, you will see `Found theme: /usr/share/grub/themes/starfield/theme.txt` in the terminal.

Your splash image will usually not be displayed when using a theme.

### Menu colors

You can set the menu colors in GRUB. The available colors for GRUB can be found in [the GRUB Manual](https://www.gnu.org/software/grub/manual/html_node/Theme-file-format.html). Here is an example:

Edit `/etc/default/grub`:

```
GRUB_COLOR_NORMAL="light-blue/black"
GRUB_COLOR_HIGHLIGHT="light-cyan/blue"

```

### Hidden menu

One of the unique features of GRUB is hiding/skipping the menu and showing it by holding `Esc` when needed. You can also adjust whether you want to see the timeout counter.

Edit `/etc/default/grub` as you wish. Here are the lines you need to add to enable this feature, the timeout has been set to five seconds and to be shown to the user:

```
GRUB_TIMEOUT=5
GRUB_TIMEOUT_STYLE='countdown'

```

GRUB_TIMEOUT is how many seconds before displaying menu.

### Disable framebuffer

Users who use NVIDIA proprietary driver might wish to disable GRUB's framebuffer as it can cause problems with the binary driver.

To disable framebuffer, edit `/etc/default/grub` and uncomment the following line:

```
GRUB_TERMINAL_OUTPUT=console

```

Another option if you want to keep the framebuffer in GRUB is to revert to text mode just before starting the kernel. To do that modify the variable in `/etc/default/grub`:

```
GRUB_GFXPAYLOAD_LINUX=text

```

## Booting ISO9660 image file directly via GRUB

GRUB supports booting from ISO images directly via loopback devices, see [Multiboot USB drive#Using GRUB and loopback devices](/index.php/Multiboot_USB_drive#Using_GRUB_and_loopback_devices "Multiboot USB drive") for examples.

## Persistent block device naming

One naming scheme for [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming") is the use of globally unique UUIDs to detect partitions instead of the "old" `/dev/sd*`. Advantages are covered up in the above linked article.

Persistent naming via file system UUIDs are used by default in GRUB.

**Note:** The `/boot/grub.cfg` file needs regeneration with the new UUID in `/etc/default/grub` every time a relevant file system is resized or recreated. Remember this when modifying partitions & file systems with a Live-CD.

Whether to use UUIDs is controlled by an option in `/etc/default/grub`:

```
GRUB_DISABLE_LINUX_UUID=true

```

## Using labels

It is possible to use labels, human-readable strings attached to file systems, by using the `--label` option to `search`. First of all, label your existing partition:

```
# tune2fs -L *LABEL* *PARTITION*

```

Then, add an entry using labels. An example of this:

```
menuentry "Arch Linux, session texte" {
  search --label --set=root archroot
  linux /boot/vmlinuz-linux root=/dev/disk/by-label/archroot ro
  initrd /boot/initramfs-linux.img
}

```

## Password protection of GRUB menu

**Warning:** If someone has physical access to your machine and is able to boot a live USB/disk (*i.e.*, BIOS allows booting from an external disk), it's fairly trivial for one to modify GRUB configuration files to bypass this if `/boot` resides on an unencrypted partition. See [GRUB#Encryption](/index.php/GRUB#Encryption "GRUB") and [Security#Disk encryption](/index.php/Security#Disk_encryption "Security").

If you want to secure GRUB so it is not possible for anyone to change boot parameters or use the command line, you can add a user/password combination to GRUB's configuration files. To do this, run the command `grub-mkpasswd-pbkdf2`. Enter a password and confirm it:

 `grub-mkpasswd-pbkdf2` 
```
[...]
Your PBKDF2 is grub.pbkdf2.sha512.10000.C8ABD3E93C4DFC83138B0C7A3D719BC650E6234310DA069E6FDB0DD4156313DA3D0D9BFFC2846C21D5A2DDA515114CF6378F8A064C94198D0618E70D23717E82.509BFA8A4217EAD0B33C87432524C0B6B64B34FBAD22D3E6E6874D9B101996C5F98AB1746FE7C7199147ECF4ABD8661C222EEEDB7D14A843261FFF2C07B1269A

```

Then, add the following to `/etc/grub.d/40_custom`:

 `/etc/grub.d/40_custom` 
```
set superusers="**username**"
password_pbkdf2 **username** **<password>**
```

where `<password>` is the string generated by `grub-mkpasswd_pbkdf2`.

Regenerate your configuration file. Your GRUB command line, boot parameters and all boot entries are now protected.

This can be relaxed and further customized with more users as described in the "Security" part of [the GRUB manual](https://www.gnu.org/software/grub/manual/grub.html#Security).

### Password protection of GRUB edit and console options only

Adding `--unrestricted` to a menu entry will allow any user to boot the OS while preventing the user from editing the entry and preventing access to the grub command console. Only a superuser or users specified with the `--user` switch will be able to edit the menu entry.

 `/boot/grub/grub.cfg`  `menuentry 'Arch Linux' --unrestricted --class arch --class gnu-linux --class os ...` 

## Hide GRUB unless the Shift key is held down

In order to achieve the fastest possible boot, instead of having GRUB wait for a timeout, it is possible for GRUB to hide the menu, unless the `Shift` key is held down during GRUB's start-up.

In order to achieve this, you should add the following line to `/etc/default/grub`:

```
 GRUB_FORCE_HIDDEN_MENU="true"

```

Then create the file in [[1]](https://gist.githubusercontent.com/anonymous/8eb2019db2e278ba99be/raw/257f15100fd46aeeb8e33a7629b209d0a14b9975/gistfile1.sh), make it exectuable, and regenerate the grub configuration:

```
# chmod a+x /etc/grub.d/31_hold_shift
# grub-mkconfig -o /boot/grub/grub.cfg

```

**Note:** This setup uses keystatus to detect keypress event so it may not work on some machines.

## Combining the use of UUIDs and basic scripting

If you like the idea of using UUIDs to avoid unreliable BIOS mappings or are struggling with GRUB's syntax, here is an example boot menu item that uses UUIDs and a small script to direct GRUB to the proper disk partitions for your system. All you need to do is replace the UUIDs in the sample with the correct UUIDs for your system. The example applies to a system with a boot and root partition. You will obviously need to modify the GRUB configuration if you have additional partitions:

```
menuentry "Arch Linux 64" {
    # Set the UUIDs for your boot and root partition respectively
    set the_boot_uuid=ece0448f-bb08-486d-9864-ac3271bd8d07
    set the_root_uuid=c55da16f-e2af-4603-9e0b-03f5f565ec4a

    # (Note: This may be the same as your boot partition)

    # Get the boot/root devices and set them in the root and grub_boot variables
    search --fs-uuid $the_root_uuid --set=root
    search --fs-uuid $the_boot_uuid --set=grub_boot

    # Check to see if boot and root are equal.
    # If they are, then append /boot to $grub_boot (Since $grub_boot is actually the root partition)
    if [ $the_boot_uuid == $the_root_uuid ] ; then
        set grub_boot=($grub_boot)/boot
    else
        set grub_boot=($grub_boot)
    fi

    # $grub_boot now points to the correct location, so the following will properly find the kernel and initrd
    linux $grub_boot/vmlinuz-linux root=/dev/disk/by-uuid/$the_root_uuid ro
    initrd $grub_boot/initramfs-linux.img
}

```

## Manually creating grub.cfg

A basic GRUB config file uses the following options:

*   `(hd*X*,*Y*)` is the partition *Y* on disk *X*, partition numbers starting at 1, disk numbers starting at 0
*   `set default=*N*` is the default boot entry that is chosen after timeout for user action
*   `set timeout=*M*` is the time *M* to wait in seconds for a user selection before default is booted
*   `menuentry "title" {entry options}` is a boot entry titled `title`
*   `set root=(hd*X*,*Y*)` sets the boot partition, where the kernel and GRUB modules are stored (boot need not be a separate partition, and may simply be a directory under the "root" partition (`/`)

## Multiple entries

### Disable submenu

If you have multiple kernels installed, say linux and linux-lts, by default `grub-mkconfig` groups them in a submenu. If you do not like this behaviour you can go back to one single menu by adding the following line to `/etc/default/grub`:

```
 GRUB_DISABLE_SUBMENU=y

```

### Recall previous entry

GRUB can remember the last entry you booted from and use this as the default entry to boot from next time. This is useful if you have multiple kernels (i.e., the current Arch one and the LTS kernel as a fallback option) or operating systems. To do this, edit `/etc/default/grub` and change the value of `GRUB_DEFAULT`:

```
GRUB_DEFAULT=saved

```

This ensures that GRUB will default to the saved entry. To enable saving the selected entry, add the following line to `/etc/default/grub`:

```
GRUB_SAVEDEFAULT=true

```

**Note:** Manually added menu items, e.g. Windows in `/etc/grub.d/40_custom` or `/boot/grub/custom.cfg`, will need `savedefault` added.

### Changing the default menu entry

To change the default selected entry, edit `/etc/default/grub` and change the value of `GRUB_DEFAULT`:

Using numbers :

```
GRUB_DEFAULT=0

```

Grub identifies entries in generated menu counted from zero. That means 0 for the first entry which is the default value, 1 for the second and so on.

Or using menu titles :

```
GRUB_DEFAULT='Advanced options for Arch Linux>Arch Linux, with Linux linux'

```

### Boot non-default entry only once

The command `grub-reboot` is very helpful to boot another entry than the default only once. GRUB loads the entry passed in the first command line argument, when the system is rebooted the next time. Most importantly GRUB returns to loading the default entry for all future booting. Changing the configuration file or selecting an entry in the GRUB menu is not necessary.

**Note:** This requires `GRUB_DEFAULT=saved` in `/etc/default/grub` (and then regenerating `grub.cfg`) or, in case of hand-made `grub.cfg`, the line `set default="${saved_entry}"`.

## Play a tune

You can play a tune through the PC-speaker while booting by modifying the variable `GRUB_INIT_TUNE`. For example, to play Berlioz's extract from Sabbath Night of Symphonie Fantastique you can add the following: (bassoon part):

`GRUB_INIT_TUNE="312 262 3 247 3 262 3 220 3 247 3 196 3 220 3 220 3 262 3 262 3 294 3 262 3 247 3 220 3 196 3 247 3 262 3 247 5 220 1 220 5"`

For information on this, you can look at `info grub -n play`.

## Manual configuration of core image for early boot

If you require a special keymap or other complex steps that GRUB is not able to configure automatically in order to make `/boot` available to the GRUB environment, you can generate a core image yourself. On UEFI systems, the core image is the `grubx64.efi` file that is loaded by the firmware on boot. Building your own core image will allow you to embed any modules required for very early boot, as well as a configuration script to bootstrap GRUB.

Firstly, taking as an example a requirement for the `dvorak` keymap embedded in early-boot in order to enter a password for a crypted `/boot` on a UEFI system:

Determine from the generated `/boot/grub/grub.cfg` file what modules are required in order to mount the crypted `/boot`. For instance, under your `menuentry` you should see lines similar to:

```
insmod diskfilter cryptodisk luks gcry_rijndael gcry_rijndael gcry_sha256
insmod ext2
cryptomount -u 1234abcdef1234abcdef1234abcdef
set root='cryptouuid/1234abcdef1234abcdef1234abcdef'
```

Take note of all of those modules: they'll need to be included in the core image. Now, create a tarball containing your keymap. This will be bundled in the core image as a memdisk:

```
# ckbcomp dvorak | grub-mklayout > dvorak.gkb
# tar cf memdisk.tar dvorak.gkb

```

Now create a configuration file to be used in the GRUB core image. This is in the same format as your regular grub config, but need contain only a few lines to find and load the main config file on the `/boot` partition:

 `early-grub.cfg` 
```
root=(memdisk)
prefix=($root)/

terminal_input at_keyboard
keymap /dvorak.gkb

cryptomount -u 1234abcdef1234abcdef1234abcdef
set root='cryptouuid/1234abcdef1234abcdef1234abcdef'
set prefix=($root)/grub

configfile grub.cfg
```

Finally, generate the core image, listing all of the modules determined to be required in the generated `grub.cfg`, along with any modules used in the `early-grub.cfg` script. The example above needs `memdisk`, `tar`, `at_keyboard`, `keylayouts` and `configfile`.

```
# grub-mkimage -c early-grub.cfg -o grubx64.efi -O x86_64-efi -m memdisk.tar diskfilter cryptodisk luks gcry_rijndael gcry_sha256 ext2 memdisk tar at_keyboard keylayouts configfile

```

The generated EFI core image can now be used in the same way as the image that is generated automatically by `grub-install`: place it in your EFI partition and enable it with `efibootmgr`, or configure as appropriate for your system firmware.