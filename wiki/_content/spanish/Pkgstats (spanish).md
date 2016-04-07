pkgstatus envía un listado de todos los paquetes instalados, [kernel modules](https://www.archlinux.org/news/pkgstats-now-collects-modules-usage/), la arquitectura y el mirror que está utilizando para el proyecto Arch Linux. Esta información es anónima y no puede ser utilizada para identificar al usuario, sinó que ayudará a los desarrolladores de Arch priorizar sus esfuerzos.

## Instalación

[Instalar](/index.php/Install "Install") el paquete [pkgstats](https://www.archlinux.org/packages/?name=pkgstats).

## Uso

*pkgstats* está configurado para ejecutarse automáticamente cada semana usando [systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers"). Una vez instalado, se activa después del siguiente reinicio.

Si no desea esperar al ciclo de reinicio, puede hacerlo manualmente [start](/index.php/Start "Start") `pkgstats.timer`.

*pkgstats* También se pueden ejecutar de forma manual: ver `pkgstats -h` para información sobre su uso.

## Resultados y Referencia

Las estadísticas se encuentran disponibles [aquí](https://www.archlinux.de/?page=Statistics).

Usted puede visitar el [hilo oficial](https://bbs.archlinux.org/viewtopic.php?id=105431) para más información.