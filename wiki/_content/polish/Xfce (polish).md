<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Wstęp](#Wstęp)
*   [2 Instalacja](#Instalacja)
*   [3 Uruchomienie](#Uruchomienie)
*   [4 Konfiguracja](#Konfiguracja)
*   [5 Informacje końcowe](#Informacje_końcowe)

## Wstęp

Xfce - środowisko graficzne dla systemów uniksowych, wzorowane na CDE. Pierwotnie, Xfce bazowało na XForms, jednakże po przepisaniu kodu źródłowego środowisko przestało bazować na tej bibliotece na rzecz GTK+.

Wszystkie pliki konfiguracyjne są napisane w XML-u, co ułatwia głębokie zmiany w środowisku. Z założenia ma być ono proste w obsłudze, ładne i szybkie. Xfce jest złożone z wielu modułów, między innymi z menedżera okien Xfwm i menedżera plików Thunar, które w połączeniu oferują w pełni funkcjonalne środowisko. Xfce może też korzystać z modułów innych środowisk graficznych zamiast swoich własnych.

## Instalacja

Aby zainstalować środowisko graficzne Xfce wydajemy polecenie:

```
# pacman -S xfce4 

```

Jeśli chcesz zainstalować dodatki:

```
# pacman -S xfce4-goodies

```

Zalecane jest zainstalowanie obserwatora plików oraz GStreamer :

```
# pacman -S gamin gstreamer0.10-base-plugins

```

## Uruchomienie

Dodajemy odpowieni wpis do `~/.xinitrc`:

 `~/.xinitrc`  `exec startxfce4` 

Jeżeli zainstalowany jest HAL:

 `~/.xinitrc`  `exec startxfce4` 

Samo środowisko uruchomimy odpowiednio:

```
$ xinit /usr/bin/startxfce4

```

## Konfiguracja

*   Na początek trzeba pamiętać o zainstalowaniu `hal` i `dbus`, oraz dodaniu ich do `/etc/rc.conf`:

```
# pacman -S hal dbus

```

*   Musimy także dodać użytkownika do grupy `power`:

```
# gpasswd -a nazwa_użytkownika power

```

## Informacje końcowe

Aby dowiedzieć się więcej o tym środowisku, przejdź do angielskojęzycznego artykułu [Xfce](/index.php/Xfce "Xfce").