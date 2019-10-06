**Estado de la traducción**
Este artículo es una traducción de [Hamachi](/index.php/Hamachi "Hamachi"), revisada por última vez el **2019-10-05**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Hamachi&diff=0&oldid=584435) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[Hamachi](https://www.vpn.net/) es un software VPN comercial propiedad de LogMeIn, Inc. Con Hamachi puede organizar dos o más equipos con conexión a Internet en su propia red virtual para una comunicación segura directa.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Configuración](#Configuración)
    *   [2.1 Utilizar la herramienta de línea de órdenes «hamachi» como usuario normal](#Utilizar_la_herramienta_de_línea_de_órdenes_«hamachi»_como_usuario_normal)
    *   [2.2 Establecer automáticamente un apodo personalizado](#Establecer_automáticamente_un_apodo_personalizado)
*   [3 Ejecutar Hamachi](#Ejecutar_Hamachi)
    *   [3.1 Systemd](#Systemd)
*   [4 Interfaz gráfica](#Interfaz_gráfica)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [logmein-hamachi](https://aur.archlinux.org/packages/logmein-hamachi/).

## Configuración

Hamachi está configurado en `/var/lib/logmein-hamachi/h2-engine-override.cfg` (cree ese archivo si no existe). Desafortunadamente, no es fácil encontrar una lista completa de posibles opciones de configuración, así que he aquí algunas de las puede usar.

### Utilizar la herramienta de línea de órdenes «hamachi» como usuario normal

Para utilizar la herramienta de línea de órdenes de `hamachi` como usuario normal, añada la siguiente línea al archivo de configuración:

```
Ipc.User sunombredeusuario

```

### Establecer automáticamente un apodo personalizado

Normalmente, Hamachi usa el nombre del equipo de su sistema como el apodo que verán otros usuarios de Hamachi. Si desea establecer automáticamente un apodo personalizado cada vez que se inicia Hamachi, añada la siguiente línea al archivo de configuración:

```
Setup.AutoNick suapododeequipo

```

También puede establecer manualmente un apodo con la herramienta de línea de órdenes de `hamachi`:

```
# hamachi set-nick YourNicknameHere

```

Sin embargo, esto debe hacerse cada vez que Hamachi se (re)inicia, por lo que si desea utilizar siempre el mismo apodo, probablemente sea más fácil configurarlo automáticamente (como se explicó anteriormente).

## Ejecutar Hamachi

[Inicie](/index.php/Start_(Espa%C3%B1ol) "Start (Español)") `logmein-hamachi.service`.

Ahora tendrá un montón de órdenes a su disposición. Estas no están en un orden particular y se explican por sí mismas.

```
$ hamachi set-nick bob
$ hamachi login
$ hamachi create my-net secretpassword
$ hamachi do-join my-net
$ hamachi go-online my-net
$ hamachi list
$ hamachi go-offline my-net

```

Para obtener una lista de todos las órdenes, ejecute:

```
$ hamachi ?

```

**Nota:** asegúrese de cambiar el estado de los canales en los que se encuentra «en línea» si desea realizar cualquier acción de red en los equipos presentes.

### Systemd

El paquete [logmein-hamachi](https://aur.archlinux.org/packages/logmein-hamachi/) también incluye un pequeño demonio [systemd (Español)](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)").

Si lo desea, puede configurar Hamachi para que se inicie en cada arranque con Systemd [activando](/index.php/Enabling "Enabling") `logmein-hamachi.service`.

## Interfaz gráfica

Los siguientes frontends de interfaz gráfica de usuario para Hamachi están disponibles en AUR:

*   [haguichi](https://aur.archlinux.org/packages/haguichi/) (Gtk3, Vala)
*   [quamachi](https://aur.archlinux.org/packages/quamachi/) (Qt4, Python)