Hay dos formas populares de configurar una terminal Linux para que trabaje de forma transparente sobre un fondo de escritorio, sin ningún borde, barra de menú o barra de herramientas. Esto es muy popular entre los desarrolladores debido a que es practico y se ve genial. Por ejemplo puede ser utilizado para ver el código fuente o tener de forma interactiva el estado de los procesos del sistema con htop. Algo parecido a conky, pero no igual.

## Contents

*   [1 La Forma Facíl](#La_Forma_Fac.C3.ADl)
*   [2 La Forma Profesional](#La_Forma_Profesional)
    *   [2.1 Paso 1](#Paso_1)
    *   [2.2 Paso 2](#Paso_2)
    *   [2.3 Paso 3](#Paso_3)
    *   [2.4 Paso 4](#Paso_4)
    *   [2.5 Paso 5](#Paso_5)

## La Forma Facíl

[Tilda](http://sourceforge.net/projects/tilda/) es una terminal Linux altamente adaptable, el autor está inspirado por las terminales clásicas mostradas en *los juegos de disparo en primera persona, Quake, Doom y Half-Life por nombrar algunos, donde la terminal no tiene bordes y está* oculta del escritorio hasta que una tecla o teclas son presionadas. *En nuestro ejemplo la instalaremos y proporcionaremos una terminal básica.*

```
# pacman -S tilda

```

En Gnome se puede encontrar dentro de Aplicaciones –> Accesorios –> Tilda.

Para lograr la apariencia deseada necesitaremos editar las configuraciones iniciales:

```
En la pestaña *General*, **desmarca** "Siempre visible".

En *Apariencia* se puede editar el **alto** y **ancho** a tu gusto,
 pero asegúrate de **marcar** "Activar Transparencia" y poner el "Nivel de Transparencia" **100%**.

En la pestaña de *Colores*, **escoge** "Verde sobre Negro" o "Personalizado".

En *Desplazamiento* debes **seleccionar** "Deshabilitado".

```

Eso es todo lo que se necesita, para ejecutar Tilda ir al menú Aplicaciones –> Accesorios –> Tilda y se podrá ver ahí. La razón por la que yo no la uso como mi terminal transparente es porque está es una solución rápida y no es muy estable, se corrompe a menudo (al menos para mi), se que otros están la pasan muy felices con Tilda. Otra razón es que no siempre se mantiene en el fondo, si tu utilizas la "tecla de despliegue" (F1) esta viene al frente.

## La Forma Profesional

Con el uso de [devilspie](http://www.burtonini.com/blog/computers/devilspie) tenemos mayor control sobre la colocación y el comportamiento sobre la ventana de la terminal. ¿Qué es Devilspie? *Devilspie puede ser configurado para detectar ventanas en el momento que son creadas, y corresponder la ventana a un conjunto de reglas. Si la terminal corresponde a las reglas, puede ejecutar una serie de acciones en esa ventana. Por ejemplo, hacer que todas las ventanas creadas por X-Chat aparescan en todos los espacios de trabajo, y la ventana principal de Gkrellm1 no aparezca en el paginador o la lista de tareas.*

### Paso 1

Instalar devilspie en Arch:

```
# pacman -S devilspie

```

### Paso 2

Crear un directorio oculto en el directorio del usuario:

```
$ mkdir ~/.devilspie

```

Hacer un archivo de configuración con extensión *.ds*, dentro del directorio devilspie. Este es el lugar donde devilspie busca por el archivo de configuración por defecto cuando inicia. Editar el archivo de configuración con tu editor favorito, para poner la ventana de terminal de la forma que deseamos.

```
$ nano ~/.devilspie/ConsolaEscritorio.ds

```

El archivo de configuración debe parecerse a esto:

```
(if
(matches (window_name) "ConsolaEscritorio")
(begin
(stick)
(below)
(undecorate)
(skip_pager)
(skip_tasklist)
(wintype "utility")
(geometry "+240+250")
(geometry "954×680")
)
)

```

Para una lista completa de opciones para la configuración devilspie, dar un vistazo a la completa [lista de opciones](http://foosel.org/linux/devilspie).

### Paso 3

Abrir una ventana de terminal gnome ir a Editar –> Perfiles –> Nuevo. Llamarlo como "ConsolaEscritorio".

Editar el Perfil, para lograr el aspecto deseado necesitamos editar las configuraciones iniciales:

```
En la pestaña *General*, **desmarca** "Mostrar la barra de menús en las terminales nuevas por omisión"

En la pestaña de *Colores*, **escoge** "Verde sobre Negro" (selecciona el que te agrade, yo prediero este).

En la pestaña de *Efectos*, **escoge** "Fondo transparente". Asegúrate de que este en "Ninguno"

En la pestaña de *Desplazamiento*, **selecciona** "Deshabilitado".

```

### Paso 4

En este paso configuramos devilspie y nuestro perfil personalizado de terminal para cargarse al inicio de la sesión.

Ir al menú Sistema –> Preferencias –> Sesiones.

Agregar un nuevo programa utilizando el signo `+`. En el primero colocaremos, "devilspie", en el nombre y comando.

El segundo programa le pondremos como nombre "gnome-terminal" y en el comando "gnome-terminal --window-with-profile=ConsolaEscritorio". Aquí estamos básicamente llamando a la terminal gnome con el perfil personalizado que creamos anteriormente.

**Note:** si se tiene problemas con la posición de la ventana se puede especificar aquí la geometría en las opciones del comando.

### Paso 5

Iniciar sesión nuevamente y se deberá obtener el aspecto deseado.

Se puede personalizar aún más para ajustar a las necesidades y estilo, tener más de una terminal; eso lo dejo a tu imaginación.