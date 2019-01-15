**Estado de la traducción**
Este artículo es una traducción de [System-tar-and-restore](/index.php/System-tar-and-restore "System-tar-and-restore"), revisada por última vez el **2019-01-13**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=System-tar-and-restore&diff=0&oldid=563114) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

**System-tar-and-restore** contiene dos scripts de bash, el programa principal **star.sh** y un wrapper con interfaz gráfica **star-gui.sh**. Hay tres modos disponibles:

*   **Copia de seguridad**: Con este modo se puede crear un archivo de copia de seguridad de su sistema con extensión *.tar*.

*   **Restaurar/Transferir**: El modo de restauración utiliza el archivo creado anteriormente para extraerlo en la(s) partición(es) deseada(s). El modo de transferencia transfiere su sistema en la(s) partición(es) deseada(s) utilizando [rsync](https://www.archlinux.org/packages/?name=rsync). Luego, en ambos casos, el script genera el fstab del sistema de destino, recompila initramfs para cada kernel disponible, genera locales y finalmente instala y configura el bootloader seleccionado.

Si planea utilizar la interfaz gráfica, instale [gtkdialog](https://aur.archlinux.org/packages/gtkdialog/) del [AUR](/index.php/AUR_(Espa%C3%B1ol) "AUR (Español)").

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") [system-tar-and-restore](https://aur.archlinux.org/packages/system-tar-and-restore/).

## Utilización

Véase el [LÉAME](https://github.com/tritonas00/system-tar-and-restore/blob/master/README.md).