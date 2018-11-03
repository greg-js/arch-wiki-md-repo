[Intel VTune Amplifier](https://software.intel.com/intel-vtune-amplifier-xe/) is a commercial software performance profiler for Intel processors. There is a free 30 day trial.

## Contents

*   [1 Linux 4.0](#Linux_4.0)
    *   [1.1 Compiling the Kernel Modules](#Compiling_the_Kernel_Modules)
*   [2 VTune Amplifier XE 2013](#VTune_Amplifier_XE_2013)
    *   [2.1 Missing asm/system.h](#Missing_asm.2Fsystem.h)
    *   [2.2 Implicit declaration of this_cpu_read](#Implicit_declaration_of_this_cpu_read)
    *   [2.3 kmap_atomic and kunmap_atomic deprecated](#kmap_atomic_and_kunmap_atomic_deprecated)
*   [3 VTune Amplifier XE 2011](#VTune_Amplifier_XE_2011)
    *   [3.1 Installing VTune](#Installing_VTune)

## Linux 4.0

VTune 2015 currently does not work with Linux 4.0, due to changes in the kernel that prevent the sepdk module from building. You need VTune 2016 which was released in August 2015\.

### Compiling the Kernel Modules

To build the kernel modules on Arch you should follow the 4th part of the README on sepdk folder. You can follow the [Compile kernel module](/index.php/Compile_kernel_module "Compile kernel module") with [Kernels/Traditional compilation#Download the kernel source](/index.php/Kernels/Traditional_compilation#Download_the_kernel_source "Kernels/Traditional compilation"), downloading the source code to `/usr/src/`, extracting it with the name following the README and following the steps to unpack the kernel source.

There is a problem on the script `./build-driver` that some users could not run the funcion `get_absolute_path()` so you should hardcode the variables `DRIVER_DIRECTORY` and `KERNEL_SRC_DIR`.

Also, there is a bug when trying to compile the kernel modules with kernel 4.10\. [Intel forum post](https://software.intel.com/en-us/forums/intel-vtune-amplifier-xe/topic/722656)

## VTune Amplifier XE 2013

Follow the instructions for 2011\. If you see errors while building the driver, it may be because intel is using deprecated functionality subsections. In the following sections, lines beginning with "-" indicates code that should be removed, lines beginning with "+" should be added.

**Note:** The following steps should not be need as of update5.

### Missing asm/system.h

Edit lwpmudrv.c as follows:

```
-#include <asm/system.h>
+#include <linux/version.h>

```

### Implicit declaration of this_cpu_read

Edit eventmux.c as follows:

```
+#include <linux/percpu.h>

```

### kmap_atomic and kunmap_atomic deprecated

Edit vtssp/user_vm.c as follows:

```
-this->m_maddr = kmap_atomic(this->m_page, in_nmi() ? KM_NMI : KM_IRQ0);
+this->m_maddr = kmap_atomic(this->m_page);
-kunmap_atomic(this->m_maddr, in_nmi() ? KM_NMI : KM_IRQ0);
+kunmap_atomic(this->m_maddr);

```

## VTune Amplifier XE 2011

Starting with update 7 of the VTune Amplifier XE 2011, you can now use it on Linux 3.x and hence on Arch Linux, even though the latter is not officially supported. See also: [VTune on Archlinux](http://software.intel.com/en-us/forums/showthread.php?t=102037&p=1#171754)

### Installing VTune

Using the following HOWTO you "install" VTune locally and can run it. Vtune requires a kernel module for all functionality. Nevertheless, VTune in user mode is very powerful and comes with lots of possibilities for profiling. Have fun!

Preparation:

*   download VTune Amplifier XE 2011 (there is a [free version](https://software.intel.com/en-us/qualify-for-free-software) for non-commercial use on linux)
*   unpack the tarball
*   install libpng12 from AUR
*   install libjpeg6 from AUR
*   install rpmextract from extra repo
*   install linux-headers from core
*   if using a custom kernel, ensure that your kernel is compiled with the following options:
    *   CONFIG_MODULES=y
    *   CONFIG_MODULE_UNLOAD=y
    *   CONFIG_SMP=y
    *   CONFIG_KPROBES=y
    *   CONFIG_PROFILING=y
    *   CONFIG_OPROFILE=y

Now to "install" vtune:

```
cd vtune_amplifier_xe_2011_update7
find -name "*.rpm" -exec rpmextract.sh {} \;

```

Kernel module:

*   Create the group vtune and add yourself.
*   Build and load the driver in /opt/intel/vtune_amplifier_xe_2011/sepdk/src/

```
./build-driver
./insmod-sep3 -g vtune

```

*   Add your license file to /opt/intel/licenses/

You can now start vtune:

```
./opt/intel/vtune_amplifier_xe_2011/bin64/amplxe-gui

```

For ease-of-use I suggest you move the ./opt/intel/vtune_amplifier_xe_2011 to your homefolder or similar and add a symlink to the amplxe-gui binary to one of your PATH folders or similar.