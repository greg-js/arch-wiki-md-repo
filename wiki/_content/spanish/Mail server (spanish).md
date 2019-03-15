**Estado de la traducción**
Este artículo es una traducción de [Mail server](/index.php/Mail_server "Mail server"), revisada por última vez el **2019-03-12**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Mail_server&diff=0&oldid=568443) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Un servidor de correo consta de varios componentes. Un [agente de transferencia de correos](https://en.wikipedia.org/wiki/es:Servidor_de_correo (MUA), debe ejecutar un servidor [POP3](https://en.wikipedia.org/wiki/es:Protocolo_de_oficina_de_correo "wikipedia:es:Protocolo de oficina de correo") y/o [IMAP](https://en.wikipedia.org/wiki/es:Protocolo_de_acceso_a_mensajes_de_Internet "wikipedia:es:Protocolo de acceso a mensajes de Internet").

```
+--------+  SMTP  +---+  +---+                     +------------------+
|Otro MTA| <----> |MTA|--|MDA|-> Almacenamiento <- |Servidor POP3/IMAP|
+--------+        +---+  +---+                     +------------------+
                    ^                                      ^
                    |      SMTP       +---+                |
                    +-----------------|MUA|----------------+
                                      +---+

```

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Software](#Software)
    *   [1.1 Servidores POP3/IMAP](#Servidores_POP3/IMAP)
    *   [1.2 MDAs autónomos](#MDAs_autónomos)
*   [2 Puertos](#Puertos)
*   [3 Registro MX](#Registro_MX)
*   [4 TLS](#TLS)
*   [5 Autenticación](#Autenticación)
    *   [5.1 Marco de políticas del remitente](#Marco_de_políticas_del_remitente)
    *   [5.2 Esquema de reescritura del remitente](#Esquema_de_reescritura_del_remitente)
    *   [5.3 DKIM](#DKIM)
*   [6 Sitios web de prueba](#Sitios_web_de_prueba)
*   [7 Consejos y trucos](#Consejos_y_trucos)

## Software

Todos estos programas, excepto Sendmail, incluyen un agente de entrega de correos.

*   **[Exim](/index.php/Exim "Exim")** — Un agente de transferencia de correos altamente configurable.

	[https://exim.org/](https://exim.org/) || [exim](https://www.archlinux.org/packages/?name=exim)

*   **[OpenSMTPD](/index.php/OpenSMTPD "OpenSMTPD")** — Un agente de transferencia de correos, parte del proyecto OpenBSD.

	[https://opensmtpd.org/](https://opensmtpd.org/) || [opensmtpd](https://www.archlinux.org/packages/?name=opensmtpd)

*   **[Postfix](/index.php/Postfix_(Espa%C3%B1ol) "Postfix (Español)")** — Un agente de transferencia de correos, destinado a ser rápido, fácil de administrar y seguro.

	[http://www.postfix.org/](http://www.postfix.org/) || [postfix](https://www.archlinux.org/packages/?name=postfix)

*   **[Sendmail](/index.php/Sendmail "Sendmail")** — Un conocido agente de transferencia de correos.

	[http://www.sendmail.org/](http://www.sendmail.org/) || [sendmail](https://aur.archlinux.org/packages/sendmail/)

### Servidores POP3/IMAP

*   **[Courier](/index.php/Courier "Courier")** — Un agente de transferencia de correos, que proporciona servicios de POP3, IMAP, correo web y listas de correo como componentes individuales.

	[https://www.courier-mta.org/](https://www.courier-mta.org/) || [courier-mta](https://aur.archlinux.org/packages/courier-mta/)

*   **[Cyrus IMAP](https://en.wikipedia.org/wiki/Cyrus_IMAP_server "wikipedia:Cyrus IMAP server")** — Un agente de transferencia de correos con un formato de cola de correos personalizado, proporciona servicios POP3 e IMAP.

	[https://www.cyrusimap.org/](https://www.cyrusimap.org/) || [cyrus-imapd](https://aur.archlinux.org/packages/cyrus-imapd/)

*   **[Dovecot](/index.php/Dovecot "Dovecot")** — Un servidor IMAP y POP3 escrito para ser seguro, rápido y fácil de configurar.

	[https://dovecot.org/](https://dovecot.org/) || [dovecot](https://www.archlinux.org/packages/?name=dovecot)

*   **[UW IMAP](/index.php/UW_IMAP "UW IMAP")** — Un servidor IMAP/POP.

	[https://www.washington.edu/imap/](https://www.washington.edu/imap/) || [imap](https://www.archlinux.org/packages/?name=imap)

### MDAs autónomos

*   **[fdm](/index.php/Fdm_(Espa%C3%B1ol) "Fdm (Español)")** — Un programa simple para entregar y filtrar correos.

	[https://github.com/nicm/fdm](https://github.com/nicm/fdm) || [fdm](https://www.archlinux.org/packages/?name=fdm)

*   **[Procmail](/index.php/Procmail "Procmail")** — Un programa para filtrar, clasificar y almacenar correos electrónicos (sin mantenimiento).

	[http://www.procmail.org/](http://www.procmail.org/) || [procmail](https://www.archlinux.org/packages/?name=procmail)

*   **Maildrop** — Un filtro de correos/agente de entrega de correos utilizado por el servidor de correos Courier.

	[https://www.courier-mta.org/maildrop/](https://www.courier-mta.org/maildrop/) || [courier-maildrop](https://aur.archlinux.org/packages/courier-maildrop/)

Véase también [Wikipedia:Comparison of e-mail servers](https://en.wikipedia.org/wiki/Comparison_of_e-mail_servers "wikipedia:Comparison of e-mail servers").

## Puertos

| Propósito | Puerto | Protocolo | Cifrado |
| Aceptar correos de otros MTAs. | 25 | SMTP | STARTTLS |
| Aceptar envíos de MUAs. | 587 | SMTP | STARTTLS |
| 465 | [SMTPS](https://en.wikipedia.org/wiki/SMTPS "wikipedia:SMTPS") | implicit TLS |
| Permitir a MUAs acceder al correo. | 110 | POP3 | STARTTLS |
| 995 | POP3S | implicit TLS |
| 143 | IMAP | STARTTLS |
| 993 | IMAPS | implicit TLS |

**Nota:** El TLS implícito es más seguro que [STARTTLS](https://en.wikipedia.org/wiki/es:STARTTLS "wikipedia:es:STARTTLS") porque este último es vulnerable al [ataque de intermediario](https://en.wikipedia.org/wiki/es:Ataque_de_intermediario "wikipedia:es:Ataque de intermediario"). Para más información, véase [[1]](https://serverfault.com/questions/523804/is-starttls-less-safe-than-tls-ssl) y el [RFC:8314](https://tools.ietf.org/html/rfc8314 "rfc:8314").

## Registro MX

El alojamiento de un servidor de correos requiere un [nombre de dominio](https://en.wikipedia.org/wiki/es:Dominio_de_Internet que apunte al nombre de dominio de su agente de transferencia de correos. El nombre de dominio utilizado como el valor del registro MX debe asignarse a al menos un [registro de direcciones](https://en.wikipedia.org/wiki/es:A_(registro) (A, AAAA) y no debe tener un [registro CNAME](https://en.wikipedia.org/wiki/CNAME_record "wikipedia:CNAME record") para cumplir con el [RFC 2181](https://tools.ietf.org/html/rfc2181#section-10.3 "rfc:2181"), de lo contrario no podrá recibir correos de algunos servidores de correo. La configuración de los registros DNS se realiza generalmente desde la interfaz de configuración de su [registrador de nombres de dominio](https://en.wikipedia.org/wiki/es:Registrador_de_dominios "wikipedia:es:Registrador de dominios").

## TLS

**Advertencia:** Si implementa [TLS](https://en.wikipedia.org/wiki/es:Transport_Layer_Security "wikipedia:es:Transport Layer Security"), asegúrese de seguir [TLS en el servidor](/index.php/Server-side_TLS "Server-side TLS") para evitar vulnerabilidades.

Para obtener un certificado, véase [OpenSSL#Usage](/index.php/OpenSSL#Usage "OpenSSL").

## Autenticación

Hay varias técnicas de [autenticación de correo](https://en.wikipedia.org/wiki/Email_authentication "wikipedia:Email authentication").

### Marco de políticas del remitente

De [Wikipedia](https://en.wikipedia.org/wiki/es:Sender_Policy_Framework "wikipedia:es:Sender Policy Framework"):

	**Marco de políticas del remitente** *(Sender Policy Framework, o SPF)* es un protocolo de validación de correos electrónicos diseñado para detectar y bloquear la falsificación de correos electrónicos al proporcionar un mecanismo para permitir que los intercambiadores de correos *(mail exchangers)* verifiquen que el correo entrante de un dominio provenga de una dirección IP autorizada por los administradores de ese dominio.

Para permitir que otros intercambiadores de correo validen los correos aparentemente enviados desde su dominio, debe establecer un registro TXT de DNS como se explica en [el artículo de Wikipedia](https://en.wikipedia.org/wiki/es:Sender_Policy_Framework "wikipedia:es:Sender Policy Framework") (también hay un [asistente en línea](https://www.spfwizard.net/)). Para validar el correo entrante usando SPF, debe configurar su agente de transferencia de correos para utilizar una implementación de SPF. Hay varias [impleementaciones SPF](http://www.openspf.org/Implementations) disponibles, [libspf2](https://www.archlinux.org/packages/?name=libspf2), [perl-mail-spf](https://www.archlinux.org/packages/?name=perl-mail-spf) y [perl-mail-spf-query](https://www.archlinux.org/packages/?name=perl-mail-spf-query) que se puede encontrar en los repositorios oficiales.

<caption>Soporte de validación SPF</caption>
| [Courier](/index.php/Courier "Courier") | Sí, incorporado |
| [Postfix](/index.php/Postfix_(Espa%C3%B1ol) "Postfix (Español)") | [Sí](/index.php/Postfix_(Espa%C3%B1ol)#Marco_de_políticas_del_remitente "Postfix (Español)") |
| [Sendmail](/index.php/Sendmail "Sendmail") | mediante [Milter](https://en.wikipedia.org/wiki/es:Milter "wikipedia:es:Milter") y [spfmilter-acme](https://aur.archlinux.org/packages/spfmilter-acme/) |
| [Exim](/index.php/Exim "Exim") | [experimental](https://github.com/Exim/exim/wiki/SPF), requiere [libspf2](https://www.archlinux.org/packages/?name=libspf2) |
| [OpenSMTPD](/index.php/OpenSMTPD "OpenSMTPD") | No |
| [Cyrus IMAP](https://en.wikipedia.org/wiki/Cyrus_IMAP_server "wikipedia:Cyrus IMAP server") | ? |

Los siguientes sitios web le permiten validar su registro SPF:

*   [Verificador de registro SPF](http://www.kitterman.com/spf/validate.html)
*   [Prueba de correo electrónico SPF](http://www.appmaildev.com/en/spf)

**Sugerencia:** SPF puede ser útil incluso para dominios que no se utilizan para enviar correos electrónicos. La publicación de una política como `v=spf1 -all` hace que cualquier servidor de correo que aplique SPF rechace los correos electrónicos de su nombre de dominio, evitando así el mal uso.

### Esquema de reescritura del remitente

El [esquema de reescritura del remitente](https://en.wikipedia.org/wiki/Sender_Rewriting_Scheme "wikipedia:Sender Rewriting Scheme") (SRS) es un esquema seguro para permitir rebotes *(bounces)* reenviables para correos electrónicos reenviados del servidor sin romper el [#Marco de políticas del remitente](#Marco_de_políticas_del_remitente).

Para [Postfix](/index.php/Postfix_(Espa%C3%B1ol) "Postfix (Español)"), véase [Esquema de reescritura del remitente](/index.php/Postfix_(Espa%C3%B1ol)#Esquema_de_reescritura_del_remitente "Postfix (Español)").

### DKIM

El [correo identificado por claves de dominio](https://en.wikipedia.org/wiki/es:DomainKeys_Identified_Mail "wikipedia:es:DomainKeys Identified Mail") (DKIM) es un método de autenticación de correo electrónico a nivel de dominio diseñado para detectar la falsificación de correos electrónicos.

Las implementaciones DKIM disponibles son [OpenDKIM](/index.php/OpenDKIM "OpenDKIM") y [dkimproxy](https://www.archlinux.org/packages/?name=dkimproxy).

## Sitios web de prueba

Hay varios sitios web útiles que pueden ayudarle a probar los registros DNS, la capacidad de entrega y el soporte de cifrado.

*   [https://mxtoolbox.com/](https://mxtoolbox.com/)
*   [http://ismyemailworking.com/](http://ismyemailworking.com/)
*   [https://www.mail-tester.com/](https://www.mail-tester.com/)
*   [https://www.checktls.com/](https://www.checktls.com/)
*   [https://pingability.com/zoneinfo.jsp](https://pingability.com/zoneinfo.jsp)

## Consejos y trucos

La mayoría de los servidores de correo pueden configurarse para eliminar las direcciones IP de los usuarios y el [agente de usuario](https://en.wikipedia.org/wiki/es:Agente_de_usuario "wikipedia:es:Agente de usuario") del correo saliente.

Los extras disponibles que normalmente se pueden integrar son:

*   [ClamAV](/index.php/ClamAV_(Espa%C3%B1ol) "ClamAV (Español)") para detectar virus en los correos electrónicos
*   [SpamAssassin](/index.php/SpamAssassin "SpamAssassin") para identificar y filtrar el spam
*   [Sieve](https://en.wikipedia.org/wiki/Sieve_(mail_filtering_language) – un lenguaje de programación de filtrado de correo
*   [webmail](https://en.wikipedia.org/wiki/es:Webmail "wikipedia:es:Webmail") como [Roundcube](/index.php/Roundcube "Roundcube") o [Squirrelmail](/index.php/Squirrelmail "Squirrelmail")