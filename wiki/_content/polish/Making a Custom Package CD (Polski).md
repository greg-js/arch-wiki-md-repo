Jeżeli chciałbyś przekopiować pakiety Arch Linux na inny komputer (na przykład z powodu wolnego połączenia internetowego) za pomocą płyty CD, podążaj za wskazówkami:

*   Utwórz repozytorium za pomocą gensync ([Custom local repository with ABS and gensync](/index.php/Custom_local_repository_with_ABS_and_gensync "Custom local repository with ABS and gensync")). Skopiuj pakiety z katalogu `/var/cache/pacman/pkg` na zaktualizowanym systemie Arch.
*   Utwórz ISO z repozytorium.
*   Zamountuj/włóż płytę do drugiego komputera.
*   Dodaj repozytorium do pliku `/etc/pacman.conf`:

```
 [mycd]
 Server = file:///mnt/cd/pkg

```

Możesz też po prostu skopiować pliki pakietów do katalogu `/var/cache/pacman/pkg` na drugim komputerze. Pacman pobierze pakiety z tego katalogu zamiast z Internetu jeżeli są aktualne.

Jeszcze inną opcją jest [utworzenie własnej płyty instalacyjnej](https://bbs.archlinux.org/viewtopic.php?id=1387).