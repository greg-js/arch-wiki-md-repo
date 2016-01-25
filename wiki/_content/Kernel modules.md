# Kernel modules

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Boot debugging](/index.php/Boot_debugging "Boot debugging")
*   [Kernels](/index.php/Kernels "Kernels")
*   [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters")
*   [Compile kernel module](/index.php/Compile_kernel_module "Compile kernel module")

[Kernel modules](https://en.wikipedia.org/wiki/Loadable_kernel_module "wikipedia:Loadable kernel module") are pieces of code that can be loaded and unloaded into the kernel upon demand. They extend the functionality of the kernel without the need to reboot the system.

To create a kernel module, you can read [The Linux Kernel Module Programming Guide](http://tldp.org/LDP/lkmpg/2.6/html/index.html). A module can be configured as built-in or loadable. To dynamically load or remove a module, it has to be configured as a loadable module in the kernel configuration (the line related to the module will therefore display the letter `M`).

## Contents

*   [1 Obtaining information](#Obtaining_information)
*   [2 Automatic module handling](#Automatic_module_handling)
*   [3 Manual module handling](#Manual_module_handling)
*   [4 Setting module options](#Setting_module_options)
    *   [4.1 Manually at load time using modprobe](#Manually_at_load_time_using_modprobe)
    *   [4.2 Using files in /etc/modprobe.d/](#Using_files_in_.2Fetc.2Fmodprobe.d.2F)
    *   [4.3 Using kernel command line](#Using_kernel_command_line)
*   [5 Aliasing](#Aliasing)
*   [6 Blacklisting](#Blacklisting)
    *   [6.1 Using files in /etc/modprobe.d/](#Using_files_in_.2Fetc.2Fmodprobe.d.2F_2)
    *   [6.2 Using kernel command line](#Using_kernel_command_line_2)
*   [7 Troubleshooting](#Troubleshooting)
    *   [7.1 Modules do not load](#Modules_do_not_load)
*   [8 See also](#See_also)

## Obtaining information

Modules are stored in `/usr/lib/modules/_kernel_release_`. You can use the command `uname -r` to get your current kernel release version.

**Note:** Module names often use underscores (`_`) or dashes (`-`); however, those symbols are interchangeable, both when using the `modprobe` command and in configuration files in `/etc/modprobe.d/`.

To show what kernel modules are currently loaded:

```
$ lsmod

```

To show information about a module:

```
$ modinfo _module_name_

```

To list the options that are set for a loaded module:

```
$ systool -v -m _module_name_

```

To display the comprehensive configuration of all the modules:

```
$ modprobe -c | less

```

To display the configuration of a particular module:

```
$ modprobe -c | grep _module_name_

```

List the dependencies of a module (or alias), including the module itself:

```
$ modprobe --show-depends _module_name_

```

## Automatic module handling

Today, all necessary modules loading is handled automatically by [udev](/index.php/Udev "Udev"), so if you do not need to use any out-of-tree kernel modules, there is no need to put modules that should be loaded at boot in any configuration file. However, there are cases where you might want to load an extra module during the boot process, or blacklist another one for your computer to function properly.

Kernel modules can be explicitly loaded during boot and are configured as a static list in files under `/etc/modules-load.d/`. Each configuration file is named in the style of `/etc/modules-load.d/<program>.conf`. Configuration files simply contain a list of kernel modules names to load, separated by newlines. Empty lines and lines whose first non-whitespace character is `#` or `;` are ignored.

 `/etc/modules-load.d/virtio-net.conf` 

```
# Load virtio-net.ko at boot
virtio-net
```

See `man modules-load.d` for more details.

## Manual module handling

Kernel modules are handled by tools provided by [kmod](https://www.archlinux.org/packages/?name=kmod) package. You can use these tools manually.

**Note:** If you have upgraded your kernel but have not yet rebooted, _modprobe_ will fail with no error message and exit with code 1, because the path `/lib/modules/$(uname -r)/` no longer exists. Check manually if this path exists when _modprobe_ failed to determine if this is the case.

To load a module:

```
# modprobe _module_name_

```

To load a module by filename (i.e. one that is not installed in `/lib/modules/$(uname -r)/`):

```
# insmod filename [args]

```

To unload a module:

```
# modprobe -r _module_name_

```

Or, alternatively:

```
# rmmod _module_name_

```

## Setting module options

To pass a parameter to a kernel module, you can pass them manually with modprobe or assure certain parameters are always applied using a modprobe configuration file or by using the kernel command line.

### Manually at load time using modprobe

The basic way to pass parameters to a module is using the modprobe command. Parameters are specified on command line using simple `_key=value_` assignments:

```
# modprobe _module_name parameter_name=parameter_value_

```

### Using files in /etc/modprobe.d/

Files in `/etc/modprobe.d/` directory can be used to pass module settings to [udev](/index.php/Udev "Udev"), which will use `modprobe` to manage the loading of the modules during system boot. Configuration files in this directory can have any name, given that they end with the `.conf` extension. The syntax is:

 `/etc/modprobe.d/myfilename.conf`  `options _module_name parameter_name=parameter_value_` 

For example:

 `/etc/modprobe.d/thinkfan.conf` 

```
# On ThinkPads, this lets the 'thinkfan' daemon control fan speed
options thinkpad_acpi fan_control=1
```

**Note:** If any of the affected modules is loaded from the initramfs, then you will need to add the appropriate `.conf` file to `FILES` in [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf") or use the `modconf` [hook](/index.php/Mkinitcpio.conf#HOOKS "Mkinitcpio.conf"), so that it will be included in the initramfs.

### Using kernel command line

If the module is built into the kernel, you can also pass options to the module using the kernel command line. For all common bootloaders, the following syntax is correct:

```
_module_name.parameter_name=parameter_value_

```

For example:

```
thinkpad_acpi.fan_control=1

```

Simply add this to your bootloader's kernel-line, as described in [Kernel Parameters](/index.php/Kernel_parameters "Kernel parameters").

## Aliasing

Aliases are alternate names for a module. For example: `alias my-mod really_long_modulename` means you can use `modprobe my-mod` instead of `modprobe really_long_modulename`. You can also use shell-style wildcards, so `alias my-mod* really_long_modulename` means that `modprobe my-mod-something` has the same effect. Create an alias:

 `/etc/modprobe.d/myalias.conf`  `alias mymod really_long_module_name` 

Some modules have aliases which are used to automatically load them when they are needed by an application. Disabling these aliases can prevent automatic loading but will still allow the modules to be manually loaded.

 `/etc/modprobe.d/modprobe.conf` 

```
# Prevent Bluetooth autoload
alias net-pf-31 off
```

## Blacklisting

Blacklisting, in the context of kernel modules, is a mechanism to prevent the kernel module from loading. This could be useful if, for example, the associated hardware is not needed, or if loading that module causes problems: for instance there may be two kernel modules that try to control the same piece of hardware, and loading them together would result in a conflict.

Some modules are loaded as part of the [initramfs](/index.php/Initramfs "Initramfs"). `mkinitcpio -M` will print out all automatically detected modules: to prevent the initramfs from loading some of those modules, blacklist them in `/etc/modprobe.d/modprobe.conf`. Running `mkinitcpio -v` will list all modules pulled in by the various hooks (e.g. `filesystems` hook, `block` hook, etc.). Remember to add that `.conf` file to the `FILES` section in `/etc/mkinitcpio.conf`, if you have not done so already, and rebuild the initramfs once you have blacklisted the modules, and reboot afterwards.

### Using files in /etc/modprobe.d/

Create a `.conf` file inside `/etc/modprobe.d/` and append a line for each module you want to blacklist, using the `blacklist` keyword. If for example you want to prevent the `pcspkr` module from loading:

 `/etc/modprobe.d/nobeep.conf` 

```
# Do not load the 'pcspkr' module on boot.
blacklist pcspkr
```

**Note:** The `blacklist` command will blacklist a module so that it will not be loaded automatically, but the module may be loaded if another non-blacklisted module depends on it or if it is loaded manually.

However, there is a workaround for this behaviour; the `install` command instructs modprobe to run a custom command instead of inserting the module in the kernel as normal, so you can force the module to always fail loading with:

 `/etc/modprobe.d/blacklist.conf` 

```
...
install _module_name_ /bin/false
...
```

This will effectively blacklist that module and any other that depends on it.

### Using kernel command line

**Tip:** This can be very useful if a broken module makes it impossible to boot your system.

You can also blacklist modules from the bootloader.

Simply add `modprobe.blacklist=modname1,modname2,modname3` to your bootloader's kernel line, as described in [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

**Note:** When you are blacklisting more than one module, note that they are separated by commas only. Spaces or anything else might presumably break the syntax.

## Troubleshooting

### Modules do not load

In case a specific module does not load and the boot log (accessible with `journalctl -b`) says that the module is blacklisted, but the directory `/etc/modprobe.d/` does not show a corresponding entry, check another modprobe source folder at `/usr/lib/modprobe.d/` for blacklisting entries.

A module will not be loaded if the "vermagic" string contained within the kernel module does not match the value of the currently running kernel. If it is known that the module is compatible with the current running kernel the "vermagic" check can be ignored with `modprobe --force-vermagic`.

**Warning:** Ignoring the version checks for a kernel module can cause a kernel to crash or a system to exhibit undefined behavior due to incompatibility. Use `--force-vermagic` only with the utmost caution.

## See also

*   [Disable PC speaker beep](/index.php/Disable_PC_speaker_beep "Disable PC speaker beep")

Retrieved from "[https://wiki.archlinux.org/index.php?title=Kernel_modules&oldid=417080](https://wiki.archlinux.org/index.php?title=Kernel_modules&oldid=417080)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Kernel](/index.php/Category:Kernel "Category:Kernel")
*   [Hardware detection and troubleshooting](/index.php/Category:Hardware_detection_and_troubleshooting "Category:Hardware detection and troubleshooting")
*   [Boot process](/index.php/Category:Boot_process "Category:Boot process")