**Estado de la traducción**
Este artículo es una traducción de [SSMTP](/index.php/SSMTP "SSMTP"), revisada por última vez el **2019-11-22**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=SSMTP&diff=0&oldid=589734) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [OpenSMTPD](/index.php/OpenSMTPD "OpenSMTPD")
*   [msmtp](/index.php/Msmtp "Msmtp")
*   [S-nail](/index.php/S-nail "S-nail")

SSMTP es un programa que entrega correo electrónico desde un ordenador local a un servidor de correo configurado (mailhub). No es un servidor de correo (como si lo es el servidor de correo rico en funciones [sendmail](/index.php/Sendmail "Sendmail")) y no recibe correo, ni expande alias, ni administra una cola. Uno de sus usos principales es reenviar el correo electrónico automatizado (como las alertas del sistema) desde su equipo a una dirección de correo electrónico externa.

**Nota:** ssmtp está desatendido Considere usar algo como [msmtp](/index.php/Msmtp "Msmtp") o [OpenSMTPD](/index.php/OpenSMTPD "OpenSMTPD") en su lugar.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Reenviar a un servidor de correo de Gmail](#Reenviar_a_un_servidor_de_correo_de_Gmail)
*   [3 Seguridad](#Seguridad)
*   [4 Enviar correo electrónico](#Enviar_correo_electrónico)
    *   [4.1 Archivos adjuntos](#Archivos_adjuntos)
    *   [4.2 Correo a usuarios locales](#Correo_a_usuarios_locales)
*   [5 Referencias](#Referencias)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [ssmtp](https://aur.archlinux.org/packages/ssmtp/).

## Reenviar a un servidor de correo de Gmail

Para configurar SSMTP, deberá editar su archivo de configuración (`/etc/ssmtp/ssmtp.conf`) e ingresar la configuración de su cuenta.

*   Si su cuenta de Gmail está protegida con autenticación de dos factores, debe generar una [App Password](https://support.google.com/mail/answer/185833) única para usar en `ssmtp.conf`. Puede hacerlo en su página [App Passwords](https://myaccount.google.com/apppasswords) de Google. Use su nombre de usuario de Gmail (no el nombre de la aplicación) en la línea `AuthUser` y use la contraseña de 16 caracteres generada en la línea `AuthPass` (se pueden omitir espacios en la contraseña).
*   Si *no* usa la autenticación de dos factores, debe [permitir el acceso a aplicaciones no seguras](https://support.google.com/accounts/answer/6010255). Puede hacerlo en su página [Less Secure Apps](https://myaccount.google.com/lesssecureapps) de Google.

 `/etc/ssmtp/ssmtp.conf` 
```

# El usuario que recibe todos los correos (UID <1000, generalmente el administrador)
root=username@gmail.com

# El servidor de correo (donde se envía el correo), tanto el puerto 465 como el 587 deberían ser aceptables
# Véase también https://support.google.com/mail/answer/78799
mailhub=smtp.gmail.com:587

# La dirección de donde proviene el correo para la autenticación del usuario
rewriteDomain=gmail.com

# El nombre de equipo completo. Debe estar formado correctamente el nombre de dominio completo o GMail rechazará la conexión.
hostname=yourlocalhost.yourlocaldomain.tld

# Utilice SSL/TLS antes de comenzar la negociación
TLS_CA_FILE=/etc/ssl/certs/ca-certificates.crt
UseTLS=Yes
UseSTARTTLS=Yes

# Usuario/Contraseña
AuthUser=username
AuthPass=password
AuthMethod=LOGIN

# 'From header' del correo electrónico, ¿puede sobrescribir el dominio predeterminado?
FromLineOverride=yes

```

**Nota:** tenga en cuenta que la configuración que se muestra es un ejemplo para Gmail. Puede que tenga que usar otras configuraciones. Si no funciona como se esperaba, lea la página de manual [ssmtp(8)](https://manpages.debian.org/stretch/ssmtp/ssmtp.8.en.html).

Crear alias para nombres de usuario locales (opcional):

 `/etc/ssmtp/revaliases` 
```
root:username@gmail.com:smtp.gmail.com:587
mainuser:username@gmail.com:smtp.gmail.com:587
```

Para probar si el servidor de Gmail reenviará correctamente su correo electrónico:

 `$ echo -n 'Subject: test

Testing ssmtp' | sendmail -v tousername@example.com` 

Cambie el texto de 'From' editando `/etc/passwd` para recibir correo de 'root at myhost' en lugar de solo 'root'.

```
# chfn -f 'root at myhost' root
# chfn -f 'mainuser at myhost' mainuser
```

Que cambia `/etc/passwd` a:

 `$ grep myhost /etc/passwd` 
```
root:x:0:0:root at myhost,,,:/root:/bin/bash
mainuser:x:1000:1000:mainuser at myhost,,,:/home/mainuser:/bin/bash
```

## Seguridad

Debido a que su contraseña de correo electrónico se almacena como texto sin formato en `/etc/ssmtp/ssmtp.conf`, es importante que este archivo sea seguro. Por defecto, todo el directorio `/etc/ssmtp` es accesible solo por root y el grupo mail. El binario `/usr/bin/ssmtp` se ejecuta como el grupo mail y puede leer este archivo. No hay ninguna razón para agregarse usted u otros usuarios al grupo mail.

## Enviar correo electrónico

Para enviar correos electrónicos desde el terminal, haga lo siguiente:

```
$ echo -e "Subject: this is the subject

this is the body" | mail user@example.com

```

o interactivamente como:

```
$ sendmail username@example.com
Subject: este es mi asunto
CC: opcional@ejemplo.com

(Ahora puede escribir el texto aquí)

```

**Nota:** cuando utilice «mail» de forma interactiva, después de escribir *Subject: asunto* y otros encabezados, presione «intro» dos veces y luego escriba el texto. Presione `Ctrl`+`d` en una línea en blanco para finalizar su mensaje y enviarlo automáticamente.

Un método alternativo para enviar correos electrónicos es crear un archivo de texto y enviarlo con *ssmtp* o *mail*

 `test-mail.txt` 
```
To:nombreusuario@ejemplo.com
From:sucuenta@gmail.com
Subject: Prueba

Este es un correo de prueba.
```

Envíe el archivo `test-mail.txt`:

```
$ sendmail -t < test-mail.txt

```

Algunos usuarios pueden preferir la sintaxis de *mail* con [s-nail](https://www.archlinux.org/packages/?name=s-nail), [mailutils](https://www.archlinux.org/packages/?name=mailutils), u otros proveedores de *mailx* en su lugar. Por ejemplo, *mail* tiene opciones para proporcionar el «*subject*» como un argumento. *mail* requiere *sendmail* y puede usar [ssmtp](https://aur.archlinux.org/packages/ssmtp/) como *sendmail*.

### Archivos adjuntos

Si necesita agregar archivos adjuntos, instale y configure [Mutt](/index.php/Mutt "Mutt") y [Msmtp](/index.php/Msmtp "Msmtp") y luego vea la sugerencia en [nixcraft](http://www.cyberciti.biz/tips/sending-mail-with-attachment.html).

Alternativamente, puede adjuntar usando *uuencode* de [sharutils](https://www.archlinux.org/packages/?name=sharutils). Para adjuntar 'file.txt' como 'myfile.txt':

```
$ uuencode file.txt myfile.txt | sendmail user@example.com

```

### Correo a usuarios locales

Los mensajes enviados a usuarios locales (o cualquier otra dirección que no termine en *@fqdn* se tratan de una de estas dos maneras:

*   el usuario de destino tiene UID < 1000 — la dirección se reemplaza por la dirección definida por `root=user@fqdn` en `/etc/ssmtp/ssmtp.conf`;
*   el usuario de destino tiene UID ≥ 1000 o el usuario es desconocido — el valor de `rewriteDomain=` en `/etc/ssmtp/ssmtp.conf` se agrega al final del identificador del usuario.

Esto puede generar problemas si los usuarios locales en su sistema no son también usuarios válidos en su `rewriteDomain`, pero están recibiendo correo de los servicios del sistema, especialmente si su dominio de reescritura es un servicio público como`gmail.com`.

Para evitar esto, puede usar *mail* desde [s-nail](https://www.archlinux.org/packages/?name=s-nail). La orden *mail* puede leer los alias definidos en `/etc/mail.rc`. Ejemplo:

 `$ grep alias /etc/mail.rc` 
```
alias git git<username@example.com>
alias archuser 'My Name'<someone@example.com>
```

Luego puede canalizar mensajes en *mail* en lugar de *sendmail*:

```
$ echo -e "Hey archuser." | mail archuser

```

**Nota:** es posible que tenga la tentación de vincular *sendmail* a `/bin/mail`. No haga eso. *sendmail* y *mail* tienen una sintaxis diferente para los argumentos y la entrada estándar. Es mejor encontrar los procesos que utiliza «sendmail» directamente y configurarlos para usar «mail» en su lugar.

## Referencias

*   [SSMTP y Gmail en los foros de Arch](https://bbs.archlinux.org/viewtopic.php?pid=446831)
*   [Enviar correo electrónico desde su sistema con sSMTP](http://tombuntu.com/index.php/2008/10/21/sending-email-from-your-system-with-ssmtp/)
*   [La guía Qnd para ssmtp](http://www.scottro.net/qnd/qnd-ssmtp.html)
*   [Soporte de GMail — Configuración de otros clientes de correo](https://support.google.com/mail/answer/78799)