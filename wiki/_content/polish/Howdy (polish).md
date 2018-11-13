[Howdy](https://github.com/boltgolt/howdy) jest programem imitującym Windows Hello na Linuxie. Używa czujniki podczerwieni komputera i kamery żeby zweryfikować twarz użytkownika.

## Contents

*   [1 Instalacja](#Instalacja)
*   [2 Konfiguracja](#Konfiguracja)
    *   [2.1 Ustaw Howdy żeby uruchamiać kiedy jest potrzebny](#Ustaw_Howdy_żeby_uruchamiać_kiedy_jest_potrzebny)
        *   [2.1.1 Przykład](#Przykład)
    *   [2.2 Dodaj poprawny czujnik podczerwieni](#Dodaj_poprawny_czujnik_podczerwieni)
    *   [2.3 Dodaj twarz do Howdy](#Dodaj_twarz_do_Howdy)
*   [3 Rozwiązywanie problemów](#Rozwiązywanie_problemów)
    *   [3.1 Wydaje się, że Howdy nie działa](#Wydaje_się,_że_Howdy_nie_działa)

## Instalacja

[Zainstaluj](/index.php/Zainstaluj "Zainstaluj") pakiet [howdy](https://aur.archlinux.org/packages/howdy/).

## Konfiguracja

### Ustaw Howdy żeby uruchamiać kiedy jest potrzebny

Aby Howdy mogł uwierzytelnić użytkownika, należy dodać niewielką zmianę do dowolnego pliku konfiguracyjnego [PAM](/index.php/PAM "PAM"), w którym może być użyta funkcja Howdy. W każdym pliku konfiguracyjnym należy dodać następujący wiersz:

```
auth sufficient pam_python.so /lib/security/howdy/pam.py

```

#### Przykład

 `/etc/pam.d/sudo` 
```
# PAM-1.0
auth    sufficient pam_python.so /lib/security/howdy/pam.py
auth    include    system-auth
account include    system-auth
session include    system-auth
```

### Dodaj poprawny czujnik podczerwieni

Określ poprawny plik `/dev/videoX` podłączony do czujnika podczerwieni. Można to zrobić za pomocą różnych programów, takich jak [cheese](https://www.archlinux.org/packages/?name=cheese) i [fswebcam](https://aur.archlinux.org/packages/fswebcam/). Po znalezieniu poprawnej nazwy pliku zedytuj plik `/lib/security/howdy/config.ini` za pomocą preferowanego edytora lub z `# howdy config`.

**Note:** [gedit](https://www.archlinux.org/packages/?name=gedit) musi być zainstalowane dla `howdy config`.

### Dodaj twarz do Howdy

Żeby dodać twarz do Howdy, uruchom:

```
# howdy add

```

## Rozwiązywanie problemów

### Wydaje się, że Howdy nie działa

Sprawdź, czy Howdy działa poprawnie, uruchamiając `howdy test` jako root. Jeśli to wydaje się działać, sprawdź wszystkie pliki konfiguracyjne PAM i sprawdź, czy działają. Niektóre programy, takie jak SDDM [[1]](https://github.com/sddm/sddm/issues/284), nie działają poprawnie z PAM, co może skutkować nieoczekiwanymi rezultatami.