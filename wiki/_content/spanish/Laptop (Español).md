## Contents

*   [1 Configuración de ordenadores portátiles](#Configuraci.C3.B3n_de_ordenadores_port.C3.A1tiles)
*   [2 Administración de energía](#Administraci.C3.B3n_de_energ.C3.ADa)
    *   [2.1 Utilidades de monitorización del estado de la batería](#Utilidades_de_monitorizaci.C3.B3n_del_estado_de_la_bater.C3.ADa)
    *   [2.2 Suspención e hibernación](#Suspenci.C3.B3n_e_hibernaci.C3.B3n)
    *   [2.3 Ajustes automáticos para extender la vida de la batería](#Ajustes_autom.C3.A1ticos_para_extender_la_vida_de_la_bater.C3.ADa)
    *   [2.4 Other tweaks](#Other_tweaks)
        *   [2.4.1 PCI-e ASPM](#PCI-e_ASPM)
        *   [2.4.2 Granola](#Granola)
        *   [2.4.3 WLAN-device](#WLAN-device)
        *   [2.4.4 Disk-related tweaks](#Disk-related_tweaks)
        *   [2.4.5 Hard drive spin down problem](#Hard_drive_spin_down_problem)
        *   [2.4.6 Tweaking the scheduler](#Tweaking_the_scheduler)
*   [3 Screen brightness](#Screen_brightness)
*   [4 Touchpad](#Touchpad)
*   [5 Hard disk shock protection](#Hard_disk_shock_protection)

## Configuración de ordenadores portátiles

Esta página contiene vínculos a las páginas necesarias para configurar un ordenador portátil para una mejor experiencia. Se puede configurar una laptop de muchas maneras, al igual que cuando se configura el un ordenador de escritorio. Aun así, hay unas cuantas diferencias claves. Cuando se configura una laptop con Archlinux, los siguientes puntos deberían ser tomados en consideración:

*   [#Power Management](#Power_Management) : Administración de energía para ordenadores portátiles, se refiere a optimizar el sistema para que la carga de la batería se mantenga hasta el último momento que sea posible. Esto puede ser llevado a cabo por una variedad de optimizaciones.

*   *   [#Suspend and Hibernate](#Suspend_and_Hibernate) : El sistema operativo puede ser suspendido manualmente tanto en la memoria o en el disco, permitiendo un (casi) completo apagado del hardware.
    *   Hard drive spindown : El sistema puede ser configurado para apagar automáticamente el disco duro después de un intervalo especificado de inactividad.
    *   Screen shut off : La pantalla puede ser configurada para apagarse automáticamente después de un intervalo especificado de inactividad.
    *   CPU frequency scaling : El procesador(s) puede ser configurado para bajar un peldaño automáticamente una frecuencia más baja cuando su carga sea baja.

*   [#Screen brightness](#Screen_brightness) : Como se configura el brillo de la pantalla?
*   La configuración de la red y la red inalámbrica es explicada en: [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration").
*   La configuración de los botones multimedia del teclado está descrita en: [Extra keyboard keys](/index.php/Extra_keyboard_keys "Extra keyboard keys").
*   [#Touchpad](#Touchpad) : Configurar la sensibilidad, aceleración, funciones del botón y los bordes de desplazamiento de algunos touchpad (Synaptics o Alps).
*   [#Hard disk shock protection](#Hard_disk_shock_protection)

Todos de estos puntos son importantes para tomar en consideración cuando se deba configurar un ordenador portátil. Afortunadamente, Archlinux proporciona todas las herramientas y programas necesario para tener el control completo de estos ordenadores. Estos programas y utilidades son destacadas abajo, con tutoriales que contienen muchos tips.

Nota: los siguientes enlaces pueden ser útiles:

*   [http://www.linux-on-laptops.com/](http://www.linux-on-laptops.com/)
*   [http://www.linlap.com/](http://www.linlap.com/)

## Administración de energía

La administración de energía es muy importante para cualquiera que desee hacer un buen uso de la capacidad de batería. Las siguientes herramientas y programas, ayudan a incrementar la vida de batería y mantener el portátil en buenas condiciones.

### Utilidades de monitorización del estado de la batería

El estado de la batería puede ser leído utilizando las utilidades ACPI en la terminal. Las utilidades de la línea de comandos que contienen las funcionalidades de ACPI son proporcionadas por el paquete [acpi](https://www.archlinux.org/packages/?name=acpi). Un simple monitor de batería que se aloja en la bandeja de sistema es [batterymon-clone](https://aur.archlinux.org/packages/batterymon-clone/) que puede ser encontrado en [Usuario de Arco Repository](/index.php/AUR "AUR").

**Tip:** Más información puede ser encontrada en el artículo [ACPI modules](/index.php/ACPI_modules "ACPI modules")

### Suspención e hibernación

El sistema se puede suspender manualmente, tanto a la memoria (standby) o al disco (hibernate) a veces, proporciona la forma más eficaz para optimizar la vida de batería, dependiendo de el patrón de uso del portátil. Así mismo, el kernel de Linux soporta relativamente estas operaciones, típicamente algunos ajustes tienen que hacerse antes de iniciar estas operaciones (generalmente debido a drivers problemáticos, módulos o hardware). Las siguientes herramientas proporcionan "wrappers" alrededor de las interfaces del kernel para suspender/reanudar:

*   [Acpid](/index.php/Acpid "Acpid")
*   [Pm-utils](/index.php/Pm-utils "Pm-utils")
*   [Uswsusp](/index.php/Uswsusp "Uswsusp")

Éstos se encuentran descritos con más detalle en [Suspende](/index.php?title=Suspende&action=edit&redlink=1 "Suspende (page does not exist)").

### Ajustes automáticos para extender la vida de la batería

As opposed to manually initiated actions like suspend/hibernate, a number of tweaks can be made to prolong the battery life of the laptop under low/idle usage.

*   [cpufrequtils](/index.php/CPU_frequency_scaling "CPU frequency scaling") provides CPU frequency scaling, a technology used primarily by notebooks which enables the OS to scale the CPU frequency up or down, depending on the current system load and/or power scheme.
*   [Laptop Mode Tools](/index.php/Laptop_Mode_Tools "Laptop Mode Tools") provides a comprehensive suite of tools to tweak a large number of power saving settings through well documented config files.
*   [PowerTOP](http://www.lesswatts.org/projects/powertop/) is a handy utility from Intel that displays which hardware/processes are using the most power on your system, and provides instructions on how to stop or remove power-wasting services. Works great for mobile Intel CPUs; provides the current CPU state and suggestions for power saving. Also works on AMD systems, but does not provide as much information about the CPU state.
*   [Powernowd](/index.php/Powernowd "Powernowd") is a program for powering down CPUs dynamically, which can be run either on an AMD-based system or an Intel-based system. However, cpufrequtils detailed above provides a more modern alternative, as seen by the fact that powernowd was created before the ondemand governor existed.

Some of these tweaks are specific to certain makes.

*   [Lapsus](/index.php/ASUS_G1#The_Lapsus_daemon_.26_KDE_applet "ASUS G1") is a set of programs providing easy access to many features of various laptops. It currently supports most features provided by asus-laptop kernel module from ACPI4Asus project, such as additional LEDs, hotkeys, backlight control etc. It also has support for some IBM laptops features provided by IBM ThinkPad ACPI Extras Driver and NVRAM device.
*   Battery tweaks for Thinkpads can be found in the [tp_smapi](/index.php/Tp_smapi "Tp smapi") article.
*   [TLP](/index.php/TLP "TLP") for Thinkpads is a set of scripts, which set many powersaving options according to the current Powersource. [TLP](/index.php/TLP "TLP") is intended to be used on Thinkpads, but most settings should work on other laptops too.

### Other tweaks

**Note:** Not only are the following tweaks _may_ not needed if using one of the more comprehensive suites such as [Laptop Mode Tools](/index.php/Laptop_Mode_Tools "Laptop Mode Tools") or [Pm-utils](/index.php/Pm-utils "Pm-utils")

#### PCI-e ASPM

On some laptops, powertop suggests enabling the `CONFIG_PCIEASPM` kernel option. It can be found under "Bus options (PCI etc.)"->"PCI Express ASPM support". This option is marked as experimental in the current kernel (2.6.35) and allows the PCI-e links to enter a power saving state.

According to [[1]](http://www.lesswatts.org/projects/devices-power-management/pcie.php), this option might degrade performance a bit, but on an Acer 3820TG laptop, it can reduce power consumption by about one third or even more.

More experience with this setting would be appreciated, so please share them [here](https://bbs.archlinux.org/viewtopic.php?id=107173)!

It seems like the option is going to be enabled by default in kernel 2.6.36; if so, the information here will be obsolete soon. However, if your system should be able to make use of this power management feature but you are receiving messages like like the following (check `/var/log/everything.log*`):

```
disabling ASPM on pre-1.1 PCI-e device.  You can enable it with 'pcie_aspm=force'

```

then add `pcie_aspm=force` to your kernel command line.

#### Granola

[Granola](https://aur.archlinux.org/packages.php?ID=36841) is a daemon that monitors the cpu usage and uses the cpufreq-userspace module to lessen power usage without any noticeable difference in performance. To use it, first install from the AUR:[[2]](https://aur.archlinux.org/packages.php?ID=36841), the default settings will work for most setups. You will need to load the cpufreq_userspace module, as well as the cpufreq scaling governor for your CPU at startup. Edit `/etc/rc.conf`: For most generic cpus:

```
 MODULES=( ... cpufreq_userspace acpi-cpufreq ... )

```

For Intel Atom or Pentium 4 cpus:

```
 MODULES=( ... cpufreq_userspace p4_clockmod ... )

```

Then add Granola to the DAEMONS array:

```
 DAEMONS=( ... granola ... )

```

and reboot.

To test if it worked, run:

```
 cat /sys/devices/system/cpu/cpu0/cpufreq/cpuinfo_cur_freq
 #OR
 cpufreq-info #if you have cpufreq-utils installed

```

and check that the cpu frequency is below maximum.

#### WLAN-device

When often en route working with your Notebook without WLAN-Access around, it might be expedient to add a little script to your system startup that automatically turns off your WLAN-Hardware to keep it from searching for Access Points and wasting power on this, when not connected:

```
#!/bin/bash

essid="`iwconfig wlan0 | grep ESSID | awk {'print $4'}`"
	if [ "$essid" == "ESSID:off/any" ] ; then
		sudo iwconfig wlan0 txpower off
	fi

```

[edit, if wlan0 ain't your WLAN-device]

Start the script according to your DE/WM options by '(sleep xx && /path/to/script)' depending on how long it usually takes to connect to your Access Point, 60 seconds are a good default value. It will check if you're connected, turning off the device if not.

```
sudo iwconfig wlan0 txpower on

```

will bring it back up, as, of course, a reboot will.

#### Disk-related tweaks

Disable file access time: every time you access (read) a file the filesystem writes an access time to the file metadata. You can disable this on individual files by using the chattr command, or you can enable it on an entire disk by setting the _noatime_ option in your fstab, as follows:

```
/dev/sda1          /          ext3          defaults,noatime          1  2

```

[Source](http://www.faqs.org/docs/securing/chap6sec73.html)

	_Note_: disabling atime causes troubles with [mutt](/index.php/Mutt "Mutt") and other applications that make use of file timestamps. Consider compromising between performance and compatibility by using mount option relatime instead, or look into [mutt work-around for noatime](http://wiki.mutt.org/?MaildirFormat).

To allow the CD/DVD rom to spin down after a while, run the following:

```
/usr/bin/hal-disable-polling --device /dev/scd0

```

Note, however, that [HAL](/index.php/HAL "HAL") has long been deprecated.

Similar functionality is available in the newer [udisks](/index.php/Udisks "Udisks"):

```
/usr/bin/udisks --inhibit-polling /dev/sr0

```

#### Hard drive spin down problem

Documented [here](https://bugs.launchpad.net/ubuntu/+source/acpi-support/+bug/59695)

To prevent your laptop hard drive from spinning down too often (result of too aggressive APM defaults) do the following:

Add the following to `/etc/rc.local`

```
hdparm -B 254 /dev/sdX _where X is your hard drive device_

```

You can also set it to 255 to completely disable spinning down. You may wish to set a lower value if you move your laptop around as lower values park the heads more often and reduce the chance of damage to your hard disk while it is being moved. If you do not move your laptop at all when you are using it, then 255 or 254 is probably best. If you do, then you might want to try a lower value. A value like 128 might be a good middle-ground.

Add the following to `/etc/pm/sleep.d/50-hdparm_pm`

```
#!/bin/sh

if [ -n "$1" ] && ([ "$1" = "resume" ] || [ "$1" = "thaw" ]); then
	hdparm -B 254 /dev/your-hard-drive > /dev/null
fi

```

and run _chmod +x /etc/pm/sleep.d/50-hdparm_pm_ to make sure it resets after suspend. Again, you can change the value 254 as you see fit.

Now the APM level should be set for your hard drive.

For some laptops, the option -S to hdparm can also be relevant (sets the spindown time for the drive). Note that all these options can also be configured using the [laptop-mode tools](/index.php/Laptop_Mode_Tools "Laptop Mode Tools"). This will allow you to set a high value when on AC and a lower value when you are running on battery power.

#### Tweaking the scheduler

For multicore and hyperthreading-enabled processors you may use _sched_mc_power_savings_ and _sched_smt_power_savings_ options respectively to make the scheduler keep idle as many cores as possible. To enable these options you can do

```
echo 1 > /sys/devices/system/cpu/sched_mc_power_savings

```

or

```
echo 1 > /sys/devices/system/cpu/sched_smt_power_savings

```

Echoing 0 will disable them. Also laptop-mode can be used to control _shed_mc_power_savings_ (see the appropriate config file in `/etc/laptop-mode/conf.d`).

## Screen brightness

To change your display brightness, first check `/sys/class/backlight`:

```
   # ls /sys/class/backlight/
   intel_backlight

```

So this particular backlight is managed by an Intel card. Keep in mind that different cards might manage this differently! It is called _acpi_video0_ on an ATI card, for instance.

Check current value:

```
   $ cat /sys/class/backlight/intel_backlight/brightness

```

In this case, the backlight managed by echoing values into `/sys/class/backlight/intel_backlight/brightness`:

```
   # echo "400" > /sys/class/backlight/intel_backlight/brightness

```

If you get a response along the lines of "invalid argument" then you didn't honor the maximum brightness. Obviously you cannot go any higher than your screens maximum brightness. The values for maximum brightness and brightness in general vary wildly among cards. This Intel card, for instance, can go up to 976 while the ATI can go up 9\. Obviously these values don't say anything about maximum effective brightness.

Check your maximum brightness:

```
   $ cat /sys/class/backlight/intel_backlight/max_brightness

```

If your laptop's Fn keys don't work or Gnome/KDE fail to correctly set the brightness using their power daemons, you can try appending **acpi_backlight=vendor** to your kernel line in your bootloader.

## Touchpad

To get your touchpad working properly, see the [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics") page. Note that your laptop may have an ALPS touchpad (such as the DELL Inspiron 6000), and not a Synaptics touchpad. In either case, see the link above.

## Hard disk shock protection

There are several laptops from different vendors featuring shock protection capabilities. As manufacturers have refused to support open source development of the required software components so far, Linux support for shock protection varies considerably between different hardware implementations.

Currently, two projects, named HDAPS and hpfall, support this kind of protection. HDAPS is for IBM/Lenovo Thinkpads and hpfall for HP/Compaq laptops

Just Check [Hard Disk Active Protection System](/index.php/HDAPS "HDAPS"). [hpfall](https://aur.archlinux.org/packages/hpfall/) can be installed from the [AUR](/index.php/AUR "AUR").