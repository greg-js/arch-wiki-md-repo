**Estado de la traducción**
Este artículo es una traducción de [Gobby](/index.php/Gobby "Gobby"), revisada por última vez el **2018-12-25**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Gobby&diff=0&oldid=560412) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

De la [página web del proyecto](http://gobby.0x539.de/trac/wiki):

*Gobby es un editor colaborativo gratuito que admite múltiples documentos en una sesión y un chat multiusuario.* Utiliza GTK+ 2 como su toolkit de ventanas y, por lo tanto, se integra muy bien en el entorno de escritorio GNOME*.*

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [gobby](https://www.archlinux.org/packages/?name=gobby). Para ejecutar el protocolo de servidor Infininote sin el front end Gobby, instale [libinfinity](https://www.archlinux.org/packages/?name=libinfinity)

## Utilización de Infininote

Para iniciar la porción del servidor, ejecute

```
/usr/bin/infinoted-0.6 --security-policy=no-tls

```

El servidor solo necesita estar ejecutándose en una máquina.

Luego, ejecute el cliente Gobby y conéctese al servidor a través de la IP o el localhost.

Si prefiere tener cifrado, dispone de TLS. Utilize:

```
infinoted-0.6 --create-key --create-certificate -k key.pem  -c cert.pem

```

La creación de claves es automática, y puede iniciar el servidor simplemente usando:

```
infinoted-0.6 -k key.pem  -c cert.pem

```

## Véase también

*   [Infinoted wiki](http://gobby.0x539.de/trac/wiki/Infinote/)