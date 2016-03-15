[dorpac](https://aur.archlinux.org/packages.php?do_Details=1&ID=3017) - le ayuda a librarse de los archivos /{boot,etc}/*.pac*

Contribuído por Jaroslaw Swierczynski <swiergot@juvepoland.com>

* * *

Escribí este sencillo guión para acelerar la gestión de los archivos .pacnew y .pacsave de mi directorio /etc. Estaba cansado de tener que hacerlo a mano casi todos los días (find, diff, vi, mv, rm, una y otra vez) y era fácil cometer un fallo.

Adicionalmente, puede ser de mayor utilidad incluso para aquellos usuarios más novatos que no saben de donde vienen estos archivos ya que explica por qué los crea pacman.

Todo lo que tiene que hacer es ejecutar dotpac (lo siento, no tenía tiempo de inventar un nombre mejor) y seguir los diálogos. No se preocupe, dotpac no hará nada si su expreso consentimiento. Tenga también en cuenta que no ofrece la posibilidad de combinar automágicamente los ficheros *.pac* con sus equivalentes en funcionamiento.

Las opiniones, sugerencias, ideas, e informes de error son bienvenidos.