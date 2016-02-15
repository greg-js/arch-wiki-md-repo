[Acer Aspire TimelineX 4820TG](http://www.acer.com/timelinex/eng/) is a 14-inch laptop that packs in an Intel Core i5-430M processor and dedicated ATI Radeon HD 5650 graphics, making it a powerful 14-inch laptop. ArchLinux works mostly works out of box, but there are few tweaks required to make the hardware fully compatible with ArchLinux.

## Contents

*   [1 Hardware](#Hardware)
*   [2 PowerSmart / Battery Optimization](#PowerSmart_.2F_Battery_Optimization)
    *   [2.1 Switchable Graphics](#Switchable_Graphics)
    *   [2.2 Enable CPU Frequency Scaling](#Enable_CPU_Frequency_Scaling)
    *   [2.3 Power Usage](#Power_Usage)
    *   [2.4 Sensors](#Sensors)
*   [3 Synaptics Touchpad](#Synaptics_Touchpad)

## Hardware

Make sure that you have [BIOS_Acer_1.25_A_A.zip](http://global-download.acer.com/GDFiles/BIOS/BIOS/BIOS_Acer_1.25_A_A.zip?acerid=634376587472171000&Step1=NOTEBOOK&Step2=ASPIRE&Step3=ASPIRE%204820TG&OS=ALL&LC=en&BC=ACER&SC=PA_7) installed.

## PowerSmart / Battery Optimization

### Switchable Graphics

This laptop contains inbuilt Intel HD & Radeon 5650 graphics adapters. The Intel HD graphics adapter is optimized for low power consumption which Radeon 5650 consumes high power.

To use Linux kernel's "Laptop Hybrid Graphics - GPU switching support" add following to [/etc/fstab](https://wiki.archlinux.org/index.php/Fstab)

```
none            /sys/kernel/debug debugfs defaults 0 0

```

This will enable /sys/kernel/debug/vgaswitcheroo/switch

```
[root@arp arp]# cat /sys/kernel/debug/vgaswitcheroo/switch
0:IGD:+:Pwr:0000:00:02.0
1:DIS: :Pwr:0000:01:00.0

```

IDN - denotes integrated Intel graphics. DIS - denotes discrete Radeon graphics.

To switch-off Radeon, do following -

```
[root@arp arp]# echo "DIGD" > /sys/kernel/debug/vgaswitcheroo/switch
[root@arp arp]# echo "OFF"  > /sys/kernel/debug/vgaswitcheroo/switch

```

```
[root@arp arp]# cat /sys/kernel/debug/vgaswitcheroo/switch
0:IGD:+:Pwr:0000:00:02.0
1:DIS: :Off:0000:01:00.0

```

To switch-on both graphics chips, do following -

```
[root@arp arp]# echo "DIGD" > /sys/kernel/debug/vgaswitcheroo/switch
[root@arp arp]# echo "DDIS" > /sys/kernel/debug/vgaswitcheroo/switch

```

Init script for switching off the Radeon card -

**Note:** There is now a vgaswitcheroo systemd service which should be used instead

```
[root@arp arp]# cat /etc/rc.d/radeon_off 

#!/bin/bash

. /etc/rc.conf
. /etc/rc.d/functions

case "$1" in

   start)
   echo "DIGD" > /sys/kernel/debug/vgaswitcheroo/switch
   echo "OFF"  > /sys/kernel/debug/vgaswitcheroo/switch
   ;;

   stop)
   echo "DIGD" > /sys/kernel/debug/vgaswitcheroo/switch
   echo "DDIS" > /sys/kernel/debug/vgaswitcheroo/switch
   ;;

   restart)
     stat_busy "Restarting radeon_off ..."
     $0 stop
     $0 start
     stat_done
   ;;

   *)
     echo "usage: $0 {start|stop|restart}"
esac

[root@arp arp]# chmod +x /etc/rc.d/radeon_off 

```

Switch the Radeon off while booting. Add following at the end of the file : [/etc/rc.sysinit](https://wiki.archlinux.org/index.php/Rc.sysinit)

```
#Switch-off discrete graphics
/etc/rc.d/radeon_off restart

/bin/dmesg >| /var/log/dmesg.log

```

### Enable CPU Frequency Scaling

Enabled by default, see [CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling") for details.

### Power Usage

The power rating before tweak -

```
Power usage (ACPI estimate): 24.1W (2.8 hours)

```

The power rating after "switching off the radeon graphics" and "enabling laptop-mode tools".

```
Power usage (ACPI estimate): 11.1W (6.5 hours)

```

### Sensors

```
[arp@arpc ~]$ sudo modprobe coretemp
[arp@arpc ~]$ sensors
acpitz-virtual-0
Adapter: Virtual device
temp1:        +53.0°C  (crit = +105.0°C)

radeon-pci-0100
Adapter: PCI adapter
temp1:       +2147355.6°C  

coretemp-isa-0000
Adapter: ISA adapter
Core 0:       +49.0°C  (high = +95.0°C, crit = +105.0°C)

coretemp-isa-0002
Adapter: ISA adapter
Core 2:       +53.0°C  (high = +95.0°C, crit = +105.0°C)

```

## Synaptics Touchpad

See [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics").