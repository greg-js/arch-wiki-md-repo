**Estado de la traducción**
Este artículo es una traducción de [Hashcat](/index.php/Hashcat "Hashcat"), revisada por última vez el **2019-11-07**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Hashcat&diff=0&oldid=587497) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[Hashcat](https://en.wikipedia.org/wiki/es:Hashcat "wikipedia:es:Hashcat") es una potente utilidad de recuperación de contraseñas hash que es compatible con más de 200 algoritmos hash. Utiliza OpenCL para mejorar el rendimiento.

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [hashcat](https://www.archlinux.org/packages/?name=hashcat).

Hashcat no puede funcionar sin [OpenCL](/index.php/OpenCL "OpenCL"), por lo que necesita instalar el paquete [GPGPU#OpenCL Runtime](/index.php/GPGPU#OpenCL_Runtime "GPGPU") para su CPU o GPU.

## Utilización

Para obtener la contraseña de *archivo_hash* con *tipo_hash* utilizando *archivo_diccionario*:

```
hashcat -m *tipo_hash* *archivo_hash* *archivo_diccionario*

```

Puede encontrar más ejemplos y detalles de uso en la [wiki de Hashcat](https://hashcat.net/wiki/).

## Véase también

*   [Sitio web oficial](https://hashcat.net/hashcat/)