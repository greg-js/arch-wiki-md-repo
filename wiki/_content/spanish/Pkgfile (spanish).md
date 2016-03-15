**pkgfile** es una herramienta para buscar ficheros en paquetes de los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Uso](#Uso)
*   [3 Comando no encontrado](#Comando_no_encontrado)
    *   [3.1 Bash](#Bash)
    *   [3.2 Zsh](#Zsh)
    *   [3.3 Fish](#Fish)
*   [4 Actualizaciones automáticas](#Actualizaciones_autom.C3.A1ticas)

## Instalación

[Instale](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") [pkgfile](https://www.archlinux.org/packages/?name=pkgfile) desde los repositorios oficiales, o [pkgfile-git](https://aur.archlinux.org/packages/pkgfile-git/) desde [AUR](/index.php/AUR "AUR").

La base de datos de *pkgfile* puede sincronizarse con:

```
# pkgfile -u

```

## Uso

Para buscar un paquete que contenga el archivo `makepkg`:

 `$ pkgfile makepkg`  `core/pacman` 

Para listar todos los archivos que provee el paquete [archlinux-keyring](https://www.archlinux.org/packages/?name=archlinux-keyring):

 `$ pkgfile -l archlinux-keyring` 
```
core/archlinux-keyring usr/
core/archlinux-keyring usr/share/
core/archlinux-keyring usr/share/pacman/
core/archlinux-keyring usr/share/pacman/keyrings/
core/archlinux-keyring usr/share/pacman/keyrings/archlinux-revoked
core/archlinux-keyring usr/share/pacman/keyrings/archlinux-trusted
core/archlinux-keyring usr/share/pacman/keyrings/archlinux.gpg
```

Lo último se puede comparar con `pacman -Ql` (vea [Consultar la base de datos de paquetes](/index.php/Pacman_(Espa%C3%B1ol)#Consultar_la_base_de_datos_de_paquetes "Pacman (Español)")), salvo que este se aplica a paquetes remotos.

## Comando no encontrado

[pkgfile](https://www.archlinux.org/packages/?name=pkgfile) incluye un hook de "comando no encontrado" para [Bash](/index.php/Bash_(Espa%C3%B1ol) "Bash (Español)") y [Zsh](/index.php/Zsh "Zsh") que buscará automáticamente en los repositorios oficiales, cuando se introduzca un comando desconocido:

 `$ abiword` 
```
abiword se encuentra en los siguientes paquetes:
  extra/abiword 2.8.6-7 usr/bin/abiword

```

Para habilitarlo cada vez que se arranca una consola, tiene que cargar el hook desde uno de los ficheros de inicialización de su intérprete de órdenes.

### Bash

 `~/.bashrc`  `source /usr/share/doc/pkgfile/command-not-found.bash` 

### Zsh

 `~/.zshrc`  `source /usr/share/doc/pkgfile/command-not-found.zsh` 

### Fish

[pkgfile](https://www.archlinux.org/packages/?name=pkgfile) no proporciona un hook específico para [Fish](/index.php/Fish "Fish"), pero es suficiente con definir su propia función `command-not-found`, que se ejecutará cuando Fish encuentre comandos desconocidos:

 `~/.config/fish/functions/command-not-found.fish` 
```
function command-not-found
        set cmd $argv[2]
        set pkgs (pkgfile -b -v $argv 2>/dev/null)
        if test -n $pkgs
                echo "$cmd puede encontrarse en los siguientes paquetes:"
                echo "$pkgs"
                return 0
        end
        return 127
end
```

## Actualizaciones automáticas

**pkgfile** viene con un servicio y un [temporizador](/index.php/Systemd/Timers "Systemd/Timers") de [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") para sincronizar automáticamente la base de datos de pkgfile. Para activar automáticamente las actualizaciones [habilite](/index.php/Systemd_(Espa%C3%B1ol)#Usar_las_unidades "Systemd (Español)") `pkgfile-update.timer`.

Por defecto, pkgfile se actualiza diariamente. Para cambiar esta programación, copie `/usr/lib/systemd/system/pkgfile-update.timer` a `/etc/systemd/system/pkgfile-update.timer` y edite este último archivo.