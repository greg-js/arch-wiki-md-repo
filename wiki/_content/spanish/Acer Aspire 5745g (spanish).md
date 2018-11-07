## Contents

*   [1 Introducción](#Introducci.C3.B3n)
*   [2 Hardware](#Hardware)
*   [3 Redes](#Redes)
    *   [3.1 Conexión inalámbrica](#Conexi.C3.B3n_inal.C3.A1mbrica)
*   [4 Gestión de energía](#Gesti.C3.B3n_de_energ.C3.ADa)
    *   [4.1 Escalado de frecuencia de CPU](#Escalado_de_frecuencia_de_CPU)
*   [5 Xorg](#Xorg)
*   [6 Panel táctil](#Panel_t.C3.A1ctil)
*   [7 Teclas de acceso rápido](#Teclas_de_acceso_r.C3.A1pido)

# Introducción

Información general sobre Acer Aspire 5745G. También hay información actualizada sobre un portátil muy parecido: [Acer Aspire 5745PG](/index.php/Acer_Aspire_5745PG "Acer Aspire 5745PG").

# Hardware

**Procesador:** Intel Core i5-450M 2.4GHz

**Vídeo:** Intel Integrated Graphics y NVIDIA GeForce GT 330M conmutable (segunda generación)

**Audio:** Intel Corporation 5 Series/3400 Series Chipset High Definition Audio (rev 05)

**TIR cableada:** Atheros Communications AR8151 v1.0 Gigabit Ethernet (rev c0)

**TIR inalámbrica:** Broadcom Corporation BCM43225 802.11b/g/n (rev 01)

```
$ lspci -nn
00:00.0 Host bridge [0600]: Intel Corporation Core Processor DRAM Controller [8086:0044] (rev 18)
00:01.0 PCI bridge [0604]: Intel Corporation Core Processor PCI Express x16 Root Port [8086:0045] (rev 18)
00:16.0 Communication controller [0780]: Intel Corporation 5 Series/3400 Series Chipset HECI Controller [8086:3b64] (rev 06)
00:1a.0 USB Controller [0c03]: Intel Corporation 5 Series/3400 Series Chipset USB2 Enhanced Host Controller [8086:3b3c] (rev 05)
00:1b.0 Audio device [0403]: Intel Corporation 5 Series/3400 Series Chipset High Definition Audio [8086:3b56] (rev 05)
00:1c.0 PCI bridge [0604]: Intel Corporation 5 Series/3400 Series Chipset PCI Express Root Port 1 [8086:3b42] (rev 05)
00:1c.5 PCI bridge [0604]: Intel Corporation 5 Series/3400 Series Chipset PCI Express Root Port 6 [8086:3b4c] (rev 05)
00:1d.0 USB Controller [0c03]: Intel Corporation 5 Series/3400 Series Chipset USB2 Enhanced Host Controller [8086:3b34] (rev 05)
00:1e.0 PCI bridge [0604]: Intel Corporation 82801 Mobile PCI Bridge [8086:2448] (rev a5)
00:1f.0 ISA bridge [0601]: Intel Corporation Mobile 5 Series Chipset LPC Interface Controller [8086:3b09] (rev 05)
00:1f.2 SATA controller [0106]: Intel Corporation 5 Series/3400 Series Chipset 4 port SATA AHCI Controller [8086:3b29] (rev 05)
00:1f.3 SMBus [0c05]: Intel Corporation 5 Series/3400 Series Chipset SMBus Controller [8086:3b30] (rev 05)
00:1f.6 Signal processing controller [1180]: Intel Corporation 5 Series/3400 Series Chipset Thermal Subsystem [8086:3b32] (rev 05)
01:00.0 VGA compatible controller [0300]: nVidia Corporation GT216 [GeForce GT 330M] [10de:0a29] (rev a2)
01:00.1 Audio device [0403]: nVidia Corporation High Definition Audio Controller [10de:0be2] (rev a1)
02:00.0 Ethernet controller [0200]: Atheros Communications AR8151 v1.0 Gigabit Ethernet [1969:1073] (rev c0)
03:00.0 Network controller [0280]: Broadcom Corporation BCM43225 802.11b/g/n [14e4:4357] (rev 01)
3f:00.0 Host bridge [0600]: Intel Corporation Core Processor QuickPath Architecture Generic Non-core Registers [8086:2c62] (rev 05)
3f:00.1 Host bridge [0600]: Intel Corporation Core Processor QuickPath Architecture System Address Decoder [8086:2d01] (rev 05)
3f:02.0 Host bridge [0600]: Intel Corporation Core Processor QPI Link 0 [8086:2d10] (rev 05)
3f:02.1 Host bridge [0600]: Intel Corporation Core Processor QPI Physical 0 [8086:2d11] (rev 05)
3f:02.2 Host bridge [0600]: Intel Corporation Core Processor Reserved [8086:2d12] (rev 05)
3f:02.3 Host bridge [0600]: Intel Corporation Core Processor Reserved [8086:2d13] (rev 05)

```

# Redes

La versión actual de livecd 2010.05 no es compatible con ethernet ni con la conexión inalámbrica, lo que puede llevarle a una situación bastante problemática, especialmente si esperaba realizar la instalación por red.

El kernel anterior a la compilación de 2010 tampoco es compatible, aunque las versiones más recientes del kernel sí lo admiten. Use una iso más reciente de [testiso](https://releng.archlinux.org/isos/) para realizar su instalación y ambas tarjetas deberían funcionar correctamente (como referencia, utilizé la versión de 2011.04.10, la cual ya no está disponible. ¡Consulte el último lanzamiento y espero que funcione!).

## Conexión inalámbrica

El controlador brcm80211 está incluido en el kernel desde la versión 2.6.37\. No es necesaria ninguna otra acción por parte del usuario. Consulte [configuración de redes inalámbricas](/index.php/Wireless_network_configuration_(Espa%C3%B1ol) "Wireless network configuration (Español)") si tiene problemas.

Puede administrar sus conexiones inalámbricas con [NetworkManager](/index.php/NetworkManager_(Espa%C3%B1ol) "NetworkManager (Español)") o [Wicd](/index.php/Wicd_(Espa%C3%B1ol) "Wicd (Español)").

# Gestión de energía

## Escalado de frecuencia de CPU

Véase [escalado de frecuencia de CPU](/index.php/CPU_frequency_scaling_(Espa%C3%B1ol) "CPU frequency scaling (Español)").

# Xorg

Consulte [NVIDIA](/index.php/NVIDIA_(Espa%C3%B1ol) "NVIDIA (Español)") o [nouveau](/index.php/Nouveau_(Espa%C3%B1ol) "Nouveau (Español)").

# Panel táctil

Debe instalar *xf86-input-synaptics*. Funcionó sin necesidad de ninguna configuración por mi parte con xorg.

Si desea usar su ratón sin xorg, puede usar [GPM](/index.php/General_purpose_mouse_(Espa%C3%B1ol) "General purpose mouse (Español)").

# Teclas de acceso rápido

Las teclas de volumen arriba/abajo y silencio se pueden asignar con [xbindkeys](/index.php/Xbindkeys "Xbindkeys").