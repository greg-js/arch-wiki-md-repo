**Estado de la traducción**
Este artículo es una traducción de [ASUS Zenbook UX390](/index.php/ASUS_Zenbook_UX390 "ASUS Zenbook UX390"), revisada por última vez el **2019-02-17**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=ASUS_Zenbook_UX390&diff=0&oldid=566831) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

## El incremento de volumen no funciona

Debido al hardware de audio con "sonido envolvente" del portátil UX390, es necesario ajustar un archivo de configuración de PulseAudio para que el incremento de volumen funcione. De lo contrario, el volumen estará o a tope o silenciado, a pesar de que parezca que se incrementa.

Edite la configuración de la ruta de salida analógica y agregue las secciones `Element Master` y `Element LFE` que se muestran a continuación.

 `/usr/share/pulseaudio/alsa-mixer/paths/analog-output.conf.common` 
```
[Element Master]
switch = mute
volume = ignore

[Element PCM]
switch = mute
volume = merge
override-map.1 = all
override-map.2 = all-left,all-right

[Element LFE]
switch = mute
volume = ignore
```

Después, reinicie PulseAudio y el incremento de volumen debería funcionar.

## El audio de la toma de auriculares siempre está silenciado

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils). Ejecute `alsamixer`, seleccione la tarjeta de sonido "HDA Intel PCH" y ajuste el control deslizante de "Auriculares" a su gusto. Para hacer el cambio permanente, es posible que tenga que ejecutar `sudo alsactl store`.