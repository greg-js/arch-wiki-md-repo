Zainteresowany w rozwijaniu Pacmana? Ta strona powinna pomóc Tobie zacząć.

Pamiętaj, że jeżeli myślisz, że czegoś brakuje na tej stronie, dodaj to! Obecni deweloperzy pacmana nie muszą wiedzię czego ludzie potrzebują wiedzieć i co powinno być na tej stronie.

## Contents

*   [1 References and Links](#References_and_Links)
*   [2 Repozytoria deweloperów](#Repozytoria_deweloper.C3.B3w)
    *   [2.1 Allan McRae](#Allan_McRae)
    *   [2.2 Dan McGee](#Dan_McGee)
    *   [2.3 Dave Reisner](#Dave_Reisner)
*   [3 Wskazówki do Gita](#Wskaz.C3.B3wki_do_Gita)

## References and Links

*   [Strona główna pacmana](https://archlinux.org/pacman/)
*   [Ostatnie WIADOMOŚCI/ChangeLog](https://projects.archlinux.org/pacman.git/plain/NEWS?id=HEAD)
*   [Internetowy interfejs Gita Pacmana](https://projects.archlinux.org/pacman.git/)
*   [Plan działania pacmana](/index.php/Pacman_Roadmap "Pacman Roadmap")

*   [Archiwa list mailingowych](https://mailman.archlinux.org/pipermail/pacman-dev/)

*   [HACKING](https://archlinux.org/pacman/HACKING.html)
*   [Poddawanie do rozważenia łatek](https://archlinux.org/pacman/submitting-patches.html)
*   [Pomoc w tłumaczeniu](https://archlinux.org/pacman/translation-help.html)

*   IRC: #archlinux-pacman na irc.freenode.net

## Repozytoria deweloperów

Garstka "stałych klientów" ma własne repozytoria z produkcją w toku, pracą i gałęziami z funkcjonalnościami, etc. Niektóre są wylistowane tutaj, ale czuj się zachęcony, aby dodać więcej o których możliwe, że wiesz.

### Allan McRae

Sieć: [https://projects.archlinux.org/users/allan/pacman.git/](https://projects.archlinux.org/users/allan/pacman.git/)
Sklonuj: [git://projects.archlinux.org/users/allan/pacman.git](git://projects.archlinux.org/users/allan/pacman.git)
Sklonuj: [https://projects.archlinux.org/git/users/allan/pacman.git](https://projects.archlinux.org/git/users/allan/pacman.git)

### Dan McGee

Sieć: [http://code.toofishes.net/cgit/dan/pacman.git/](http://code.toofishes.net/cgit/dan/pacman.git/)
Sklonuj: [git://code.toofishes.net/dan/pacman.git](git://code.toofishes.net/dan/pacman.git)
Sklonuj: [http://code.toofishes.net/git/dan/pacman.git](http://code.toofishes.net/git/dan/pacman.git)

### Dave Reisner

Sieć: [https://github.com/falconindy/pacman](https://github.com/falconindy/pacman)
Sklonuj: [git://github.com/falconindy/pacman.git](git://github.com/falconindy/pacman.git)
Sklonuj: [https://github.com/falconindy/pacman.git](https://github.com/falconindy/pacman.git)

## Wskazówki do Gita

Zanim zaczniesz używać tych wskazówek, jest wysoce zalecane przeczytanie [Super krótkiego przewodnika po Gicie](/index.php/Super_Quick_Git_Guide "Super Quick Git Guide").

Sklonuj repozytorium gita - potrzebne tylko raz

```
 git clone [git://projects.archlinux.org/pacman.git](git://projects.archlinux.org/pacman.git) pacman

```

Włącz użyteczne skrypty (hooki)

```
 mv .git/hooks/applypatch-msg.sample .git/hooks/applypatch-msg
 mv .git/hooks/commit-msg.sample .git/hooks/commit-msg
 mv .git/hooks/pre-commit.sample .git/hooks/pre-commit
 mv .git/hooks/pre-rebase.sample .git/hooks/pre-rebase

```

lub

```
 rename .sample "" .git/hooks/*.sample

```

Zawsze pracuj na nowej lokalnej gałęzi aby uchronić siebie samego przed bólem głowy.

Stwórz łatkę do głownej gałęzi

```
 git format-patch master

```

Popraw łatkę (Nie używaj tego po "pushu")

```
 git commit -a --amend -s

```

Uaktualnij główną gałąź

```
 git checkout master
 git pull

```

Połącz zmiany w głównej gałęzi z "<gałęzią>"

```
 git rebase master <branch>

```

Otrzymaj gałęź "mainteinera"

```
 git checkout -b maint origin/maint

```

Dodaj zdalne repozytorium

```
  git remote add toofishes [git://code.toofishes.net/dan/pacman.git](git://code.toofishes.net/dan/pacman.git)

```

Zdobądź roboczą gałąź Dana McGee

```
  git branch -r
  git checkout -b toofishes-working toofishes/working

```