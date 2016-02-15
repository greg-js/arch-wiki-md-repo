Ak chcete skopírovať balíky z jedného počítača na druhý pomocou CD, vykonajte nasledujúce kroky:

*   Vytvorte repozitár balíkov pomocou gensync ([Custom local repository with ABS and gensync](/index.php/Custom_local_repository_with_ABS_and_gensync "Custom local repository with ABS and gensync")). Skopírujte balíky z `/var/cache/pacman/pkg` na prvom počítači.
*   Vytvorte ISO repozitára.
*   Pripojte CD na druhom počítači.
*   Pridajte vlastný repozitár do `/etc/pacman.conf`:

```
 [mycd]
 Server = file:///mnt/cd/pkg

```