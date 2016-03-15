## Instalación

Gamin tiene conflictos con [fam](https://aur.archlinux.org/packages/fam/). Si FAM está instalado, quitarlo antes, ignorando las dependencias:

```
# pacman -Rd fam

```

Luego, instalar [gamin](https://www.archlinux.org/packages/?name=gamin).

Quitar `fam` de la sección `DAEMONS` de su archivo `/etc/[rc.conf](/index.php/Rc.conf "Rc.conf")`. No hace falta cargar `gamin` en la sección `DAEMONS` de su archivo `/etc/[rc.conf](/index.php/Rc.conf "Rc.conf")` ya que Gamin arranca en forma automática cuando se necesita.