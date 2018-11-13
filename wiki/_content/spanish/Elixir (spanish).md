**Estado de la traducción**
Este artículo es una traducción de [Elixir](/index.php/Elixir "Elixir"), revisada por última vez el **2018-10-14**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Elixir&diff=0&oldid=546028) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[Elixir](https://en.wikipedia.org/wiki/es:Elixir_(lenguaje_de_programaci%C3%B3n) es un lenguaje dinámico y funcional diseñado para crear aplicaciones escalables y de fácil mantenibilidad. Aprovecha la máquina virtual de [Erlang](https://www.erlang.org/), conocida por ejecutar sistemas de baja latencia, distribuidos y tolerantes a fallos, mientras que también se utiliza con éxito en el desarrollo web y el entornos de software integrado.

## Contents

*   [1 Instalación](#Instalación)
    *   [1.1 Versión única](#Versión_única)
    *   [1.2 Varias versiones](#Varias_versiones)
*   [2 Configuración](#Configuración)
*   [3 Véase también](#Véase_también)

## Instalación

### Versión única

Para la última versión de Elixir, [instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [elixir](https://www.archlinux.org/packages/?name=elixir) de los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)"). Este incluye Erlang, que es necesario para ejecutar Elixir.

### Varias versiones

Si desea ejecutar varias versiones de Elixir y/o Erlang, estas herramientas ayudan a instalar y administrar varias versiones de Elixir/Erlang:

*   [asdf](https://github.com/asdf-vm/asdf) - Elixir y Erlang
*   [exenv](https://github.com/mururu/exenv) - Solo Elixir
*   [kiex](https://github.com/taylor/kiex) - Solo Elixir
*   [kerl](https://github.com/kerl/kerl) - Solo Erlang

## Configuración

Asegúrese de tener la ruta *bin* de Elixir en su variable de entorno PATH para facilitar el desarrollo.

*   Versión única

	`/usr/bin`

*   Varias versiones

	Por favor, consulte la herramienta que utilizó para instalar Elixir

En ambos casos, debe encontrar su [archivo de perfil del intérprete de órdenes](http://unix.stackexchange.com/questions/117467/how-to-permanently-set-environmental-variables/117470#117470) y luego añadirlo al final de este archivo, la siguiente línea refleja la ruta a su instalación de Elixir:

```
 export PATH="$PATH:/ruta/al/bin/de/elixir"

```

## Véase también

*   [Elixir](http://elixir-lang.org/)
*   [Erlang](https://www.erlang.org/)