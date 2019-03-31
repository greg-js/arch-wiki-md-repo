**Estado de la traducción**
Este artículo es una traducción de [WPS_Office](/index.php/WPS_Office "WPS Office"), revisada por última vez el **2019-03-26**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=WPS_Office&diff=0&oldid=569889) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[WPS Office para Linux](https://www.wps.com/linux) es una alternativa eficiente, estable y compatible para Microsoft Office con interfaz de usuario moderna que admite transferencia de archivos entre dispositivos, copia de seguridad en la nube. La suite contiene Writer, Presentation y Spreadsheet.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Ayudas de idioma](#Ayudas_de_idioma)
    *   [2.1 Idioma de la interface](#Idioma_de_la_interface)
    *   [2.2 Correción ortográfica](#Correción_ortográfica)
*   [3 Tema](#Tema)
*   [4 Solución de problemas](#Solución_de_problemas)
    *   [4.1 Cuál es la órden para iniciar WPS Office](#Cuál_es_la_órden_para_iniciar_WPS_Office)
    *   [4.2 Las fórmulas no se muestran de forma normal](#Las_fórmulas_no_se_muestran_de_forma_normal)
    *   [4.3 Archivo de Microsoft Office en KDE es reconozido como Zip](#Archivo_de_Microsoft_Office_en_KDE_es_reconozido_como_Zip)
    *   [4.4 Framework de método de introducción Fcitx no puede introducir en WPS](#Framework_de_método_de_introducción_Fcitx_no_puede_introducir_en_WPS)
*   [5 Véase también](#Véase_también)

## Instalación

Instale [wps-office](https://aur.archlinux.org/packages/wps-office/) de [AUR](/index.php/AUR "AUR")

**Nota:**

*   opcionalmente puede instalar las fuentes que necesita WPS: [ttf-wps-fonts](https://aur.archlinux.org/packages/ttf-wps-fonts/)

## Ayudas de idioma

### Idioma de la interface

Para cambiar el idioma de la interface de WPS puede instalar [wps-office-mui-fr-fr](https://aur.archlinux.org/packages/wps-office-mui-fr-fr/) para Francés, [wps-office-mui-ja-jp](https://aur.archlinux.org/packages/wps-office-mui-ja-jp/) para Japonés, etc. Después establezca su idioma al seleccionar *Review->Spell Check->Set Language* escoger su idioma y reiniciar WPS.

### Correción ortográfica

Para la correción ortográfica, necesita instalar [wps-office-extension-german-dictionary](https://aur.archlinux.org/packages/wps-office-extension-german-dictionary/) para Alemán, [wps-office-extension-french-dictionary](https://aur.archlinux.org/packages/wps-office-extension-french-dictionary/) para Francés, etc. Deespués, personalize la correción ortográfica al seleccionar *Tool -> Options -> Language -> choose*, escoger su idioma y reiniciar WPS.

## Tema

## Solución de problemas

### Cuál es la órden para iniciar WPS Office

wps,et,wpp es el comando para iniciar WPS Writer, WPS Spreadsheet y WPS Presentation

### Las fórmulas no se muestran de forma normal

El desplegado de la mayoría de las fórmulas Matemáticas necesitan las fuentes que se muestran a continuación:

```
symbol.ttf webdings.ttf wingding.ttf wingdng2.ttf wingdng3.ttf monotypesorts.ttf MTExtra.ttf

```

[ttf-wps-fonts](https://aur.archlinux.org/packages/ttf-wps-fonts/) en [AUR](/index.php/AUR "AUR") contiene todas éstas fuentes excepto *monotypesorts.ttf*, puede instarla directamente.

### Archivo de Microsoft Office en KDE es reconozido como Zip

Después de instalar WPS Office, los archivos de Microsoft Office serán reconocidos como zip, y no se pueden abrir con WPS, puede cambiar éste tipo de reconocimiento al eliminar el archivo mime en */usr/share/packages/*:

```
sudo rm /usr/share/mime/packages/wps-office-*.xml
sudo update-mime-database /usr/share/mime

```

### Framework de método de introducción Fcitx no puede introducir en WPS

Agregue las siguientes líneas a /usr/bin/wps /usr/bin/et /usr/bin/wpp de manera separada para añadir fcitx a Writer, Spreadsheet y Presentation:

```
export XMODIFIERS="@im=fcitx"
export QT_IM_MODULE="fcitx"

```

## Véase también

*   [WPS Office Community](http://wps-community.org/)
*   [WPS For Linux](https://www.wps.com/office/linux/)