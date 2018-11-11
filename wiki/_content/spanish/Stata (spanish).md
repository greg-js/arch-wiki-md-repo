**Estado de la traducción**
Este artículo es una traducción de [Stata](/index.php/Stata "Stata"), revisada por última vez el **2018-10-29**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Stata&diff=0&oldid=551964) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[Stata](https://www.stata.com/) es un paquete de software estadístico de propósito general para *nix, Windows y Mac. A continuación se le explicará cómo instalar Stata y las librerías necesarias.

## Contents

*   [1 Librerías necesarias](#Librer.C3.ADas_necesarias)
*   [2 Instalar Stata](#Instalar_Stata)
*   [3 Consejos y trucos](#Consejos_y_trucos)
*   [4 Solución de problemas](#Soluci.C3.B3n_de_problemas)

## Librerías necesarias

Stata depende de [libpng12](https://www.archlinux.org/packages/?name=libpng12). Stata también utiliza el framework GTK+.

Si está ejecutando STATA 14/15 y recibe un mensaje sobre la falta de libncurses.so.5 [instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") [ncurses5-compat-libs](https://aur.archlinux.org/packages/ncurses5-compat-libs/).

## Instalar Stata

Una vez que haya instalado estos paquetes, debe extraer los archivos de instalación en la carpeta donde desea colocar Stata. Stata recomienda ponerlo bajo `/usr/local/`. Por ejemplo:

```
# mkdir /usr/local/stata15

```

Una vez que haya creado el directorio, cámbiese a él:

```
$ cd /usr/local/stata15

```

Luego desde el directorio, extraiga el archivo de instalación

```
# tar xvf /path/to/Stata15Linux64.tar.gz

```

Y ejecute el archivo de instalación:

```
# ./install

```

Siga las instrucciones y terminará la instalación de Stata.

En una instalación predeterminada de Arch Linux, los iconos no se mostrarán si se inicia. Esto se debe a que Stata se está construyendo contra versiones anteriores de librerías. Consulte la sección de solución de problemas para saber cómo solucionarlo.

## Consejos y trucos

Para agregar Stata a su ruta, agregue lo siguiente al final de su ruta en su [bashrc](/index.php/Bashrc_(Espa%C3%B1ol)#Archivos_de_configuraci.C3.B3n "Bashrc (Español)"):

 `~/.bashrc` 
```
PATH=$PATH:/usr/local/stata12/

```

## Solución de problemas

Stata 12 y 13 se crearon al menos en versiones anteriores de libpng y zlib. Por lo tanto, faltarán íconos al iniciar Xstata (la interfaz gráfica). La solución **NO** es volver a una versión anterior de las librerías de su sistema, sino seguir los consejos proporcionados por el departamento técnico de StataCorp [aquí](http://www.statalist.org/forums/forum/general-stata-discussion/general/2199-linux-stata-bug-libpng-on-newer-opensuse-posiblemente-other-distributions). Implica compilar las versiones anteriores de libpng y zlib y colocarlas en una carpeta con la que su sistema no interactuará. Luego se debe hacer un wrapper para Stata para hacer referencia a estas librerías. Estos pasos se han automatizado mediante un script en bitbucket, que se encuentra [aquí](https://bitbucket.org/vilhuberl/stata-png-fix).