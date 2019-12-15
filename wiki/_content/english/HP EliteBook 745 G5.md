| **Device** | **Status** | **Modules** |
| AMD graphics | **Working** |
| VGA | **Working** |
| HDMI | **Working** |
| Ethernet | **Working** |
| Wireless | **Working** |
| Bluetooth | **Working** |
| Audio | **Working** |
| Touchpad | **Working** |
| Pointing Stick | **Working** |
| Camera | **Working** |
| Fingerprint reader | **Not working** |
| Smart Card Reader | **Working** |
| Function Keys | **Working (exception)** |
| 3G modem | **Not working** |
| Dock | **Working** |

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Configuration](#Configuration)
    *   [1.1 UEFI Setup](#UEFI_Setup)
    *   [1.2 Kernel options](#Kernel_options)
    *   [1.3 AMD Graphics](#AMD_Graphics)
    *   [1.4 SmartCard Reader](#SmartCard_Reader)
    *   [1.5 Function Keys](#Function_Keys)

## Configuration

### UEFI Setup

The last firmware is mandatory to modify the BIOS parameters. At the moment of writing this entry: 01.09.01 Rev.A. In upgraded BIOS, disable the secure boot to be able to load any [boot loader](/index.php/Boot_loader "Boot loader").

From Windows, it's easy to force the UEFI priority: [http://www.rodsbooks.com/refind/installing.html#windows](http://www.rodsbooks.com/refind/installing.html#windows)

Be careful with rEFInd: [https://www.reddit.com/r/archlinux/comments/cgkhop/help_refind_boot_manager_hangs_seconds_after/](https://www.reddit.com/r/archlinux/comments/cgkhop/help_refind_boot_manager_hangs_seconds_after/) In this specific case, avoid option scanfor internal.

### Kernel options

System freezes randomly when the proper parameters are not loaded [https://www.reddit.com/r/linuxhardware/comments/afktfv/linux_freezes_and_amd_2500u_chipset/](https://www.reddit.com/r/linuxhardware/comments/afktfv/linux_freezes_and_amd_2500u_chipset/)

Recommended [kernel options](/index.php/Kernel_parameters "Kernel parameters"):

```
acpi_backlight=vendor idle=nomwait amdgpu.gpu_recovery=1 amd_iommu=pt audit_enabled=0

```

### AMD Graphics

Use [AMDGPU](/index.php/AMDGPU "AMDGPU"). To avoid any problem, make sure `amdgpu` has been set as the first module in the [Mkinitcpio#MODULES](/index.php/Mkinitcpio#MODULES "Mkinitcpio") array, e.g. `MODULES=(amdgpu radeon)`. Take care as the original EFI partition could have not enough space for amdgpu and radeon modules.

### SmartCard Reader

Works perfectly with [ccid](https://www.archlinux.org/packages/?name=ccid) & [opensc](https://www.archlinux.org/packages/?name=opensc) . Read [Smartcards](/index.php/Smartcards "Smartcards") for more info.

### Function Keys

Usual function keys work out of the box. Keyboard Backlight controls work out of the system, so it is perfectly working in Linux. However, rare keys as telephone or calendar are not assigned to anything. You can remap using [udev](/index.php/Map_scancodes_to_keycodes#Example_for_custom_hwdb "Map scancodes to keycodes"). For example, the call key can be remapped as an insert key by creating /etc/udev/hwdb.d/90-custom-keyboard.hwdb that contains this:

```
evdev:atkbd:dmi:bvn*:bvr*:bd*:svn*:pn*:pvr*
 KEYBOARD_KEY_66=insert

```