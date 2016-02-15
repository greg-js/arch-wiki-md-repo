**Tor** es una implementación 'open source' de 2da generación del [enrutamiento de cebolla](https://es.wikipedia.org/wiki/Encaminamiento_de_cebolla) que provee libre acceso a una red proxy anónimos. Su principal objetivo es proteger el anónimato en Internet del [análisis de tráfico](https://es.wikipedia.org/wiki/Análisis_de_tráfico).

## Introducción

Los usuarios de la Red Tor ejecutan un enrutamiento de cebolla (_onion proxy_ en ingles) en sus computadoras. Este software se conecta a Tor, periódicamente negocia un circuito virtual a través de la red Tor. Tor emplea criptografía en forma de capas (de ahí la analogía con la cebolla), lo que garantiza confidencialidad directa entre los routers. Al mismo tiempo, el software proxy onion presenta una interfaz [SOCKS](https://es.wikipedia.org/wiki/SOCKS) a sus clientes. Las aplicaciones que funcionan en SOCKS pueden apuntar a Tor, quien luego multiplexa el tráfico a través de un circuito virtual Tor.

**Advertencia:** Tor en si mismo no es todo lo que necesitas para mantener el anonimato. Hay otros escollos que te debes cuidar (ver: [¿Quieres que Tor funcione realmente?](https://www.torproject.org/download/download.html.en#warning)).

A través de este proceso el _onion proxy_ maneja el trafico en la red para brindar anonimato al usuario final. El anonimato del usuario se mantiene encriptando el trafico, enviadolo a traves de otros nodos de la red Tor, y desencriptandolo en un último nodo para recibir tu tráfico antes de reenviarlo al servidor que fue especificado. Aunque Tor es considerado más seguro que las conexiones directas DNS (sin proxy) comunmente usadas, pueden ser considerablemente más lentas debido a la gran cantidad de tráfico re encaminado. Además, aunque Tor provee protección contra el análisis del tráfico, no puede evitar la confirmación en los límites de la red Tor (entrando y saliendo de la red).

Vea [Wikipedia:Tor](https://es.wikipedia.org/wiki/Tor)para más información.

## Instalación

[Instalar](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") [tor](https://www.archlinux.org/packages/?name=tor) está disponible en los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").

El [arm](https://www.archlinux.org/packages/?name=arm) (de sus siglas en ingles Anonymizing Relay Monitor) es un paquete que provee una terminal para monitorear el uso de banda ancha, detalles de la conexión y más.

Además, hay una interfaz basada en [Qt (en ingles)](/index.php/Qt "Qt") para Tor en el paquete [vidalia](https://aur.archlinux.org/packages/vidalia/). Además de controlar el proceso de Tor, Vidalia te permite ver y configurar el estado de Tor, monitorear el uso de banda ancha, y ver, filtrar y buscar los mensajes registrados.

**Advertencia:** Hay quienes en el proyecto [no recomiendan](https://www.whonix.org/wiki/Tor_Controller#Vidalia_recommended_against) usar _vidalia_.