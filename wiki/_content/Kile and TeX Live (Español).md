# Kile and TeX Live (Español)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Este artículo resume como instalar el editor de LaTeX Kile con TeXLive en vez de con TeTeX (el cual ya no está mantenido). Para más información sobre como instalar TeXLive en Arch Linux, visite el artículo de [TeXLive](/index.php/Texlive "Texlive").

## Contents

*   [1 Paso 1: Instalar TeXLive](#Paso_1:_Instalar_TeXLive)
*   [2 Paso 2: Instalar Okular](#Paso_2:_Instalar_Okular)
*   [3 Paso 3: Instalar Kile](#Paso_3:_Instalar_Kile)
*   [4 Solución de problemas](#Soluci.C3.B3n_de_problemas)
    *   [4.1 Avisos de pdfTeX](#Avisos_de_pdfTeX)

## Paso 1: Instalar TeXLive

La mejor manera de empezar es instalar el paquete texlive-most.

```
# pacman -S texlive-most

```

Asegúrese de haber habilitado el repositorio community (en /etc/pacman.conf). Si se encuentra con errores durante la instalación del estilo "tal comando no se pudo encontrar", pruebe a ejecutar:

```
$ export PATH=$PATH:/opt/texlive/bin

```

antes de instalar.

## Paso 2: Instalar Okular

Simplemente ejecute:

```
# pacman -S kdegraphics-okular 

```

Dese cuenta que okular puede leer tanto .pdf como .dvi por lo que no deberían hacer falta otras herramientas.

## Paso 3: Instalar Kile

Finalmente tiene que instalar Kile.

```
# pacman -S kile

```

Inicie Kile y, desde su menú, compruebe que todas las dependencias están solucionadas usando "Preferencias > Verificar sistema". Kile le preguntará por Acrobat Reader (el paquete en pacman se llama acroread), pero es opcional.

Dese cuenta que si instaló Kile antes de instalar los paquetes requeridos (como kdvi), puede instalarlos sin tener que reinstalar Kile para que sea completamente funcional.

Disfrute de Kile y TeXLive.

## Solución de problemas

### Avisos de pdfTeX

Si recibe avisos como:

```
pdfTeX aviso: pdflatex [...] la entrada fontmap para [...] ya existe, duplicados ignorados

```

intente eliminar los ficheros map pcr8y.map, phv8y.map, ptm8y.map del fichero de configuración updmap.cfg y finalmente ejecute updmap.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Kile_and_TeX_Live_(Español)&oldid=411586](https://wiki.archlinux.org/index.php?title=Kile_and_TeX_Live_(Español)&oldid=411586)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [TeX (Español)](/index.php/Category:TeX_(Espa%C3%B1ol) "Category:TeX (Español)")