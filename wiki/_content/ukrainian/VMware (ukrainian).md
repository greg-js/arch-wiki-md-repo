Ця стаття про встановлення VMware в Arch Linux, вам також може буде цікаво прочитати про [Встановлення Arch Linux на VMware](/index.php?title=Installing_Arch_Linux_in_VMware_(%D0%A3%D0%BA%D1%80%D0%B0%D1%97%D0%BD%D1%81%D1%8C%D0%BA%D0%B0)&action=edit&redlink=1 "Installing Arch Linux in VMware (Українська) (page does not exist)").

## Contents

*   [1 Встановлення VMware Server](#.D0.92.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.BD.D1.8F_VMware_Server)
    *   [1.1 VMware Server Console](#VMware_Server_Console)
    *   [1.2 Note](#Note)
*   [2 VMware Workstation or VMware Player](#VMware_Workstation_or_VMware_Player)
    *   [2.1 Installation](#Installation)
    *   [2.2 VMware modules and patches](#VMware_modules_and_patches)
    *   [2.3 Installation (concluded)](#Installation_.28concluded.29)
    *   [2.4 Uninstallation](#Uninstallation)
    *   [2.5 Extracting the VMware BIOS](#Extracting_the_VMware_BIOS)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Kernel upgrades and VMware modules](#Kernel_upgrades_and_VMware_modules)
    *   [3.2 error: implicit declaration of function ‘iommu_unmap_range’](#error:_implicit_declaration_of_function_.E2.80.98iommu_unmap_range.E2.80.99)
    *   [3.3 error: implicit declaration of function ‘kernel_locked’](#error:_implicit_declaration_of_function_.E2.80.98kernel_locked.E2.80.99)
    *   [3.4 error: ‘struct sock’ has no member named ‘sk_sleep’](#error:_.E2.80.98struct_sock.E2.80.99_has_no_member_named_.E2.80.98sk_sleep.E2.80.99)
    *   [3.5 Compiling modules on kernel 2.6.32](#Compiling_modules_on_kernel_2.6.32)
    *   [3.6 Printing from the guest OS](#Printing_from_the_guest_OS)
    *   [3.7 VMware 7.xx gui won't start](#VMware_7.xx_gui_won.27t_start)

## Встановлення VMware Server

Встановіть [vmware-server](https://aur.archlinux.org/packages/vmware-server/) з [AUR](/index.php/AUR "AUR").

### VMware Server Console

Install [vmware-server-console](https://aur.archlinux.org/packages/vmware-server-console/) from the [AUR](/index.php/AUR "AUR"). Alternatively, on Arch64, the [bin32](https://aur.archlinux.org/packages.php?ID=31169) version can also be installed.

### Note

On both cases, the vmware image is not included in the [AUR](/index.php/AUR "AUR") anymore. So you should:

*   download and extract the tarball from the AUR
*   download the image from [VMWare website](http://www.vmware.com/products/server/).
*   copy VMware-server-2.0.2-203138.i386.tar.gz to the build directory
*   finish building

## VMware Workstation or VMware Player

### Installation

**Note:** This will **not** install with pacman, so the files installed will **not** be traceable/removable with pacman.

To install Workstation or Player on a Linux host using a bundle:

**1.** Download `VMware-Workstation-<version>.<release>.<architecture>.bundle` or `VMware-Player-<version>-<release>.<architecture>.bundle` from the VMware site. (`Note:` you can also try the testing (Beta/RC) versions found in here: [http://communities.vmware.com/community/beta/ws](http://communities.vmware.com/community/beta/ws) but please note that they indeed are beta and so there's no guarantee you will not run into issues).

**2.** In a terminal cd to the directory where you downloaded the file.

**3.** Become root and create a fake System V init style directory for VMware and start the installation (the `--console` flag uses terminal instead of the GUI and the `--custom` asks all the unnecessary questions that nobody cares about - but we need it to select the `System service` runlevels directory):

```
# mkdir -p /etc/rc.d/vmware.d/{rc{0..6},init}.d
# chmod +x VMware-<edition>-<version>.<release>.<architecture>.bundle
# ./VMware-<edition>-<version>.<release>.<architecture>.bundle --console --custom

```

**4.** (Read &) accept the EULA to continue.

**5.** Accept the default settings until it prompts for `System service` runlevels then set to:

```
/etc/rc.d/vmware.d/

```

**6.** For `System service scripts` set to:

```
/etc/rc.d

```

It might happen that you need to set the directory for `System service scripts` as `/etc/rc.d/vmware.d/init.d` (the default) or else the installation would fail. If you do, you can create a symlink from `/etc/rc.d/vmware.d/init.d/vmware` to `/etc/rc.d/vmware` afterwards or the other way around (note that you can't remove the `VMware System service script` after you've placed it somewhere because that's where VMware will be looking for it).

**7.** (Optional) Enter the directory path to the Integrated Virtual Debugger for Eclipse if Eclipse is installed.

**8.** Mash enter to install. Note that if nothing happens at this point and you are returned to the prompt, try re-running the installation without the `--console` option.

**9.** At this point you would want to install the modules. First you need to either change the `lsmod binary path` in `/etc/rc.d/vmware` at the lines 88 and 108 from:

```
/sbin/lsmod

```

to:

```
/bin/lsmod

```

or create a symlink from `/bin/lsmod` to `/sbin/lsmod` with:

```
# ln -s /bin/lsmod /sbin/lsmod

```

### VMware modules and patches

*   For 2.6.39 kernel and VMware player 3.1.4, there is a required

**Note:** like the scripts below, you must extract all of the VMware sources out first and then run this patch. The patch is setup for the source to be in the same local directory of the patch. If you want to run the patch directly against the source in the directory where it already resides, change every instance of "source-original" in the patch file to "/usr/lib/vmware/modules/source" after extracting all five of the tar files in that directory. Patch and then tar them again.

```
$ wget [http://weltall.heliohost.org/wordpress/wp-content/uploads/2011/05/vmware2.6.39fixed.patch](http://weltall.heliohost.org/wordpress/wp-content/uploads/2011/05/vmware2.6.39fixed.patch)

```

*   For 2.6.38 kernel and VMware player 3.1.4, there is no patch required

*   For 2.6.37 kernel and VMware 7.x.x (tested with 7.1.3), there's a script to patch the VMware sources (run as root):

**Note:** This script also works for 2.6.38 kernels and VMware 7.1.4

```
$ cd /tmp
$ wget [http://www.russo79.com/vmware7.1.3-patch-kernel-2.6.37.sh](http://www.russo79.com/vmware7.1.3-patch-kernel-2.6.37.sh)
# chmod +x vmware7.1.3-patch-kernel-2.6.37.sh
# ./vmware7.1.3-patch-kernel-2.6.37.sh

```

This script was based on the patch taken from [http://communities.vmware.com/thread/293321](http://communities.vmware.com/thread/293321)

*   For 2.6.37 kernel and VMware player 3.1.4, there is no patch required

*   For 2.6.36 kernel and VMware 7.x.x, there's a script to patch the vmmon (run as root):

```
$ cd /tmp
$ wget [http://files.archlinux.org.il/vmmon_fix_2.6.36.sh](http://files.archlinux.org.il/vmmon_fix_2.6.36.sh)
# chmod +x vmmon_fix_2.6.36.sh
# ./vmmon_fix_2.6.36.sh

```

*   For 2.6.35 kernel and VMware 7.x.x, there's a script to patch the VMware sources :

```
$ cd /tmp
$ wget [http://www.sputnick-area.net/scripts/vmware7.1.1-patch-kernel-2.6.35.bash](http://www.sputnick-area.net/scripts/vmware7.1.1-patch-kernel-2.6.35.bash)
# chmod +x vmware7.1.1-patch-kernel-2.6.35.bash
# ./vmware7.1.1-patch-kernel-2.6.35.bash

```

### Installation (concluded)

Now you can install the modules. You can do this with either by launching VMware and letting it install the modules from there with the GUI or alternatively you can execute the command:

```
# vmware-modconfig --console --install-all

```

**10.** (Optional) Add vmware to the DAEMONS array in /etc/rc.conf so that the service is started automatically on boot.

**11.** Install and run [HAL](/index.php/HAL "HAL")

```
#/etc/rc.d/hal start

```

**12.** Now, open your VMware Workstation (`vmware` in the console) to configure & use!

### Uninstallation

Check the product name

```
# vmware-installer -l

```

uninstall product

```
# vmware-installer -u <vmware-product>

```

Manually included parts in /etc/rc.d have to be deleted manually. Don't forget to remove vmware from the /etc/rc.conf DAEMONS array.

### Extracting the VMware BIOS

To extract the VMware BIOS, which can be manipulated and later used with your virtual machines:

```
$ objcopy /usr/lib/vmware/bin/vmware-vmx -O binary -j bios440 --set-section-flags bios440=a bios440.rom.Z
$ perl -e 'use Compress::Zlib; my $v; read STDIN, $v, '$(stat -c%s "./bios440.rom.Z")'; $v = uncompress($v); print $v;' < bios440.rom.Z > bios440.rom

```

Once you've modified the BIOS in whatever way required, move it to the directory where your VM is stored, and add it to the `.vmx` file:

```
bios440.filename = "bios440.rom"

```

## Troubleshooting

### Kernel upgrades and VMware modules

If when you ran

```
./VMware-<edition>-<version>.<release>.<architecture>.bundle

```

you get back to the prompt and VMware don't ask you to makes choices, then you probably have an old install, so you should rename /etc/vmware-installer/ :

```
# mv /etc/vmware-installer /etc/vmware-installer.old

```

If you get an error like this when launching up a Virtual Machine:

```
Could not open /dev/vmmon: No such file or directory.
Please make sure that the kernel module `vmmon' is loaded.

```

It means that at least the one VMware service isn't started up. You can start them all up by running (as root):

```
# /etc/rc.d/vmware start

```

If, on the other hand VMware complains about kernel headers like this:

```
Kernel headers for version 2.6.xx-xxxx were not found. If you installed them.......

```

Install them with the following:

```
# pacman -S kernel26-headers

```

### error: implicit declaration of function ‘iommu_unmap_range’

If the following error happens while compiling modules

```
...
/tmp/vmware-root/modules/vmmon-only/linux/iommu.c:403:7: erreur: implicit declaration of function ‘iommu_unmap_range’
make[2]: *** [/tmp/vmware-root/modules/vmmon-only/linux/iommu.o] Erreur 1
make[1]: *** [_module_/tmp/vmware-root/modules/vmmon-only] Erreur 2
make[1]: quittant le répertoire « /usr/src/linux-2.6.35-ARCH »
make: *** [vmmon.ko] Erreur 2

```

This error is due to a change in the kernel API, the change is merely just a change of name which removes the suffixed '_range' from the iommu functions. You can manually patch the sources by removing the _range suffix with a quick sed expression:

```
cd /tmp
tar xvf /usr/lib/vmware/modules/source/vmmon.tar
sed 's/_range//' -i vmmon-only/linux/iommu.c
tar cvf /usr/lib/vmware/modules/source/vmmon.tar vmmon-only

```

Please note that when upgrading the kernel you will have to rebuild the vmware modules with:

```
$ vmware-modconfig --console --install-all

```

Otherwise your whole system might crash when trying to power up VMs so keep that in mind.

### error: implicit declaration of function ‘kernel_locked’

If you're getting this error it means you're most likely on a 2.6.36 > kernel and require some additional attention. Attention that VMware rarely pays.

There's a patch available for this and several more compile errors over at [[1]](http://communities.vmware.com/thread/293321)

### error: ‘struct sock’ has no member named ‘sk_sleep’

This error often occures when compiling the vsock module, the error looks something like:

```
make[1]: Entering directory `/usr/src/linux-headers-2.6.35-7-generic-pae'
  CC [M]  /tmp/vmware-root/modules/vsock-only/linux/af_vsock.o
/tmp/vmware-root/modules/vsock-only/linux/af_vsock.c:312: warning: initialization from incompatible pointer type
/tmp/vmware-root/modules/vsock-only/linux/af_vsock.c:359: warning: initialization from incompatible pointer type
/tmp/vmware-root/modules/vsock-only/linux/af_vsock.c: In function ‘VSockVmciStreamConnect’:
/tmp/vmware-root/modules/vsock-only/linux/af_vsock.c:3224: error: ‘struct sock’ has no member named ‘sk_sleep’
/tmp/vmware-root/modules/vsock-only/linux/af_vsock.c:3247: error: ‘struct sock’ has no member named ‘sk_sleep’

```

...

To fix this we do a similar approach as the one mentioned above:

```
cd /tmp
tar xvf /usr/lib/vmware/modules/source/vsock.tar
sed 's/\([a-z_]*\)->compat_sk_sleep/compat_sk_sleep(\1)/g' -i vsock-only/linux/af_vsock.c
tar cvf /usr/lib/vmware/modules/source/vsock.tar vsock-only

```

Then rerun:

```
$ vmware-modconfig --console --install-all

```

And you should be fine.

### Compiling modules on kernel 2.6.32

**Note:** not needed with vmware 7.x.x

To patch VMware modules we have to add **#include "compat_sched.h"** to some modules's source:

```
cd /tmp
tar xf /usr/lib/vmware/modules/source/vmnet.tar
nano vmnet-only/vnetUserListener.c (near line 37 add **#include "compat_sched.h"**)
tar cf /usr/lib/vmware/modules/source/vmnet.tar vmnet-only
tar xf /usr/lib/vmware/modules/source/vmci.tar
nano vmci-only/linux/vmciKernelIf.c vmci-only/include/pgtbl.h (add **#include "compat_sched.h"** around 30 line)
tar cf /usr/lib/vmware/modules/source/vmci.tar vmci-only
vmware-modconfig --console --install-all

```

You can also use a ready script: [http://communities.vmware.com/thread/239221](http://communities.vmware.com/thread/239221)

### Printing from the guest OS

If you've configured your guest OS to use the printers on your host, and the print jobs aren't going through, there may be a permissions problem with the ThinPrint CUPS filter (**thnucups**), which is used by VMware.

From `/var/log/cups/error_log`:

```
E [22/Nov/2010:14:10:11 -0800] Unable to execute /usr/lib/cups/filter/thnucups: insecure file permissions (0104755)

```

This should fix that:

```
$ sudo chmod u-sw /usr/lib/cups/filter/thnucups
$ sudo /etc/rc.d/cupsd restart

```

### VMware 7.xx gui won't start

When executing vmware from a terminal, you see the following output but the GUI won't start,

```
$ vmware
Logging to /tmp/vmware-jcosta/setup-5527.log
filename:       /lib/modules/2.6.38-ck/misc/vmmon.ko
supported:      external
license:        GPL v2
description:    VMware Virtual Machine Monitor.
author:         VMware, Inc.
depends:
vermagic:       2.6.38-ck SMP preempt mod_unload
filename:       /lib/modules/2.6.38-ck/misc/vmnet.ko
supported:      external
license:        GPL v2
description:    VMware Virtual Networking Driver.
author:         VMware, Inc.
depends:
vermagic:       2.6.38-ck SMP preempt mod_unload
filename:       /lib/modules/2.6.38-ck/misc/vmblock.ko
supported:      external
version:        1.1.2.0
license:        GPL v2
description:    VMware Blocking File System
author:         VMware, Inc.
srcversion:     400149ED038D22A87322D56
depends:
vermagic:       2.6.38-ck SMP preempt mod_unload
parm:           root:The directory the file system redirects to. (charp)
filename:       /lib/modules/2.6.38-ck/misc/vmci.ko
supported:      external
license:        GPL v2
description:    VMware Virtual Machine Communication Interface (VMCI).
author:         VMware, Inc.
depends:
vermagic:       2.6.38-ck SMP preempt mod_unload
filename:       /lib/modules/2.6.38-ck/misc/vsock.ko
supported:      external
license:        GPL v2
version:        1.0.0.0
description:    VMware Virtual Socket Family
author:         VMware, Inc.
srcversion:     CF8ABF14AFA7E44C2CC4C9C
depends:        vmci
vermagic:       2.6.38-ck SMP preempt mod_unload
filename:       /lib/modules/2.6.38-ck/misc/vmmon.ko
supported:      external
license:        GPL v2
description:    VMware Virtual Machine Monitor.
author:         VMware, Inc.
depends:
vermagic:       2.6.38-ck SMP preempt mod_unload

```

This seems to be a problem with glibmm-2.28, downgrade glibmm to 2.24.2.1, and it should work.