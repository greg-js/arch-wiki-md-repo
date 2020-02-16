**Estado de la traducción**
Este artículo es una traducción de [Pacman development](/index.php/Pacman_development "Pacman development"), revisada por última vez el **2020-02-10**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Pacman_development&diff=0&oldid=593147) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

¿Interesado en el desarrollo de Pacman? Esta página debería ayudarle a comenzar.

Recuerde que si **usted** piensa que algo pertenece a esta página, ¡añádalo! Es probable que los desarrolladores actuales de pacman no sepan lo que las personas necesitan saber y que deberían estar en esta página.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Referencias y enlaces](#Referencias_y_enlaces)
*   [2 Repositorios del desarrollador](#Repositorios_del_desarrollador)
    *   [2.1 Allan McRae](#Allan_McRae)
    *   [2.2 Andrew Gregory](#Andrew_Gregory)
    *   [2.3 Eli Schwartz](#Eli_Schwartz)
*   [3 Consejos de Git](#Consejos_de_Git)

## Referencias y enlaces

*   [Página principal de Pacman](https://archlinux.org/pacman/)
*   [Últimas noticias/ChangeLog](https://projects.archlinux.org/pacman.git/plain/NEWS?id=HEAD)
*   [Interfaz Web del Git de Pacman](https://projects.archlinux.org/pacman.git/)
*   [Pacman Roadmap](/index.php/Pacman_Roadmap "Pacman Roadmap")

*   [Archivos de la lista de correo](https://mailman.archlinux.org/pipermail/pacman-dev/)

*   [HACKING](https://archlinux.org/pacman/HACKING.html)
*   [Enviar parches](https://archlinux.org/pacman/submitting-patches.html)
*   [Ayuda en la traducción](https://archlinux.org/pacman/translation-help.html)

*   IRC: #archlinux-pacman en irc.freenode.net

## Repositorios del desarrollador

Algunos de los "regulares" tienen sus propios repositorios con trabajo en progreso, ramas de trabajo y características, etc. Varios se listan aquí, pero siéntase libre de añadir más que pueda conocer.

### Allan McRae

Web: [https://projects.archlinux.org/users/allan/pacman.git/](https://projects.archlinux.org/users/allan/pacman.git/)
Clone: [git://projects.archlinux.org/users/allan/pacman.git](git://projects.archlinux.org/users/allan/pacman.git)
Clone: [https://projects.archlinux.org/git/users/allan/pacman.git](https://projects.archlinux.org/git/users/allan/pacman.git)

### Andrew Gregory

Web: [https://github.com/andrewgregory/pacman/](https://github.com/andrewgregory/pacman/)
Clone: [https://github.com/andrewgregory/pacman.git](https://github.com/andrewgregory/pacman.git)

### Eli Schwartz

Web: [https://git.archlinux.org/users/eschwartz/pacman.git](https://git.archlinux.org/users/eschwartz/pacman.git)
Clone: [git://git.archlinux.org/users/eschwartz/pacman.git](git://git.archlinux.org/users/eschwartz/pacman.git)

## Consejos de Git

Antes de utilizar estos consejos, se recomienda encarecidamente leer el artículo [Git](/index.php/Git_(Espa%C3%B1ol) "Git (Español)").

Clone el repositorio git - solo necesario una vez:

```
git clone [https://projects.archlinux.org/pacman.git](https://projects.archlinux.org/pacman.git) pacman

```

Active los *hooks* útiles:

```
mv .git/hooks/applypatch-msg.sample .git/hooks/applypatch-msg
mv .git/hooks/commit-msg.sample .git/hooks/commit-msg
mv .git/hooks/pre-commit.sample .git/hooks/pre-commit
mv .git/hooks/pre-rebase.sample .git/hooks/pre-rebase

```

o

```
rename .sample "" .git/hooks/*.sample

```

Siempre haga su trabajo en una rama local nueva para evitarse dolores de cabeza.

Para parchear la rama principal:

```
git format-patch master

```

Para parchear Amend (no lo utilice después de un *push*):

```
git commit -a --amend -s

```

Para actualizar la rama principal:

```
git checkout master
git pull

```

Para combinar los cambios en la rama principal desde "<rama>":

```
git rebase master <rama>

```

Para obtener la rama *maint*:

```
git checkout -b maint origin/maint

```

Para añadir un repositorio remoto:

```
git remote add toofishes [git://code.toofishes.net/dan/pacman.git](git://code.toofishes.net/dan/pacman.git)

```

Para obtener la rama de trabajo de toofishes:

```
git branch -r
git checkout -b toofishes-working toofishes/working

```