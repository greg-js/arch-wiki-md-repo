**Estado de la traducción**
Este artículo es una traducción de [Classroom/git 2016](/index.php/Classroom/git_2016 "Classroom/git 2016"), revisada por última vez el **2018-10-05**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Classroom/git_2016&diff=0&oldid=546271) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Esta es la página de registro para una clase/taller de GIT que se llevará a cabo en 2016\. Solo necesita registrarse si desea acceder al repositorio de git alojado por Arch Linux Women para la clase. Todavía puedes ir a la clase y aprender sin registrarte. Las instrucciones para compartir su clave ssh se encuentran a continuación.

## Contents

*   [1 Cree una clave SSH](#Cree_una_clave_SSH)
*   [2 Comparta su clave pública](#Comparta_su_clave_p.C3.BAblica)
*   [3 Registrase](#Registrase)
    *   [3.1 Ayuda](#Ayuda)

### Cree una clave SSH

Necesitará una clave ssh para acceder a git en los servidores [Arch Women](https://archwomen.org). Si no tiene una clave, puede crearla ejecutando:

```
 ssh-keygen

```

Para obtener más información sobre la creación de pares de claves, véase [Claves SSH](/index.php/SSH_keys "SSH keys").

### Comparta su clave pública

Después de generar pares de claves, debe tener una clave pública y una privada en `~/.ssh`. La clave pública tiene la extensión `.pub`. Para pegar su clave pública a [ptpb.pw](https://ptpb.pw) haga:

```
cat ~/.ssh/id_rsa.pub | curl -F c=@- https://ptpb.pw/

```

**Asegúrese** de que la clave que pegue tiene la extensión `.pub`, no querrá compartir públicamente su clave privada.

## Registrase

Añada el apodo que desee usar en git y un enlace a su clave pública a la tabla.

| Apodo | Clave pública SSH |
| meskarune | [public key](https://ptpb.pw/vj4X/sh) |
| ripelascra | [public key](https://ptpb.pw/9HEG/sh) |
| therue | [public key](https://ptpb.pw/2pnP/sh) |
| cirrusUK | [public key](https://ptpb.pw/6di9/sh) |
| 5225225 | [public key](https://ptpb.pw/TVjm/sh) |
| merriment | [public key](https://ptpb.pw/OtzU/sh) |
| apodo | clave |

### Ayuda

Si tiene preguntas o necesita ayuda adicional, únase a los canales irc #archlinux-newbie o #archlinux-women en irc.freenode.net.