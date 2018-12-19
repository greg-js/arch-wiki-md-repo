**Estado de la traducción**
Este artículo es una traducción de [Logitech G300](/index.php/Logitech_G300 "Logitech G300"), revisada por última vez el **2018-12-17**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Logitech_G300&diff=0&oldid=559343) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

## Controladores de la comunidad del G300

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") [ratslap](https://aur.archlinux.org/packages/ratslap/) para obtener los controladores del ratón. Este paquete le permite cambiar los colores, reasignar botones e incluso crear macros personalizados. Después de la instalación, use el binario ratslap para cambiar el ratón.

## Cómo hacer que el G300 funcione correctamente

Esta página de la Wiki le mostrará cómo hacer que su ratón G300 funcione como es deseado.

El G300 es reconocido tanto como un ratón como un teclado por el sistema; puede comprobarlo ejecutando la siguiente orden:

```
xinput list | grep G300

```

Tenemos que deshabilitar el teclado G300 para hacer que funcione correctamente.

He aquí el código:

```
#!/bin/sh
DEVICE_ID=$(xinput list |  grep "Logitech Gaming Mouse G300" | grep keyboard | sed 's/.*id=\([0-9]*\).*/\1/')

if xinput -list-props $DEVICE_ID | grep "Device Enabled" | grep "1$" > /dev/null
then
        xinput set-int-prop $DEVICE_ID "Device Enabled" 8 0
fi

```

Simplemente ejecute el código de arriba para ver si funciona.

También puede pegarlo en su xinitrc.d para que se cargue automáticamente.

## Configurar los botones

El script anterior funciona según lo previsto, pero también deshabilita los botones, dado que deshabilitamos la función de teclado del g300.

Para hacer que el ratón funcione como un ratón y poder utilizar los botones, podemos usar [ratslap](https://aur.archlinux.org/packages/?O=0&K=ratslap) del [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)") para las personalizaciones (los colores y los botones).