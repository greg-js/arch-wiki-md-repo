**Estado de la traducción:** este artículo es una versión traducida de [Freenet](/index.php/Freenet "Freenet"). Fecha de la última traducción/revisión: **2018-09-29**. Puede ayudar a actualizar la traducción, si advierte que la versión inglesa ha cambiado: [ver cambios](https://wiki.archlinux.org/index.php?title=Freenet&diff=0&oldid=544969).

[Freenet](http://freenetproject.org/) es un programa libre y de código abierto que tiene como objetivo proporcionar el anonimato y la libertad de expresión a través de una red punto-a-punto descentralizada. Freenet permite a sus usuarios compartir archivos de forma anónima, publicar freesites sin miedo a la censura y más. Los datos se cifran y enrutan a través de múltiples nodos, lo que hace casi imposible identificar quién solicitó la información y cuál es su contenido.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Configuración](#Configuraci.C3.B3n)
    *   [2.1 Asistente](#Asistente)
    *   [2.2 Configuración manual](#Configuraci.C3.B3n_manual)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [freenet](https://aur.archlinux.org/packages/freenet/).

[Inicie/active](/index.php/Start/enable_(Espa%C3%B1ol) "Start/enable (Español)") `freenet.service`.

## Configuración

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