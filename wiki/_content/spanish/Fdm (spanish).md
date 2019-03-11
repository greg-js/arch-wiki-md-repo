**Estado de la traducción**
Este artículo es una traducción de [Fdm](/index.php/Fdm "Fdm"), revisada por última vez el **2018-10-18**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Fdm&diff=0&oldid=548286) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Alpine](/index.php/Alpine "Alpine")
*   [msmtp](/index.php/Msmtp "Msmtp")
*   [Mutt](/index.php/Mutt_(Espa%C3%B1ol) "Mutt (Español)")
*   [Postfix](/index.php/Postfix_(Espa%C3%B1ol) "Postfix (Español)")
*   [SSMTP](/index.php/SSMTP "SSMTP")

**fdm** (*fetch and deliver mail*), es un programa simple para entregar y filtrar correo. Al compararlo con otras aplicaciones con el mismo propósito muestra que tiene similitudes muy orientadas a los principios de diseño de [Mutt](/index.php/Mutt_(Espa%C3%B1ol) "Mutt (Español)").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Configuración](#Configuración)
    *   [2.1 mbox](#mbox)
    *   [2.2 maildir](#maildir)
    *   [2.3 Configuración final](#Configuración_final)
*   [3 Pruebas](#Pruebas)
*   [4 Utilización extendida](#Utilización_extendida)
    *   [4.1 Filtrado adicional](#Filtrado_adicional)
    *   [4.2 Automatización con cron](#Automatización_con_cron)
*   [5 Véase también](#Véase_también)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [fdm](https://www.archlinux.org/packages/?name=fdm).

## Configuración

*fdm* admite el probado formato mbox junto con la nueva especificación maildir.

### mbox

Alpine utiliza el formato mbox, por lo que se necesita configurar algunos archivos.

```
$ cd
$ mkdir mail
$ touch mail/INBOX .fdm.conf 
$ chmod 600 .fdm.conf mail/INBOX

```

### maildir

Mutt prefiere un directorio de correo capitulado y puede usar el formato maildir. Si planea utilizar Mutt, haga la siguiente configuración.

```
$ cd
$ touch .fdm.conf; chmod 600 .fdm.conf
$ mkdir -p Mail/INBOX/{new,cur,tmp}

```

### Configuración final

Modifique `.fdm.conf`, y añada sus cuentas de correo electrónico y reglas básicas de filtrado. Utilice mbox o maildir, pero no ambos.

```
## .fdm.conf
## Accounts and rules for:
#> foo@example.com
#> bar@gmail.com
## Last edit 21-Dec-09

# Catch-all action (mbox):
action "inbox" mbox "%h/mail/INBOX"
# Catch-all action (maildir):
# action "inbox" maildir "%h/Mail/INBOX"

account "foo" imaps server "imap.example.com"
	user "foo@example.com" pass "supersecret"

account "bar" imaps server "imap.gmail.com"
        user "bar@gmail.com" pass "evenmoresecret"

# Match all mail and deliver using the 'inbox' action.
match all action "inbox"

```

Esto recopilará el correo de las cuentas listadas y lo entregará a la carpeta de INBOX que creemos. Consulte la página de manual [fdm(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fdm.1) para obtener información específica sobre como conectarse a otros tipos de servidores de correo (POP3, por ejemplo).

**Sugerencia:** También puede especificar su nombre de inicio de sesión y/o contraseña en el archivo `.netrc`.

## Pruebas

Una vez que tenga esta configuración a su gusto, intente recoger su correo ejecutando fdm manualmente.

```
$ fdm -kv fetch

```

Esto mantendrá su correo intacto en el servidor en caso de que haya errores. Revise la salida para asegurarse de que todo funcionó según lo planeado. Abra su lector de correo favorito (MUA) y asegúrese de poder leer el correo que se acaba de entregar.

## Utilización extendida

*Características no esenciales que se añaden a la usabilidad de* fdm

### Filtrado adicional

Si desea que el correo de una determinada cuenta vaya a un buzón específico, puede añadir las siguientes líneas a su archivo fdm.conf. Desde el archivo de configuración anterior, si quisiera filtrar el correo de `*bar@gmail.com*` en su propia carpeta `*bar-mail*`, añadiría esto debajo de la línea "action" *(acción)* existente:

```
action *bar-deliver* mbox "%h/mail/*bar-mail*"

```

Cambie el `mbox` a `maildir` si es necesario, también asegúrese de que la ruta sea correcta.

Para activar la nueva acción, añada esto antes de la línea "match" *(coincidencia)* existente:

```
match account *bar* action *bar-deliver*

```

Tras esto, todo el correo a `*bar@gmail.com* `se colocará en la carpeta de correo `*bar-mail*`.

### Automatización con cron

Si todo salió bien, configure una tarea [cron](/index.php/Cron "Cron") para comprobar su correo con regularidad.

```
$ crontab -e
*/15 * * * * fdm fetch >> $HOME/[Mm]ail/fdm.log

```

## Véase también

*   [Sitio oficial de fdm (github)](https://github.com/nicm/fdm)
*   [fdm-users Lista de correo](https://lists.sourceforge.net/lists/listinfo/fdm-users)