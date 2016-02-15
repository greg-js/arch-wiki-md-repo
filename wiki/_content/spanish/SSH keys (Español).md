## Contents

*   [1 ¿Que son las Llaves SSH?](#.C2.BFQue_son_las_Llaves_SSH.3F)
    *   [1.1 Generando las llaves SSH](#Generando_las_llaves_SSH)
    *   [1.2 Copiando las llaves al servidor remoto](#Copiando_las_llaves_al_servidor_remoto)
*   [2 Recuerde la frase-de-paso](#Recuerde_la_frase-de-paso)
    *   [2.1 Agente SSH](#Agente_SSH)
        *   [2.1.1 Usando GnuPG Agent](#Usando_GnuPG_Agent)
        *   [2.1.2 Usando keychain](#Usando_keychain)
        *   [2.1.3 Usando ssh-agent y x11-show-askpass](#Usando_ssh-agent_y_x11-show-askpass)
    *   [2.2 GNOME Keyring (llavero)](#GNOME_Keyring_.28llavero.29)
*   [3 Resolucion de problemas](#Resolucion_de_problemas)
*   [4 Links Utiles / Informacion (en ingles)](#Links_Utiles_.2F_Informacion_.28en_ingles.29)

## ¿Que son las Llaves SSH?

Al usar una llave SSH ( una publica y una privada para ser precisos), usted puede conectarse fácilmente a un servidor, o a múltiples servidores, sin tener que ingresar un password cada vez.

Es posible configurar tus llaves sin una frase-de-paso, sin embargo eso seria imprudente, si alguien obtiene su clave, podría usarla. Esta guiá describe como configurar su sistema para que las llaves-de-paso sean recordadas de forma segura.

### Generando las llaves SSH

Si todavía no tiene OpenSSH instalado, instalelo ahora ya que no viene por defecto en Arch.

```
     #pacman -S openssh

```

Las llaves pueden ser generadas corriendo el comando ssh-keygen como usuario

```
$ ssh-keygen -b 1024 -t dsa
Generating public/private dsa key pair.
Enter file in which to save the key (/home/mith/.ssh/id_dsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/mith/.ssh/id_dsa.
Your public key has been saved in /home/mith/.ssh/id_dsa.pub.
The key fingerprint is:
x6:68:xx:93:98:8x:87:95:7x:2x:4x:x9:81:xx:56:94 mith@middleearth

```

Le pedirá por una locación (debe dejar la que le muestre por defecto), sin embargo la frase-de-paso es el punto importante! Debe ser consiente del criterio que hace una buena frase-de-paso.

¿Que acabamos de hacer? Generamos un par de llave publica/privada dsa(`-t dsa`) de 1024 bits de largo(`-b 1024`) con el comando ssh-keygen.

Si quiere crear un par de llave RSA en vez de DSA solo debe usar `-t rsa` ( no debe especificar el largo "-b" por defecto el largo para RSA es de 2048 y es suficiente)

**Note:** NOTA: Una llave DSA debe ser exactamente de 1024 bits por especificación. Una llave RSA puede ser entre 768 bits y 4096 bits.

### Copiando las llaves al servidor remoto

Ahora que hemos generados las llaves, necesitamos copiarlas al servidor remoto. Por defecto, para OpenSSH, la llave publica necesita ser concatenada dentro de `~/.ssh/authorized_keys`.

```
$ scp ~/.ssh/id_dsa.pub mith@metawire.org:

```

Esto copia la llave publica (`id_dsa.pub`) al servidor remoto vía `scp` ( notese los `:` al final de la dirección del servidor). el archivo acabara en el directorio home, pero se puede especificar la dirección que uno desee.

Inmediatamente en el servidor remoto, necesitamos crear el directorio `~/.ssh`, en el caso de no existir, y concatenar la llave al archivo `authorized_keys`:

```
$ ssh mith@metawire.org
mith@metawire.org's password:
$ mkdir ~/.ssh
$ cat ~/id_dsa.pub >> ~/.ssh/authorized_keys
$ rm ~/id_dsa.pub
$ chmod 600 ~/.ssh/authorized_keys

```

Los últimos dos comando eliminan la llave publica del servidor ( la cual ya no se necesita), y otorgan los permisos correctos al archivo `authorized_keys`.

Si se desconecta del servidor, e intenta re-conectar, este le debería preguntar por la frase-de-paso de la llave:

```
$ ssh mith@metawire.org
Enter passphrase for key '/home/mith/.ssh/id_dsa':

```

Si no le permite acceder con la llave, vuelva a verificar los permisos del archivo `authorized_keys`.

También verifique los permisos del directorio `~/.ssh`, los cuales deberían NO dejar escribir para 'group' y 'other'. Ejecute el siguiente comando para desabilitar los permisos de escritura para 'group' y 'other' en el directorio `~/.ssh`:

```
$ chmod go-w ~/.ssh

```

## Recuerde la frase-de-paso

Ahora puede acceder al servidor usando la llave en vez del password, pero como se facilita el asunto, ¿aun necesita entrar la frase-de-paso? La respuesta es usar un agente SSH, ¡un programa que recuerda las frases-de-paso de sus llaves! Hay muchas herramientas disponibles para esto, solo debe conocerlas y elegir la que le parezca mas apropiada a sus necesidades.

### Agente SSH

ssh-agent el el agente por defecto que incluye OpenSSH.

```
$ ssh-agent
SSH_AUTH_SOCK=/tmp/ssh-vEGjCM2147/agent.2147; export SSH_AUTH_SOCK;
SSH_AGENT_PID=2148; export SSH_AGENT_PID;
echo Agent pid 2148;

```

Cuando ejecuta `ssh-agent`, se mostrara en pantalla las variables de entorno que serán usadas. Para hacer uso de estas variables, ejecute `eval`.

```
$ eval `ssh-agent`
Agent pid 2157

```

Puede agregarlo al archivo `/etc/profile` para que se ejecute cada vez que inicia sesión:

```
# echo 'eval `ssh-agent`' >> /etc/profile

```

Note las forma correcta de poner las comillas, las externas son simples, mientras que dentro se usan las invertidas.

Ahora que el `ssh-agent` esta corriendo, necesitamos decirle que tenemos una llave privada, y donde esta.

```
$ ssh-add ~/.ssh/id_dsa
Enter passphrase for /home/user/.ssh/id_dsa:
Identity added: /home/user/.ssh/id_dsa (/home/user/.ssh/id_dsa)

```

Nos preguntara por nuestra frase-de-paso, la ingresamos, y es todo. Ahora puede ingresar al servidor remoto sin tener que entrar su password.

La única desventaja es que cada nueva instancia de `ssh-agent` necesita ser ejecutada por cada consola (shell) que se abra, esto significa que se debe correr `ssh-agent` cada vez en cada consola. Hay una solución para esto, con un programa o mas bien un script llamado [keychain](http://www.gentoo.org/proj/en/keychain/index.xml) que cubrirá las siguientes sesiones.

#### Usando GnuPG Agent

El agente [GnuPG](/index.php/GnuPG "GnuPG"), es distribuido en el paquete {Package Official|gnupg2}}, posee una emulación del agente de OpenSSH. si usas GPG debería considerar usar este agente para mantener cuidadas sus llaves. De otra forma puede interesarle el dialogo de entrada de PIN que provee que gestiona las frases-de-paso, es diferente al de keychain.

Para empezar a usar el agente GPG primero hay que correr `gpg-agent` con las opciones `--enable-ssh-support`. Por ejemplo (no olvide darle los permisos de ejecución):

 `/etc/profile.d/gpg-agent.sh` 

```
#!/bin/sh

# Inicia el agente GnuPG y habilita la emulación del agente de OpenSSH 
gnupginf="${HOME}/.gnupg/gpg-agent.info"

if pgrep -u "${USER}" gpg-agent >/dev/null 2>&1; then
    eval `cat $gnupginf`
    eval `cut -d= -f1 $gnupginf | xargs echo export`
else
    eval `gpg-agent --enable-ssh-support --daemon`
fi

```

Una vez que gpg-agent este corriendo puede usar `ssh-add` para verificar las llaves, justo como lo hizo con ssh-agent. La lista de las llaves aprobadas se guarda en el archivo `~/.gnupg/sshcontrol`. Cuando su calve es aprobada obtendrá un dialogo de entrada de PIN pidiendo la frase-de-paso ( si es necesario). Puede controlar el almacenamiento de las frases-de-entrada en el archivo `~/.gnupg/gpg-agent.conf`. El siguiente ejemplo hará que gpg-agent mantenga las llaves por 3 horas:

```
 # Cache settings
 default-cache-ttl 10800
 default-cache-ttl-ssh 10800

```

Otra configuración útil para este archivo es incluir un programa para la entrada del PIN (GTK, QT o ncurses ):

```
 # Environment file
 write-env-file /home/username/.gnupg/gpg-agent.info

 # Keyboard control
 #no-grab

 # PIN entry program
 #pinentry-program /usr/bin/pinentry-curses
 #pinentry-program /usr/bin/pinentry-qt4
 pinentry-program /usr/bin/pinentry-gtk-2

```

#### Usando keychain

[Keychain](http://www.funtoo.org/en/security/keychain/intro/) administra una o mas llaves privadas, que se le hayan especificado. Cuando se inicializa, preguntara por la frase-de-paso para la clave privada, y la guardara. De esta manera sus llaves privadas estarán protegidas por password, pero no deberá ingresar su password una y otra vez.

Instalar keychain de los repositorios extra:

```
# pacman -S keychain

```

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

**Tip:** Si quiere mayor seguridad reemplace -Q con --clear pero es menos conveniente.

Si es necesario, reemplace `~/.ssh/id_dsa` con `~/.ssh/id_rsa`. Para aquellos que usan una shell que no es Bash, vean`keychain --help` o `man keychain` para detalles en otras Shells.

Cierre su shell y vuélvala a abrir, Keychain deberá aparecer y si es la primera vez que corre, le preguntara por la frase-de-paso de la llave privada especificada.

#### Usando ssh-agent y x11-show-askpass

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

Si usa el escritorio [GNOME](/index.php/GNOME "GNOME"), la herramienta [Gnome Keyring](/index.php/Gnome_Keyring "Gnome Keyring") puede ser usada como un agente de SSH. Visite el articulo [Gnome Keyring](/index.php/Gnome_Keyring "Gnome Keyring").

## Resolucion de problemas

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