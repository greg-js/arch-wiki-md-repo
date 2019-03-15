**Estado de la traducción**
Este artículo es una traducción de [Postfix](/index.php/Postfix "Postfix"), revisada por última vez el **2019-03-10**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Postfix&diff=0&oldid=568296) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

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
        *   [6.1.4 Solución de problemas](#Solución_de_problemas)
    *   [6.2 SpamAssassin](#SpamAssassin)
        *   [6.2.1 Configuración genérica independiente de SpamAssassin](#Configuración_genérica_independiente_de_SpamAssassin)
        *   [6.2.2 SpamAssassin combinado con Dovecot LDA / Sieve (Filtrado de correo)](#SpamAssassin_combinado_con_Dovecot_LDA_/_Sieve_(Filtrado_de_correo))
        *   [6.2.3 SpamAssassin combinado con Dovecot LMTP / Sieve](#SpamAssassin_combinado_con_Dovecot_LMTP_/_Sieve)
    *   [6.3 Procesamiento de correo basado en reglas](#Procesamiento_de_correo_basado_en_reglas)
    *   [6.4 Marco de políticas del remitente](#Marco_de_políticas_del_remitente)
    *   [6.5 Esquema de reescritura del remitente](#Esquema_de_reescritura_del_remitente)
*   [7 Solución de problemas](#Solución_de_problemas_2)
    *   [7.1 Warning: "database /etc/postfix/*.db is older than source file .."](#Warning:_"database_/etc/postfix/*.db_is_older_than_source_file_..")
*   [8 Véase también](#Véase_también)

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

Para añadir su propia lista de clientes en la lista blanca además de los predeterminados, cree el archivo `/etc/postfix/whitelist_clients.local` e introduzca un dominio por línea, luego [reinicie](/index.php/Restart_(Espa%C3%B1ol) "Restart (Español)") `postgrey.service` para que los cambios surtan efecto.

#### Solución de problemas

Si especifica `--unix=/path/to/socket` y el archivo de socket no se crea, asegúrese de haber eliminado el valor predeterminado `--inet=127.0.0.1:10030` del archivo de servicio.

Para una documentación completa de las posibles opciones véase `perldoc postgrey`.

### SpamAssassin

Esta sección describe cómo integrar [SpamAssassin](/index.php/SpamAssassin "SpamAssassin").

#### Configuración genérica independiente de SpamAssassin

**Nota:** Si desea combinar SpamAssassin y Dovecot Mail Filtering, ignore las siguientes dos líneas y continúe después.

Edite `/etc/postfix/master.cf` y añada el filtro de contenido bajo smtp.

```
smtp      inet  n       -       n       -       -       smtpd
  -o content_filter=spamassassin
```

También añada la siguiente entrada de servicio para SpamAssassin.

```
spamassassin unix -     n       n       -       -       pipe
  flags=R user=spamd argv=/usr/bin/vendor_perl/spamc -e /usr/bin/sendmail -oi -f ${sender} ${recipient}
```

Ahora puede [iniciar](/index.php/Start_(Espa%C3%B1ol) "Start (Español)") y [activar](/index.php/Enable_(Espa%C3%B1ol) "Enable (Español)") `spamassassin.service`.

#### SpamAssassin combinado con Dovecot LDA / Sieve (Filtrado de correo)

Configure LDA y Sieve-Plugin como se describe en [Dovecot#Sieve](/index.php/Dovecot#Sieve "Dovecot"). Pero ignore la última línea `mailbox_command...` .

En su lugar, añada una tubería *(pipe)* en `/etc/postfix/master.cf`:

```
 dovecot   unix  -       n       n       -       -       pipe
       flags=DRhu user=vmail:vmail argv=/usr/bin/vendor_perl/spamc -u spamd -e /usr/lib/dovecot/dovecot-lda -f ${sender} -d ${recipient}

```

Y actívelo en `/etc/postfix/main.cf`:

```
 virtual_transport = dovecot

```

#### SpamAssassin combinado con Dovecot LMTP / Sieve

Configure LMTP y Sieve como se describe en [Dovecot#Sieve](/index.php/Dovecot#Sieve "Dovecot").

Edite `/etc/dovecot/conf.d/90-plugins.conf` y añada:

```
 sieve_before = /etc/dovecot/sieve.before.d/
 sieve_extensions = +vnd.dovecot.filter
 sieve_plugins = sieve_extprograms
 sieve_filter_bin_dir = /etc/dovecot/sieve-filter
 sieve_filter_exec_timeout = 120s #this is often needed for the long running spamassassin scans, default is otherwise 10s

```

Cree el directorio y coloque spamassassin como un binario que pueda ser ejecutado por dovecot:

```
 # mkdir /etc/dovecot/sieve-filter
 # ln -s /usr/bin/vendor_perl/spamc /etc/dovecot/sieve-filter/spamc

```

Cree un nuevo archivo, `/etc/dovecot/sieve.before.d/spamassassin.sieve` que contenga:

```
 require [ "vnd.dovecot.filter" ];
 filter "spamc" [ "-d", "127.0.0.1", "--no-safe-fallback" ];

```

Compile las reglas sieve `spamassassin.svbin`:

```
 # cd /etc/dovecot/sieve.before.d
 # sievec spamassassin.sieve

```

Finalmente, [reinicie](/index.php/Restart_(Espa%C3%B1ol) "Restart (Español)") `dovecot.service`.

### Procesamiento de correo basado en reglas

Con los servicios de políticas se puede ajustar fácilmente el comportamiento de Postfix en la entrega de correos. [postfwd](https://www.archlinux.org/packages/?name=postfwd) y policyd ([policyd-mysql](https://aur.archlinux.org/packages/policyd-mysql/), [policyd-pgsql](https://aur.archlinux.org/packages/policyd-pgsql/) o [policyd-sqlite](https://aur.archlinux.org/packages/policyd-sqlite/)) proporcionan servicios para hacerlo. Esto le permite, por ejemplo, implementar listas grises y negras de remitentes y receptores, así como el control de políticas [SPF](/index.php/SPF "SPF").

Los servicios de políticas son servicios independientes y están conectados a Postfix tal que así:

 `/etc/postfix/main.cf` 
```
smtpd_recipient_restrictions =
  ...
  check_policy_service unix:/run/policyd.sock
  check_policy_service inet:127.0.0.1:10040

```

La colocación de los servicios de políticas al final de la cola reduce la carga, ya que solo se procesan los correos legítimos. Asegúrese de colocarlo antes de la primera declaración permisiva para capturar todos los mensajes entrantes.

### Marco de políticas del remitente

Para utilizar el [marco de políticas del remitente](/index.php/Sender_Policy_Framework "Sender Policy Framework") con Postfix, [instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") [python-postfix-policyd-spf](https://aur.archlinux.org/packages/python-postfix-policyd-spf/).

Edite `/etc/python-policyd-spf/policyd-spf.conf` a sus necesidades. Una versión ampliamente comentada se puede encontrar en `/etc/python-policyd-spf/policyd-spf.conf.commented`. Preste especial atención a la política de verificación HELO, ya que la configuración estándar rechaza estrictamente los fallos HELO.

En el archivo `main.cf`, añada un tiempo de espera para policyd:

 `/etc/postfix/main.cf`  `policy-spf_time_limit = 3600s` 

A continuación, añada un transporte:

 `/etc/postfix/master.cf` 
```
policy-spf  unix  -       n       n       -       0       spawn
     user=nobody argv=/usr/bin/policyd-spf
```

Por último, debe añadir policyd a `smtpd_recipient_restrictions`. Para minimizar la carga, sitúela al final de las restricciones pero por encima de cualquier línea `reject_rbl_client` DNSBL:

 `/etc/postfix/main.cf` 
```
smtpd_recipient_restrictions=
     ...
     permit_sasl_authenticated
     permit_mynetworks
     reject_unauth_destination
     check_policy_service unix:private/policy-spf
```

Puede comprobar su configuración con lo siguiente:

 `/etc/python-policyd-spf/policyd-spf.conf`  `defaultSeedOnly = 0` 

### Esquema de reescritura del remitente

Para utilizar el [esquema de reescritura del remitente](/index.php/Sender_Rewriting_Scheme "Sender Rewriting Scheme") con Postfix, [instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") [postsrsd](https://aur.archlinux.org/packages/postsrsd/) y ajuste la configuración:

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

Active e inicie el demonio, asegurándose de que se ejecute también después de reiniciar. A continuación, configure Postfix en consecuencia ajustando las siguientes líneas:

 `/etc/postfix/main.cf` 
```
sender_canonical_maps = tcp:localhost:10001
sender_canonical_classes = envelope_sender
recipient_canonical_maps = tcp:localhost:10002
recipient_canonical_classes= envelope_recipient,header_recipient
```

Reinicie Postfix y comience a reenviar correo.

## Solución de problemas

### Warning: "database /etc/postfix/*.db is older than source file .."

Si recibe alguna o ambas advertencias con `journalctl`:

```
warning: database /etc/postfix/virtual.db is older than source file /etc/postfix/virtual
warning: database /etc/postfix/transport.db is older than source file /etc/postfix/transport

```

Entonces puede solucionarlo utilizando estas órdenes dependiendo de los mensajes que reciba:

```
postmap /etc/postfix/transport
postmap /etc/postfix/virtual

```

Y [reiniciar](/index.php/Restart_(Espa%C3%B1ol) "Restart (Español)") `postfix.service`.

## Véase también

*   [Documentación oficial](http://www.postfix.org/documentation.html)
*   [Documentación de Ubuntu sobre Postfix](https://help.ubuntu.com/community/Postfix)
*   [Fuera de la oficina](http://linox.be/index.php/2005/07/13/44/) para Squirrelmail