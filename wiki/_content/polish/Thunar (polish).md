## Contents

*   [1 Wstęp](#Wstęp)
*   [2 Instalacja](#Instalacja)
*   [3 Informacje końcowe](#Informacje_końcowe)
*   [4 Zobacz również](#Zobacz_również)

## Wstęp

Thunar - menedżer plików stworzony przez Benedikta Meurera. Thunar jest podobny do Nautilusa - menadżera plików z GNOME. Głównym założeniem projektu jest łatwość obsługi. W założeniach twórców Thunar ma być menedżerem "lekkim" (nie wymagającym dużych zasobów systemowych) i szybkim. Można rozszerzać jego możliwości za pomocą wtyczek. Użytkownik ma także możliwość dodawania konfigurowalnych "akcji", dostępnych poprzez menu kontekstowe.

## Instalacja

```
# pacman -Sy thunar

```

Dodatkowe wtyczki i rozszerzenia:

```
# pacman -S thunar-volman thunar-thumbnailers ffmpegthumbnailer thunar-archive-plugin thunar-media-tags-plugin

```

Thunar wymaga zainstalowanych i uruchomionych `dbus` i `hal`:

```
# pacman -S dbus hal

```

Dodajemy odpowiednie wpisy do sekcji DAEMONS w pliku `/etc/rc.conf`:

 `/etc/rc.conf`  `DAEMONS=(... hal ...)` 

Następnie uruchamiamy `dbus` i `hal`:

```
# /etc/rc.d/hal start

```

Nie zapomnijmy dodać użytkownika do odpowiednich grup:

```
# gpasswd -a nazwa_użytkownika hal
# gpasswd -a nazwa_użytkownika dbus
# gpasswd -a nazwa_użytkownika optical
# gpasswd -a nazwa_użytkownika storage

```

## Informacje końcowe

Aby dowiedzieć się więcej o tym menedżerze, przejdź do angielskojęzycznego artykułu [Thunar](/index.php/Thunar "Thunar").

## Zobacz również

*   [Strona projektu](http://thunar.xfce.org/index.html)