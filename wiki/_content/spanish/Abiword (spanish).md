[Abiword](http://www.abisource.com/) es un procesador de texto que ofrece una alternativa más ligera para [LibreOffice](/index.php/LibreOffice "LibreOffice") Writer, mientras que al mismo tiempo que proporciona una gran funcionalidad. Abiword es compatible con muchos tipos de documentos estándar, tales como documentos de OpenOffice.org/LibreOffice, documentos de Microsoft Word, documentos de WordPerfect, Rich Text Format documentos y páginas Web HTML.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Cambio de combinaciones de teclas](#Cambio_de_combinaciones_de_teclas)
*   [3 Fuentes de LaTeX](#Fuentes_de_LaTeX)
*   [4 Enlaces externos](#Enlaces_externos)

## Instalación

Antes de instalar, usted querrá instalar un diccionarios si desea; usar la corrección ortográfica.

```
 # pacman -S aspell-es

```

Para instalar, ejecute:

```
 # pacman -S abiword

```

Para intalar plugins adicionales:

```
 # pacman -S abiword-plugins

```

Para solucionar pequeños problemas de texto cursor y desalineados, instalar [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/) del [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)") y:

```
# pacman -S ttf-freefont

```

## Cambio de combinaciones de teclas

Ver [this wiki post](http://www.abisource.com/wiki/Keyboard_bindings) acerca de cómo cambiar las combinaciones de teclado por defecto en Abiword.

## Fuentes de LaTeX

El paquete [abiword-plugins](https://www.archlinux.org/packages/?name=abiword-plugins) viene con una función que permite al usuario insertar códigos de LaTeX en un documento. Para visualizar correctamente los símbolos de matemáticas, es necesario descargar [latex-xft-fonts](http://movementarian.org/latex-xft-fonts-0.1.tar.gz)y guardarlo en el directorio `/usr/share/fonts`. Para instalar la fuente, descomprimir el archivo

```
 # Tar-xzf (nombre del archivo tar.gz)

```

y luego ejecutar

```
 # Fc-cache-fv

```

## Enlaces externos

*   [Pagina official](http://www.abisource.com/)