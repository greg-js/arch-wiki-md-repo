[hwdetect](https://projects.archlinux.org/svntogit/packages.git/tree/hwdetect/trunk/hwdetect) is a hardware detection script primarily used to load or list modules for use in [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf"). As such, it informs its user about which kernel modules are required to drive the hardware. This is in contrast to many other tools, that only query the hardware, and show raw information, leaving the user with the task to associate that information with the required drivers. The script makes use of information exported by the [sysfs](https://en.wikipedia.org/wiki/Sysfs "wikipedia:Sysfs") subsystem employed by the Linux kernel.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Examples](#Examples)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Unused modules](#Unused_modules)
    *   [3.2 Higher level modules](#Higher_level_modules)
*   [4 See also](#See_also)

## Installation

Install the [hwdetect](https://www.archlinux.org/packages/?name=hwdetect) package.

## Usage

See the [hwdetect source](https://projects.archlinux.org/svntogit/packages.git/tree/hwdetect/trunk/hwdetect), or run `hwdetect --help`.

### Examples

You can use the following method to populate `MODULES` in [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf").

```
# hwdetect --show-modules

```

The command should have similar output to the following (system-dependant):

```
SOUND    : pcspkr
OTHER    : 8139cp 8139too ac

```

Depending on what is used, copy the module names to replace the `MODULES` section in `/etc/mkinitcpio.conf`. The system should now boot faster, as some, or all, of the hardware detection and modules dependencies calculations is already stated.

**Note:**

*   The tool has dedicated output for usage within `/etc/mkinitcpio.conf`.
*   If any of the module names change because newer kernels have newer modules, or you install new hardware on your computer, you will need to generate the list of modules again and update `MODULES`.

## Tips and tricks

### Unused modules

To generated a list of modules currently not used, use the following script:

```
#!/bin/bash
for m in $(hwdetect --show-modules | cut -d ':' -f 2 | tr '
' ' '); do
    if ! grep -sq $(echo $m|tr - _) <(lsmod); then
        echo $m;
    fi
done

```

### Higher level modules

The converse script is also of interest as it lists modules which are higher level in the sense that they are less related to specific pieces of hardware:

```
#!/bin/bash
lowLevelModules=$(hwdetect --show-modules | cut -d ':' -f 2 | tr '
' ' ' | tr - _)
for m in $(lsmod | grep -v '^Module' - | cut -d ' ' -f 1 | tr '
' ' '); do
    if ! echo $lowLevelModules | grep -q $m -; then
        echo $m;
    fi
done

```

## See also

*   [lspci, and other hardware detection related tools](https://en.wikipedia.org/wiki/Lspci)