Related articles

*   [Pacman_(Česky)](/index.php/Pacman_(%C4%8Cesky) "Pacman (Česky)")

**pkgfile** je nástroj pro vyhledávání souborů z balíků v oficiálních úložištích.

## Instalace

Nainstalujte balíček [pkgfile](https://www.archlinux.org/packages/?name=pkgfile). Alternativně balíček vývojové verze [pkgfile-git](https://aur.archlinux.org/packages/pkgfile-git/).

Databáze *pkgfile* může být synchronizována pomocí:

```
# pkgfile -u

```

## Použití

Chcete-li hledat balíček, který je vlastníkem souboru `makepkg`:

 `$ pkgfile makepkg`  `core/pacman` 

Chcete-li zobrazit všechny soubory poskytnuté [archlinux-keyring](https://www.archlinux.org/packages/?name=archlinux-keyring):

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