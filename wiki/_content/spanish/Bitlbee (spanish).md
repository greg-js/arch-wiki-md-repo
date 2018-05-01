## Introducción

Tener cuentas de msn, yahoo, jabber, facebook, icq o gmail desde weechat Se puede usando Bitlbee. Esta aplicación es una especie de pasarela para conectar desde clientes de irc a redes de mensajeria instantánea. De esa manera puedes gestionar tus cuentas de chat desde el mismo cliente de irc.

## Instalación

[Instale](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") los paquetes [bitlbee](https://www.archlinux.org/packages/?name=bitlbee) y [weechat](https://www.archlinux.org/packages/?name=weechat) de los repositorios oficiales.

## Configuración

Abrimos weechat y una vez que conecte con nuestra red de irc habitual, en cualquier ventana pondremos lo siguiente para conectar con un servidor público de bitlbee

/connect im.bitlbee.org

Nos registraremos en el sistema. register contraseña >> pon la contraseña que vayas a usar de ahora en adelante en el servidor de bitlbee.

En los comandos de bitlbee no se pone la barra al principio del comando (/)

Ya registrados, nos identificamos:

identify contraseña -> y ya estaremos correctamente logueados en bitlbee

El siguiente paso es dar de alta las cuentas que vayamos a usar, lo cual se hace de la siguiente forma dependiendo de la red que usemos. Se pueden dar de alta las cuentas que quieras, ya que bitlbee es multiprotocolo:

MSN: account add msn usuario@hotmail.com contraseña YAHOO: account add yahoo usuario contraseña GTALK: account add jabber usuario@gmail.com contraseña talk.google.com:5223:ssl JABBER: account add jabber usuario@jabber.org contraseña ICQ: account add oscar id contraseña login.icq.com AOL: account add oscar id contraseña login.oscar.aol.com

Si ya hemos creado toda/s nuestras cuentas, ahora deberemos conectar y guardar:

account on -> conecta todas las cuentas save -> guardar todos los cambios realizados

Otros comandos relacionados con las cuentas son:

account list -> nos da una lista de las cuentas existentes account on id -> conecta la cuenta número id account off id -> desconecta la cuenta con ese id account off -> desconecta de todas las cuentas account del id -> borra la cuenta número id

Para la gestión de usuarios, disponemos de los siguientes comandos:

add id usuario@loquesea.com -> añadir usuario a una cuenta determinada remove usuario -> borra usuario info usuario -> muestra información sobre el usuario block/allow usuario -> ignora/reacepta al usuario remane usuario usuario2 -> renombra usuario a usuario2

Para comprobar quién está conectado:

blist -> lista de usuarios conectados blist all -> lista de TODOS los usuarios, conectados o no blist online -> lista de contactos conectados blist offline -> lista de contactos desconectados blist away -> lista de contactos ausentes

Cuando queramos desconectar de todas las cuentas no debemos olvidar hacerlo también de bitlbee. Lo más cómodo es usar un alias, por ejemplo:

/alias im connect im.bitlbee.org;account on -> para conectar a todas las cuentas /alias imoff account off;disconnect;wc -> cerramos las cuentas, desconectamos de bitlbee y cerramos la ventana.