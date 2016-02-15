Tato stránka popisuje, jak nainstalovat, nastavit a používat **lm_sensors**, pomocí kterého můžeš monitorovat teplotu CPU, základní desky a rychlost větráčků.

## Contents

*   [1 Instalace lm_sensors](#Instalace_lm_sensors)
*   [2 Nastavování lm_sensors](#Nastavov.C3.A1n.C3.AD_lm_sensors)
*   [3 čtení hodnot SPD z paměťových modulů](#.C4.8Dten.C3.AD_hodnot_SPD_z_pam.C4.9B.C5.A5ov.C3.BDch_modul.C5.AF)
*   [4 Používání lm_sensors](#Pou.C5.BE.C3.ADv.C3.A1n.C3.AD_lm_sensors)

### Instalace lm_sensors

1.  Nainstaluj balíček pomocí Pacmana
     `# pacman -S lm_sensors` 

### Nastavování lm_sensors

1.  Použij **sensors-detect** pro detekování a vytvoření seznamu jaderných modulů
     `# sensors-detect` Tohle vytvoří konfiguraci a uloží ji v **/etc/sysconfig/lm_sensors**
2.  Nastav automatické načítání modulů při startu přidáním **sensors** do pole **DAEMONS** v **/etc/rc.conf** `DAEMONS=(syslog-ng crond ... sensors ...)` 
3.  Pro vyzkoušení tvého nastavení nyní načti moduly použití sensors init skriptu `# /etc/rc.d/sensors start` Potom použij příkaz **sensors** `$ sensors` Mělo by se vypsat něco podobného tomuto:

```
lm85-i2c-0-2e
Adapter: SMBus I801 adapter at c800
V1.5:       +1.47 V  (min =  +0.00 V, max =  +3.32 V)
VCore:      +1.34 V  (min =  +0.00 V, max =  +2.99 V)
V3.3:       +3.32 V  (min =  +0.00 V, max =  +4.38 V)
V5:        +5.05 V  (min =  +0.00 V, max =  +6.64 V)
V12:      +11.94 V  (min =  +0.00 V, max = +15.94 V)
CPU_Fan:   1760 RPM  (min =    0 RPM)
fan2:         0 RPM  (min =    0 RPM)
fan3:         0 RPM  (min =    0 RPM)
fan4:         0 RPM  (min =    0 RPM)
CPU Temp:    +51°C  (low  =  -127°C, high =  +127°C)
Board Temp:
             +46°C  (low  =  -127°C, high =  +127°C)
Remote Temp:
             +45°C  (low  =  -127°C, high =  +127°C)
CPU_PWM:    77
Fan2_PWM:   87
Fan3_PWM:   87
vid:      +1.088 V  (VRM Version 10.0)

```

### čtení hodnot SPD z paměťových modulů

Pro čtení hodnot časování z SPD paměťových modulů, načti modul eeprom `# modprobe eeprom` a spusť tento perl skript:

[decode-dimms.pl](http://www.lm-sensors.org/browser/lm-sensors/trunk/prog/eeprom/decode-dimms.pl)

### Používání lm_sensors

*   Nyní můžeš používat lm_sensors ve front-endech jako **xsensors**, **gkrellm**, **xfce4-sensors-plugin**, **GNOME Computer Temperature Monitor** applet a **ksensors**.