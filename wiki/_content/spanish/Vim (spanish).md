Vim (**Vi** I**M**Proved), es un editor de texto derivado de Vi. Es notoriamente conocido por su empinada curva de aprendizaje, y su poco amistosa interfaz de usuario. No obstante, debido a su eficiencia, variedad de añadidos ("plugins") y posibilidades de personalización, vim es uno de los editores de texto más populares entre programadores y usuarios de sistemas tipo Unix (junto con [Emacs](/index.php/Emacs "Emacs")*). Existe también una versión gráfica, gVim, que proporciona un sistema de menús al usuario.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Configuración](#Configuraci.C3.B3n)
*   [3 Guía rápida de VIM](#Gu.C3.ADa_r.C3.A1pida_de_VIM)
    *   [3.1 Cómo iniciar vim](#C.C3.B3mo_iniciar_vim)
    *   [3.2 Cómo introducir texto](#C.C3.B3mo_introducir_texto)
    *   [3.3 Cómo mover el cursor](#C.C3.B3mo_mover_el_cursor)
    *   [3.4 Cómo borrar texto](#C.C3.B3mo_borrar_texto)
    *   [3.5 Cómo insertar texto](#C.C3.B3mo_insertar_texto)
    *   [3.6 Cómo Cortar, Copiar y Pegar](#C.C3.B3mo_Cortar.2C_Copiar_y_Pegar)
    *   [3.7 Cortar, Copiar y Pegar en modo visual](#Cortar.2C_Copiar_y_Pegar_en_modo_visual)
    *   [3.8 Deshacer ("Undo")](#Deshacer_.28.22Undo.22.29)
    *   [3.9 Cómo buscar una palabra](#C.C3.B3mo_buscar_una_palabra)
    *   [3.10 Cómo sustituir texto](#C.C3.B3mo_sustituir_texto)
    *   [3.11 Cómo salir de vim](#C.C3.B3mo_salir_de_vim)
*   [4 El tutor de Vim](#El_tutor_de_Vim)
*   [5 Enlaces externos](#Enlaces_externos)

## Instalación

*   [vim](https://www.archlinux.org/packages/?name=vim) y [gvim](https://www.archlinux.org/packages/?name=gvim) están en los repositorios oficiales. Instala estos con [pacman](/index.php/Pacman "Pacman").

## Configuración

El archivo de configuración de vim está situado en el directorio personal del usuario (`~/`) con el nombre .vimrc. Puede encontrar un archivo .vimrc de ejemplo en `/etc/vimrc`.

```
"Sample .vimrc
set nocompatible
set showmatch
set incsearch
set ignorecase  
set smartcase
set history=100
set backspace=eol,start,indent
set ruler
set tabstop=4
set shiftwidth=4
set expandtab
set virtualedit=all
set background=dark
set vb t_vg=
set mouse=v
set textwidth=79
set formatoptions=tcrq

```

*   Para instalar [gvim](https://www.archlinux.org/packages/?name=gvim) (es igual que vim pero con gráficos gtk2 y configurado con `/etc/gvimrc` y `~/.gvimrc`)

```
pacman -S gvim

```

*   Se encuentra disponible vía [pacman](/index.php/Pacman "Pacman") un grupo seleccionado de guiones muy populares para vim.

```
pacman -S vim-plugins

```

## Guía rápida de VIM

### Cómo iniciar vim

*   para iniciar vim y editar un archivo (nuevo o creado anteriormente)

```
vim *nombrearchivo*

```

*   para iniciar vim y abrir un archivo nuevo

```
vim

```

(puede darle nombre al archivo después, cuando lo grabe).

### Cómo introducir texto

Vim es un editor *modal*. Existen muchos modos, pero los modos habituales de vim son:

*   modo de inserción, en el cual, todo lo que teclee (excepto algunas teclas especiales) aparecerá en pantalla y se convertirá en parte integrante de su buffer de archivo
*   modo de órdenes (también llamado modo normal), en el cual lo que teclee se interpreta como una orden.
*   el así llamdo modo de la última línea o modo "ex", donde puede grabar un archivo o abrir otro, etc.
*   modo visual, el cual le permite cortar, copiar y pegar expeditivamente grandes porciones de texto mediante el teclado o el ratón.

Abra un nuevo archivo de texto con vim:

```
vim mitexto

```

Justo después de iniciar vim, usted está en modo de órdenes.

*   Cambiar entre modos

1\. De modo de órdenes a modo de inserción, pulse **i**

Escriba algo de texto.

2\. De modo de inserción a modo de órdenes, pulse **ESC**

Ahora está usted en modo de órdenes. Vim está esperado sus órdenes. Dese cuenta que si intenta escribir algo, obtiene resultados extraños e inesperados, porque, esto..., bien, usted necesita conocer alguns órdenes más, y Vim no está en modo de inserción.

3\. Pulse **ESC** de nuevo para asegurarse de que está usted verdaderamente en modo de órdenes Y pulse **:** (dos puntos, "colon" en inglés)

Ahora está usted en modo "ex"", el cual nos permitirá grabar nuestro primer archivo. Teclee:

```
wq

```

por "**w**rite" (escribir) y "**q**uit" (abandonar).

Su archivo ha sido escrito a disco y vim sale.

Nos ocuparemos del modo visual más tarde.

### Cómo mover el cursor

En ambos modos, el de órdenes y el de inserción, las flechas de cursor hacer que el cursor se mueva, y con gvim puede usted "pinchar" en la pantalla para llevar el cursor a otra posición. Sin embargo, ésta no es la manera ***a la vim*** de hacer las cosas. La manera más efectiva de mover el cursor es entrando primero en modo de órdenes pulsando ESC y moverse entonces por el texto utilizando las ordenes para mover el cursor propias de vim. Las 4 órdenes básicas son:

*   **j** mueve el curso una línea abajo

*   **k** mueve el cursor un línea arriba

*   **h** mueve el cursor un carácter a la izquierda

*   **l** mueve el cursor un carácter a la derecha

Recuerde: estas órdenes sólo funcionan en modo de óredenes. Al principio se puede sentir un poco incómodo. Una vez se familiarice con el uso de estas órdenes querrá aferrarse a ellas y se olvidará de las flechas de cursor.

Más sobre cómo mover el cursor:

*   **0** (cero) mueve el cursor al principio de la línea

*   **$** mueve el cursor al final de la línea

*   **w** mueve el cursor al primer carácter de la siguiente palabra

*   **e** mueve el cursor al último carácter de la siguiente palabra

*   **(** mueve el cursor al principio de la oración

*   **)** mueve el cursor al principio de la siguiente oración

*   **{** mueve el cursor al principio del párrafo

*   **}** mueve el cursor al principio del siguiente párrafo

*   **PGUP** o **<CTR>F** adelanta una página

*   **PGDOWN** or **<CTR>B** retrocede una página

### Cómo borrar texto

Primero le diré que la tecla SUPRIMIR ("DELETE")" siempre funciona, y que la tecla RETROCESO ("BACKSPACE") funciona con el texto que haya usted introducido en el modo de inserción. Le sugiero sin embargo que no use ninguna. En vez de eso, oblíguese a utilizar las ordenes de borrado propias de vim.

1\. Asegúrese de que está en modo de órdenes pulsando ESC

2\. Mueva el cursor sobre el carácter que quiera suprimir

3\. pulse **x** , el carácter desaparece

**x** es tan sólo una de las muchas y potentes órdenes de borrado. Recuerde, trate de utilizar las órdenes de movimiento del cursor**j k h l** para localizar su objetivo, y no abandone el modo de órdenes.

### Cómo insertar texto

1\. En modo de órdenes, mueva el cursor a la posición deseada

2\. pulse **i**, para entrar en modo de inserción. Esto **i**nsertará justo delante del carácter actual.

o bien

3\. pulse **a** para entrar en modo de inserción. Esto **a**dosará texto justo a la derecha del carácter actual.

### Cómo Cortar, Copiar y Pegar

Si ejecuta la versión con interfaz gráfico de vim, gvim, puede utilizar el ratón y los menús de persiana para hacerlo---de la misma manera que con otro editor. Sin embargo, éste no es el estilo preferido. Se sentirá mucho mejor si puede prescindir del ratón en su vida.

1\. Entre en modo de órdenes pulsando ESC

2\. Mueva el cursor a la línea que quiere copiar, pulsando j o k

3\. pulse

```
yy

```

para hacer una copia de la línea, o bien

```
dd

```

para cortarla y guardar una copia

4\. mueva ahora el cursor (pulsando k o j) al punto donde quiera pegar esta copia

5\. pulse

```
p

```

para pegar el buffer después de la línea actual, o bien

```
P

```

para pegar el buffer justo en la línea anterior de la actual

Si quiere copiar o cortar varias líneas, introduzca un número delante de la orden "yy"" o de "dd", así:

```
8yy

```

para copiar 8 líneas.

### Cortar, Copiar y Pegar en modo visual

*   El modo visual es como el modo de órdenes, pero las órdenes de movimiento se extienden a un área remarcada. Cuando se utiliza una orden que no sea de movimiento, se ejecuta ésta para toda el área remarcada. Cortar, copiar y pegar grandes porciones de texto es más eficiente hacerlo en modo visual.

Pulse **v** para entrar en modo visual desde el modo de órdenes, utilice entonces el cursor para ir arriba y abajo. Según lo hace, las líneas de texto se remarcarán. (También puede utilizar el ratón para remarcar áreas de texto.)

Para copiar la sección remarcada o "yank" (llevarse):

```
y

```

Para cortar la sección remarcada o "delete" (suprimir):

```
d

```

Para pegar o "put" (colocar):

```
p

```

para colocarlo "antes de"", o bien

```
P

```

para colocarlo "después de".

### Deshacer ("Undo")

Ahora que ha aprendido cómo cortar y suprimir, puede que necesito como deshacer algún error

```
u

```

deshará la última acción. Pulsándola repetidamente deshará las acciones sucesivas en orden inverso. De igual manera, utilice

```
Ctrl-R

```

para "volver a hacer" ("redo").

### Cómo buscar una palabra

Suponga que quiere encontrar todas las palabras "manzana" que haya en su archivo

1\. Asegúrese de que está en modo de órdenes pulsando ESC

2\. Teclee

```
/manzana

```

y pulse seguidamente ENTER para encontrar cualquier ocurrencia de "manzana". Cuando teclee la barra de dividir ("slash"), ésta y todos los caracteres siguientes se mostrarán al fondo de la pantalla. Después de pulsar ENTER, el cursor se colocará sobre la primera ocurrencia de "manzana" si la encuentra, y el objetivo estará remarcado.

3\. Después de encontrar su primera "manzana", puede continuar tecleando

```
n

```

para encontrar más "manzana"s

### Cómo sustituir texto

Asegúrese primero de que está en modo de órdenes pulsando ESC.

*   para reemplazar un único carácter, mueva el cursor sobre el carácter y pulse **r** seguido del reemplazo.
*   para reemplazar la primera ocurrencia de "viejo" en la línea actual por "nuevo"

```
:s/viejo/nuevo/

```

*   para reemplazar todas las ocurrencias de "viejo" en la línea actual por "nuevo"

```
:s/viejo/nuevo/g

```

*   para reemplazar la primera ocurrencia de "viejo" en todas las líneas entre la línea n1 y la n2 por "nuevo"

```
:n1,n2s/viejo/nuevo/

```

*   para reemplazar todas las ocurrencias de "viejo" entre las línesa n1 y n2 por "nuevo"

```
:n1,n2s/viejo/nuevo/g

```

*   para reemplazar todas las ocurrencias de "viejo" en el buffer completo por "nuevo", con un indicador para pedir la confirmación.

```
:1,$s/viejo/nuevo/gc

```

*   para reemplazar todas las ocurrencias de "viejo" en el buffer completo por "nuevo", con un indicador para pedir la confirmación.

```
:%s/viejo/nuevo/gc

```

### Cómo salir de vim

*   Para grabar y salir: pulse ESC para entrar en modo de órdenes, entonces:

```
:wq

```

o bien

```
:x

```

o bien

```
ZZ

```

*   grabe su archivo como **nuevonombre** antes de salir: pulse ESC, teclee entonces

```
:wq nuevonombre

```

*   Salir sin grabar, pulse ESC, teclee entonces

```
:q

```

*   Salida forzada

Si :q no funciona, será debido probablemente a que no grabó los cambios. Si quiere grabarlos, use :wq. Si no quiere conservar los cambios, teclee

```
:q!

```

## El tutor de Vim

Para saber más, ejecute:

```
vimtutor

```

desde la línea de comandos. Vim abrirá el archivo del tutor.

## Enlaces externos

*   [El sitio web oficial](http://www.vim.org/)
*   [Documentation de Vim](http://vimdoc.sourceforge.net/)