**M**usic **O**n **C**onsole jest lekkim odtwarzaczem muzyki składającym się z dwóch części, z serwera (Moc) i z graficznego interfejsu (Mocp). Ogólnie jest podobny do [mpd](/index.php/Music_Player_Daemon_(Polski) "Music Player Daemon (Polski)"), ale w przeciwieństwie do _mpd_, Moc jest instalowany z razem ze standardowym interfejsem. Serwer Moc nie pozwala na zdalny dostęp.

## Contents

*   [1 Installacja](#Installacja)
*   [2 Konfiguracja](#Konfiguracja)
*   [3 Korzystanie](#Korzystanie)
*   [4 scroobler Last.fm](#scroobler_Last.fm)
    *   [4.1 mocp-scrobbler](#mocp-scrobbler)
*   [5 Alternatywne interfejsy](#Alternatywne_interfejsy)
*   [6 Plik usługi dla systemd](#Plik_us.C5.82ugi_dla_systemd)
*   [7 Rozwiązywanie problemów](#Rozwi.C4.85zywanie_problem.C3.B3w)
    *   [7.1 MOC nie uruchamia się](#MOC_nie_uruchamia_si.C4.99)
    *   [7.2 Dziwne znaki](#Dziwne_znaki)
    *   [7.3 FATAL_ERROR: Layout1 is malformed](#FATAL_ERROR:_Layout1_is_malformed)
*   [8 Zobacz także](#Zobacz_tak.C5.BCe)

## Installacja

Zainstaluj pakiet [moc](https://www.archlinux.org/packages/?name=moc) za pomocą Pacmana. Jeżeli chcesz, możesz zainstalować najnowsze wydanie rozwojowe za pomocą [moc-svn](https://aur.archlinux.org/packages/moc-svn/).

## Konfiguracja

Pakiet zawiera przykładowy plik konfiguracyjny znajdujący się w położeniu `/usr/share/doc/moc/config.example`. By skonfigurować _moc_, skopiuj ten plik do `~/.moc/config` i wyedytuj stosownie do swoich potrzeb.

By uzyskać instrukcje dotyczące konfiguracji i skrótów klawiszowych, przeczytaj `/usr/share/doc/moc/keymap.example`.

Jeżeli chcesz używać _Moc_ z serwerem dziwięku [OSS](/index.php?title=OSS_(Polski)&action=edit&redlink=1 "OSS (Polski) (page does not exist)") v4.1, sprawdź [OSS#MOC](/index.php/OSS#MOC "OSS").

## Korzystanie

Uruchom _moc_ za pomocą komendy:

```
$ mocp

```

Ta komenda uruchomi interfejs i serwer jednocześnie. Poniżej znajduje się lista dostępnych skrótów klawiszowych (wielkość znaków ma znaczenie):

| Uruchom odtwarzanie | `Enter` |
| Pauza | `Space` or `p` |
| Odtwórz następny utwór | `n` |
| Otwórz poprzedni utwór | `b` |
| Przestaw z przeglądania listy odtwarzania do
przeglądania plików (i odwrotnie) | `Tab` |
| Dodaj jeden utwór do listy odtwarzania | `a` |
| Skasuj utwór z listy odtwarzania | `d` |
| Dodaj cały folder do listy odtwarzania (z podfolderami) | `Shift+a` |
| Wyczyść listę odtwarzania | `Shift+c` |
| Podgłoś o 5% | `.` (kropka) |
| Przycisz o 5% | `,` (przecinek) |
| Podgłoś o 1% | `>` |
| Przycisz o 1% | `<` |
| Ustaw głośność na 10% | `meta+1` |
| Ustaw głośność na 20% | `meta+2` |
| Zamknij otwarzacz | `q` |

**Note:** By wyłączyć serwer _moc_, użyj `Shift+q` lub:

```
$ mocp -x

```

## scroobler Last.fm

### mocp-scrobbler

[mocp-scrobbler](https://aur.archlinux.org/packages/mocp-scrobbler/) jest scrooblerem Last.fm/Libre.fm dla MOC ze wsparciem dla powiadomień o odtwarzanych utworach, działania w tle i pamięci podręcznej. Do działania wymaga jedynie [Pythona](/index.php/Python "Python") 3.

Skopiuj przykładowy plik konfiguracyjny do swojego katalogu domowego:

```
mkdir ~/.mocpscrob/
cp /usr/share/doc/mocp-scrobbler/config.example  ~/.mocpscrob/config

```

I wyedytuj `~/.mocpscrob/config` aby dodać swój login i hasło. zmienna `password` może być zastąpiona zmienną `password_md5` przy pierwszym uruchomieniu. Jej pierwotna wartość zostanie wtedy zastąpiona hashem md5\. Jeżeli chcesz zmienić hasło, po prostu dodaj hasło jeszcze raz, i zmienna `password_md5` zostanie nadpisana. Aby scrooblować utwory, uruchom _mocp-scrobbler_ w tle przed _mocp_. Możesz także użyć [aliasu](/index.php/Alias "Alias"):

```
alias mocp='/usr/bin/mocp-scrobbler.py -d; mocp'

```

## Alternatywne interfejsy

*   **dmenu_mocp** — Interfejs Dmenu dla MOC

	[https://github.com/mutantturkey/mocicon](https://github.com/mutantturkey/mocicon) || [dmenu_mocp](https://aur.archlinux.org/packages/dmenu_mocp/)

*   **mocicon** — Aplet dla paneli napisany w GTK

	[http://mocicon.sourceforge.net/](http://mocicon.sourceforge.net/) || [mocicon](https://aur.archlinux.org/packages/mocicon/)

*   **moc-tray** — Szybki i prosty dostęp do podstawowych funkcji moc w zasobniku.

	[https://code.google.com/p/moc-tray/](https://code.google.com/p/moc-tray/) || [moc-tray](https://www.archlinux.org/packages/?name=moc-tray)

*   **eXo** — Interfejs dla MOC napisany w QT, wspiera scroobling.

	[https://bitbucket.org/blaze/exo/](https://bitbucket.org/blaze/exo/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/?K=exo)</small>

## Plik usługi dla systemd

 `/etc/systemd/system/moc@.service` 

```
[Unit]
Description=MOC server
ConditionPathExists=/usr/bin/mocp
After=network.target sound.target

[Service]
RemainAfterExit=yes
User=%I
ExecStart=/usr/bin/mocp -S
ExecStop=/usr/bin/mocp -x
WorkingDirectory=/home/%I/

[Install]
WantedBy=multi-user.target

```

[Uruchom](/index.php/Enable "Enable") tą usługę dla odpowiednich użytkowników

## Rozwiązywanie problemów

### MOC nie uruchamia się

Jeżeli MOC nie chce się uruchomić, jest to najprawdopodobniej wina błędnej konfiguracji jednego z plików w `~/.moc/`. Możesz spróbować naprawić błąd, lub w ostateczności wykasować cały folder.

### Dziwne znaki

Jeżeli widzisz jakieś dziwne znaczki w _moc_ zamiast normalnych linii (Pionowe linie do rozdzielenia przestrzeni, itp.), możesz mieć czcionki niekompatybilne z MOC. Zmień je na poprawnie wyświetlające linie,lub zmodyfikuj plik `.moc/config` by używać znaków ASCII do rysowania linii:

```
ASCIILines = no

```

### FATAL_ERROR: Layout1 is malformed

Jeżeli MOC wykracza się z takim błędem, spróbuj dodać linię do: `.moc/config`:

```
Layout1 = directory(0,0,50%,100%): playlist(50%,0,100%,100%)

```

lub

```
Layout1 = directory(0,0,50%,100%): playlist(50%,0,FILL,100%)

```

Sprawdź [oryginalny raport błędu](http://moc.daper.net/node/262) i [Raport zgłoszony na Debian Bugs](https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=485059).

## Zobacz także

*   [Oficjalna Dokumentacja](http://moc.daper.net/documentation)