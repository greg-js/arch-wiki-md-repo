**Estado de la traducción**
Este artículo es una traducción de [Abiword](/index.php/Abiword "Abiword"), revisada por última vez el **2018-11-09**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Abiword&diff=0&oldid=511501) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[Abiword](http://www.abisource.com/) es un procesador de textos que ofrece una alternativa más liviana que [LibreOffice](/index.php/LibreOffice_(Espa%C3%B1ol) "LibreOffice (Español)") Writer y [OpenOffice](/index.php/OpenOffice "OpenOffice") Writer, mientras que al mismo tiempo proporciona una gran funcionalidad. Abiword admite muchos tipos de documentos estándar, como documentos ODF, documentos Microsoft Word, documentos WordPerfect, documentos Rich Text Format y páginas web HTML.

## Contents

*   [1 Instalación](#Instalación)
*   [2 Plantillas](#Plantillas)
*   [3 Comprobación de gramática](#Comprobación_de_gramática)
*   [4 Cambiar los atajos de teclado](#Cambiar_los_atajos_de_teclado)
*   [5 Fuentes LaTeX](#Fuentes_LaTeX)
*   [6 Solución de problemas](#Solución_de_problemas)
    *   [6.1 Solución para el cuelgue del diálogo de impresión](#Solución_para_el_cuelgue_del_diálogo_de_impresión)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [abiword](https://www.archlinux.org/packages/?name=abiword). Es posible que desee instalar diccionarios si desea realizar una revisión ortográfica, el cual puede ser proporcionado por el paquete [aspell-en](https://www.archlinux.org/packages/?name=aspell-en) para el idioma inglés.

Para solucionar los problemas del cursor pequeño y el texto desalineado, instale [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation) desde los repositorios oficiales o [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/) desde [AUR](/index.php/AUR_(Espa%C3%B1ol) "AUR (Español)") y [ttf-freefont](https://www.archlinux.org/packages/?name=ttf-freefont) desde los repositorios oficiales.

## Plantillas

Si desea cambiar los estilos predeterminados en Abiword, debe abrir un nuevo documento, cambiarlo según sus propias necesidades y guardarlo como el nombre de la plantilla *normal.awt* en el directorio `~/.AbiSuite/templates`. Después de eso, sus nuevos documentos seguirán la plantilla.

Las instrucciones anteriores no funcionan para Abiword 3.0\. Lo siguiente funciona:

En un documento nuevo, elija *Formato > Crear y modificar estilos...* en el menú, ajuste el estilo Normal a lo que prefiera y guárdelo como `~/normal.awt`. Entonces ejecute:

```
sudo mv ~/normal.awt /usr/share/abiword-3.0/templates/

```

También se pueden modificar otros estilos en `/usr/share/abiword-3.0/templates/`.

## Comprobación de gramática

Habilite la revisión gramatical desde *Editar > Preferencias > Corrección ortográfica > Verificación automática de gramática*.

## Cambiar los atajos de teclado

Consulte [esta publicación en la wiki](http://www.abisource.com/wiki/Keyboard_bindings) sobre cómo cambiar los atajos de teclado predeterminados en Abiword.

Si ese método no funciona, agregue `KeyBindings="viEdit"` a `/usr/share/abiword-3.0/system.profile` dentro de la etiqueta `SystemDefaults` .

## Fuentes LaTeX

El paquete [abiword](https://www.archlinux.org/packages/?name=abiword) viene con una función que le permite al usuario insertar códigos LaTeX en un documento. Para que se muestren correctamente los símbolos matemáticos, es necesario descargar [latex-xft-fonts](http://movementarian.org/latex-xft-fonts-0.1.tar.gz) y guardarlo en el directorio `/usr/share/fonts`. Para instalar la fuente, extraiga el tarball y luego ejecute lo siguiente:

```
# fc-cache -fv

```

## Solución de problemas

### Solución para el cuelgue del diálogo de impresión

**Nota:** Este error ha sido reportado como inexistente para la versión 2.8.1 o superior. Sin embargo, esta sección permanecerá para las versiones anteriores o por si vuelve a aparecer

Por alguna razón, las versiones actuales de Abiword y libgnomeprint no se llevan bien. La plantilla predeterminada `.abw` hace que el programa se bloquee cuando el usuario intenta imprimir. La solución es forzar a abiword a trabajar con el formato `.rtf` en su lugar. Al seguir los pasos que se muestran a continuación, establecerá el formato de guardado predeterminado a .rtf y engañará a Abiword para que use un archivo `.rtf` como plantilla predeterminada.

Abra `~/.AbiSuite/AbiWord.Profile` y añada la siguiente línea en la segunda sección <scheme>.

```
DefaultSaveFormat=".rtf"

```

Debería ser algo así:

```
<Scheme
   name="_custom_"
   ZoomPercentage="64"
   DefaultSaveFormat=".rtf"
/>

```

Es necesario entonces cambiar la plantilla por defecto. Debe seguir exactamente estos pasos.

1.  Abra Abiword y guarde un documento en blanco titulado `normal.rtf` en `~/.AbiSuite/templates/`. Si el directorio no existe, créelo.
2.  Cambie el nombre del archivo a *normal.awt*.

¡Sencillamente **no** guarde un archivo `.awt` en blanco! Debe engañar a Abiword para que use una plantilla `.rtf` para que esto funcione.

Tan pronto como se resuelva el conflicto entre Abiword y libgnomeprint, estas instrucciones ya no serán necesarias y deberán eliminarse.