## Czym jest AUR?

ArchLinux User Community Repository (AUR) - po polsku oznacza repozytorium społeczności użytkowników Arch Linuksa. Jest zbiorem [PKGBUILDów](/index.php/PKGBUILD_(Polski) "PKGBUILD (Polski)") pisanych przez użytkowników Arch Linuksa. Mówiąc prostym językiem, AUR to pakiety, których nie dołączono jeszcze do oficjalnego repozytorium [community], a do tego kandydują. Użytkownicy głosują na poszczególne pakiety, które po osiągnięciu pozytywnej opinii społeczności trafiają do zbioru pakietów oficjalnych.

## Jak zacząć korzystanie z AUR?

Jeżeli zamierzasz korzystać z pakietów z AUR, zainstaluj grupę `base-devel`:

```
# pacman -S base-devel

```

Aby zainstalować pakiet z AUR, należy go pobrać, rozpakować, skompilować i zainstalować. Robią to poniższe komendy:

```
wget [https://aur.archlinux.org/packages/nazwa_pakietu/nazwa_pakietu.tar.gz](https://aur.archlinux.org/packages/nazwa_pakietu/nazwa_pakietu.tar.gz)
tar zxvf nazwa_pakietu.tar.gz
cd nazwa_pakietu
makepkg -sri

```

[makepkg -sri](/index.php?title=Makepkg_(Polski)&action=edit&redlink=1 "Makepkg (Polski) (page does not exist)") spowoduje ściągnięcie kodu, rozwiązanie zależności przy pomocy [pacman](/index.php/Pacman_(Polski) "Pacman (Polski)"), skompilowanie i zapakowanie go, zainstalowanie paczki. Na samym końcu usuwane są zależności, które były potrzebne tylko na czas instalacji.

Jeśli znasz już zasadę budowania pakietów, możesz zainstalować [program](/index.php/Pacman_(Polski)#Nak.C5.82adki_na_Pacmana "Pacman (Polski)"), który wykona część niezbędnej pracy.

Sporą listę narzędzi wspomagających pracę z pakietami z AUR znajdziesz w angielskojęzycznym artykule [AUR helpers](/index.php/AUR_helpers "AUR helpers").

## Czym różni się ABS od AUR?

[Arch Build System](/index.php/Arch_Build_System_(Polski) "Arch Build System (Polski)") zawiera paczki stworzone wyłącznie przez developerów. Założeniem AUR jest korzystanie tylko z PKGBUILDów stworzonych przez zwykłych użytkowników, członków społeczności. Nie ma się jednak czego bać. Paczki, nawet gdy zdobędą dużą ilości głosów, są jeszcze dodatkowo sprawdzane przez tzw. Trusted Usera (TU).