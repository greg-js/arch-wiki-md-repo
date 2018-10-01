**Estado de la traducción:** este artículo es una versión traducida de [IRC channel](/index.php/IRC_channel "IRC channel"). Fecha de la última traducción/revisión: **2018-09-29**. Puede ayudar a actualizar la traducción, si advierte que la versión inglesa ha cambiado: [ver cambios](https://wiki.archlinux.org/index.php?title=IRC_channel&diff=0&oldid=544842).

Artículos relacionados

*   [ArchWiki:IRC](/index.php/ArchWiki:IRC "ArchWiki:IRC")
*   [Comunidades internacionales](/index.php/International_communities_(Espa%C3%B1ol) "International communities (Español)")
*   [phrik](/index.php/Phrik "Phrik")

**Nota:** No modifique esta página a menos que sea un operador de canal en #archlinux. Le invitamos a que use la página de discusión.

Para unirse a los canales [IRC](https://en.wikipedia.org/wiki/es:Internet_Relay_Chat se incluye en el artículo oficial de [instalación](/index.php/Installation_guide_(Espa%C3%B1ol) "Installation guide (Español)").

Debe familiarizarse con nuestro [código de conducta](/index.php/Code_of_conduct_(Espa%C3%B1ol) "Code of conduct (Español)") y en particular con el de [IRC](/index.php/Code_of_conduct_(Espa%C3%B1ol)#IRC "Code of conduct (Español)") antes de unirse a cualquiera de los canales oficiales. Para obtener una lista de las abreviaturas comúnmente utilizadas, véase [terminología de Arch](/index.php/Arch_terminology_(Espa%C3%B1ol) "Arch terminology (Español)") y [jerga de IRC](http://www.ircbeginner.com/ircinfo/abbreviations.html).

## Contents

*   [1 Canales principales](#Canales_principales)
    *   [1.1 Registro](#Registro)
    *   [1.2 Operadores del canal](#Operadores_del_canal)
*   [2 Otros canales](#Otros_canales)
    *   [2.1 Canales IRC internacionales](#Canales_IRC_internacionales)

## Canales principales

**Nota:**

*   Debido al abuso, varias puertas de enlace y clientes web pueden ser prohibidos algunas veces. Si tiene problemas, use un cliente IRC "*apropiado*" o solicite a uno de los operadores una exención de prohibición (`+e`).
*   Las estadísticas del canal se registran para [#archlinux-offtopic](https://alyp.tk/stats/aotstats.html). Hable con *jp/alyptik* si desea optar por no participar permanentemente.

Esta sección trata sobre [#archlinux](ircs://chat.freenode.net/archlinux), el canal de soporte principal de Arch Linux en [IRC](https://en.wikipedia.org/wiki/es:Internet_Relay_Chat "wikipedia:es:Internet Relay Chat"), y [#archlinux-offtopic](ircs://chat.freenode.net/archlinux-offtopic), el canal social principal de Arch Linux, ambos disponibles en la red [Freenode](https://freenode.net/).

El tema central de **#archlinux** es el soporte y la discusión general sobre Arch Linux.

### Registro

Para reducir los mensajes no deseado *(spam)*, **#archlinux** y **# archlinux-offtopic** tienen el modo de canal configurado en `+r` y `+q $~a`. Esto significa que debe identificarse a través de `NickServ` para poder unirse a estos canales y enviar mensajes, respectivamente. Si no está registrado e identificado, será reenviado a **# archlinux-unregistered**.

Para registrarse en NickServ, siga el [FAQ de freenode](https://freenode.net/kb/answer/registration), así como también `NickServ help` cuando se conecte a *chat.freenode.net*:

```
/query NickServ HELP REGISTER
/query NickServ HELP IDENTIFY

```

**Nota:**

*   Si sucede que `/query` no funciona en su cliente, puede probar con `/quote NickServ <comando>` o `/msg NickServ <comando>`.
*   Algunos clientes de IRC tienen un comportamiento por el cual intentan unirse automáticamente a los canales antes de que se haya identificado con NickServ, y para resolverlo debe habilitar SASL. Busque la documentación de su cliente IRC o consulte la página de freenode [SASL](https://freenode.net/kb/answer/sasl) para encontrar instrucciones sobre como habilitarlo.
*   Puede obtener una lista de personas que pueden ayudarle escribiendo `/msg ChanServ ACCESS #archlinux LIST`, o unirse a **#freenode** y preguntar allí.

### Operadores del canal

Los operadores de arco son operaciones tanto en **#archlinux** como en **#archlinux-offtopic**. Véase la lista a continuación o ejecute `/msg phrik listops` en freenode.

Si por algún motivo necesita la ayuda de un operador, no dude en `/query` o `/msg` a nosotros. Aquí está la lista de operadores a 8 de febrero de 2016:

*   alad
*   brain0
*   falconindy
*   gehidore
*   grawity
*   heftig
*   jelle
*   MrElendig / Mion
*   Namarrgon
*   pid1
*   tigrmesh / tigr
*   vodik
*   wonder / ioni

## Otros canales

El tamaño de nuestra comunidad condujo a la creación de múltiples canales de IRC. Para obtener una lista de todos los canales en **[chat.freenode.net](ircs://chat.freenode.net)** que contienen `archlinux` en su nombre, utilice el comando `/query alis list *archlinux*`.

| Canal | Descripción |
| [#archlinux64](ircs://chat.freenode.net/archlinux64) | Debate específico para x86_64, principalmente en inglés. |
| [#archlinux-aur](ircs://chat.freenode.net/archlinux-aur) | Debate general sobre [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)"). |
| [#archlinux-aurweb](ircs://chat.freenode.net/archlinux-aurweb) | Debate sobre el desarrollo de [aurweb](https://projects.archlinux.org/aurweb.git/). |
| [#archlinux-bugs](ircs://chat.freenode.net/archlinux-bugs) | Debate centrado en errores. |
| [#archlinux-classroom](ircs://chat.freenode.net/archlinux-classroom) | Un proyecto que desarrolla y aloja clases para la comunidad Arch Linux. |
| [#archlinux-devops](ircs://chat.freenode.net/archlinux-devops) | Debate sobre la infraestructura interna de Arch Linux y devops. |
| [#archlinux-multilib](ircs://chat.freenode.net/archlinux-multilib) | Debate sobre el proyecto Arch Linux Multilib y empaquetado. |
| [#archlinux-newbie](ircs://chat.freenode.net/archlinux-newbie) | Un espacio para aprender, probar cosas nuevas y pedir ayuda sin temor al ridículo. |
| [#archlinux-pacman](ircs://chat.freenode.net/archlinux-pacman) | Debate y desarrollo de [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)"). |
| [#archlinux-projects](ircs://chat.freenode.net/archlinux-projects) | Debate y desarrollo de proyectos (mkinitcpio, abs, dbscripts, devtools, ...) |
| [#archlinux-reproducible](ircs://chat.freenode.net/archlinux-reproducible) | Debate para lograr compilaciones reproducibles. |
| [#archlinux-security](ircs://chat.freenode.net/archlinux-security) | Debate de problemas de seguridad dentro de los paquetes de Arch. |
| [#archlinux-testing](ircs://chat.freenode.net/archlinux-testing) | Debate sobre los repositorios de prueba. |
| [#archlinux-wiki](ircs://chat.freenode.net/archlinux-wiki) | Debate sobre [ArchWiki](/index.php/ArchWiki_(Espa%C3%B1ol) "ArchWiki (Español)"), sus artículos y [foros](https://bbs.archlinux.org/). |
| [#archlinux-women](ircs://chat.freenode.net/archlinux-women) | Debate sobre género e igualdad, principalmente en inglés. |
| [#archlinux-proaudio](ircs://chat.freenode.net/archlinux-proaudio) | Debate sobre [audio profesional](/index.php/Professional_audio "Professional audio") en Arch. También en el canal no oficial #archaudio. |

### Canales IRC internacionales

Los debates internacionales están disponibles en los siguientes canales, también ubicados en la red IRC **[chat.freenode.net](ircs://chat.freenode.net)**, a menos que se indique lo contrario.

| Canal | Descripción |
| [#archlinux-za](ircs://chat.freenode.net/archlinux-za) | Debate (Afrikaans, English) |
| [#archlinux-br](ircs://chat.freenode.net/archlinux-br) | Debate (Brasileño) |
| [#archlinux-cn](ircs://chat.freenode.net/archlinux-cn) | Debate (Chino); también en **[irc.oftc.net#arch-cn](ircs://irc.oftc.net/arch-cn)** |
| [#archlinux-cr](ircs://chat.freenode.net/archlinux-cr) | Debate (Costa Rica) |
| [#archlinux.cz](ircs://chat.freenode.net/archlinux.cz) | Debate (Checo) |
| [#archlinux.dk](ircs://chat.freenode.net/archlinux.dk) | Debate (Danés) |
| [#archlinux.fi](ircs://chat.freenode.net/archlinux.fi) | Debate (Finlandés) |
| [#archlinux-fr](ircs://chat.freenode.net/archlinux-fr) | Debate (Francés) |
| [#archlinux-gaelic](ircs://chat.freenode.net/archlinux-gaelic) | Debate (Gaélico) |
| [#archlinux.de](ircs://chat.freenode.net/archlinux.de) | Debate (Alemán) |
| [#archlinux-greece](ircs://chat.freenode.net/archlinux-greece) | Debate (Griego) |
| [#archlinux-il](ircs://chat.freenode.net/archlinux-il) | Debate (Hebreo) |
| [#archlinux.hu](ircs://chat.freenode.net/archlinux.hu) | Debate (Húngaro) |
| [#archlinux-it](ircs://chat.freenode.net/archlinux-it) | Debate (Italiano); también en **[irc.azzurra.org#archlinux](irc://irc.azzurra.org/archlinux)** |
| [#archlinux-nordics](ircs://chat.freenode.net/archlinux-nordics) | Debate (los nórdicos: danés, finlandés, noruego y sueco) |
| [#archlinux-kr](ircs://chat.freenode.net/archlinux-kr) | Debate (Koreano) |
| [#archlinux-ir](ircs://chat.freenode.net/archlinux-ir) | Debate (Persa) |
| [#archlinux.org.pl](ircs://chat.freenode.net/archlinux.org.pl) | Debate (Polaco) |
| [#archlinux-pt](ircs://chat.freenode.net/archlinux-pt) | Debate (Portugués) |
| [#archlinux.ro](ircs://chat.freenode.net/archlinux.ro) | Debate (Rumano) |
| [#archlinux-ru](ircs://chat.freenode.net/archlinux-ru) | Debate (Ruso); también en **[irc.mibbit.net#archlinux-ru](irc://irc.mibbit.net/archlinux-ru)** |
| [#archlinux-rs](ircs://chat.freenode.net/archlinux-rs) | Debate (Serbio) |
| [#archlinux-es](ircs://chat.freenode.net/archlinux-es) | Debate (Español) |
| [#archlinux.se](ircs://chat.freenode.net/archlinux.se) | Debate (Sueco) |
| [#archlinux-tr](ircs://chat.freenode.net/archlinux-tr) | Debate (Turko) |
| [#archlinux-ve](ircs://chat.freenode.net/archlinux-ve) | Debate (Venezolano) |
| [#archlinuxvn](ircs://chat.freenode.net/archlinuxvn) | Debate (Vietnamita, Tiếng Việt) |