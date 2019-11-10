**Estado de la traducción**
Este artículo es una traducción de [Freenet](/index.php/Freenet "Freenet"), revisada por última vez el **2019-11-08**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Freenet&diff=0&oldid=588157) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[Freenet](http://freenetproject.org/) es un programa libre y de código abierto que tiene como objetivo proporcionar el anonimato y la libertad de expresión a través de una red punto-a-punto descentralizada. Freenet permite a sus usuarios compartir archivos de forma anónima, publicar freesites sin miedo a la censura y más. Los datos se cifran y enrutan a través de múltiples nodos, lo que hace casi imposible identificar quién solicitó la información y cuál es su contenido.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Configuración](#Configuración)
    *   [2.1 Asistente](#Asistente)
    *   [2.2 Configuración manual](#Configuración_manual)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [freenet](https://aur.archlinux.org/packages/freenet/).

## Configuración

[Inicie/active](/index.php/Start/enable_(Espa%C3%B1ol) "Start/enable (Español)") el servicio `freenet.service`.

Puede permitir que el asistente le guíe a través de la configuración o póngase manos a la obra configurando Freenet manualmente. Es posible que desee leer sobre [TrueCrypt](/index.php/TrueCrypt "TrueCrypt") o [EncFS](/index.php/EncFS "EncFS") para proteger los datos que compartirá antes de continuar.

### Asistente

Debe visitar la interfaz web de Freenet en [http://127.0.0.1:8888/](http://127.0.0.1:8888/) y asegúrese de seguir cuidadosamente las instrucciones. Utilizar el modo privado de su navegador mientras accede a Freenet es una buena costumbre.

### Configuración manual

La [Wiki de Freenet](http://wiki.freenetproject.org/Main_Page) le será útil si decide configurar las cosas a mano. La configuración manual se realiza editando

```
/opt/freenet/freenet.ini

```

y

```
/opt/freenet/wrapper.conf

```