Debido a las vueltas que he tenido con los gestores de correo creo que al final he conseguido con claws-mail todo los que necesitaba. A continuación voy a explicar en uns sencillos pasos como configurar este gestor de correo para hacerlo funcionar con GMail para recibir el correo a traves de pop.

Requisitos:

*   Cuenta Gmail
*   Claws-mail
*   Modulo traycon.so

1º Primero vamos a configurar GMail para poder recibir el correo. Para ello nos dirigimos a gmail desde nuestro navegador y entramos en **configuración/Reenvío y correo POP** y activamos la recepción de correo pop. Está parte cada usuario puede dejarla como desee, si quiere guardar una copia también en el servidor u otros datos, guardamos cambios y listo. Luego vamos a "mi cuenta" en google apps, acceso y seguridad, bajamos hasta encontrar la opción "Permitir el acceso de aplicaciones menos seguras" la cual debe estar habilitada o de lo contrario nos marcará error de autenticación al sincronizar con gmail.

2º [Instalamos](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") el paquete [claws-mail](https://www.archlinux.org/packages/?name=claws-mail).

Al ejecutarlo nos aparecerá un asistente, lo cancelamos, ya que debemos cambiar más cosas luego y mejor hacerlo todo de 1 vez.

Ya en la pantalla de claws-mail nos dirijimos a **Configuración/Crear una nueva cuenta...** y aquí es donde se configura todo. Veremos una pantalla con diversas pestañas que iremos repasando para completar todos los datos.

*   **Básicas:**
    *   Nombre de la cuenta: loquesea
    *   Nombre Completo: El nombre que queramos que salga de al recibir alguien el correo
    *   Correo: loquesea@gmail.com
    *   Servidor recepción: pop.gmail.com
    *   Servidor smtp: smtp@gmail.com
    *   Usuario: loquesea@gmail.com (Muy Importante: Debe ir la dirección de correo, NO la nick con el que accedemos via web)
    *   Contraseña: loquesea

*   **Recibir:** Lo dejamos por defecto, NO marcamos "Utilizar autentificación segura APOP"

*   **Enviar:** Marcamos (MUY IMPORTANTE) "Autentificación SMTP (SMTP AUTH)", modo de autentificación

"automático" (usuario y contraseña en blanco), lo demás desmarcado.

Pasamos a la pestaña SSL

*   **SSL:** Marcamos "Usar SSL para la conexión POP", "Usar SSL para la conexión SMTP" y activamos "Usar SSL no-bloqueante".

*   **Avanzados:** Puerto SMTP: 465 Puertos POP3: 995

Guardamos y listo.

Nos vamos a Configuración/Preferencias/Recepción y activamos **comprobar correo cada X minutos** (cada uno que ponga el tiempo jeje).

Bien ya tenemos claws-mail configurado, podemos comprobar como podemos recibir y enviar correctamente.

Ahora nos dirigimos a [http://www.claws-mail.org/plugins.php](http://www.claws-mail.org/plugins.php) para bajarnos el módulo que deseemos. Luego nos dirigimos a Configuración/Modulos y cargamos el que deseemos.

En mi caso instalé el paquete **claws-mail-extra-plugins** y activé el plugins **Trayicon**, que nos permite minimizarlo y ver si ha recibido correo en un solo icono.

NOTA: Este paquete se encuentra en AUR, para instalarlo bajamos el PKGBUILD y ejecutamos:

```
# makepkg -sic PKGBUILD

```