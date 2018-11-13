**Estado de la traducción**
Este artículo es una traducción de [GNU Radio](/index.php/GNU_Radio "GNU Radio"), revisada por última vez el **2018-10-25**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=GNU_Radio&diff=0&oldid=550988) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [DVB-T](/index.php/DVB-T "DVB-T")
*   [RTL-SDR](/index.php/RTL-SDR "RTL-SDR")

[GNU Radio](http://gnuradio.org/redmine/projects/gnuradio/wiki) es un conjunto de herramientas de desarrollo de software de código abierto y gratuito que proporciona bloques de procesamiento de señales para implementar radios de software. Puede usarse con hardware de RF externo de bajo coste y fácilmente disponible para crear radios definidos por software, o sin hardware en un entorno de semi-simulación. Es ampliamente utilizado en entornos aficionados, académicos y comerciales para apoyar tanto la investigación de comunicaciones inalámbricas como los sistemas de radio del mundo real.

## Contents

*   [1 Paquetes](#Paquetes)
*   [2 Solución de problemas](#Solución_de_problemas)
    *   [2.1 GetSize() doesn't work without window](#GetSize()_doesn't_work_without_window)
    *   [2.2 TypeError: in method 'source_sptr_set_gain_mode', argument 2 of type 'bool'](#TypeError:_in_method_'source_sptr_set_gain_mode',_argument_2_of_type_'bool')

## Paquetes

La última versión estable de GNU Radio se puede instalar con [gnuradio](https://www.archlinux.org/packages/?name=gnuradio) desde los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").

La última tecnología es [gnuradio-git](https://aur.archlinux.org/packages/gnuradio-git/) disponible en el [AUR](/index.php/AUR "AUR"), y en algunos casos puede que sea necesario construir VOLK por separado de [libvolk-git](https://aur.archlinux.org/packages/libvolk-git/).

Si desea `gnuradio-companion`, simplemente instale el paquete [gnuradio-companion](https://www.archlinux.org/packages/?name=gnuradio-companion) que instalará GNU Radio así como algunos paquetes adicionales necesarios.

Otro paquete popular es [gnuradio-osmosdr](https://www.archlinux.org/packages/?name=gnuradio-osmosdr), que proporciona los bloques fuente GRC para muchos de los dispositivos SDR populares (Funcube Dongle, [RTL-SDR](/index.php/RTL-SDR "RTL-SDR"), USRP, OsmoSDR, BladeRF y HackRF).

## Solución de problemas

### GetSize() doesn't work without window

Si se producen errores de este tipo al ejecutar grafos de flujo, asegúrese de que esté instalada la dependencia opcional [python2-opengl](https://www.archlinux.org/packages/?name=python2-opengl).

Este problema debería ser arreglado en la próxima versión de GNU Radio. [[1]](https://bbs.archlinux.org/viewtopic.php?id=182732)

### TypeError: in method 'source_sptr_set_gain_mode', argument 2 of type 'bool'

Cuando utilice una fuente RTL-SDR (osmocom), es posible que vea este error. La solución es establecer manualmente el Modo Ganancia (Gain Mode) a `True` o `False`.