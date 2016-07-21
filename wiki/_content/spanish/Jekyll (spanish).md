[Jekyll](http://jekyllrb.com/) es un generador de sitios estáticos diseñado para blogs. Escrito en Ruby y desarrollado por co-fundador de GitHub [Tom Preston-Werner](http://tom.preston-werner.com/). Toma como punto de partida una carpeta base (que es el sitio web estático crudo), lo pasa a través de conversores Textile, Markdown y Liquid generando un sitio web estático completo listo para ser servido a través de Apache u otro servidor web. Es el motor de las [Páginas de GitHub](http://pages.github.com/).

## Instalación

Jekyll se puede instalar en Arch Linux con el gestor de paquetes [RubyGems](https://en.wikipedia.org/wiki/RubyGems "wikipedia:RubyGems") o usando el paquete correspondiente en el [AUR](/index.php/AUR "AUR"). Ambos métodos requieren tener instalado el paquete Ruby de los repositorios oficiales.

## RubyGems (recomendado)

**Nota:** RubyGems 1.8 y superiores muestran [numerosas advertencias no-críticas](https://github.com/rspec/rspec-core/issues/345).

La mejor forma de instalar Jekyll es con [RubyGems](/index.php/Ruby#RubyGems "Ruby"), un gestor de paquetes para el lenguaje de programación [Ruby](/index.php/Ruby "Ruby"). RubyGems se instala junto con el paquete [ruby](https://www.archlinux.org/packages/?name=ruby), el cual se encuentra en los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").

Jekyll se puede instalar para todos los usuarios del sistema usando el comando `gem` como root. Para métodos alternos de instalación, visite la página de [Ruby](/index.php/Ruby#RubyGems "Ruby").

Antes de instalar Jekyll asegurese de actualizar RubyGems.

```
$ sudo gem update

```

entonces instale Jekyll usando el comando `gem`.

```
$ gem install jekyll

```

Vea [Ruby#RubyGems](/index.php/Ruby#RubyGems "Ruby") para mayor información sobre la gestion de Gem en Arch, poniendo especial enfasis en establecer la variable PATH