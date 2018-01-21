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

To use Linux kernel's "Laptop Hybrid Graphics - GPU switching support" add following to [fstab](/index.php/Fstab "Fstab"):

```
none            /sys/kernel/debug debugfs defaults 0 0

```

This will enable `/sys/kernel/debug/vgaswitcheroo/switch`.

 `# cat /sys/kernel/debug/vgaswitcheroo/switch` 
```
0:IGD:+:Pwr:0000:00:02.0
1:DIS: :Pwr:0000:01:00.0

```

IDN - denotes integrated Intel graphics. DIS - denotes discrete Radeon graphics.

To switch-off Radeon:

```
# echo "DIGD" > /sys/kernel/debug/vgaswitcheroo/switch
# echo "OFF"  > /sys/kernel/debug/vgaswitcheroo/switch

```
 `# cat /sys/kernel/debug/vgaswitcheroo/switch` 
```
0:IGD:+:Pwr:0000:00:02.0
1:DIS: :Off:0000:01:00.0

```

To switch-on both graphics chips:

```
# echo "DIGD" > /sys/kernel/debug/vgaswitcheroo/switch
# echo "DDIS" > /sys/kernel/debug/vgaswitcheroo/switch

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

[Install](/index.php/Install "Install") [lm_sensors](https://www.archlinux.org/packages/?name=lm_sensors).

## Synaptics Touchpad

See [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics").