Tento článek obsahuje pár triků, pomocí kterých můžete zrychlit boot vašeho systému.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Úprava bootovacích souborů](#Úprava_bootovacích_souborů)
    *   [1.1 Mkinitcpio.conf](#Mkinitcpio.conf)
    *   [1.2 Rc.conf](#Rc.conf)
    *   [1.3 Rc.sysinit](#Rc.sysinit)
    *   [1.4 Inittab](#Inittab)
*   [2 Kompilace jádra](#Kompilace_jádra)
    *   [2.1 General Setup](#General_Setup)
    *   [2.2 Loadable Module Support](#Loadable_Module_Support)
    *   [2.3 Block Layer](#Block_Layer)
    *   [2.4 Processor type and features](#Processor_type_and_features)
    *   [2.5 Bus Options](#Bus_Options)
    *   [2.6 Network](#Network)
    *   [2.7 Device Drivers](#Device_Drivers)
    *   [2.8 Network Device support](#Network_Device_support)
    *   [2.9 Input device support](#Input_device_support)
    *   [2.10 Character Devices](#Character_Devices)
    *   [2.11 Misc Devices](#Misc_Devices)
    *   [2.12 Graphics support](#Graphics_support)
    *   [2.13 File systems](#File_systems)
    *   [2.14 Instrumentation Support](#Instrumentation_Support)
    *   [2.15 Kernel Hacking](#Kernel_Hacking)

## Úprava bootovacích souborů

### Mkinitcpio.conf

Otevřete jako root v textovém editoru /etc/mkinitcpio.conf a vymažte všechny položky v HOOKS, které nepotřebujete.

```
HOOKS="base udev autodetect sata usbinput filesystems"

```

[Přečtěte si](/index.php/Mkinitcpio "Mkinitcpio") více o tom, které HOOKy můžete odstranit.

### Rc.conf

Otevřete jako root v textovém editoru /etc/rc.conf jako root a nalistujte si sekci věnovanou hardwaru.

```
MOD_AUTOLOAD="yes"

```

Pokud máte zapnuté automatické nahrávání modulů, není důvod proč je vybírat ručně. Proto promažte MODULES jako zde.

```
MODULES=()

```

V sekci věnované sítím si ověřte, jestli máte nastavené jenom ty sítě, které potřebujete. Také manuální konfigurace je rychlejší než DHCP.

Poté vypněte všechny služby, které nepotřebujete.

```
DAEMONS=(alsa network gdm)

```

Nakonec posňte váš grafický přihlašovací démon na začátek (pokud nějaký máte) a všem službám nastavte spouštění na pozadí.

```
DAEMONS=(@gdm @alsa @network)

```

### Rc.sysinit

Otevřete jako root v textovém editoru /etc/rc.sysinit a najděte

```
/sbin/modprobe $mod

```

Přidáním '&' na konec se budou všechny moduly nahrávat na pozadí.

```
/sbin/modprobe $mod &

```

### Inittab

Otevřete jako root v textovém editoru /etc/inittab a najděte řádky s obsahem ohledně agetty.

```
c1:2345:respawn:/sbin/agetty 38400 vc/1 linux
c2:2345:respawn:/sbin/agetty 38400 vc/2 linux
c3:2345:respawn:/sbin/agetty 38400 vc/3 linux
c4:2345:respawn:/sbin/agetty 38400 vc/4 linux
c5:2345:respawn:/sbin/agetty 38400 vc/5 linux
c6:2345:respawn:/sbin/agetty 38400 vc/6 linux

```

Agetty terminály jsou ty, které vidíte při stisknutí Ctrl+Alt+F1-6. Nyní, pokud potřebujete jenom dva nebo tři, zakomentujte ty ostatní.

```
c1:2345:respawn:/sbin/agetty 38400 vc/1 linux
c2:2345:respawn:/sbin/agetty 38400 vc/2 linux
#c3:2345:respawn:/sbin/agetty 38400 vc/3 linux
#c4:2345:respawn:/sbin/agetty 38400 vc/4 linux
#c5:2345:respawn:/sbin/agetty 38400 vc/5 linux
#c6:2345:respawn:/sbin/agetty 38400 vc/6 linux

```

## Kompilace jádra

Ke zmenšením času potřebného pro boot je odlehčené jádro nutností. [Přečtěte si více o kompilování jádra.](/index.php/Kernel_Compilation_From_Source "Kernel Compilation From Source")

Zde jsou nějaké tipy od XxX Owned XxX ( [http://ubuntuforums.org/showpost.php?p=1174954&postcount=507](http://ubuntuforums.org/showpost.php?p=1174954&postcount=507) ). Varování: Některé z těchto tipů můžou způsobit, že se jádro nezkompiluje správně. Použijte je pouze na vlastní riziko.

S=Zapnout U=Vypnout

Pokud víte o něčem, co zde chybí, nic vám nebrání to sem přidat!

### General Setup

```
S: Support for paging of anonymous memory. (swap)

```

### Loadable Module Support

```
U: Module Versioning Support
U: Source checksum for all modules

```

### Block Layer

```
U: Large Block Devices (Uncheck all if possible)
// IO Schedulers // 
U: Anticipatory I/O Schedulers
U: Deadline I/O Schedulers

```

### Processor type and features

```
U: Symmetric processing support (Unless your processor(s) support(s) it)
U: Generic x86 support
S: HPET Timer Support
S: Voluntary Kernel Preemption (Desktop) (Under Preemption Model)
S: Local APCI support on uniprocessors
S: IOAPCI support on uniprocessors (Under Local APCI support)
S: Off (Under High Memory support if you have under 1 gig of ram)
S: Sparse Memory (Under Memory Model, some computers will not have this option)
S: MTRR support
S: Use register arguements
S: Enable seccomp to compute untrusted bytecode
S: 1000hz (Under Timer Frequency)
// Firmware Drivers // 
U: Anything that you don't need.

```

### Bus Options

```
S: Message Signaled Interrupts (MSI and MSIX) (PCI_MSI)

```

### Network

```
U: Anything/Everything in Amateur Radio, IrDA, and Bluetooth if you don't need it.
// Network Options // 
S: Packet socket:mmapped IO

```

### Device Drivers

```
// ATA/ATAP/MFR/RLL support // 
S: Use PCI DMA by Default
U: IDE Taskfile Acess
// Raid and LVM // 
U: Unselect if you do not need it.
// I2O support // 
U: Unselect if you do not need it. Most people do not.

```

### Network Device support

```
U: EQL support
U: Universial TUN/TAP device driver support
U: FDDI Driver support
U: HIPPI driver support
U: SLIP (serial line) support
U: Traffic Support
U: Network console loggin support
// ARCnet support // 
U: Unselect if you do not require/need it.
// Ethernet Support (1000 MB) // 
U: Uselect the cards that you don't have.
// Ethernet Support (10000 MB) // 
U: Unselect what you do not need.
// Token Ring Devices // 
U: Unselect if you are not connected to a Token ring network.
// WAN interfaces support // 
U: Unselect the some cards/the whole thing if you do not need it.
// ISDN subsystem // 
U: ISDN support (If you do not require it)

```

### Input device support

```
U: Touchscreen interface
U: Touchscreens (Under the TouchScreens subcatergory)

```

### Character Devices

```
U: Any video cards that you do not need.
// Watchdog cards // 
U: Watch Dog Timer support

```

### Misc Devices

```
U: Device driver for IBM/RSA service drivers
// Video Capture Adapters // 
U: Unselect anything that you don't need.
// Radio Adapters // 
U: Unselect anything that you don't need.
// Digital Video Broadcasting Devices // 
U: DVB for Linux

```

### Graphics support

```
U: Unselect any graphics cards that you don't have.
// Logo Configuration // 
S: Bootup Logo (and anything under it)

```

### File systems

```
U: Unselect any file systems that you are NOT going to use. (Minix, ROM, Quota, etc.)
// DOS/FAT/NT Filesystems // 
S: NTFS write support
// Network File Systems // 
U: NFS file system support
U: NFS server support
U: NCP file system support
U: Coda file system support
U: Andrew file system support
U: Plan 9 resource sharing support
// Partition Types // 
U: Advanced partition selection
// Native Language Support // 
U: Unselect all but your native language

```

### Instrumentation Support

```
U: Profiling Support
U: Kprobes

```

### Kernel Hacking

```
U: Show timing information on printks
U: Magic SysRq Key
U: Kernel Hacking
U: Debug Filesystem
U: Compile the kernel with frame unwind information

```