**Estado de la traducción:** este artículo es una versión traducida de [ACPI modules](/index.php/ACPI_modules "ACPI modules"). Fecha de la última traducción/revisión: **2018-09-13**. Puedes ayudar a actualizar la traducción, si adviertes que la versión inglesa ha cambiado: [ver cambios](https://wiki.archlinux.org/index.php?title=ACPI_modules&diff=0&oldid=541074).

Artículos relacionados

*   [acpid](/index.php/Acpid_(Espa%C3%B1ol) "Acpid (Español)")
*   [DSDT](/index.php/DSDT "DSDT")

De [ACPI site](http://www.acpi.info/):

	*ACPI (Advanced Configuration and Power Interface) es una especificación abierta de la industria co-desarrollada por Hewlett-Packard, Intel, Microsoft, Phoenix y Toshiba.*

Los módulos ACPI son módulos del kernel para diferentes partes de ACPI. Permiten funciones ACPI especiales o añaden información en `/proc` o `/sys`. Esta información puede ser analizada por [acpid](/index.php/Acpid_(Espa%C3%B1ol) "Acpid (Español)") para eventos u otras aplicaciones de supervisión.

## Contents

*   [1 ¿Qué módulos están disponibles?](#.C2.BFQu.C3.A9_m.C3.B3dulos_est.C3.A1n_disponibles.3F)
*   [2 Cómo seleccionar los adecuados](#C.C3.B3mo_seleccionar_los_adecuados)
*   [3 Obteniendo información](#Obteniendo_informaci.C3.B3n)
*   [4 Solución de problemas](#Soluci.C3.B3n_de_problemas)
    *   [4.1 Corregir DSDT](#Corregir_DSDT)
    *   [4.2 Corregir ACPI para portátiles](#Corregir_ACPI_para_port.C3.A1tiles)
*   [5 Consulte también](#Consulte_tambi.C3.A9n)

## ¿Qué módulos están disponibles?

Esta es una pequeña lista y un resumen de los módulos del kernel de ACPI:

*   ac (estado del conector de alimentación)
*   asus-laptop (útil en portátiles ASUS/medion)
*   battery (estado de la batería)
*   bay (estado de las bahías)
*   button (eventos de botón de captura, como LID o POWER BUTTON)
*   container (estado del contenedor)
*   dock (estado de la estación de acoplamiento, *docking station*)
*   fan (estado del los ventiladores)
*   i2c_ec (driver EC SMBUs)
*   thinkpad_acpi (útil en portátiles Lenovo Thinkpad)
*   processor (estado de los procesadores)
*   sbs (estado de la batería inteligente)
*   thermal (estado de los sensores de temperatura)
*   toshiba_acpi (útil en portátiles Toshiba)
*   video (estado de los dispositivos de vídeo)

lista completa de su kernel en ejecución:

 `$ ls -l /usr/lib/modules/$(uname -r)/kernel/drivers/acpi` 
```
total 112
-rw-r--r-- 1 root root  2808 Aug 29 23:58 ac.ko.gz
-rw-r--r-- 1 root root  3021 Aug 29 23:58 acpi_ipmi.ko.gz
-rw-r--r-- 1 root root  3354 Aug 29 23:58 acpi_memhotplug.ko.gz
-rw-r--r-- 1 root root  4628 Aug 29 23:58 acpi_pad.ko.gz
drwxr-xr-x 2 root root  4096 Aug 29 23:59 apei
-rw-r--r-- 1 root root  7120 Aug 29 23:58 battery.ko.gz
-rw-r--r-- 1 root root  3700 Aug 29 23:58 button.ko.gz
-rw-r--r-- 1 root root  2181 Aug 29 23:58 container.ko.gz
-rw-r--r-- 1 root root  1525 Aug 29 23:58 custom_method.ko.gz
-rw-r--r-- 1 root root  1909 Aug 29 23:58 ec_sys.ko.gz
-rw-r--r-- 1 root root  2001 Aug 29 23:58 fan.ko.gz
-rw-r--r-- 1 root root  1532 Aug 29 23:58 hed.ko.gz
-rw-r--r-- 1 root root  3241 Aug 29 23:58 pci_slot.ko.gz
-rw-r--r-- 1 root root 17742 Aug 29 23:58 processor.ko.gz
-rw-r--r-- 1 root root  3073 Aug 29 23:58 sbshc.ko.gz
-rw-r--r-- 1 root root  7098 Aug 29 23:58 sbs.ko.gz
-rw-r--r-- 1 root root  6311 Aug 29 23:58 thermal.ko.gz
-rw-r--r-- 1 root root  8891 Aug 29 23:58 video.ko.gz

```

## Cómo seleccionar los adecuados

Debe ir probando los módulos que funcionan en su máquina:

```
# modprobe <módulo>

```

A continuación, compruebe si el módulo es compatible con su hardware utilizando:

```
$ dmesg

```

**Sugerencia:** Puede ser útil añadir una búsqueda de texto *grep* para restringir los resultados.

```
$ dmesg | grep acpi
[    0.000000] ACPI: LAPIC (acpi_id[0x00] lapic_id[0x00] enabled)
[    0.000000] ACPI: LAPIC (acpi_id[0x01] lapic_id[0x04] enabled)
[    0.000000] ACPI: LAPIC (acpi_id[0x02] lapic_id[0x01] enabled)
[    0.000000] ACPI: LAPIC (acpi_id[0x03] lapic_id[0x05] enabled)
[    0.000000] ACPI: LAPIC_NMI (acpi_id[0x00] high edge lint[0x1])
[    0.000000] ACPI: LAPIC_NMI (acpi_id[0x01] high edge lint[0x1])
[    0.000000] ACPI: LAPIC_NMI (acpi_id[0x02] high edge lint[0x1])
[    0.000000] ACPI: LAPIC_NMI (acpi_id[0x03] high edge lint[0x1])
[    5.066752] ACPI: acpi_idle yielding to intel_idle
[    5.438998] acpi device:04: registered as cooling_device4

```

Añada los que estén funcionando a los archivos de configuración en `/etc/modules-load.d`. `/etc/modules-load.d` se describe en [Kernel modules (Español)#Automatic module handling](/index.php/Kernel_modules_(Espa%C3%B1ol)#Automatic_module_handling "Kernel modules (Español)").

## Obteniendo información

Para obtener la información de la batería, simplemente [instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [acpi](https://www.archlinux.org/packages/?name=acpi) de los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)") y ejecute:

```
acpi -i

```

El uso de `/proc` para almacenar información ACPI ha sido desaconsejado y desaprobado desde Linux 2.6.24\. Los mismos datos están ahora disponibles en `/sys`, y las partes de interés pueden (deberían) suscribirse a los eventos ACPI desde el kernel a través de netlink. Por ejemplo, para la batería:

```
/sys/class/power_supply/BAT0/

```

## Solución de problemas

### Corregir DSDT

Si persisten los problemas con la administración de energía a pesar de haber cargado los módulos adecuados, un [DSDT](https://en.wikipedia.org/wiki/DSDT#ACPI_Tables "wikipedia:DSDT") poco amistoso para Linux podría ser la causa. Consulte el artículo de la wiki en [DSDT](/index.php/DSDT "DSDT").

### Corregir ACPI para portátiles

A veces verá "ACPI: EC: input buffer is not empty, aborting transaction". Este es un problema con ACPI, más específicamente una incompatibilidad de la BIOS. Puede haber cuatro formas de resolver este problema:

*   Si está disponible, actualice la BIOS.

*   Utilice `acpi=off` como [parámetro del kernel](/index.php/Kernel_parameters_(Espa%C3%B1ol) "Kernel parameters (Español)"), sin embargo, esto matará todas las funciones ACPI, como la carga de la batería y el ahorro de energía.

*   En algunos casos, se informó que desactivando [DPMS](/index.php/DPMS "DPMS") se solucionó el problema [[1]](https://ubuntuforums.org/showthread.php?p=8030130#10). Sin embargo, el brillo de la pantalla ya no puede ser totalmente controlable: `$ xset dpms force off` 

*   Construir un [kernel](/index.php/Kernel_(Espa%C3%B1ol) "Kernel (Español)") a medida con los parches en [bugs.launchpad.net](https://bugs.launchpad.net/ubuntu/+source/linux/+bug/578506).

## Consulte también

*   [Wikipedia:es:Advanced Configuration and Power Interface](https://en.wikipedia.org/wiki/es:Advanced_Configuration_and_Power_Interface "wikipedia:es:Advanced Configuration and Power Interface")