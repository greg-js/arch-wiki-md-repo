**Mutt** es un cliente correo renombrado por sus poderosas características. Mutt, a pesar de más de una decada desde su lanzamiento, sigue siendo el cliente de correo favorito de un gran número de usuarios expertos. Desafortunadamente, una instalación por defecto de Mutt está plagada por combinación de teclas complicadas y una enorme cantidad de documentación. Esta guía ayudará al usuario promedio a instalar y correr Mutt, y comenzar a personalizarlo como sea necesario.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Descripción](#Descripción)
*   [2 Instalación](#Instalación)
    *   [2.1 Notas](#Notas)
*   [3 Configuración](#Configuración)
    *   [3.1 IMAP](#IMAP)
        *   [3.1.1 Usando el soporte nativo de IMAP](#Usando_el_soporte_nativo_de_IMAP)
            *   [3.1.1.1 spoolfile](#spoolfile)
            *   [3.1.1.2 imap_user](#imap_user)
            *   [3.1.1.3 folder](#folder)
            *   [3.1.1.4 mailboxes](#mailboxes)
            *   [3.1.1.5 Resumen](#Resumen)
        *   [3.1.2 Soporte externo de IMAP](#Soporte_externo_de_IMAP)
    *   [3.2 POP3](#POP3)
        *   [3.2.1 Recuperando correo](#Recuperando_correo)
        *   [3.2.2 Ordenando correo](#Ordenando_correo)
    *   [3.3 MailDir](#MailDir)
    *   [3.4 SMTP](#SMTP)
        *   [3.4.1 Usando el soporte nativo de SMTP](#Usando_el_soporte_nativo_de_SMTP)
        *   [3.4.2 Soporte externo de SMTP](#Soporte_externo_de_SMTP)
*   [4 Personalizando](#Personalizando)
    *   [4.1 Imprimiendo](#Imprimiendo)
    *   [4.2 Bloque de firma](#Bloque_de_firma)
        *   [4.2.1 Firma aleatoria](#Firma_aleatoria)
    *   [4.3 Visualizando URLs y abriendo Firefox](#Visualizando_URLs_y_abriendo_Firefox)
    *   [4.4 Mutt y Vim](#Mutt_y_Vim)
    *   [4.5 Visualizando HTML dentro de una configuración Vim/Mutt](#Visualizando_HTML_dentro_de_una_configuración_Vim/Mutt)
    *   [4.6 Mutt y GNU nano](#Mutt_y_GNU_nano)
*   [5 Sugerencias y Trucos](#Sugerencias_y_Trucos)
    *   [5.1 Use Mutt para enviar correo desde la línea de comandos](#Use_Mutt_para_enviar_correo_desde_la_línea_de_comandos)
    *   [5.2 Como mostrar un correo durante la composición de otro](#Como_mostrar_un_correo_durante_la_composición_de_otro)

## Descripción

Mutt se enfoca en ser un *Mail User Agent*, y fue originalmente escrito sólo para ver correo. Debido a esto, la recuperación de correo, características de envío y filtrado implementadas posteriormente son básicas comparadas con otras aplicaciones. La mayoría de las instalaciones de Mutt dependen de programas externos para estas tareas.

De todos modos, el paquete [mutt](https://www.archlinux.org/packages/?name=mutt) de Arch ha sido compilado con soporte para IMAP, POP3 y SMTP, y por tanto no requiere programas externos para tratar con el correo.

Este articulo cubrirá el envío/recepción con el IMAP nativo, y una configuración dependiente de [OfflineIMAP](/index.php/OfflineIMAP "OfflineIMAP") o [getmail](/index.php/Getmail "Getmail") (POP3) para recuperar correo, [procmail](/index.php/Procmail "Procmail") para filtrarlo en el caso de POP3, y [msmtp](/index.php/Msmtp "Msmtp") para enviarlo.

## Instalación

Instale Mutt:

```
# pacman -S mutt

```

Opcionalmente instale aplicaciones asistentes para una configuración con IMAP:

```
# pacman -S offlineimap msmtp

```

O si está usando POP3:

```
# pacman -S getmail procmail

```

### Notas

*   Si sólo necesita los métodos de atenticación LOGIN y PLAIN, estos se satisfacen con la dependencia [libsasl](https://www.archlinux.org/packages/?name=libsasl).
*   Si quiere (o necesita) usar CRAM-MD5, GSSAPI o DIGEST-MD5, instale también el paquete [cyrus-sasl-gssapi](https://www.archlinux.org/packages/?name=cyrus-sasl-gssapi) y listo.
*   Si está usando Gmail como su servidor de smtp, puede que necesite instalar el paquete [cyrus-sasl](https://www.archlinux.org/packages/?name=cyrus-sasl).

## Configuración

Esta sección cubre la configuración de IMAP, [#POP3](#POP3), [#MailDir](#MailDir) y [#SMTP](#SMTP).

Note que Mutt reconecerá dos ubicaciones para su archivo de configuración: `~/.muttrc` y `~/.mutt/muttrc`. Ambas ubicaciones funcionan.

### IMAP

*Configuraciones nativa y externa*

#### Usando el soporte nativo de IMAP

La versión pacman de Mutt está compilada con soporte de IMAP. Por lo menos mecesita tener 4 líneas en su archivo muttrc para poder acceder a su correo.

##### spoolfile

En vez de un *spool* local de correo, especifique el servidor `imap`.

```
set spoolfile=imap[s]://imap.servidor.dominio[:puerto]/carpeta

```

Use `imaps` para cifrado o `imap` en caso contrario. El número de puerto es sólo necesario cuando el puerto de su servidor no es estándar. Termine con el nombre de la carpeta donde llega el correo nuevo, que es casi siempre INBOX. Por ejemplo:

```
set spoolfile=imaps://imap.gmail.com/INBOX

```

##### imap_user

```
set imap_user=NOMBRE_USUARIO

```

Continuando con el ejemplo anterior, recuerde que Gmail requiere su dirección de correo completa (esto no es estándar):

```
set imap_user=your.username@gmail.com

```

##### folder

En vez de un directorio local que contiene todo su correo (y directorios), use su servidor (y la carpeta más alta en la jerarquía, de ser necesario).

```
set folder=imap[s]://imap.server.domain[:port]/[folder/]

```

No necesita usar una carpeta, pero puede ser conveniente si tiene todas sus demás carpetas dentro de su INBOX, por ejemplo. Lo que configure aquí como su carpeta puede ser accedido después en Mutt con solo un signo de igual (=). Ejemplo:

```
set folder=imaps://imap.gmail.com/

```

##### mailboxes

Las carpetas imap que deban ser revisadas regularmente en caso de haber correos nuevos deben estar listadas aquí (todas en la misma línea).

```
mailboxes <lista de carpetas>

```

Ahora puede usar '=' o '+' como substituto de la ruta completa de la `carpeta` que fue configurada arriba. Por ejemplo:

```
mailboxes =INBOX =familia
mailboxes imaps://imap.gmail.com/INBOX imaps://imap.gmail.com/familia

```

Éstas dos versiones son equivalentes, pero la primera es mucho más conveniente. También, Mutt está configurado por defecto para incluir una *macro* atada a la tecla 'y' que le permitirá cambiarse a cualquiera de las carpetas listadas en *mailboxes*.

##### Resumen

Usando estas opciones, podrá ejecutar mutt, introducir su contraseña IMAP, y comenzar a leer su correo. Aquí hay un fragmento de muttrc (para Gmail) con algunas otras líneas que puede considerar agregar para un mejor soporte de IMAP.

```
set folder      = imaps://imap.gmail.com/
set spoolfile   = imaps://imap.gmail.com/INBOX
set imap_user   = su.usuario@gmail.com
set imap_pass   = su.contrasena.imap
mailboxes       = +INBOX

# almacene las cabeceras de mensajes localmente para acelerar las cosas
set header_cache = ~/.mutt/hcache

# especifique dondo guardar y/o buscar los mensajes pospuestos
set postponed = +[Gmail]/Drafts

# permitir a mutt abrir nuevas conexiones imap automaticamente
set imap_passive = no

# mantener viva la conexion imap preguntando intermitentemente (tiempo en segundos)
set imap_keepalive = 300

# que tan frequetemente se revisara si hay correo nuevo (tiempo en segundos)
set mail_check = 120
```

#### Soporte externo de IMAP

Aunque la funcionalidad de IMAP está integrada en Mutt, éste no descarga el correo para uso fuera de línea. El artículo [OfflineIMAP](/index.php/OfflineIMAP "OfflineIMAP") describe como descargar su correo a una carpeta local para que pueda ser procesada por Mutt.

Considere el uso de aplicaciones como [spamassassin](https://www.archlinux.org/packages/?name=spamassassin) o [imapfilter](https://aur.archlinux.org/packages/imapfilter/) para ordenar el correo.

### POP3

*Recuperando y ordenando el correo con aplicaciones externas*

#### Recuperando correo

Cree el directorio `~/.getmail/`. Abra el archivo `~/.getmail/getmailrc` en su editor de texto favorito.

Aquí hay un archivo `getmailrc` ejemplo usado con una cuenta de gmail

```
[retriever]
type = SimplePOP3SSLRetriever
server = pop.gmail.com
username = nombre_usuario@gmail.com
port = 995
password = contrasena

[destination]
type = Maildir
path = ~/mail/
```

Puede modificar esto de acuerdo a la especificación de su servicio POP3.

En esta guía el correo se almacenará en el formato `maildir` format. Los dos formatos principales de buzón de correo son `mbox` y `maildir`. La diferencia principal entre éstos es que `mbox` es un archivo, con todos sus correos y sus cabeceras almacenados en él, mientras que `maildir` es un árbol de directorios. Cada correo es su propio archivo, lo que usualmente acelera las cosas.

Una `maildir` es sólo una carpeta con las carpetas `cur`, `new` y `tmp` en ella.

```
   mkdir -p ~/mail/{cur,new,tmp}

```

Ahora ejecute getmail. Si funciona bien, puede crear un cronjob para getmail que se ejecute cada n horas/minutos. Escriba `crontab -e` para editar cronjobs, e introduzca lo siguiente:

```
 */30 * * * * /usr/bin/getmail

```

Ésto ejecutará `getmail` cada 30 minutos.

#### Ordenando correo

[Procmail](/index.php/Procmail "Procmail") es una herramienta de ordenamiento extremadamente poderosa. Para los propósitos de este wiki se harán algunos orednamientos primitivos para comenzar.

Debe editar su getmailrc para pasar el correo recuperado a procmail:

```
[destination]
type = MDA_external
path = /usr/bin/procmail
```

Ahora, abra `.procmailrc` en su editor favorito. Lo siguiente ordenará todo el correo proveniente de la lista de correos canguros-felices, y todo el correo proveniente de su amigo pepe en sus propios maildirs.

```
MAILDIR=$HOME/mail
DEFAULT=$MAILDIR/inbox/
LOGFILE=$MAILDIR/log

:0:
* ^To: canguros-felices@proveedor_amable.com
canguros-felices/

:0:
* ^From: pepe@ejemplo.net
pepe/
```

Después de guardar su `.procmailrc`, ejecute getmail y vea si procmail tiene éxito ordenando su correo en los directorios apropiados.

**Nota:** Un error fácil de cometer con .procmailrc es la configuración de permisos. procmail requiere que el permiso sea 644 y dará mensajes de error sin sentido si no lo hace.

### MailDir

MailDir es un formato genérico y estandarizado. Casi todo *MUA* es capaz de manejar MailDirs y el soporte de Mutt es excelente. Sólo se requiere realizar algunos pasos simples para hacer que Mutt los use. Abra su muttrc con su editor favorito y agregue las siguientes líneas:

```
set mbox_type=Maildir
set folder=$HOME/Mail
set spoolfile=+/INBOX
set header_cache=~/.hcache
```

Esta es la configuración mínima que le permite acceder su MailDir y revisar nuevos correos locales en INBOX. Esta configuración tambien almacena las cabeceras de los correos para acelerar los listados de directorio. Puede que no esté activado en su compilación (pero es seguro que está activado en el paquete de Arch). Note que esto no afecta de ninguna manera a OfflineIMAP. Éste siempre sincroniza todos los directorios en un servidor. `spoolfile` le dice a Mutt qué directorios locales revisar por nuevos correos. Puede querer agregar más *Spoolfiles* (por ejemplo los directorios de listas de correos) y quizás otras cosas. Pero esto es tema para el manual de Mutt y está fuera del alcance de este documento.

### SMTP

Sin importar si usa POP o IMAP para recibir correo probablemente enviará correo usando SMTP.

#### Usando el soporte nativo de SMTP

La version pacman de Mutt está compilada con soporte de SMTP. Consulte el manual en línea [muttrc(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/muttrc.5) para mayor información.

Por ejemplo:

```
set my_pass='contrasena'
set my_user=nombre_usuario@gmail.com

set smtp_url=smtps://$my_user:$my_pass@smtp.gmail.com
set ssl_force_tls = yes
```

#### Soporte externo de SMTP

Se puede utilizar un agente SMTP externo como [msmtp](/index.php/Msmtp "Msmtp") o [SSMTP](/index.php?title=SSMTP_(Espa%C3%B1ol)&action=edit&redlink=1 "SSMTP (Español) (page does not exist)"). Esta sección cubre exclusivamente la configuración de Mutt para msmtp.

Edite el archivo de configuración de Mutt o creelo si no está presente:

 `muttrc` 
```
set realname='Canguro Molesto'

set sendmail="/usr/bin/msmtp"

set edit_headers=yes
set folder=~/mail
set mbox=+mbox
set spoolfile=+inbox
set record=+sent
set postponed=+drafts
set mbox_type=Maildir

mailboxes +inbox +pepe +canguros-felices
```

Ahora, ejecute `mutt`:

```
$ mutt

```

Debería poder ver todo el correo en `~/mail/inbox`. Pulse `m` para redactar un mensaje; se utilizará el editor definido en la variable de entorno `EDITOR`. Si la variable no está definida, escriba en la consola $ export EDITOR=binario_del_editor

Para propósitos de prueba, remita el correo a usted mismo. Después de escribir el correo, guarde y salga del editor. Regresará a Mutt, que ahora mostrará información acerca de su correo. Presione `y` para enviarlo.

## Personalizando

### Imprimiendo

Puede instalar [muttprint](https://aur.archlinux.org/packages/muttprint/) del [AUR](/index.php/AUR "AUR") para una calidad de impresión superior. Inserte en su archivo muttrc:

```
set print_command="/usr/bin/muttprint %s -p {PrinterName}"

```

### Bloque de firma

Cree un archivo .signature en su directorio home. Su firma será anexada al al final de su correo.

#### Firma aleatoria

Puede utilizar fortune para agregar una firma aleatoria a mutt.

 `$ pacman -S fortune-mod` 

Cree un archivo fortune y agregue la siguiente línea a su .muttrc:

 `set signature="fortune ruta_al_archivo_fortune"` 

### Visualizando URLs y abriendo Firefox

Debe comenzar creando un directorio .mutt en $HOME si no lo ha hecho. Ahí, cree un archivo llamado macros. Ingrese lo siguiente:

```
 macro pager \cb <pipe-entry>'urlview'<enter> 'Seguir enlaces con urlview'

```

Instale [urlview](https://aur.archlinux.org/packages/urlview/) desde el [AUR](/index.php/AUR "AUR").

Cree un archivo .urlview en $HOME e ingrese lo siguiente:

```
REGEXP (((http|https|ftp|gopher)|mailto)[.:][^ >"\t]*|www\.[-a-z0-9.]+)[^ .,;\t>">\):]
COMMAND firefox %s 

```

Cuando lea un correo, al presionar ctrl+b listará todos los urls del correo. Navegue hacia arriba o abajo con la teclas direccionales y presione enter en el url deseado. Se ejecutará firefox e irá al sitio seleccionado.

*   Nota - Si tiene problemas con urlview debido a la codificación url de Mutt puede probar [extract_url.pl](http://www.memoryhole.net/~kyle/extract_url/)

### Mutt y Vim

*   Para limitar el ancho del texto a 72 carácteres, edite su archivo .[vimrc](/index.php/Vim "Vim") y agregué:

```
au BufRead /tmp/mutt-* set tw=72

```

*   Otra opción es usar el complemento de tipo de archivo de correo de Vim para activar otras opciones centradas en correo además de la opción de 72 carácteres de ancho. Edite `~/.vim/filetype.vim`, creándolo de ser necesario y agregue:

```

augroup filetypedetect
  " Mail
  autocmd BufRead,BufNewFile *mutt-*              setfiletype mail
augroup END

```

*   Para configurar un directorio tmp diferente, ej. ~/.tmp, agregue una linea a su muttrc como sigue:

```
set tmpdir="~/.tmp"

```

*   Para re-formatear un texto modificado vea la ayuda contextual de Vim:

```
:h 10.7

```

### Visualizando HTML dentro de una configuración Vim/Mutt

Esta configuración pasa el cuerpo html a lynx y luego a Vim, manteniendo la visualización de correo uniforme y discreta.

Instale lynx:

```
pacman -S lynx

```

Si *~/.mutt/mailcap* no existe va a necesitar crearlo y guardar lo siguiente en el:

```
text/html; lynx -dump %s; nametemplate=%s.html; copiousoutput

```

Edite muttrc y agregue lo siguiente:

```
set mailcap_path 	= ~/.mutt/mailcap

```

Para abrir los mensajes html automáticamente en lynx, agregue esta línea adicional al muttrc:

```
auto_view text/html

```

Lo bonito de esto es, en vez de ver un cuerpo html como código fuente o ser abierto por un programa separado, en este caso lynx, se analiza como html para Vim, cualquier enlace url en el correo se puede mostrar con Ctrl+b.

### Mutt y GNU nano

[nano](/index.php/Nano_(Espa%C3%B1ol) "Nano (Español)") es otro agradable editor de consola para usar con Mutt.

Para limitar el ancho del texto a 72 carácteres, edite su archivo .nanorc y agregue:

```
 set fill 72

```

Además, en el archivo muttrc, puede especificar la línea para comenzar a editar de manera que salte la cabecera del correo:

```
 set editor="nano +7"

```

## Sugerencias y Trucos

### Use Mutt para enviar correo desde la línea de comandos

Las páginas man mostrarán todas las instrucciones disponibles y cómo usarlas, pero aquí hay un par de ejemplos. Puede usar Mutt para enviar alertas, mensajes de registro (log) o alguna otra información de sistema, bien cuando inicie una sesión, a través del .bash_profile, o bien como una tarea programada usando [cron](/index.php/Cron "Cron").

Enviar un mensaje:

```
mutt -s "Asunto" alguien@algunservidor.com < /var/log/algunlog

```

Enviar un mensaje con adjunto:

```
mutt -s "Asunto" -a algunarchivo alguien@algunservidor.com < /tmp/alguntexto.txt

```

### Como mostrar un correo durante la composición de otro

Una queja común con Mutt es que al componer un nuevo correo (o respuesta), no se puede abrir otro correo (para revisar con otro correspondiente, por ejemplo) sin cerrar el correo actual (postponer). Lo siguiente propone una solución:

Primero, ejecute Mutt como de costumbre. Luego, ejecute otra ventana de terminal. Ahora ejecute un nuevo Mutt con

```
mutt -R

```

Esto ejecuta Mutt en modo sólo lectura, y puede revisar otros correos a su conveniencia. Se sugiere que siempre ejecute el segundo Mutt enmodo sólo lectura, debido a que fácilmente surgiran conflictos de otra manera.

Ahora, esta solución requiere un poco deescritura, así que es deseable automatizarlo. Lo siguiente funciona con [Awesome](/index.php/Awesome_(Espa%C3%B1ol) "Awesome (Español)"), en otros MV's o AE's es posible que existan soluciones similares: busque en la web como agregar una combinación de teclas, y haga que la tecla deseada ejecute:

```
$TERM -e mutt -R 

```

Donde $TERM es su terminal.

Para Awesome: edite su rc.lua, y agregue lo siguiente en una de las primeras líneas, después de terminal = "su_terminal" etc.

```
mailview = terminal .. " -e mutt -R"

```

Esto autmáticamente usa su terminal preferido, ".." es concatenación en Lua. Note el espacio antes de -e.

Luego agregue lo siguiente dentro de --{{{ Key bindings

```
awful.key({ modkey,           }, "m", function() awful.util.spawn(mailview) end),

```

Omita la coma final si esta esla última línea. Puede, por supuesto, usar otra tecla distinata a "m". Ahora guarde y salga, y revise su sintáxis con:

```
awesome -k

```

Si está bien, ¡reinicie awesome y pruebe!

Ahora, un ejemplo de uso: Ejecute mutt como de costumbre. Cree un nuevo correo, y luego presione "Mod4"+"m". Ésto abre su buzón en un nuevo terminal, y puede explorar y leer otros correos. Ahora, un bono elegante: Salga de este Mutt sólo lectura con "q", y ¡la ventana terminal que éste creo desaparece!