Related articles

*   [Desktop Notifications (Polski)](/index.php?title=Desktop_Notifications_(Polski)&action=edit&redlink=1 "Desktop Notifications (Polski) (page does not exist)")

[Dunst](https://dunst-project.org/) jest lekkim zamiennikiem dla notification-daemons dostarczanym przez większość środowisk graficznych.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalacja](#Instalacja)
*   [2 Wygląd](#Wygląd)
    *   [2.1 Paczki ikon](#Paczki_ikon)
*   [3 Skróty klawiszowe](#Skróty_klawiszowe)
*   [4 Skryptowanie](#Skryptowanie)
*   [5 Naprawianie problemów](#Naprawianie_problemów)

## Instalacja

[Zainstaluj](/index.php/Zainstaluj "Zainstaluj") pakiet [dunst](https://www.archlinux.org/packages/?name=dunst). Nie ma potrzeby żeby startować lub uruchamiać dunst; jest automatycznie uruchamiany przez systemd kiedy programy wysyłają powiadomienia programy przez dbus.

Przykładowy plik konfiguracyjny można znaleść w `/usr/share/dunst/dunstrc`. Skopiuj ten plik do `~/.config/dunst/dunstrc` i zedytuj go do swoich potrzeb.

## Wygląd

Dunst pozwala na używanie markapu htmla w powiadomieniach. Niektórymi przykładami jest pogrubienie, kursywa, przekreślenie i podkreślenie. Dla pełnego odniesienia zobacz [[1]](https://developer.gnome.org/pango/stable/PangoMarkupFormat.html). HTML może być usunięty z powiadomień jeżeli `markup` jest ustawiony na `none`.

The formatting of the notification can be specified. Options are as follows:

```
%a  appname
%s  summary
%b  body
%i  iconname (including its path)
%I  iconname (without its path)
%p  progress value if set ([  0%] to [100%]) or nothing

```

These can be used in conjunction with HTML markup. For example the `format` can be set to `<b>%s</b>
%b` for a bolded notification summary, a newline and the body unformatted.

### Paczki ikon

Ikony są ustawione w opcji `icon_path`. Ikony statusów i urządzeń są potrzebne. Domyślnie Dunst szuka ikon [gnome-icon-theme](https://www.archlinux.org/packages/?name=gnome-icon-theme). Dla przykładu żeby użyć [adwaita-icon-theme](https://www.archlinux.org/packages/?name=adwaita-icon-theme) (sukcesor gnome-icon-theme), użyj wzamian:

```
icon_path = /usr/share/icons/Adwaita/16x16/status/:/usr/share/icons/Adwaita/16x16/devices/

```

## Skróty klawiszowe

Można ustawić progi nieaktywności, aby powiadomienie pozostało na ekranie, jeśli użytkownik jest nieaktywny dłużej niż ten próg.

Żeby zamknąć zanim czas upłynie użyj `Control+Space`. Jeżeli kilka powiadomień jest na ekranie `Control+Shift+Spacja` zamknie je wszystkie.

**Tip:** Komendy dla wyłączania i pokazywania spowrotem mogą być zmienione. Jeżeli używamy symbol, on musi być wypisany jak np, `period` dla kropki.

List historii może być sprawdzona używając `Control+Grawis` (grawis oznacza ```). Menu kontekstowe może być otwarte używając `Control+Shift+Kropka`. Menu kontekstowe używa dmenu żeby odfiltrować URLe i otworzyć je w twojej przeglądarce. Domyślna przeglądarka może być ustawiona w pliku konfiguracyjnym w ten sposób:

```
browser = /usr/bin/chromium 

```

## Skryptowanie

Dunst może być skonfigurowany żeby uruchamiać skrypty bazując na treści powiadomienia. Tu jest przykład używając dunsta żeby uruchomić skrypt kiedy [pidgin](https://www.archlinux.org/packages/?name=pidgin) wysyła wiadomość:

```
[signed_on]
   appname = Pidgin
   summary = "*signed on*"
   urgency = low
   script = do_something.sh

```

## Naprawianie problemów

Kiedy używamy dunsta bez menadżera wyświetlania, wartość środowiska `DISPLAY` może być nie ustawiona poprawnie.[[2]](https://github.com/dunst-project/dunst/issues/347)

Żeby to naprawić, dodaj poniższą rzecz do swojego `.xinitrc`

```
systemctl --user import-environment DISPLAY

```