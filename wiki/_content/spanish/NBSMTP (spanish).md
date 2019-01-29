**Estado de la traducción**
Este artículo es una traducción de [NBSMTP](/index.php/NBSMTP "NBSMTP"), revisada por última vez el **2019-01-28**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=NBSMTP&diff=0&oldid=565085) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

De la página del manual de **nbSMTP**:

	*nbSMTP es un cliente SMTP ligero. Simplemente toma un mensaje de STDIN y lo envía a un relayhost. Un relayhost está pensado para ser un servidor SMTP completo y realmente enviará el mensaje*.

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [nbsmtp](https://aur.archlinux.org/packages/nbsmtp/) del [AUR](/index.php/AUR_(Espa%C3%B1ol) "AUR (Español)").

## Reenviar a un servidor de correo de Gmail

Para configurar **nbSMTP**, edite el archivo de configuración `~/.nbsmtprc` e ingrese la configuración de su cuenta:

```
relayhost=smtp.gmail.com
port=587
use_starttls=True
fromaddr=myusername@gmail.com
auth_user=myusername@gmail.com
auth_pass=myultrasecretpassword

```

Tenga cuidado con los permisos de este archivo. Se recomienda ejecutar lo siguiente:

```
chmod 600 ~/.nbsmtprc

```

Para probar la configuración, cree un archivo llamado `testemail` con el siguiente contenido:

```
To: myusername@gmail.com
From: myusername@gmail.com
Subject: nbsmtp test
hello email world

```

y luego ejecute:

```
/usr/bin/nbsmtp < testemail

```