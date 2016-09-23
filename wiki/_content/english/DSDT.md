DSDT (Differentiated System Description Table) is a part of the [ACPI](https://en.wikipedia.org/wiki/Advanced_Configuration_and_Power_Interface "wikipedia:Advanced Configuration and Power Interface") specification. It supplies information about supported power events in a given system. ACPI tables are provided in firmware from the manufacturer. A common Linux problem is missing ACPI functionality, such as: fans not running, screens not turning off when the lid is closed, etc. This can stem from DSDTs made with Windows specifically in mind, which can be patched after installation. The goal of this article is to analyze and rebuild a faulty DSDT, so that the kernel can override the default one.

Basically a DSDT table is the code run on ACPI (Power Management) events.

**Note:** The goal of the [Linux ACPI](https://01.org/linux-acpi) project is that Linux should work on unmodified firmware. If you still find this type of workaround necessary on modern kernels then you should consider [submiting a bug report](/index.php/Reporting_bug_guidelines "Reporting bug guidelines").

## Contents

*   [1 Before you start...](#Before_you_start...)
    *   [1.1 Tell the kernel to report a version of Windows](#Tell_the_kernel_to_report_a_version_of_Windows)
    *   [1.2 Find a fixed DSDT](#Find_a_fixed_DSDT)
*   [2 Recompiling it yourself](#Recompiling_it_yourself)
*   [3 Using modified code](#Using_modified_code)
    *   [3.1 Using a CPIO archive](#Using_a_CPIO_archive)
    *   [3.2 Compiling into the kernel](#Compiling_into_the_kernel)
    *   [3.3 Loading at runtime](#Loading_at_runtime)
*   [4 Verify successful override](#Verify_successful_override)
*   [5 See also](#See_also)

## Before you start...

*   It is possible that the hardware manufacturer has released an updated firmware which fixes ACPI related problems. Installing an updated firmware is often preferred over this method because it would avoid duplication of effort.
*   This process does tamper with some fairly fundamental code on your installation. You will want to be absolutely sure of the changes you make. You might also wish to [clone your disk](/index.php/Disk_cloning "Disk cloning") beforehand.
*   Even before attempting to fix your DSDT yourself, you can attempt a couple of different shortcuts:

### Tell the kernel to report a version of Windows

Use the variable **acpi_os_name** as a kernel parameter. For example:

```
 acpi_os_name="Microsoft Windows NT"

```

Or

```
 acpi_osi="!Windows2012"

```

appended to the kernel line in grub legacy configuration

other strings to test:

*   "Microsoft Windows XP"
*   "Microsoft Windows 2000"
*   "Microsoft Windows 2000.1"
*   "Microsoft Windows ME: Millennium Edition"
*   "Windows 2001"
*   "Windows 2006"
*   "Windows 2009"
*   "Windows 2012"
*   when all that fails, you can even try "Linux"

Out of curiousity, you can follow the steps below to extract your DSDT and search the .dsl file. Just grep for "Windows" and see what pops up.

### Find a fixed DSDT

A DSDT file is originally written in ACPI Source language (an .asl/.dsl file). Using a compiler this can produce an 'ACPI Machine Language' file (.aml) or a hex table (.hex). To incorporate the file in your Arch install, you will need to get hold of a compiled .aml file. - whether this means compiling it yourself or trusting some stranger on the Internet is at your discretion. If you do download a file from the world wide web, it will most likely be a compressed .asl file. So you will need to unzip it and compile it. The upside to this is that you won't have to research specific code fixes yourself.

Arch users with the same laptop as you are: a minority of a minority of a minority. Try browsing other distro/linux forums for talk about the same model. Likelihood is that they have the same problems and either because there is a lot of them, or because they're tech savvy -- someone there has produced a working DSDT and maybe even provides a precompiled version (again, use at your own risk). Search engines are your best tools. Try keeping it short: 'model name' + 'dsdt' will probably produce results.

## Recompiling it yourself

Your best resources in this endeavor are going to be [ACPI Spec homepage](http://www.acpi.info), and [Linux ACPI Project](http://www.lesswatts.org/projects/acpi/) which supercedes the activity that occurred at *acpi.sourceforge.net*. In a nutshell, you can use Intel's ASL compiler to turn your systems DSDT table into source code, locate/fix the errors, and recompile.

You'll need to install [iasl](https://www.archlinux.org/packages/?name=iasl) to modify code, and be familiar with [Kernel Compilation#Compilation](/index.php/Kernel_Compilation#Compilation "Kernel Compilation") to install it.

**What compiled the original code?** Check if your system's DSDT was compiled using Intel or Microsoft compiler:

 ` $ dmesg|grep DSDT ` 
```
ACPI: DSDT 00000000bf7e5000 0A35F (v02 Intel  CALPELLA 06040000 INTL 20060912)
ACPI: EC: Look up EC in DSDT

```

In case Microsoft's compiler had been used, abbreviation INTL would instead be MSFT. In the example, there were 5 errors on decompiling/recompiling the DSDT. Two of them were easy to fix after a bit of googling and delving into the ACPI specification. Three of them were due to different versions of compiler used and are, as later discovered, handled by the ACPICA at boot-time. The ACPICA component of the kernel can handle most of the trivial errors you get while compiling the DSDT. So do not fret yourself over compile errors if your system is *working the way it should*.

1.) Extract ACPI tables (as root): `# cat /sys/firmware/acpi/tables/DSDT > dsdt.dat`

2.) Decompile: `iasl -d dsdt.dat`

3.) Recompile: `iasl -tc dsdt.dsl`

4.) Examine errors and fix. e.g.:
```
dsdt.dsl   6727:                         Name (_PLD, Buffer (0x10)  
Error    4105 -          Invalid object type for reserved name ^  (found BUFFER, requires Package) 
```
 ` nano +6727 dsdt.dsl`  `(_PLD, Package(1) {Buffer (0x10)...` 

5.) Compile fixed code: `iasl -tc dsdt.dsl` (Might want to try option -ic for C include file to insert into kernel source)

If it says no errors and no warnings you should be good to go.

## Using modified code

**Warning:** After each BIOS update you will need to fix DSDT again and repeat these steps!

There are at least three ways to use a custom DSDT:

*   creating a CPIO archive that is loaded by the bootloader
*   compiling it into the kernel
*   loading it at runtime (not supported)

### Using a CPIO archive

This method has the advantage that you do not need to recompile your kernel, and updating the kernel will not make it necessary to repeat these steps.

This method requires the following kernel config to be enabled (true for the [linux](https://www.archlinux.org/packages/?name=linux) package):

*   `ACPI_TABLE_UPGRADE=y` (Linux kernel 4.6+)
*   `CONFIG_ACPI_INITRD_TABLE_OVERRIDE=y` (Linux kernel <=4.5)

See [[1]](https://www.kernel.org/doc/Documentation/acpi/initrd_table_override.txt) for details.

First, create the following folder structure:

```
$ mkdir -p kernel/firmware/acpi

```

Copy the fixed ACPI tables into the just created `kernel/firmware/acpi` folder, for example:

```
$ cp dsdt.aml ssdt1.aml kernel/firmware/acpi

```

Within the same folder where the newly created `kernel/` folder resides, run:

```
$ find kernel | cpio -H newc --create > acpi_override

```

This creates the CPIO archive containing the fixed ACPI tables. Copy the archive to the `boot` directory.

```
# cp acpi_override /boot

```

Lastly, configure the [bootloader](/index.php/Bootloader "Bootloader") to load your CPIO archive. For example, using [Systemd-boot](/index.php/Systemd-boot "Systemd-boot"), `/boot/loader/entries/arch.conf` might look like this:

```
title	 Arch Linux
linux	 /vmlinuz-linux
initrd   /acpi_override
initrd	 /initramfs-linux.img
options  root=PARTUUID=ec9d5998-a9db-4bd8-8ea0-35a45df04701 resume=PARTUUID=58d0aa86-d39b-4fe1-81cf-45e7add275a0 ...

```

Now all that is left to do is to reboot and to [verify the result.](#Verify_successful_override)

### Compiling into the kernel

You'll want to be familiar with [compiling your own kernel](/index.php/Kernels "Kernels"). The most straightforward way is with the "traditional" approach. After compiling DSDT, iasl produce two files: `dsdt.hex` and `dsdt.aml`.

**Using `menuconfig`:**

*   Disable "Select only drivers that don't need compile-time external firmware". Located in "Device Drivers -> Generic Driver Options".
*   Enable "Include Custom DSDT" and specify the absolute path of your fixed DSDT file (`dsdt.hex`, not `dsdt.aml`). Located in "Power management and ACPI options -> ACPI (Advanced Configuration and Power Interface) Support".

### Loading at runtime

**Warning:** The mkinitcpio method is no longer supported, since the DSDT hook has been removed, see [[2]](https://bugs.archlinux.org/task/27906).

Luckily the Arch stock kernel supports using a custom DSDT so, first copy the **.aml** file compiled by iasl to:

```
/boot/dsdt.aml

```

The bootloader will replace the DSDT so we need a method to include our custom DSDT table into the bootloader image. Copy the following to **/etc/grub.d/01_acpi**

```
#!/bin/sh
set -e

```

```
# Uncomment to load custom ACPI table
GRUB_CUSTOM_ACPI="/boot/dsdt.aml"

# DON'T MODIFY ANYTHING BELOW THIS LINE!

prefix=/usr
exec_prefix=${prefix}
libdir=${exec_prefix}/lib

. /usr/share/grub/grub-mkconfig_lib
#. ${libdir}/grub/grub-mkconfig_lib

# Load custom ACPI table
if [ x${GRUB_CUSTOM_ACPI} != x ] && [ -f ${GRUB_CUSTOM_ACPI} ] \
        && is_path_readable_by_grub ${GRUB_CUSTOM_ACPI}; then
    echo "Found custom ACPI table: ${GRUB_CUSTOM_ACPI}" >&2
    prepare_grub_to_access_device `${grub_probe} --target=device ${GRUB_CUSTOM_ACPI}` | sed -e "s/^/  /"
    cat << EOF
acpi (\$root)`make_system_path_relative_to_its_root ${GRUB_CUSTOM_ACPI}`
EOF
fi

```

Make sure to make this file executable, or it will be ignored by **grub-mkconfig**

```
chmod +x /etc/grub.d/01_acpi

```

This will tell GRUB to include the DSDT into its core.img (change GRUB_CUSTOM_ACPI to reflect the path to your .aml file). Next you will need a new boot image. If you use GRUB run:

```
grub-mkconfig -o /boot/grub/grub.cfg

```

Lastly, recreate your initrd

```
mkinitcpio -p linux

```

and reboot. Done!

To check if you are really using your own DSDT read your table again `# cat /sys/firmware/acpi/tables/DSDT > dsdt.dat` and decompile it with `iasl -d dsdt.dat`

## Verify successful override

1.  Run `dmesg | grep ACPI`.
2.  Look for clues that suggest an override, for example:

```
[    0.000000] ACPI: Override [DSDT-   A M I], this is unsafe: tainting kernel
[    0.000000] ACPI: DSDT 00000000be9b1190 Logical table override, new table: ffffffff81865af0
[    0.000000] ACPI: DSDT ffffffff81865af0 0BBA3 (v02 ALASKA    A M I 000000F3 INTL 20130517)

```

## See also

*   [Upgrading ACPI tables via initrd](https://www.kernel.org/doc/Documentation/acpi/initrd_table_override.txt)