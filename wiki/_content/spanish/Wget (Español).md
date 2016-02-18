A veces se hace necesario ejecutar wget desde dentro de una red cuyo proxy requiere autentificación, o cuando pacman debe utilizar un proxy que requiera dicha autentification. Lo primero se puede conseguir de manera sencilla definiendo dos variables, en ~/.bashrc (tenga en cuenta que en este ejemplo se utiliza un proxy en la dirección 192.168.10.11, y escuchando en el puerto 8080):

```
export http_proxy="http://192.168.10.11:8080"
export ftp_proxy="http://192.168.10.11:8080"

```

Entonces, ejecute tiene tan sólo que ejecutar wget con dos argumentos extra: *--proxy-user="string" --proxy-passwd="string"*

Por ejemplo (Nombre de dominio: Wonderwall, usuario JohnDoe, contraseña Go4It"):

 `wget --proxy-user "Wonderwall\JohnDoe" --proxy-passwd "Go4It" URL` 

Es posible establecer un alias, lo que de nuevo puede hacerse en ~/.bashrc, tal como:

```
alias wget 'wget --proxy-user "Wonderwall\JohnDoe" --proxy-passwd="Go4It"'

```

Esto, sin embargo, representa un riesgo para la seguridad, ya que la contraseña es accesible para todo aquel que pueda leer su archivo .bashrc, o ver su lista de alias. Por otra parte, en cualquier sistema donde alguien pueda leer el arbol /proc completo, es posible ver cualquier argumento pasado en línea de órdenes, tal como el usuario y la contraseña.

Alternativamente, puede establecer el par usuario/contraseña en las variables http_proxy/ftp_proxy variables:

```
export http_proxy="http://wonderwall\\johndoe:Go4It@192.168.10.11:8080"
export ftp_proxy="http://wonderwall\\johndoe:Go4It@192.168.10.11:8080"

```

Para hacer que pacman utilice automáticamente wget y el proxy, defina la variables de entorno (en ~/.bashrc) y coloque la orden wget en el archivo /etc/pacman.conf, en la sección [options]:

```
XferCommand = /usr/bin/wget --proxy-user "domain\user" --proxy-passwd="password" --passive-ftp -c -O %o %u

```