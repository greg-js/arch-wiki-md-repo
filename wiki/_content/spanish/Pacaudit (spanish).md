**Estado de la traducción**
Este artículo es una traducción de [Pacaudit](/index.php/Pacaudit "Pacaudit"), revisada por última vez el **2019-02-11**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Pacaudit&diff=0&oldid=566381) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[pacaudit](https://aur.archlinux.org/packages/pacaudit/) audita los paquetes instalados en Arch Linux contra las vulnerabilidades conocidas que se encuentran listadas en [https://security.archlinux.org](https://security.archlinux.org).

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [pacaudit](https://aur.archlinux.org/packages/pacaudit/).

## Utilización

Para iniciar [pacaudit](https://aur.archlinux.org/packages/pacaudit/), ejecute la orden

```
$ pacaudit

```

Para mostrar todos los paquetes vulnerables por nombre y la suma de todos los paquetes vulnerables, ejecute

```
$ pacaudit -v

```

Para mostrar todos los paquetes vulnerables por nombre, con CVE, gravedad y la suma de todos los paquetes vulnerables, ejecute

```
$ pacaudit -n

```

Mostrará "OK" si no se instalaron paquetes vulnerables, "WARNING" si no se instaló ningún paquete vulnerable con gravedad ALTA o superior y "CRITICAL" en el resto de casos.

## Desarrollo

Por favor, reporte bugs, solicite características y estrellas en Github: [https://github.com/steffenfritz/pacaudit](https://github.com/steffenfritz/pacaudit).