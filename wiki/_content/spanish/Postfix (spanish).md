**Estado de la traducción**
Este artículo es una traducción de [Postfix](/index.php/Postfix "Postfix"), revisada por última vez el **2019-03-01**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Postfix&diff=0&oldid=567766) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Postfix with SASL](/index.php/Postfix_with_SASL "Postfix with SASL")
*   [Virtual user mail system](/index.php/Virtual_user_mail_system "Virtual user mail system")
*   [OpenDMARC](/index.php/OpenDMARC "OpenDMARC")
*   [OpenDKIM](/index.php/OpenDKIM "OpenDKIM")

[Postfix](https://en.wikipedia.org/wiki/es:Postfix "wikipedia:es:Postfix") es un [agente de transferencia de correo](/index.php/Mail_transfer_agent "Mail transfer agent") que de acuerdo con [su sitio web](http://www.postfix.org/):

	intenta ser rápido, fácil de administrar y seguro, al mismo tiempo que es lo suficientemente compatible con sendmail para no molestar a los usuarios existentes. Por lo tanto, el exterior es parecido a sendmail, pero el interior es completamente diferente.

Este artículo se basa en [Servidor de correo](/index.php/Mail_server "Mail server"). El objetivo de este artículo es configurar Postfix y explicar qué hacen los archivos de configuración básicos. Hay instrucciones para configurar la entrega solo para usuarios locales del sistema y un enlace a una guía para la entrega a usuarios virtuales.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Configuración](#Configuración)
    *   [2.1 Alias](#Alias)
    *   [2.2 Correo local](#Correo_local)
    *   [2.3 Correo virtual](#Correo_virtual)
    *   [2.4 Comprobar configuración](#Comprobar_configuración)
*   [3 Iniciar Postfix](#Iniciar_Postfix)
*   [4 TLS](#TLS)
    *   [4.1 SMTP seguro (enviando)](#SMTP_seguro_(enviando))
    *   [4.2 SMTP seguro (recibiendo)](#SMTP_seguro_(recibiendo))
*   [5 Consejos y trucos](#Consejos_y_trucos)
    *   [5.1 Lista negra de correos electrónicos entrantes](#Lista_negra_de_correos_electrónicos_entrantes)
    *   [5.2 Ocultar la IP y el agente de usuario del remitente en el encabezado Received](#Ocultar_la_IP_y_el_agente_de_usuario_del_remitente_en_el_encabezado_Received)
    *   [5.3 Postfix en una jaula chroot](#Postfix_en_una_jaula_chroot)
    *   [5.4 DANE (DNSSEC)](#DANE_(DNSSEC))
        *   [5.4.1 Registro de recursos](#Registro_de_recursos)
        *   [5.4.2 Configuración](#Configuración_2)
*   [6 Extras](#Extras)
    *   [6.1 Postgrey](#Postgrey)
        *   [6.1.1 Instalación](#Instalación_2)
        *   [6.1.2 Configuración](#Configuración_3)
        *   [6.1.3 Lista blanca](#Lista_blanca)
        *   [6.1.4 Troubleshooting](#Troubleshooting)
    *   [6.2 SpamAssassin](#SpamAssassin)
        *   [6.2.1 SpamAssassin stand-alone generic setup](#SpamAssassin_stand-alone_generic_setup)
        *   [6.2.2 SpamAssassin combined with Dovecot LDA / Sieve (Mailfiltering)](#SpamAssassin_combined_with_Dovecot_LDA_/_Sieve_(Mailfiltering))
        *   [6.2.3 SpamAssassin combined with Dovecot LMTP / Sieve](#SpamAssassin_combined_with_Dovecot_LMTP_/_Sieve)
    *   [6.3 Rule-based mail processing](#Rule-based_mail_processing)
    *   [6.4 Sender Policy Framework](#Sender_Policy_Framework)
    *   [6.5 Sender Rewriting Scheme](#Sender_Rewriting_Scheme)
*   [7 Troubleshooting](#Troubleshooting_2)
    *   [7.1 Warning: "database /etc/postfix/*.db is older than source file .."](#Warning:_"database_/etc/postfix/*.db_is_older_than_source_file_..")
*   [8 See also](#See_also)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [postfix](https://www.archlinux.org/packages/?name=postfix).

## Configuración

Véase [Configuración básica de Postfix](http://www.postfix.org/BASIC_CONFIGURATION_README.html). Los archivos de configuración están en `/etc/postfix` por defecto. Los dos archivos más importantes son:

*   `master.cf`, define qué servicios de Postfix están habilitados y cómo se conectan los clientes con ellos, véase [master(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/master.5)
*   `main.cf`, el archivo de configuración principal, véase [postconf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/postconf.5)

Los cambios de configuración necesitan un [reinicio](/index.php/Reload_(Espa%C3%B1ol) "Reload (Español)") de `postfix.service` para tener efecto.

### Alias

Véase [aliases(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/postfix/aliases.5.es).

Puede especificar los alias (también conocidos como reenviadores) en `/etc/postfix/aliases`.

Debe asignar todo el correo dirigido a *root* a otra cuenta, ya que no es una buena idea leer el correo como superusuario.

Descomente la siguiente línea, y cambie `tú` a una cuenta real.

```
root: tú

```

Una vez que haya terminado de editar `/etc/postfix/aliases` debe ejecutar la orden postalias:

```
postalias /etc/postfix/aliases

```

Para cambios posteriores puedes utilizar:

```
newaliases

```

**Sugerencia:** Alternativamente puede crear el archivo `~/.forward`, por ejemplo `/root/.forward` para el superusuario. Especifique el usuario al que se debe reenviar el correo del superusuario, por ejemplo *usuario@localhost*. `/root/.forward` 
```
usuario@localhost

```

### Correo local

Para enviar correo solo a los usuarios locales del sistema (que están en `/etc/passwd`) actualice `/etc/postfix/main.cf` para reflejar la siguiente configuración. Descomente, cambie o añada las siguientes líneas:

```
myhostname = localhost
mydomain = localdomain
mydestination = $myhostname, localhost.$mydomain, localhost
inet_interfaces = $myhostname, localhost
mynetworks_style = host
default_transport = error: outside mail is not deliverable

```

Todos los demás ajustes pueden permanecer sin cambios. Después de configurar el archivo de configuración anterior, es posible que desee configurar algunos [#Alias](#Alias) y luego [#Iniciar Postfix](#Iniciar_Postfix).

### Correo virtual

El correo virtual es un correo que no se asigna a una cuenta de usuario (`/etc/passwd`).

Véase [Virtual user mail system with Postfix, Dovecot and Roundcube](/index.php/Virtual_user_mail_system_with_Postfix,_Dovecot_and_Roundcube "Virtual user mail system with Postfix, Dovecot and Roundcube") para una guía completa de cómo configurarlo.

### Comprobar configuración

Ejecute la orden `postfix check`. Debería mostrar cualquier cosa que pueda haber hecho mal en un archivo de configuración.

Para ver todas sus configuraciones, escriba `postconf`. Para ver en qué se diferencian de los valores por defecto, pruebe `postconf -n`.

## Iniciar Postfix

**Nota:** Debe ejecutar `newaliases` al menos una vez para que Postfix se ejecute, incluso si no configuró ningún [#Alias](#Alias).

[Inicie/active](/index.php/Start/enable_(Espa%C3%B1ol) "Start/enable (Español)") `postfix.service`.

## TLS

Para más información, véase [Soporte TLS en Postfix](http://www.postfix.org/TLS_README.html).

### SMTP seguro (enviando)

Por defecto, Postfix/sendmailno enviará correo electrónico cifrado a otros servidores SMTP. Para utilizar TLS cuando esté disponible, añada la siguiente línea a `main.cf`:

 `/etc/postfix/main.cf`  `smtp_tls_security_level = may` 

Para *forzar* TLS (y fallar cuando el servidor remoto no lo soporte), cambie `may` a `encrypt`. Note, sin embargo, que esto viola el [RFC:2487](https://tools.ietf.org/html/rfc2487 "rfc:2487") si el servidor SMTP es referenciado públicamente.

### SMTP seguro (recibiendo)

**Advertencia:** Si implementa [TLS](https://en.wikipedia.org/wiki/es:Transport_Layer_Security "wikipedia:es:Transport Layer Security"), asegúrese de seguir la [guía de weakdh.org](https://weakdh.org/sysadmin.html) para prevenir FREAK/Logjam. Desde mediados de 2015, la configuración predeterminada ha sido segura contra [POODLE](https://en.wikipedia.org/wiki/es:Ataque_POODLE "wikipedia:es:Ataque POODLE"). Para más información véase [Server-side TLS](/index.php/Server-side_TLS "Server-side TLS").

Por defecto, Postfix no aceptará el correo seguro.

Necesita [obtener un certificado](/index.php/Obtain_a_certificate "Obtain a certificate"). Apunte Postfix a sus certificados TLS añadiendo las líneas siguientes a `main.cf`:

 `/etc/postfix/main.cf` 
```
smtpd_tls_security_level = may
smtpd_tls_cert_file = **/ruta/al/cert.pem**
smtpd_tls_key_file = **/ruta/al/key.pem**
```

Hay dos formas de aceptar el correo seguro. STARTTLS sobre SMTP (puerto 587) y SMTPS (puerto 465). Este último fue previamente desaprobado pero fue reintegrado por el [RFC:8314](https://tools.ietf.org/html/rfc8314 "rfc:8314").

Para activar STARTTLS sobre SMTP (puerto 587), descomente las siguientes líneas en `master.cf`:

 `/etc/postfix/master.cf` 
```
submission inet n       -       n       -       -       smtpd
  -o syslog_name=postfix/submission
  -o smtpd_tls_security_level=encrypt
  -o smtpd_sasl_auth_enable=yes
  -o smtpd_tls_auth_only=yes
  -o smtpd_reject_unlisted_recipient=no
#  -o smtpd_client_restrictions=$mua_client_restrictions
#  -o smtpd_helo_restrictions=$mua_helo_restrictions
#  -o smtpd_sender_restrictions=$mua_sender_restrictions
  -o smtpd_recipient_restrictions=
  -o smtpd_relay_restrictions=permit_sasl_authenticated,reject
  -o milter_macro_daemon_name=ORIGINATING
```

Las opciones `smtpd_*_restrictions` permanecen comentadas porque `$mua_*_restrictions` no están definidas en main.cf por defecto. Si defide configurar alguna `$mua_*_restrictions`, descomente esas líneas también.

Para activar SMTPS (puerto 465), descomente las líneas siguientes en `master.cf`:

 `/etc/postfix/master.cf` 
```
**smtps**     inet  n       -       n       -       -       smtpd
  -o syslog_name=postfix/smtps
  -o smtpd_tls_wrappermode=yes
  -o smtpd_sasl_auth_enable=yes
  -o smtpd_reject_unlisted_recipient=no
#  -o smtpd_client_restrictions=$mua_client_restrictions
#  -o smtpd_helo_restrictions=$mua_helo_restrictions
#  -o smtpd_sender_restrictions=$mua_sender_restrictions
  -o smtpd_recipient_restrictions=
  -o smtpd_relay_restrictions=permit_sasl_authenticated,reject
  -o milter_macro_daemon_name=ORIGINATING

```

Y en primera línea, reemplace `**smtps**` con `submissions`. (este es el nombre oficial del servicio según [IANA](https://www.iana.org/assignments/service-names-port-numbers/service-names-port-numbers.txt); Postfix todavía hace referencia al nombre antiguo)

El razonamiento que rodea a las líneas `$smtpd_*_restrictions` es el mismo que arriba.

**Nota:** Si obtiene un mensaje de error como `postfix/master[5309]: fatal: 0.0.0.0:smtps: Servname not supported for ai_socktype`, asegúrese de tener la siguiente línea en `postfix/master.cf`:
```
submissions inet n       -       n       -       -       smtpd

```

También asegúrese de que `/etc/services` está actualizado e incluye la siguiente línea:

```
submissions 465/tcp

```

## Consejos y trucos

### Lista negra de correos electrónicos entrantes

La lista negra de correos electrónicos entrantes por dirección del remitente se puede hacer fácilmente con Postfix.

Cree y abra el fichero `/etc/postfix/blacklist_incoming` y añada la dirección de correo electrónico del remitente:

```
usuario@ejemplo.com REJECT

```

Luego use la orden `postmap` para crear una base de datos:

```
# postmap hash:blacklist_incoming

```

Añada el siguiente código antes de la primera regla permisiva en `main.cf`:

```
smtpd_recipient_restrictions = check_sender_access hash:/etc/postfix/blacklist_incoming

```

Finalmente [reinicie](/index.php/Restart_(Espa%C3%B1ol) "Restart (Español)") `postfix.service`.

### Ocultar la IP y el agente de usuario del remitente en el encabezado Received

Este es un problema de privacidad principalmente, si utiliza Thunderbird y envía un correo electrónico. El encabezado Received contendrá su IP LAN y WAN e información sobre el cliente de correo electrónico que utilizó. (Fuente original: [AskUbuntu](http://askubuntu.com/questions/78163/when-sending-email-with-postfix-how-can-i-hide-the-senders-ip-and-username-in)) Lo que queremos hacer es eliminar el encabezado Received de los correos electrónicos salientes.

Para hacer esto, primero añada la siguiente línea a `main.cf`:

```
smtp_header_checks = regexp:/etc/postfix/smtp_header_checks

```

Cree `/etc/postfix/smtp_header_checks` con este contenido:

```
/^Received: .*/     IGNORE
/^User-Agent: .*/   IGNORE

```

Finalmente, [reinicie](/index.php/Restart_(Espa%C3%B1ol) "Restart (Español)") `postfix.service`.

### Postfix en una jaula chroot

Postfix no se pone en una jaula chroot por defecto. La documentación de Postfix [[1]](http://www.postfix.org/BASIC_CONFIGURATION_README.html#chroot_setup) proporciona detalles sobre cómo llevar a cabo tal enjaulado. Los pasos se describen a continuación y se basan en el script de configuración de chroot que se proporciona en el código fuente de Postfix.

Primero, entre en el archivo `master.cf` en el directorio `/etc/postfix` y cambie todas las entradas chroot a 'yes' (y) excepto para los servicios `qmgr`, `proxymap`, `proxywrite`, `local`, y `virtual`

Segundo, cree dos funciones que nos ayudarán más adelante con la copia de archivos en la jaula chroot (véase el último paso)

```
CP="cp -p"

```

```
cond_copy() {
  # find files as per pattern in $1
  # if any, copy to directory $2
  dir=`dirname "$1"`
  pat=`basename "$1"`
  lr=`find "$dir" -maxdepth 1 -name "$pat"`
  if test ! -d "$2" ; then exit 1 ; fi
  if test "x$lr" != "x" ; then $CP $1 "$2" ; fi
}

```

A continuación, haga los nuevos directorios para la jaula:

```
set -e
umask 022

```

```
POSTFIX_DIR=${POSTFIX_DIR-/var/spool/postfix}
cd ${POSTFIX_DIR}

```

```
mkdir -p etc lib usr/lib/zoneinfo
test -d /lib64 && mkdir -p lib64

```

Encuentra el archivo localtime:

```
lt=/etc/localtime
if test ! -f $lt ; then lt=/usr/lib/zoneinfo/localtime ; fi
if test ! -f $lt ; then lt=/usr/share/zoneinfo/localtime ; fi
if test ! -f $lt ; then echo "cannot find localtime" ; exit 1 ; fi
rm -f etc/localtime

```

Copie localtime y algunos archivos de sistema en el directorio etc del chroot:

```
$CP -f $lt /etc/services /etc/resolv.conf /etc/nsswitch.conf etc
$CP -f /etc/host.conf /etc/hosts /etc/passwd etc
ln -s -f /etc/localtime usr/lib/zoneinfo

```

Copie las bibliotecas requeridas en el chroot utilizando la función creada previamente `cond_copy`

```
cond_copy '/usr/lib/libnss_*.so*' lib
cond_copy '/usr/lib/libresolv.so*' lib
cond_copy '/usr/lib/libdb.so*' lib

```

Y no olvide [recargar](/index.php/Reload_(Espa%C3%B1ol) "Reload (Español)") Postfix.

### DANE (DNSSEC)

#### Registro de recursos

**Advertencia:** Esta no es una sección trivial. Tenga en cuenta que debe estar seguro de lo que está haciendo. Mejor lea antes [Errores comunes](https://dane.sys4.de/common_mistakes).

[DANE](/index.php/DANE "DANE") admite varios tipos de registros, sin embargo, no todos ellos son adecuados en Postfix.

El uso del certificado 0 no es compatible, el 1 se asigna al 3 y 2 es opcional, por lo tanto es recomendable publicar un registro "3". Más en [Registros de recursos](/index.php/DANE#Resource_Record "DANE").

#### Configuración

DANE oportunista *(opportunistic)* se configura de esta manera:

 `/etc/postfix/main.cf` 
```
smtpd_use_tls = yes
smtp_dns_support_level = dnssec
smtp_tls_security_level = dane

```
 `/etc/postfix/master.cf` 
```
dane       unix  -       -       n       -       -       smtp
  -o smtp_dns_support_level=dnssec
  -o smtp_tls_security_level=dane

```

Para utilizar políticas por dominio, por ejemplo DANE oportunista para ejemplo.org y DANE obligatorio *(mandatory)* para ejemplo.com, utilice algo como esto:

 `/etc/postfix/main.cf` 
```
indexed = ${default_database_type}:${config_directory}/

# Per-destination TLS policy
#
smtp_tls_policy_maps = ${indexed}tls_policy

# default_transport = smtp, but some destinations are special:
#
transport_maps = ${indexed}transport

```
 `transport` 
```
ejemplo.com dane
ejemplo.org dane

```
 `tls_policy` 
```
ejemplo.com dane-only

```

**Nota:** Para DANE obligatorio global, cambie `smtp_tls_security_level` a `dane-only`. Tenga en cuenta que esto provoca un error tempfail en Postfix (responder con un código de error `4.X.X`) en todos los envíos que no utilicen DANE.

La documentación completa se encuentra [aquí](http://www.postfix.org/TLS_README.html#client_tls_dane).

## Extras

*   **[PostfixAdmin](/index.php/PostfixAdmin "PostfixAdmin")** — Una interfaz administrativa basada en web para Postfix.

	[http://postfixadmin.sourceforge.net/](http://postfixadmin.sourceforge.net/) || [postfixadmin](https://www.archlinux.org/packages/?name=postfixadmin)

### Postgrey

[Postgrey](http://postgrey.schweikert.ch/) se puede utilizar para activar [listas grises](https://en.wikipedia.org/wiki/es:Lista_gris "wikipedia:es:Lista gris") en un servidor de correo Postfix.

#### Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [postgrey](https://www.archlinux.org/packages/?name=postgrey). Para tenerlo funcionando rápidamente, edite el archivo de configuración de Postfix y añada estas líneas:

 `/etc/postfix/main.cf` 
```
smtpd_recipient_restrictions =
  check_policy_service inet:127.0.0.1:10030

```

Luego [inicie/active](/index.php/Start/enable_(Espa%C3%B1ol) "Start/enable (Español)") el servicio `postgrey`. Después, recargue el servicio `postfix`. Ahora la lista gris debería estar activada.

#### Configuración

La configuración se realiza mediante la edición del archivo `postgrey.service`. Primero cópielo para editarlo.

```
# cp /usr/lib/systemd/system/postgrey.service /etc/systemd/system/

```

#### Lista blanca

Para añadir listas blancas automáticas (los envíos exitosos entran en la lista blanca y no tienen que esperar nunca más), puede añadir la opción `--auto-whitelist-clients=N` y reemplazar `N` por un número adecuadamente pequeño (o dejarlo en su valor por defecto de 5).

...en realidad, el método preferido debería ser la anulación *(override)*:

```
cat /etc/systemd/system/postgrey.service.d/override.conf

```

```
[Service]
ExecStart=
ExecStart=/usr/bin/postgrey --inet=127.0.0.1:10030 \
       --pidfile=/run/postgrey/postgrey.pid \
       --group=postgrey --user=postgrey \
       --daemonize \
       --greylist-text="Greylisted for %%s seconds" \
       --auto-whitelist-clients

```

To add your own list of whitelisted clients in addition to the default ones, create the file `/etc/postfix/whitelist_clients.local` and enter one host or domain per line, then restart `postgrey.service` so the changes take effect.

#### Troubleshooting

If you specify `--unix=/path/to/socket` and the socket file is not created ensure you have removed the default `--inet=127.0.0.1:10030` from the service file.

For a full documentation of possible options see `perldoc postgrey`.

### SpamAssassin

This section describes how to integrate [SpamAssassin](/index.php/SpamAssassin "SpamAssassin").

#### SpamAssassin stand-alone generic setup

**Note:** If you want to combine SpamAssassin and Dovecot Mail Filtering, ignore the next two lines and continue further down instead.

Edit `/etc/postfix/master.cf` and add the content filter under smtp.

```
smtp      inet  n       -       n       -       -       smtpd
  -o content_filter=spamassassin
```

Also add the following service entry for SpamAssassin

```
spamassassin unix -     n       n       -       -       pipe
  flags=R user=spamd argv=/usr/bin/vendor_perl/spamc -e /usr/bin/sendmail -oi -f ${sender} ${recipient}
```

Now you can [start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") `spamassassin.service`.

#### SpamAssassin combined with Dovecot LDA / Sieve (Mailfiltering)

Set up LDA and the Sieve-Plugin as described in [Dovecot#Sieve](/index.php/Dovecot#Sieve "Dovecot"). But ignore the last line `mailbox_command...` .

Instead add a pipe in `/etc/postfix/master.cf`:

```
 dovecot   unix  -       n       n       -       -       pipe
       flags=DRhu user=vmail:vmail argv=/usr/bin/vendor_perl/spamc -u spamd -e /usr/lib/dovecot/dovecot-lda -f ${sender} -d ${recipient}

```

And activate it in `/etc/postfix/main.cf`:

```
 virtual_transport = dovecot

```

#### SpamAssassin combined with Dovecot LMTP / Sieve

Set up the LMTP and Sieve as described in [Dovecot#Sieve](/index.php/Dovecot#Sieve "Dovecot").

Edit `/etc/dovecot/conf.d/90-plugins.conf` and add:

```
 sieve_before = /etc/dovecot/sieve.before.d/
 sieve_extensions = +vnd.dovecot.filter
 sieve_plugins = sieve_extprograms
 sieve_filter_bin_dir = /etc/dovecot/sieve-filter
 sieve_filter_exec_timeout = 120s #this is often needed for the long running spamassassin scans, default is otherwise 10s

```

Create the directory and put spamassassin in as a binary that can be ran by dovecot:

```
 # mkdir /etc/dovecot/sieve-filter
 # ln -s /usr/bin/vendor_perl/spamc /etc/dovecot/sieve-filter/spamc

```

Create a new file, `/etc/dovecot/sieve.before.d/spamassassin.sieve` which contains:

```
 require [ "vnd.dovecot.filter" ];
 filter "spamc" [ "-d", "127.0.0.1", "--no-safe-fallback" ];

```

Compile the sieve rules `spamassassin.svbin`:

```
 # cd /etc/dovecot/sieve.before.d
 # sievec spamassassin.sieve

```

Finally, [restart](/index.php/Restart "Restart") `dovecot.service`.

### Rule-based mail processing

With policy services one can easily finetune Postfix' behaviour of mail delivery. [postfwd](https://www.archlinux.org/packages/?name=postfwd) and [policyd](https://aur.archlinux.org/pkgbase/policyd) provide services to do so. This allows you to e.g. implement time-aware grey- and blacklisting of senders and receivers as well as [SPF](/index.php/SPF "SPF") policy checking.

Policy services are standalone services and connected to Postfix like this:

 `/etc/postfix/main.cf` 
```
smtpd_recipient_restrictions =
  ...
  check_policy_service unix:/run/policyd.sock
  check_policy_service inet:127.0.0.1:10040

```

Placing policy services at the end of the queue reduces load, as only legitimate mails are processed. Be sure to place it before the first permit statement to catch all incoming messages.

### Sender Policy Framework

To use the [Sender Policy Framework](/index.php/Sender_Policy_Framework "Sender Policy Framework") with Postfix, [install](/index.php/Install "Install") [python-postfix-policyd-spf](https://aur.archlinux.org/packages/python-postfix-policyd-spf/).

Edit `/etc/python-policyd-spf/policyd-spf.conf` to your needs. An extensively commented version can be found at `/etc/python-policyd-spf/policyd-spf.conf.commented`. Pay some extra attention to the HELO check policy, as standard settings strictly reject HELO failures.

In the main.cf add a timeout for the policyd:

 `/etc/postfix/main.cf`  `policy-spf_time_limit = 3600s` 

Then add a transport

 `/etc/postfix/master.cf` 
```
policy-spf  unix  -       n       n       -       0       spawn
     user=nobody argv=/usr/bin/policyd-spf
```

Lastly you need to add the policyd to the `smtpd_recipient_restrictions`. To minimize load put it to the end of the restrictions but above any `reject_rbl_client` DNSBL line:

 `/etc/postfix/main.cf` 
```
smtpd_recipient_restrictions=
     ...
     permit_sasl_authenticated
     permit_mynetworks
     reject_unauth_destination
     check_policy_service unix:private/policy-spf
```

You can test your Setup with the following:

 `/etc/python-policyd-spf/policyd-spf.conf`  `defaultSeedOnly = 0` 

### Sender Rewriting Scheme

To use the [Sender Rewriting Scheme](/index.php/Sender_Rewriting_Scheme "Sender Rewriting Scheme") with Postfix, [install](/index.php/Install "Install") [postsrsd](https://aur.archlinux.org/packages/postsrsd/) and adjust the settings:

 `/etc/postsrsd/postsrsd` 
```
SRS_DOMAIN=yourdomain.tld
SRS_EXCLUDE_DOMAINS=yourotherdomain.tld,yet.anotherdomain.tld
SRS_SEPARATOR==
SRS_SECRET=/etc/postsrsd/postsrsd.secret
SRS_FORWARD_PORT=10001
SRS_REVERSE_PORT=10002
RUN_AS=postsrsd
CHROOT=/usr/lib/postsrsd
```

Enable and start the daemon, making sure it runs after reboot as well. Then configure Postfix accordingly by tweaking the following lines:

 `/etc/postfix/main.cf` 
```
sender_canonical_maps = tcp:localhost:10001
sender_canonical_classes = envelope_sender
recipient_canonical_maps = tcp:localhost:10002
recipient_canonical_classes= envelope_recipient,header_recipient
```

Restart Postfix and start forwarding mail.

## Troubleshooting

### Warning: "database /etc/postfix/*.db is older than source file .."

If you get one or both warnings with `journalctl`

```
warning: database /etc/postfix/virtual.db is older than source file /etc/postfix/virtual
warning: database /etc/postfix/transport.db is older than source file /etc/postfix/transport

```

then you can fix it by using these commands depending on the messages you get

```
postmap /etc/postfix/transport
postmap /etc/postfix/virtual

```

and restart `postfix.service`

## See also

*   [Official documentation](http://www.postfix.org/documentation.html)
*   [Postfix Ubuntu documentation](https://help.ubuntu.com/community/Postfix)
*   [Out of Office](http://linox.be/index.php/2005/07/13/44/) for Squirrelmail