**Estado de la traducción**
Este artículo es una traducción de [Bazaar](/index.php/Bazaar "Bazaar"), revisada por última vez el **2018-10-21**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Bazaar&diff=0&oldid=549368) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[Bazaar](https://bazaar.canonical.com/) es un sistema de control de versiones que le ayuda a rastrear el historial del proyecto a lo largo del tiempo y a colaborar fácilmente con otros.

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [bzr](https://www.archlinux.org/packages/?name=bzr). Para la versión de desarrollo, instale el paquete [bzr-bzr](https://aur.archlinux.org/packages/bzr-bzr/). El explorador de Bazaar lo proporciona el paquete [bzr-explorer](https://aur.archlinux.org/packages/bzr-explorer/).

## Utilización

Véase [bzr(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/bzr.1).

### Configurando el servidor Bazaar con xinetd

Añada un [usuario](/index.php/User_(Espa%C3%B1ol) "User (Español)") `*bzr-usr*` si es necesario.

Cree un repositorio:

```
$ bzr init /home/bzr/repo.bzr
$ chown -R *bzr_usr* /home/bzr/repo.bzr

```

Añada la configuración para *xinetd*:

```
service bzr
{
	flags			= REUSE
	socket_type		= stream
	wait			= no
	user			= *bzr_usr*
	server			= /usr/bin/bzr
	server_args		= serve --inet --directory=/home/bzr/repo.bzr
	env			= HOME=/home/bzr
	log_on_failure		+= USERID
	disable			= no
	cps			= 50 10
	instances		= 60
}
```