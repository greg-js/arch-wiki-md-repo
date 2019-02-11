**Estado de la traducción**
Este artículo es una traducción de [Erlang](/index.php/Erlang "Erlang"), revisada por última vez el **2019-02-08**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Erlang&diff=0&oldid=566062) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[Erlang](https://www.erlang.org/) es un lenguaje de programación con las cualidades específicas de datos inmutables y computación distribuida.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Utilización](#Utilización)
*   [3 Consejos y trucos](#Consejos_y_trucos)
    *   [3.1 Modo Emacs](#Modo_Emacs)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [erlang](https://www.archlinux.org/packages/?name=erlang).

## Utilización

Para obtener más detalles, véase la [documentación de Erlang](http://erlang.org/doc/getting_started/intro.html).

Para activar la consola, ejecute la orden `erl`

En la cual puede ingresar órdenes como:

```
   Erlang/OTP 21 [erts-10.1] [source] [64-bit] [smp:4:4] [ds:4:4:10] [async-threads:1] [hipe]
   Eshell V10.1  (abort with ^G)
   1> 1 + 2.
   3
   2> (2 + 3) * 4 / 5.
   4.0
   3>

```

## Consejos y trucos

### Modo Emacs

Para configurar el modo [Emacs](/index.php/Emacs_(Espa%C3%B1ol) "Emacs (Español)") incluido, `erlang-mode`, véase la [documentación](http://erlang.org/doc/apps/tools/erlang_mode_chapter.html#setup-on-unix) (la ruta OTP es `/usr/lib/erlang`).