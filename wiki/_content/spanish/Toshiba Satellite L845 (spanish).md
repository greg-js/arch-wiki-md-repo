**Estado de la traducción**
Este artículo es una traducción de [Toshiba Satellite L845](/index.php/Toshiba_Satellite_L845 "Toshiba Satellite L845"), revisada por última vez el **2019-02-09**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Toshiba_Satellite_L845&diff=0&oldid=557934) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

## Corregir las teclas Fn

Si las teclas Fn no funcionan o muestran un comportamiento incorrecto (por ejemplo, las teclas de brillo suspenden el portátil), se puede corregir haciendo lo siguiente:

En `/etc/default/grub` encuentre la línea que dice `GRUB_CMDLINE_LINUX=""` y agregue los siguientes parámetros del kernel:

```
acpi_osi=Linux acpi_backlight=vendor

```

Luego, en `/etc/modprobe.d/blacklist.conf` agregue la siguiente línea:

```
blacklist toshiba_acpi

```

Si `blacklist.conf` no existe, créelo.

Finalmente, haga `sudo update-grub` y reinicie.