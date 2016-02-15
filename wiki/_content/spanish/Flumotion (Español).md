[Flumotion](http://www.flumotion.net) es un servidor multimedia de "streaming" creado con el respaldo de Fluendo. Presenta intuitivas herramientas gráficas de administración, haciendo sencilla la tarea de configurar y manipular "streams" de audio y video incluso para los administradores de sistemas novatos.

## Contents

*   [1 Instalar Flumotion](#Instalar_Flumotion)
*   [2 Cambiar el usuario y la contraseña por defecto](#Cambiar_el_usuario_y_la_contrase.C3.B1a_por_defecto)
*   [3 Arrancando el gestor](#Arrancando_el_gestor)
*   [4 Arrancar el «worker»](#Arrancar_el_.C2.ABworker.C2.BB)
*   [5 Iniciar la herramienta de configuración](#Iniciar_la_herramienta_de_configuraci.C3.B3n)

## Instalar Flumotion

Habilite primero el repositorio [community] y haga entonces:

```
# pacman -S flumotion

```

## Cambiar el usuario y la contraseña por defecto

Ejecute:

```
htpasswd -nb user password

```

Reemplace el usuario:PSfNpHTkpTx1M con la salida de htpasswd en `/etc/flumotion/managers/default/planet.xml`

A continuación, sitúe su usuario y contraseña en los lugares adecuados en `/etc/flumotion/workers/default.xml`

## Arrancando el gestor

```
flumotion-manager -d 3 /etc/flumotion/managers/default/planet.xml

```

**Nota:** Puede especificar un archivo de certificado PEM diferente pasándole al gestor el parámetro --certificate.

## Arrancar el «worker»

```
flumotion-worker -d 3 -u user -p password

```

## Iniciar la herramienta de configuración

*   GUI: `flumotion-admin`
*   ncurses: `flumotion-admin-text`