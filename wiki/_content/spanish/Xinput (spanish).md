**Estado de la traducción**
Este artículo es una traducción de [Xinput](/index.php/Xinput "Xinput"), revisada por última vez el **2018-11-27**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Xinput&diff=0&oldid=550564) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Xorg](/index.php/Xorg_(Espa%C3%B1ol) "Xorg (Español)")
*   [libinput](/index.php/Libinput_(Espa%C3%B1ol) "Libinput (Español)")

*xinput* es una utilidad para configurar y probar dispositivos de entrada de X, como ratones, teclados y paneles táctiles. Se encuentra en el paquete [xorg-xinput](https://www.archlinux.org/packages/?name=xorg-xinput).

## Listar los dispositivos

Para enumerar qué dispositivos xinput se encuentran disponibles, utilize:

 `$ xinput list` 
```
⎡ Virtual core pointer                    	id=2	[master pointer  (3)]
⎜   ↳ Virtual core XTEST pointer              	id=4	[slave  pointer  (2)]
⎜   ↳ SYNA7813:00 06CB:16DB                   	id=13	[slave  pointer  (2)]
⎜   ↳ ETPS/2 Elantech Touchpad                	id=15	[slave  pointer  (2)]
⎜   ↳ dougav’s mouse                        	id=9	[slave  pointer  (2)]
⎣ Virtual core keyboard                   	id=3	[master keyboard (2)]
    ↳ Virtual core XTEST keyboard             	id=5	[slave  keyboard (3)]
    ↳ Power Button                            	id=6	[slave  keyboard (3)]
    ↳ Video Bus                               	id=7	[slave  keyboard (3)]
    ↳ Power Button                            	id=8	[slave  keyboard (3)]
    ↳ Clavier de Dawud W Vong                 	id=10	[slave  keyboard (3)]
    ↳ HP Wide Vision HD                       	id=11	[slave  keyboard (3)]
    ↳ Intel Virtual Button driver             	id=12	[slave  keyboard (3)]
    ↳ AT Translated Set 2 keyboard            	id=14	[slave  keyboard (3)]
    ↳ HP WMI hotkeys                          	id=16	[slave  keyboard (3)]
    ↳ HP Wireless hotkeys                     	id=17	[slave  keyboard (3)]
```

## Ejemplos de utilización

He aquí algunas de las formas en que se puede utilizar *xinput*.

### Eliminar el botón central y derecho del ratón

```
$ xinput set-button-map 'dougav’s mouse' 1 1 1

```