<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Explorando dispositivos de Android](#Explorando_dispositivos_de_Android)
*   [2 Desarrollo en Android](#Desarrollo_en_Android)
    *   [2.1 Android Studio](#Android_Studio)
    *   [2.2 Instalación del SDK](#Instalación_del_SDK)
        *   [2.2.1 Emulator de Android](#Emulator_de_Android)
        *   [2.2.2 Otros paquetes de SDK en AUR](#Otros_paquetes_de_SDK_en_AUR)
        *   [2.2.3 Cambiar el dueño de /opt/android-sdk](#Cambiar_el_dueño_de_/opt/android-sdk)
*   [3 Compilación](#Compilación)
    *   [3.1 Paquetes requeridos](#Paquetes_requeridos)
    *   [3.2 Kit de desarrollo de Java](#Kit_de_desarrollo_de_Java)
    *   [3.3 Configurando el entorno de Compilación](#Configurando_el_entorno_de_Compilación)
    *   [3.4 Descarga de código fuente](#Descarga_de_código_fuente)
    *   [3.5 Compilación del código](#Compilación_del_código)
    *   [3.6 Probando la construcción](#Probando_la_construcción)
    *   [3.7 Crear una imagen para instalar](#Crear_una_imagen_para_instalar)
*   [4 Instalación](#Instalación)
    *   [4.1 Fastboot](#Fastboot)
    *   [4.2 Dispositivos Samsung](#Dispositivos_Samsung)
        *   [4.2.1 Heimdall](#Heimdall)
        *   [4.2.2 Odin con Virtualbox](#Odin_con_Virtualbox)

## Explorando dispositivos de Android

Cuando un dispositivo moderno de Android se conecta a un computador con el cable USB, se puede usar el [Protocolo de transferencia de medios](/index.php/Media_Transfer_Protocol "Media Transfer Protocol") (MTP en ingles) para transferir archivos y el [#Puente de depurado de Android](#Puente_de_depurado_de_Android) (ADB en ingles) para depurar.

Archivos pueden ser transferidos con varios protocolos ([SSH](/index.php/Secure_Shell_(Espa%C3%B1ol) "Secure Shell (Español)"), [FTP](/index.php/Category:File_Transfer_Protocol_(Espa%C3%B1ol) "Category:File Transfer Protocol (Español)"), [Samba](/index.php/Samba_(Espa%C3%B1ol) "Samba (Español)"), HTTP). Solo es necesario establecer un servidor y un cliente, mediante aplicaciones Android puede convertirse en uno de estos.

## Desarrollo en Android

Para desarrollar aplicaciones en Android necesita tres requisitos:

*   el componente básico de Android SDK
*   uno o múltiples paquetes de plataforma de Android SDK
*   interfaz de usuario

La interfaz oficial es [#Android Studio](#Android_Studio), la cual contiene su propio gestor de SDK.

### Android Studio

[Android Studio](https://developer.android.com/studio/index.html) es el entorno oficial de desarrollo de Android basado en [IntelliJ Idea](https://www.jetbrains.com/idea/). Contiene herramientas de desarrollo y depuración de Android integradas.

Se puede [instalar](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") con el paquete [android-studio](https://aur.archlinux.org/packages/android-studio/).

**Nota:**

*   Asegurese de [establecer su ambiente de java](/index.php/Java_(Espa%C3%B1ol)#Cambiar_el_ambiente_de_Java "Java (Español)") de lo contrario Android Studio no arrancara.
*   Si Android Studio muestra una ventana en blanco, intente [exportar](/index.php/Environment_variables_(Espa%C3%B1ol) "Environment variables (Español)") `_JAVA_AWT_WM_NONREPARENTING=1`, vea [issue #57675](https://code.google.com/p/android/issues/detail?id=57675).

Normalmente, aplicaciones son construidas en el GUI de Android Studio. Para construir desde una terminal de comandos usando por ejemplo `./gradlew assembleDebug`), agregue lo siguiente a su archivo `~/.bashrc`:

```
export ANDROID_SDK_ROOT=/opt/android-sdk

```

### Instalación del SDK

Los paquetes del SDK de Android pueden ser instalados directamente usando [#Android Studio](#Android_Studio) y su [gestionador de SDK](https://developer.android.com/studio/intro/update#sdk-manager), también es posible usar la herramienta de terminal [sdkmanager](https://developer.android.com/studio/command-line/sdkmanager) (la cual hace parte de las herramientas del SDK de Android). Algunos paquetes del SDK también estan disponibles en el [AUR](/index.php/AUR_(Espa%C3%B1ol) "AUR (Español)").

Los [paquetes del SDK requeridos](https://developer.android.com/studio/intro/update#recommended) son:

| Paquete Android SDK | Estilo del SDK | Paquete en AUR | Dummy en AUR | Herramientas de terminal |
| [SDK Tools](https://developer.android.com/studio/releases/sdk-tools) | tools | [android-sdk](https://aur.archlinux.org/packages/android-sdk/) | [android-sdk-dummy](https://aur.archlinux.org/packages/android-sdk-dummy/) | sdkmanager, apkanalizer, avdmanager, mksdcard, proguard |
| [SDK Build-Tools](https://developer.android.com/studio/releases/build-tools) | build-tools;*version* | [android-sdk-build-tools](https://aur.archlinux.org/packages/android-sdk-build-tools/) | [android-sdk-build-tools-dummy](https://aur.archlinux.org/packages/android-sdk-build-tools-dummy/) | apksigner, zipalign |
| [SDK Platform-Tools](https://developer.android.com/studio/releases/platform-tools) | platform-tools | [android-sdk-platform-tools](https://aur.archlinux.org/packages/android-sdk-platform-tools/) | [android-sdk-platform-tools-dummy](https://aur.archlinux.org/packages/android-sdk-platform-tools-dummy/) | [adb](/index.php/Adb "Adb"), [#fastboot](#Fastboot) y systrace |
| [SDK Platform](https://developer.android.com/studio/releases/platforms) | platforms;android-*level* | [android-platform](https://aur.archlinux.org/packages/android-platform/), [older versions](https://aur.archlinux.org/packages/?K=android-platform-) | No se necesita |

El paquete [android-tools](https://www.archlinux.org/packages/?name=android-tools) proporciona [adb](/index.php/Adb "Adb"), [#fastboot](#Fastboot), `e2fsdroid`, `mke2fs.android`, `mkbootimg` y `ext2simg`.

**Nota:**  

*   El SDK de Android contiene binarios de 32-bit, debe habilitar el repositorio [multilib](/index.php/Multilib_(Espa%C3%B1ol) "Multilib (Español)"). De lo contrario encontrara un error `error: target not found: lib32-*`.
*   Si ha decidido instalar los paquetes con el gestor interno de Android Studio, instale los paquetes en la columna *Dummy en AUR* para instalar los programas requeridos.

#### Emulator de Android

El [Emulador de Android](https://developer.android.com/studio/run/emulator) esta disponible como el paquete de SDK `emulator` o el paquete [android-emulator](https://aur.archlinux.org/packages/android-emulator/). Un paquete dummy [android-emulator-dummy](https://aur.archlinux.org/packages/android-emulator-dummy/) también.

Para iniciar el emulador de Android es necesario tener una imagen de sistema de Intel o ARM. Se pueden instalar desde [AUR](/index.php/AUR_(Espa%C3%B1ol) "AUR (Español)") [[1]](https://aur.archlinux.org/packages/?K=android-+system+image), con `sdkmanager` o usando el [gestor AVD](https://developer.android.com/studio/run/managing-avds) en Android Studio.

#### Otros paquetes de SDK en AUR

La [Libreria de Soporte de Android](https://developer.android.com/topic/libraries/support-library/) esta disponible desde el repositorio [Maven de Google](https://developer.android.com/studio/build/dependencies#google-maven). También lo puede instalar localmente a traves del paquete de SDK `extras;android;m2repository`, disponible en [android-support-repository](https://aur.archlinux.org/packages/android-support-repository/).

#### Cambiar el dueño de /opt/android-sdk

El SDK de Android será instalado en `/opt/android-sdk/`. Esta carpeta tiene permisos de root, así que debe ejecutar el gestor de SDK como root, de lo contrario no podrá modificar nada en esta carpeta. Si desea usar su usuario regular, es necesario crear el grupo sdkusers:

```
# groupadd sdkusers

```

Agregue su usuario a este grupo:

```
# gpasswd -a <ususario> sdkusers

```

Cambie el grupo de la carpeta:

```
# chown -R :sdkusers /opt/android-sdk/

```

Cambie los permisos de la carpeta para que el usuario agregado a este grupo pueda hacer cambios:

```
# chmod -R g+w /opt/android-sdk/

```

Reinicie sesión o como su <usuario> ejecute en una terminal:

```
$ newgrp sdkusers

```

**Nota:** Como una alternativa a la instalación global con los paquetes de [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)"), el SDK pude ser instalado en la carpeta raíz del usuario con las siguientes [instrucciones](https://developer.android.com/sdk/index.html)(en ingles). También se pueden usar los paquetes android-*-dummy del [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)") para manejar dependencias del sistema.

## Compilación

Nótese que estas instrucciones están basadas en [instrucciones oficiales de AOSP](https://source.android.com/source/building). Otros sistemas derivados como LineageOS normalmente requieren mas pasos.

### Paquetes requeridos

Para construir cualquier versión de Android, es necesario instalar lo siguiente:

*   [lib32-gcc-libs](https://www.archlinux.org/packages/?name=lib32-gcc-libs) [git](https://www.archlinux.org/packages/?name=git) [gnupg](https://www.archlinux.org/packages/?name=gnupg) [flex](https://www.archlinux.org/packages/?name=flex) [bison](https://www.archlinux.org/packages/?name=bison) [gperf](https://www.archlinux.org/packages/?name=gperf) [sdl](https://www.archlinux.org/packages/?name=sdl) [wxgtk2](https://www.archlinux.org/packages/?name=wxgtk2) [squashfs-tools](https://www.archlinux.org/packages/?name=squashfs-tools) [curl](https://www.archlinux.org/packages/?name=curl) [ncurses](https://www.archlinux.org/packages/?name=ncurses) [zlib](https://www.archlinux.org/packages/?name=zlib) [schedtool](https://www.archlinux.org/packages/?name=schedtool) [perl-switch](https://www.archlinux.org/packages/?name=perl-switch) [zip](https://www.archlinux.org/packages/?name=zip) [unzip](https://www.archlinux.org/packages/?name=unzip) [libxslt](https://www.archlinux.org/packages/?name=libxslt) [python2-virtualenv](https://www.archlinux.org/packages/?name=python2-virtualenv) [bc](https://www.archlinux.org/packages/?name=bc) [rsync](https://www.archlinux.org/packages/?name=rsync) [ncurses5-compat-libs](https://aur.archlinux.org/packages/ncurses5-compat-libs/) [lib32-zlib](https://www.archlinux.org/packages/?name=lib32-zlib) [lib32-ncurses](https://www.archlinux.org/packages/?name=lib32-ncurses) [lib32-readline](https://www.archlinux.org/packages/?name=lib32-readline) [lib32-ncurses5-compat-libs](https://aur.archlinux.org/packages/lib32-ncurses5-compat-libs/)

El meta paquete [aosp-devel](https://aur.archlinux.org/packages/aosp-devel/) provee todos estos paquetes para una instalación mas simple.

Adicionalmente, LineageOS requiere los siguientes paquetes: [xml2](https://aur.archlinux.org/packages/xml2/), [lzop](https://www.archlinux.org/packages/?name=lzop), [pngcrush](https://www.archlinux.org/packages/?name=pngcrush), [imagemagick](https://www.archlinux.org/packages/?name=imagemagick)

Estos pueden ser instalados con el meta paquete [lineageos-devel](https://aur.archlinux.org/packages/lineageos-devel/).

### Kit de desarrollo de Java

La [versión JDK requerida](https://source.android.com/source/requirements) depende de la versión de Android que se quiere construir:

*   Para Android 7 y 8 (Nougat y Oreo), OpenJDK 8 es necesario, el cual esta disponible en el paquete [jdk8-openjdk](https://www.archlinux.org/packages/?name=jdk8-openjdk).
*   Para Android 5 y 6 (Lollipop y Marshmallow), OpenJDK 7 es necesario, el cual esta disponible en el paquete [jdk7-openjdk](https://www.archlinux.org/packages/?name=jdk7-openjdk).

Versiones anterires requieren **Oracle JDK** instalado en el sistema de construcción. Estas **no funcionaran** con OpenJDK.

*   Para Android 2.3 a 4.4 (Gingerbread a KitKat), Java 6 es necesario, el cual esta disponible en el paquete [jdk6](https://aur.archlinux.org/packages/jdk6/).
*   Para Android 1.5 a 2.2 (Cupcake a Froyo), Java 5 es necesario, el cual esta disponible en el paquete [jdk5](https://aur.archlinux.org/packages/jdk5/).

**Nota:** Android espera que Java este en `/usr/lib/jvm/java-*versión*-openjdk-amd64`.

Para evitar este requisito, la variable de entorno JAVA_HOME debe ser establecida:

```
$ export JAVA_HOME=/usr/lib/jvm/java-*versión*-openjdk

```
Este cambio solo sera valido para la sesión actual en esa terminal.

### Configurando el entorno de Compilación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [repo](https://www.archlinux.org/packages/?name=repo).

Cree un directorio para la construcción:

```
$ mkdir ~/android
$ cd ~/android

```

El proceso de construcción de Android espera que `python` sea python2\. Cree un entorno virtual con python2 y activelo:

```
$ virtualenv2 venv
$ source venv/bin/activate

```

**Nota:**

*   Esta activación solo es valida por la sesión actual en la terminal. El entorno virtual sera guardado en el directorio `venv`.
*   Durante la construcción es posible encontrar errores de módulos que no existen en python. Una solución es crear enlaces simbolicos de `/usr/lib/python2.7/*` a `~/android/venv/lib/python2.7/`, cambie el directorio *android* si su directorio de construcción es diferente.

Ejemplo:

```
$ ln -s /usr/lib/python2.7/* ~/android/venv/lib/python2.7/

```

o, asumiendo que el directorio de construcción es Data/Android_Build:

```
$ ln -s /usr/lib/python2.7/* /Data/Android_Build/venv/lib/python2.7/

```

### Descarga de código fuente

Esto clonara los repositorio. El usuario '*solo* debe hacer esto la primera vez que se quiere construir Android, o si se quieren cambiar ramas.

*   El comando `repo` tiene la opción `-j` que funciona similarmente a la usada en `make`. Esta controla el numero de descargas simultaneas, se debe ajustar este valor dependiendo en la velocidad de descarga disponible.

*   Es necesario especificar una **rama** (lanzamiento de Android) con la opción `-b`. Si no se especifica ninguna rama, se obtendrá la **rama maestra**.

```
 $ repo init -u https://android.googlesource.com/platform/manifest -b master
 $ repo sync -j4

```

**Nota:** Para disminuir tiempos de sincronización aun mas, se puede usar la opción `-c` de tal manera:
```
$ repo sync -j8 -c

```

La opción `-c` solo sincronizara la rama especificada en el manifiesto, lo cual es definida por la rama seleccionada con la opción `-b`, o la rama por defecto que el mantenedor eligió.

Es necesario esperar un largo tiempo. Solo el código sin compilar, junto con los directorios `.repo` y `.git` son mas de 10GB. Desde Android 6.0.1, el código fuente completo es alrededor de 40GB.

**Nota:** Si desea actualizar su copia local del código de Android, en algún momento en el futuro, simplemente entre al directorio de construcción, active el entorno virtual y re-sincronice:
```
$ repo sync

```

### Compilación del código

Esto debe funcionar para la construcción de AOSP:

```
$ source build/envsetup.sh
$ lunch full-eng
$ make -j4

```

Si se ejecuta **lunch** sin argumentos, preguntara que tipo de construcción se debe crear. Use la opción `-j` con un numero entre uno y el doble de núcleos disponibles.

La construcción va a tomar bastante tiempo.

**Nota:**

*   Asegúrese de tener suficiente RAM. Android usara bastante el directorio `/tmp`. Por defecto la partición donde el directorio `/tmp` esta montado debe ser la mitad del RAM disponible. Si esta se llena totalmente la construcción fallara. 4GB de RAM o más es recomendable. Alternativamente, se puede remover tmpfs del [fstab](/index.php/Fstab_(Espa%C3%B1ol) "Fstab (Español)").
*   Por ejemplo en una maquina dual-E5520 (2 CPUs, 4 núcleos por CPU, 2 hilos por nucleo), la construcción mas rápida se hace con comandos entre `make -j16` and `make -j32`.

### Probando la construcción

Cuando termine, ejecute/compruebe la imagen final:

```
$ emulator

```

### Crear una imagen para instalar

Para crear una imagen que puede ser instalada es necesario ejecutar:

```
make -j8 updatepackage

```

Esto creara una imagen dentro de un archivo zip en el directorio `**out/target/product/hammerhead**`, asumiendo que *hammerhead* es su dispositivo. Este archivo zip ya se puede instalar.

## Instalación

En caso que se desee instalar el sistema original en su dispositivo después de probar diferentes ROMs, busque las instrucciones para su dispositivo en el [foro de XDA](http://forum.xda-developers.com/).

### Fastboot

Fastboot así como [ADB](/index.php/Android_Debug_Bridge_(Espa%C3%B1ol) "Android Debug Bridge (Español)") están incluidos en el paquete [android-tools](https://www.archlinux.org/packages/?name=android-tools).

**Nota:** Restaurar el firmware de un dispositivo con `fastboot` puede ser complicado, una buena idea es revisar los foros de los [desarrolladores de XDA](http://www.xda-developers.com/) por un firmware original, el cual normalmente es un archivo `*.zip`. Dentro de este generalmente se encuentran los archivos del firmware y un script `flash-all.sh`. Por ejemplo, para el [Google Nexus](https://developers.google.com/android/nexus/images) o para el [OnePlus One en XDA](http://forum.xda-developers.com/oneplus-one/general/guide-return-opo-to-100-stock-t2826541).

### Dispositivos Samsung

Los dispositivos producidos por Samsung no se pueden (re-)instalar usando `fastboot`. La alternativa es usar **Heimdall** o **Odin**, usando una maquina virtual con Windows:

#### Heimdall

[Heimdall](http://glassechidna.com.au/heimdall/) es un set de herramientas que funciona en varias plataformas de codigo abierto usado para instalar firmware, también conocido como ROMs en dispositivos Samsung. Puede ser instalado con el paquete [heimdall](https://www.archlinux.org/packages/?name=heimdall).

Las instrucciones de instalacion se encuentran en [repositorio de GitLab](https://gitlab.com/BenjaminDobell/Heimdall/tree/master/Linux) o en los [foros de XDA](http://forum.xda-developers.com/showthread.php?t=1922461).

#### Odin con Virtualbox

**Nota:** Esta sección solo cubre la preparación y **no** la instalación. Busque en los [foros de XDA](http://www.xda-developers.com) para encontrar las indicaciones exactas para su dispositivo. Por ejemplo el [Samsung Galaxy S4](https://forum.xda-developers.com/showthread.php?t=2265477).

Es posible restaurar el [firmware de Android](http://www.sammobile.com/firmwares/) en el dispositivo de Samsung usando [Odin](http://odindownload.com/), pero dentro de una maquina virtual, en este caso usando [VirtualBox](/index.php/VirtualBox_(Espa%C3%B1ol) "VirtualBox (Español)").

Preparacion del anfitrion Arch Linux:

1.  Instale el paquete [virtualbox](https://www.archlinux.org/packages/?name=virtualbox) junto con el [paquete de extensiones](/index.php/VirtualBox_(Espa%C3%B1ol)#Paquete_de_extensiones "VirtualBox (Español)") y [adiciones de huésped](/index.php/VirtualBox_(Espa%C3%B1ol)#Disco_de_«Guest_Additions» "VirtualBox (Español)").
2.  Instale su versión preferida, pero compatible con Odin de Windows.
3.  En la configuracion de VirtualBox de su sistema de Windows, navegue a *USB*, y asegúrese que la opción **USB 2.0 (EHCI)** esta habilitada.
4.  Cuando la maquina virtual inicie, vaya al menú de *dispositivos > USB* y seleccione su dispositivo Samsung en la lista. El cual esta conectado a su computadora via USB

Preparación del sistema huésped de Windows:

1.  Instale los [controladores de Samsung](http://androidxda.com/download-samsung-usb-drivers).
2.  Instale [Odin](http://odindownload.com/).
3.  Descargue el [firmware de Samsung (Android)](http://www.sammobile.com/firmwares/) para su dispositivo.

Compruebe que su configuración funciona:

1.  Ponga su dispositivo en modo *Download* y conéctelo a su computadora con linux.
2.  En la ventana de la maquina virtual seleccione su dispositivo *dispositivos > USB > ...Samsung...*
3.  Inicie Odin en la maquina virtual, en la casilla blanca en la parte baja-izquierda de la ventana se debe leer algo similar a:

```
<ID:0/003> Added!!

```

lo cual indica que su dispositivo es visible para Odin y para el sistema operativo de Windows, ahora esta listo para instalar.