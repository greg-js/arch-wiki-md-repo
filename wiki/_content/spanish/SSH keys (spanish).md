Al usar una llave SSH ( una publica y una privada para ser precisos), se puede conectarse fácilmente a un servidor, o a múltiples servidores, sin tener que ingresar una contraseña cada vez [Criptografía_asimétrica](https://en.wikipedia.org/wiki/es:Criptograf%C3%ADa_asim%C3%A9trica "wikipedia:es:Criptografía asimétrica") y [Protocolos_desafío-respuesta](https://en.wikipedia.org/wiki/es:Protocolos_desaf%C3%ADo-respuesta "wikipedia:es:Protocolos desafío-respuesta"). Una ventaja inmediata de este método sobre el clásico método de autenticación con contraseña, es que es posible autenticarse sin necesidad de enviar la contraseña por la red, así que alguien espiando la red no podrá interceptar e intentar descifrar la contraseña ya que esta nunca sera enviada. Adicionalmente, el uso de llaves de SSH virtualmente elimina el riesgo de ataques de fuerza bruta al reducir la probabilidad de que un atacante adivine las credenciales correctamente.

Ademas de ofrecer seguridad adicional, autenticación con llaves SSH puede ser mas conveniente que el método tradicional de autenticación con contraseña. Cuando se usa con un programa conocido como Agente SSH, las llaves SSH le permiten conectarse con uno o múltiples servidores sin necesidad de tener que recordar la contraseña de cada sistema.

Llaves SSH también tienen algunas desventajas y puede que no funcionen en todos los ambientes, pero en muchas circunstancias pueden ofrecer bastantes ventajas. Un entendimiento general de como funcionan las llaves SSH le ayudaran a decidir como y cuando usarlas para satisfacer su caso especifico.

Este articulo asume que el lector tiene un conocimiento básico del protocolo de [Shell Segura](/index.php/Secure_Shell_(Espa%C3%B1ol) "Secure Shell (Español)") y que el paquete [openssh](https://www.archlinux.org/packages/?name=openssh) ha sido [instalado](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)").

## Contents

*   [1 Informacion preliminar](#Informacion_preliminar)
*   [2 Generando las llaves SSH](#Generando_las_llaves_SSH)
    *   [2.1 Seleccionar el tipo autenticación de la llave](#Seleccionar_el_tipo_autenticación_de_la_llave)
        *   [2.1.1 RSA](#RSA)
        *   [2.1.2 ECDSA](#ECDSA)
        *   [2.1.3 Ed25519](#Ed25519)
    *   [2.2 Selección de ubicación y contraseña](#Selección_de_ubicación_y_contraseña)
        *   [2.2.1 Cambiar la contraseña de la llave privada sin cambiar la llave](#Cambiar_la_contraseña_de_la_llave_privada_sin_cambiar_la_llave)
        *   [2.2.2 Manejo de llaves múltiples](#Manejo_de_llaves_múltiples)
*   [3 Copiar llaves a un servidor remoto](#Copiar_llaves_a_un_servidor_remoto)
    *   [3.1 Método simple](#Método_simple)
    *   [3.2 Método manual](#Método_manual)
*   [4 Agentes de SSH](#Agentes_de_SSH)
    *   [4.1 ssh-agent](#ssh-agent)
        *   [4.1.1 Iniciar ssh-agent con systemd/user](#Iniciar_ssh-agent_con_systemd/user)
    *   [4.2 Agente GnuPG](#Agente_GnuPG)
    *   [4.3 Keychain](#Keychain)
    *   [4.4 x11-show-askpass](#x11-show-askpass)
    *   [4.5 GNOME Keyring (llavero)](#GNOME_Keyring_(llavero))
*   [5 Resolución de problemas](#Resolución_de_problemas)
*   [6 Links Utiles / Informacion (en ingles)](#Links_Utiles_/_Informacion_(en_ingles))

## Informacion preliminar

Las llaves de SSH siempre son generadas en pares con una llamada *llave privada* y otra llamada *llave pública*. La llave privada solo es conocida por el usuario y debe ser guardada con cuidado. En contraste, la llave pública puede ser compartida libremente con cualquier servidor SSH con el que se quiere conectar.

Si un servidor SSH tiene su llave pública y nota que hay un intento de conexión, usa su llave pública para construir y enviar un desafío. Este desafío es un mensaje encriptado y debe ser respondido apropiadamente antes de que el servidor le dé acceso. Lo que hace este mensaje particularmente seguro es que solo se puede descifrar con la llave privada. Mientras que la llave pública puede ser usada para encriptar el mensaje, no puede ser usada para descifrarlo. Solo el usuario, que tiene la llave privada puede ser capaz de descifrar correctamente el desafío y producir la respuesta adecuada.

Este intercambio de desafío-respuesta ocurre como una tarea de fondo y es invisible para el usuario. Mientras se tenga la llave privada, la cual es guardada normalmente en la carpeta `~/.ssh/`, su cliente SSH debería ser capaz de responder apropiadamente al servidor.

Una llave privada es un secreto a guardar, por ende se aconseja que cuando se guarde se haga de manera encriptada. Cuando la llave encriptada es requerida, una contraseña debe ser ingresada para descifrarla. Aunque superficialmente esto parece como si se estuviera poniendo una contraseña para ingresar al servidor de SSH, esta contraseña solo se usa para descifrar la llave privada en el sistema local. Esta contraseña no se transmite sobre la red.

## Generando las llaves SSH

Un par de llaves SSH puede ser generado ejecutando el comando `ssh-keygen`, por defecto usando seguridad 2048-bit RSA (y SHA256) la cual de acuerdo a [ssh-keygen(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ssh-keygen.1) es "*considerada generalmente suficiente*" y debe ser compatible con virtualmente todos los servidores y clientes:

```
$ ssh-keygen

```

```
Generating public/private rsa key pair.
Enter file in which to save the key (/home/<username>/.ssh/id_rsa):   ### Ubicación de las llaves
Enter passphrase (empty for no passphrase):                           ### Contraseña de la llave
Enter same passphrase again:                                          ### Repetir la contraseña
Your identification has been saved in /home/<username>/.ssh/id_rsa.   ### Nombre llave privada
Your public key has been saved in /home/<username>/.ssh/id_rsa.pub.   ### Nombre llave publica
The key fingerprint is:
SHA256:gGJtSsV8BM+7w018d39Ji57F8iO6c0N2GZq3/RY2NhI username@hostname
The key's randomart image is:
+---[RSA 2048]----+
|   ooo.          |
|   oo+.          |
|  + +.+          |
| o +   +     E . |
|  .   . S . . =.o|
|     . + . . B+@o|
|      + .   oo*=O|
|       .   ..+=o+|
|           o=ooo+|
+----[SHA256]-----+
```

La [imagen de arte aleatorio](http://www.cs.berkeley.edu/~dawnsong/papers/randomart.pdf) fue [introducida en OpenSSH 5.1](http://www.openssh.com/txt/release-5.1) como una forma más simple de identificar la huella de la llave.

**Nota:** Si utiliza una contraseña para su llave, es *muy recomendado* usar la opción `-o` en el comando `ssh-keygen`. Así, su llave privada se guardara en el nuevo formato de OpenSSH, el cual ha mejorado bastante contra ataques de fuerza bruta, pero no es soportado por versiones de OpenSSH inferiores a 6.5\. De acuerdo a [ssh-keygen(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ssh-keygen.1), llaves de Ed25519 siempre usan el nuevo formato. También use la opción `-a` para especificar el numero de rondas de KDF en el cifrado de la contraseña.

También es posible agregar un comentario opcional a la llave publica con el parámetro `-C`, para identificar la llave más fácilmente en lugares como `~/.ssh/known_hosts`, `~/.ssh/authorized_keys` y `ssh-add -L`. Por ejemplo:

```
$ ssh-keygen -C "$(whoami)@$(hostname)-$(date -I)"    ### usuario@nombredemaquina-fecha

```

Creara un comentario diciendo el usuario que creo la llave, en que maquina y la fecha.

El parámetro `-o`, puede ser usado para guardar la llave privada en el nuevo formato de OpenSSH, el cual ha incrementado la resistencia a ataques de fuerza bruta, pero no es soportado por versiones de OpenSSH anteriores a 6.5 [lanzamiento 2014-01-29](https://lwn.net/Articles/583485/). Use el parámetro `-a` para especificar el numero de rondas de KDF. De acuerdo a [ssh-keygen(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ssh-keygen.1), llaves de Ed25519 siempre usan el nuevo formato de llave privada.

### Seleccionar el tipo autenticación de la llave

OpenSSH soporta varios algoritmos (para llaves de autenticacion), los cuales se pueden dividir en dos grupos dependiendo en las propiedades matemáticas que se usan:

1.  [DSA](https://en.wikipedia.org/wiki/es:DSA "wikipedia:es:DSA") y [RSA](https://en.wikipedia.org/wiki/es:RSA "wikipedia:es:RSA"), que dependen en la [dificultad práctica](https://en.wikipedia.org/wiki/es:Factorizaci%C3%B3n_de_enteros#Dificultad_y_complejidad "wikipedia:es:Factorización de enteros") de factorizar el producto de dos números primos largos.
2.  [ECDSA](https://en.wikipedia.org/wiki/es:ECDSA "wikipedia:es:ECDSA") y [Ed25519](https://en.wikipedia.org/wiki/Curve25519 "wikipedia:Curve25519"), que dependen del problema de curva eliptica del [logaritmo discreto](https://en.wikipedia.org/wiki/es:Logaritmo_discreto "wikipedia:es:Logaritmo discreto").

[Criptografía de curva elíptica](https://en.wikipedia.org/wiki/es:Criptograf%C3%ADa_de_curva_el%C3%ADptica "wikipedia:es:Criptografía de curva elíptica") (ECC) es una adición relativamente reciente al ecosistema de llaves publicas criptográficas. Una de sus ventajas más importantes es la habilidad de proveer el mismo nivel de seguridad con llaves más cortas, lo cual se transforma en menos recursos usados al crear, cifrar o descifrar mensajes y reduce los costos de transmisión y guardado.

OpenSSH 7.0 hizo llaves de tipo [DSA obsoletas](https://www.archlinux.org/news/openssh-70p1-deprecates-ssh-dss-keys/) debido a vulnerabilidades descubiertas, así que las únicas opciones en el sistema criptográfico son RSA o alguno de los dos tipos de ECC.

Llaves de [#RSA](#RSA) proveerán mayor portabilidad, mientras que [#Ed25519](#Ed25519) le proveeran la mejor seguridad requiriendo versiones recientes de servidor y cliente. [#Ed25519](#Ed25519) es probablemente más compatible que Ed25519 (aunque menos que RSA), pero sospechas sobre su seguridad existen (ver abajo).

**Nota:** Estas llaves son usadas al autenticar un usuario, seleccionar una llave más segura no quiere decir que más recursos de CPU se usaran cuando se transfieren datos por SSH.

#### RSA

`ssh-keygen` usa por defecto RSA, así que no hay necesidad de especificarlo con el parámetro `-t`. Este provee la mejor compatibilidad de todos los algoritmos, pero requiere que la llave sea más larga para proveer suficiente seguridad.

El tamaño mínimo de la llave es 1024 bits,por defecto es 2048 (vea [ssh-keygen(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ssh-keygen.1)), el máximo es 16384.

Si se desea generar un par de llaves RSA más seguro, simplemente use el parámetro `-b` con el valor bit deseado:

```
$ ssh-keygen -b 4096

```

```
Generating public/private rsa key pair.
Enter file in which to save the key (/home/<username>/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/<username>/.ssh/id_rsa.
Your public key has been saved in /home/<username>/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:+Pqo84NC+vAQQ9lUV0z+/zPHsyCe8oZpy6hLkIa7qfk <username>@<hostname>
The key's randomart image is:
+---[RSA 4096]----+
|   ... .+o       |
|  +   . ..       |
| o .     .       |
|. . .  .  .      |
|o. +  . S  .     |
| o+ .  .    .    |
|o+   o  . o. o . |
|.=+ + .oo=..o o+o|
|+=E..**+oo=+   o*|
+----[SHA256]-----+
```

Es importante tener en cuenta que existen desventajas en llaves más largas.[[1]](https://security.stackexchange.com/a/25377)[[2]](https://www.gnupg.org/faq/gnupg-faq.html#no_default_of_rsa4096) Las preguntas frecuentes del proyecto GnuPG dice: "*Si se desea más seguridad que RSA-2048, la mejor opción es usar curvas elípticas en lugar de seguir usando RSA*".[[3]](https://www.gnupg.org/faq/gnupg-faq.html#please_use_ecc)

En contraste, en un reporte de [sistema Criptográfico de la NSA](https://www.nsa.gov/ia/programs/suiteb_cryptography/index.shtml) se sugiere una llave mínima de 3072-bit para RSA mientras "*[se prepara] la transición al algoritmo resistente a computadores cuanticos*".[[4]](http://www.keylength.com/en/6/)

#### ECDSA

El algoritmo de firmado de curva elíptica (ECDSA, siglas en ingles), fue introducido como el algoritmo recomendado de autenticación [en OpenSSH 5.7](http://www.openssh.com/txt/release-5.7). Algunos vendedores deshabilitaron la implementación requerida debido a potenciales brechas de patentes.

Hay dos fuentes de preocupación con este algoritmo:

1.  *Preocupación política*, la confianza de productos producidos por NIST [es cuestionada](https://crypto.stackexchange.com/questions/10263/should-we-trust-the-nist-recommended-ecc-parameters) después de revelaciones que la NSA insertan backdoors en software, hardware y estándares publicados. Criptografos conocidos [expresaron](https://www.schneier.com/blog/archives/2013/09/the_nsa_is_brea.html#c1675929) [dudas](http://safecurves.cr.yp.to/rigid.html)
2.  [sobre](https://www.hyperelliptic.org/tanja/vortraege/20130531.pdf) las curvas fabricadas por NIST, y como voluntariamente en el pasado las ha hecho [más](https://www.schneier.com/blog/archives/2007/11/the_strange_sto.html) [susceptibles](http://www.scientificamerican.com/article/nsa-nist-encryption-scandal/).
3.  *Preocupación técnica*, sobre la dificultad de [implementar el estándar adecuadamente](http://blog.cr.yp.to/20140323-ecdsa.html) y la [lentitud y fallas de diseño](http://www.gossamer-threads.com/lists/openssh/dev/57162#57162) que reducen la seguridad en implementaciones insuficientemente precavidas.

Estas preocupaciones están mejor resumidas en [libssh curve25519 introduction](https://git.libssh.org/projects/libssh.git/tree/doc/curve25519-sha256@libssh.org.txt#n4) (en ingles). Aunque las preocupaciones políticas todavía son debatidas, hay un [consenso](https://news.ycombinator.com/item?id=7597653) que [#Ed25519](#Ed25519) es técnicamente superior y debería ser preferida.

#### Ed25519

[Ed25519](http://ed25519.cr.yp.to/) fue introducida en [OpenSSH 6.5](http://www.openssh.com/txt/release-6.5) en Enero de 2014: "*Ed25519 es un esquema de firmado con curva elíptica que ofrece mejor seguridad que ECDSA y rendimiento como DSA*". Sus mejores ventajas son su velocidad, resistencia a ataques de canal de lado y la ausencia de constantes embebidas en el codigo.[[5]](https://git.libssh.org/projects/libssh.git/tree/doc/curve25519-sha256@libssh.org.txt) Vea también [este blog](https://blog.mozilla.org/warner/2011/11/29/ed25519-keys/) por un desarrollador de Mozilla explicando como funciona.

Esta implementado en varias [aplicaciones y librerías](https://en.wikipedia.org/wiki/Curve25519#Popularity "wikipedia:Curve25519") y es el [algoritmo por defecto](https://www.libssh.org/2013/11/03/openssh-introduces-curve25519-sha256libssh-org-key-exchange/) (lo cual diferente a *firmado* de llaves) en OpenSSH.

Un par de llaves SSH de tipo Ed25519 se pueden generar ejecutando:

```
$ ssh-keygen -t ed25519

```

No hay necesidad de elegir el tamaño de la llave, ya que todas las llaves Ed25519 tienen 256 bits. Estas también dependen del [nuevo formato de llaves](http://www.gossamer-threads.com/lists/openssh/dev/57162#57162) el cual "*usa derivation de llaves basada en la función de bcrypt, lo cual hace que ataques de fuerza bruta en contra de llaves robadas sean mucho más lentos*".

Por esas razones, compatibilidad con versiones antiguas de OpenSSH o con [otros servidores y clientes SSH](/index.php/Secure_Shell_(Espa%C3%B1ol)#Otros_servidores_y_clientes_SSH "Secure Shell (Español)") puede ser complicada.

### Selección de ubicación y contraseña

Al ejecutar el comando `ssh-keygen`, se le preguntara por la ubicación deseada de su llave privada. Por defecto, las llaves son guardadas en la carpeta `~/.ssh/` y se les nombra de acuerdo y tipo de encriptado usado. Se recomienda que acepte el nombre y la ubicación predeterminados para que los ejemplos de códigos posteriores en este artículo funcionen correctamente.

Cuando se le pregunte por una contraseña, seleccione algo que no sea fácil de adivinar. Una contraseña aleatoria y larga es generalmente mucho más difícil de descifrar si cae en manos equivocadas.

También es posible crear su llave privada sin contraseña. Mientras que esto es conveniente, es necesario que entienda los riesgos asociados. Sin una contraseña, su llave privada va a ser guardada en el disco de manera no encriptada. Todos aquellos que ganen acceso al archivo de su llave privada podrán asumir su identidad en un servidor SSH. Además, sin contraseña, también debe confiar en el usuario root, que puede pasar permisos de archivos y puede acceder a su llave en cualquier momento.

#### Cambiar la contraseña de la llave privada sin cambiar la llave

Si la contraseña seleccionada originalmente ya no se desea o debe ser cambiada, se puede ejecutar el comando `ssh-keygen` para cambiar la contraseña sin cambiar el contenido de la llave.

Para cambiar la contraseña de una llave privada RSA, ejecute:

```
$ ssh-keygen -f ~/.ssh/id_rsa -p

```

#### Manejo de llaves múltiples

Es posible —aunque [no se considera buena práctica](http://security.stackexchange.com/questions/10963/whats-the-common-pragmatic-strategy-for-managing-key-pairs)— usar la misma llave de SSH para múltiples servidores.

Claro que es relativamente fácil mantener diferentes llaves para diferente servidores usando la directiva `IdentityFile` en su archivo de configuración de OpenSSH:

 `~/.ssh/config` 
```
Host SERVIDOR1
   IdentitiesOnly yes
   IdentityFile ~/.ssh/id_rsa_SERVIDOR1

Host SERVIDOR2
   IdentitiesOnly yes
   IdentityFile ~/.ssh/id_ed25519_SERVIDOR2

```

Vea [ssh_config(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ssh_config.5) para una descripción completa de estas opciones.

## Copiar llaves a un servidor remoto

Una vez se generen un par de llaves, es necesario copiar la llave pública al servidor remoto para que se pueda usar autenticación vía SSH. La llave publica lleva el mismo nombre que la llave privada excepto que tiene una extensión `.pub`. Nótese que la llave privada no se comparte y permanece en la maquina local.

### Método simple

**Nota:** Este método puede que falle si el servidor usa una shell diferente a `sh`, por ejemplo `tcsh` y usa OpenSSH mas antiguo que 6.6.1p1\. Vea [este reporte de bug](https://bugzilla.redhat.com/show_bug.cgi?id=1045191).

Si la llave publica esta en `~/.ssh/id_rsa.pub`, simplemente ejecute el siguiente comando:

```
$ ssh-copy-id servidor-remoto.org

```

Si el usuario difiere en la maquina remota, asegúrese de prefijar el usuario seguido por `@` al nombre del servidor.

```
$ ssh-copy-id nombreusuarion@servidor-remoto.org

```

Si el nombre del archivo de la llave publica es diferente a `~/.ssh/id_rsa.pub`, obtendrá un error diciendo `/usr/bin/ssh-copy-id: ERROR: No identities found` (Identidad no encontrada). En este caso, se debe proveer la ubicación del archivo de la llave publica explícitamente.

```
$ ssh-copy-id -i ~/.ssh/id_ed25519.pub nombreusuarion@servidor-remoto.org

```

Si el servidor esta esperando una conexión en un puerto diferente al 22 (por defecto), necesita incluirlo en el comando.

```
$ ssh-copy-id -i ~/.ssh/id_ed25519.pub -p 221 nombreusuarion@servidor-remoto.org

```

### Método manual

Por defecto, para OpenSSH, la llave publica necesita ser agregada en el archivo `~/.ssh/authorized_keys`. Se inicia copiando la llave publica al servidor remoto.

```
$ scp ~/.ssh/id_ed25519.pub nombreusuarion@servidor-remoto.org:

```

Esto copiara la llave publica (`id_ed25519.pub`) en el directorio raíz del usuario en el servidor remoto vía `scp` (nótese los `:` al final de la dirección del servidor).

En el servidor remoto, sera necesario crear el directorio `~/.ssh` en caso de no existir, y agregar la llave al archivo `authorized_keys`:

```
$ ssh nombreusuarion@servidor-remoto.org
nombreusuarion@servidor-remoto.org's password:
$ mkdir ~/.ssh
$ chmod 700 ~/.ssh
$ cat ~/id_ed25519.pub >> ~/.ssh/authorized_keys
$ rm ~/id_ed25519.pub
$ chmod 600 ~/.ssh/authorized_keys

```

Los últimos dos comando eliminan la llave publica del servidor ( la cual ya no se necesita), y otorgan los permisos correctos al archivo `authorized_keys`.

## Agentes de SSH

Si la llave privada esta encriptada con una contraseña, esta debe ser introducida cada vez que se intente conectar a un servidor. Cada ejecución individual de programas como `ssh` o `scp` necesitaran la contraseña para descifrar la llave privada antes de autentificar y proceder.

Un Agente de SSH es un programa el cual guarda su llave descifrada y la provee a los diferentes clientes de SSH en su nombre. En este caso, la contraseña solo es proporcionada una vez, al agregar la llave al cache del Agente de SSH. Esto es muy conveniente al hacer conexiones de SSH frecuentes.

Un Agente esta típicamente configurado a ejecutarse automáticamente cuando se inicie la sesión y persistirá hasta el cierre de la misma. Una variedad de Agentes, GUIs y configuraciones están disponibles para lograr este objetivo. Esta sección proveerá una reseña de un numero de diferentes soluciones que se pueden adaptar a las necesidades especificas.

### ssh-agent

`ssh-agent` es el agente por defecto incluido en OpenSSH. Puede ser usado directamente o puede ser usado como back-end de algún otro programa, algunos ejemplos serán discutidos en la parte inferior.

Cuando se ejecuta `ssh-agent`, se mostrará en pantalla las variables de entorno que serán usadas, y una tarea de fondo sera creada.

```
$ ssh-agent
SSH_AUTH_SOCK=/tmp/ssh-vEGjCM2147/agent.2147; export SSH_AUTH_SOCK;
SSH_AGENT_PID=2148; export SSH_AGENT_PID;
echo Agent pid 2148;

```

Para hacer uso de estas variables, ejecute `eval`.

```
$ eval `ssh-agent`
Agent pid 2157

```

Ahora que `ssh-agent` se esta ejecutando, es necesario agregar la llave privada.

```
$ ssh-add ~/.ssh/id_ed25519
Enter passphrase for /home/user/.ssh/id_ed25519:
Identity added: /home/user/.ssh/id_ed25519 (/home/user/.ssh/id_ed25519)

```

Si la llave esta encriptada, `ssh-add` preguntara por la contraseña. Una vez que la llave privada ha sido añadida satisfactoriamente al agente, sera posible hacer conexiones de SSH sin necesidad de ingresar la contraseña.

**Sugerencia:** Para hacer que todos los clientes de `ssh`, incluyendo `git` guarden la llave en el agente en el primer uso, agregue la configuración `AddKeysToAgent yes` al archivo `~/.ssh/config`. Otros valores posibles son `confirm`, `ask` y `no` (por defecto).

Para iniciar el agente automáticamente y asegurarse que solamente un proceso de `ssh-agent` se esta ejecutando, agregue lo siguiente al archivo `~/.bashrc`:

```
if ! pgrep -u "$USER" ssh-agent > /dev/null; then
    ssh-agent > ~/.ssh-agent-thing
fi
if [[ "$SSH_AGENT_PID" == "" ]]; then
    eval "$(<~/.ssh-agent-thing)"
fi

```

Esto ejecutara un proceso de `ssh-agent` si no existe alguno. Si hay un proceso ejecutándose, se tomara el resultado de `ssh-agent` y se evaluara para configurar las variables de entorno necesarias.

También existen GUIs para `ssh-agent` y agentes alternativos descritos posteriormente que evitan este problema.

#### Iniciar ssh-agent con systemd/user

Es posible usar [systemd/user](/index.php/Systemd/User_(Espa%C3%B1ol) "Systemd/User (Español)") lo cual facilita el inicio del agente.

 `~/.config/systemd/user/ssh-agent.service` 
```
[Unit]
Description=SSH key agent

[Service]
Type=simple
Environment=SSH_AUTH_SOCK=%t/ssh-agent.socket
ExecStart=/usr/bin/ssh-agent -D -a $SSH_AUTH_SOCK

[Install]
WantedBy=*default*.target

```

Agregue `SSH_AUTH_SOCK DEFAULT="${XDG_RUNTIME_DIR}/ssh-agent.socket"` al archivo `~/.pam_environment`. Después [active](/index.php/Systemd_(Espa%C3%B1ol)#Usar_las_unidades "Systemd (Español)") o [active inicio automatico](/index.php/Systemd_(Espa%C3%B1ol)#Usar_las_unidades "Systemd (Español)") de la unidad.

**Nota:** SI esta usando GNOME, esta variable de entorno es sobre escrita por defecto. Vea [GNOME/Keyring#Disable keyring daemon components](/index.php/GNOME/Keyring#Disable_keyring_daemon_components "GNOME/Keyring").

### Agente GnuPG

El [gpg-agent](/index.php/GnuPG_(Espa%C3%B1ol)#gpg-agent "GnuPG (Español)") tiene emulación de OpenSSH. Vea [GnuPG#SSH agent](/index.php/GnuPG#SSH_agent "GnuPG") para la configuracion necesaria.

### Keychain

[Keychain](http://www.funtoo.org/en/security/keychain/intro/) administra una o mas llaves privadas, que se le hayan especificado. Cuando se inicializa, preguntara por la frase-de-paso para la clave privada, y la guardara. De esta manera sus llaves privadas estarán protegidas por password, pero no deberá ingresar su password una y otra vez.

[Instale](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") el paquete [keychain](https://www.archlinux.org/packages/?name=keychain), disponible en los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)")

Cree el siguiente archivo y hágalo ejecutable:

 `/etc/profile.d/keychain.sh` 
```
eval `keychain --eval --nogui -Q -q id_rsa`

```

o

 `/etc/profile.d/keychain.sh` 
```
/usr/bin/keychain -Q -q --nogui ~/.ssh/id_dsa
[[ -f $HOME/.keychain/$HOSTNAME-sh ]] && source $HOME/.keychain/$HOSTNAME-sh

```

o

anexe

```
eval `keychain --eval --agents ssh id_dsa`

```

a su `.bashrc` o `.bash_profile`.

**Sugerencia:** Si quiere mayor seguridad reemplace -Q con --clear pero es menos conveniente.

Si es necesario, reemplace `~/.ssh/id_dsa` con `~/.ssh/id_rsa`. Para aquellos que usan una shell que no es Bash, vean`keychain --help` o [keychain(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/keychain.1) para detalles en otras Shells.

Cierre su shell y vuélvala a abrir, Keychain deberá aparecer y si es la primera vez que corre, le preguntara por la frase-de-paso de la llave privada especificada.

### x11-show-askpass

Necesita iniciar ssh-agent cada vez que inicia una nueva sesión de X. El ssh-agent se cerrara cuando al sesión de X termine

Se puede instalar una variante de x11-ssh-askpass la cual le pedirá su frase-de-paso cada vez que abra una nueva sesión de X. También puede usar el x11-ssh-askpass original de [AUR](/index.php/AUR "AUR") o ksshkpass (usa kdelibs):

```
# pacman -S ksshaskpass

```

o openssh-askpass (usa qt):

```
# pacman -S openssh-askpass

```

Luego de instalarlo, cierre su sesión de X y recarguela a partir de ahora se le preguntara su frase-de-paso en el inicio de la sesión X.

### GNOME Keyring (llavero)

Si usa el escritorio [GNOME](/index.php/GNOME_(Espa%C3%B1ol) "GNOME (Español)"), la herramienta [Gnome Keyring](/index.php/Gnome_Keyring "Gnome Keyring") puede ser usada como un agente de SSH. Visite el articulo [Gnome Keyring](/index.php/Gnome_Keyring "Gnome Keyring").

## Resolución de problemas

Si cree que el servidor SSH esta ignorando sus claves, asegúrese de que tiene los permisos adecuados sobre los archivos relevantes.

Para la maquina local:

```
$ chmod 700 ~/
$ chmod 700 ~/.ssh
$ chmod 600 ~/.ssh/id_rsa

```

Para la maquina remota:

```
$ chmod 700 ~/
$ chmod 700 ~/.ssh
$ chmod 600 ~/.ssh/authorized_keys

```

Si no fuera eso, ejecute el servidor ssh en modo de depuración y monitoree la salida mientras se hace la conexión:

```
# /usr/sbin/sshd -d

```

## Links Utiles / Informacion (en ingles)

*   [Como: Configurar las llaves SSH](http://www.arches.uga.edu/~pkeck/ssh/)
*   [Manejo de llaves en OpenSSH , Parte 1](http://www-106.ibm.com/developerworks/linux/library/l-keyc.html)
*   [Manejo de llaves en OpenSSH , Parte 2](http://www-106.ibm.com/developerworks/linux/library/l-keyc2/)
*   [Manejo de llaves en OpenSSH , Parte 3](http://www-106.ibm.com/developerworks/library/l-keyc3/)
*   [Comenzado con SSH](http://kimmo.suominen.com/docs/ssh/)
*   Manual: [ssh-keygen(1)](http://www.openbsd.org/cgi-bin/man.cgi?query=ssh-keygen&apropos=0&sektion=0&manpath=OpenBSD+Current&arch=i386&format=html)