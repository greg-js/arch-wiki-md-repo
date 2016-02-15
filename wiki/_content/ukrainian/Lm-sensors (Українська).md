## Contents

*   [1 Встановлення lm_sensors](#.D0.92.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.BD.D1.8F_lm_sensors)
*   [2 Налаштування lm_sensors](#.D0.9D.D0.B0.D0.BB.D0.B0.D1.88.D1.82.D1.83.D0.B2.D0.B0.D0.BD.D0.BD.D1.8F_lm_sensors)
*   [3 Використання lm_sensors](#.D0.92.D0.B8.D0.BA.D0.BE.D1.80.D0.B8.D1.81.D1.82.D0.B0.D0.BD.D0.BD.D1.8F_lm_sensors)
*   [4 Посилання на зовнішні ресурси](#.D0.9F.D0.BE.D1.81.D0.B8.D0.BB.D0.B0.D0.BD.D0.BD.D1.8F_.D0.BD.D0.B0_.D0.B7.D0.BE.D0.B2.D0.BD.D1.96.D1.88.D0.BD.D1.96_.D1.80.D0.B5.D1.81.D1.83.D1.80.D1.81.D0.B8)

### Встановлення lm_sensors

Для встановлення пакету через Pacman
 `# pacman -S lm_sensors` 

### Налаштування lm_sensors

Використовуючи **sensors-detect** визначте список модулів ядра
 `# sensors-detect` Ця команда створить конфігуріційний файл **/etc/sysconfig/lm_sensors** Для автоматичного завантаження модулів ядра під час завантаження комп'ютера додайте **sensors** до змінної **DAEMONS** у **/etc/rc.conf** `DAEMONS=(syslog-ng crond ... sensors ...)` Для перевірки налаштувань запустіть прямо зараз скрипт `# /etc/rc.d/sensors start` Далі викличте команду **sensors** `$ sensors` Ви повинні побачити щось на зразок

```
 it8712-isa-0290
 Adapter: ISA adapter
 VCore 1:   +1.39 V  (min =  +0.00 V, max =  +4.08 V)
 VCore 2:   +0.00 V  (min =  +0.00 V, max =  +4.08 V)   ALARM
 +3.3V:     +3.20 V  (min =  +0.00 V, max =  +4.08 V)
 +5V:       +4.84 V  (min =  +0.00 V, max =  +6.85 V)
 +12V:     +11.65 V  (min =  +0.00 V, max = +16.32 V)
 -12V:      -5.02 V  (min = -27.36 V, max =  +3.93 V)
 -5V:      -13.64 V  (min = -13.64 V, max =  +4.03 V)   ALARM
 Stdby:     +4.84 V  (min =  +0.00 V, max =  +6.85 V)
 VBat:      +3.04 V
 fan1:     1562 RPM  (min =  811 RPM, div = 8)
 fan2:        0 RPM  (min =    0 RPM, div = 8)
 fan3:     5443 RPM  (min =    0 RPM, div = 8)
 M/B Temp:    +48°C  (low  =    -1°C, high =  +127°C)   sensor = thermistor
 CPU Temp:    +45°C  (low  =    -1°C, high =  +127°C)   sensor = thermistor
 Temp3:       +30°C  (low  =    -1°C, high =  +127°C)   sensor = thermistor

 k8temp-pci-00c3
 Adapter: PCI adapter
 Core0 Temp:
              +51°C

```

### Використання lm_sensors

Ви маєте можливість використовувати lm_sensors у **gkrellm**, [xfce4-sensors-plugin](http://goodies.xfce.org/projects/panel-plugins/xfce4-sensors-plugin) чи **ksensors**.

### Посилання на зовнішні ресурси

[xfce4-sensors-plugin](http://goodies.xfce.org/projects/panel-plugins/xfce4-sensors-plugin)