**Daemon** (pl. **Demon**) jest programem działającym w tle, który czeka na wykonanie jakiegoś zadania oraz oferuje usługi. Dobrym przykładem jest serwer WWW, który czeka na zapytania by wyświetlić stronę lub serwer ssh oczekujący kogoś, kto będzie się chciał zalogować. Chociaż są to w pełni funkcjonalne aplikacje, będąc demonami ich praca nie jest tak widoczna. To demony prowadzą logi twojego systemu (np. syslog, metalog) czy zmniejszają taktowanie procesora, gdy system nie jest obciążony.

## Contents

*   [1 Uruchamianie na starcie systemu](#Uruchamianie_na_starcie_systemu)
*   [2 Ręczne zarządzanie demonami](#R.C4.99czne_zarz.C4.85dzanie_demonami)
*   [3 Podstawy](#Podstawy)
*   [4 Start demonów w tle](#Start_demon.C3.B3w_w_tle)
*   [5 GUI dla menadżera daemonów w ArchLinux](#GUI_dla_menad.C5.BCera_daemon.C3.B3w_w_ArchLinux)
*   [6 Lista popularnych daemonów](#Lista_popularnych_daemon.C3.B3w)

## Uruchamianie na starcie systemu

Domyślna instalacja Arch Linux zostawia kilka usług (lub demonów) włączanych w czasie bootowania. Możesz dodawać lub usuwać usługi przez edycję listy DAEMONS w swoim pliku [rc.conf](/index.php/Rc.conf "Rc.conf"). Na początku będzie wyglądała tak:

```
DAEMONS=(syslog-ng network netfs crond)

```

Będą uruchamiane w kolejności jakiej są na liście. Możesz któryś wyłączyć nie usuwając go z listy poprzez dodanie na jego początku wykrzyknika (!). Możesz także uruchomić go w tle. Dodaj tylko małpę (@) przed nazwą demona.

## Ręczne zarządzanie demonami

Możesz zobaczyć jaka usługa ma swój skrypt startowy przeglądając katalog /etc/rc.d/. Możesz także ręcznie uruchomić, zatrzymać, albo zrestartować każdy demon poleceniem

```
/etc/rc.d/*nazwa_daemona* {start|stop|restart}

```

Demony mogą oferować również inne polecenia. Po listę dostępnych komend odsyłam do dokumentacji.

## Podstawy

Nie ma potrzeby dodawania innych usług do DAEMONSów, jeśli nie czujesz takiej potrzeby. Jednakże zwykły użytkownik desktopa doda przynajmniej [CUPS](/index.php/CUPS "CUPS") i [HAL](/index.php/HAL "HAL"). Jeśli zainstalujesz nowe usługi, będziesz musiał dodać je ręcznie do listy DAEMONS w pliku /etc/rc.conf. (Lista DAEMONS zazwyczaj znajduje się w ostatniej linijce pliku rc.conf.)

**Note:** Some services will start other services. For example, HAL will automatically start [D-Bus](/index.php/D-Bus "D-Bus") and [Acpid](/index.php/Acpid "Acpid"). Keep in mind, as it has been mentioned elsewhere, that HAL would sometimes fail to automatically start D-Bus, without the user's awareness. It is considered good practice to add D-Bus explicitly before HAL and not to "background" it. This will let the user know during bootup if it fails to start, before other services dependent on D-Bus break.

## Start demonów w tle

Jest to przydatne jeśli chcesz uruchamiać kolejną usługę z listy przed startem poprzedniej. Od ciebie zależy, które usługi mają uruchamiać się w tle. Nie startuj w tle wszystkiego, co będzie natychmiast potrzebne, np. do uruchomienia kolenych demonów z listy. Tutaj mamy przykład:

```
DAEMONS=(syslog-ng gensplash network netfs dbus hal @avahi-daemon @samba @crond @openntpd @cups @mpd)

```

Odpalając *openntpd* w tle może prowadzić do błędów w synchronizacji między aktualnym czasem a zapisanym na komputerze. Jeśli zauważyłeś sporą różnicę czasów, spróbuj uruchomić *openntpd* w trybie normalnym (nie w tle).

## GUI dla menadżera daemonów w ArchLinux

Istnieje możliwość instalacji [ArchLinux Daemon Manager](http://img130.imageshack.us/img130/4200/aldmgui03.png) z [AUR](https://aur.archlinux.org/packages.php?ID=29606). Program pozwala na łatwiejszą zmianę ustawień w /etc/rc.conf używając aplikacji GTK "aldm-gui" lub z wprowadzać zmiany z linii komend "aldm".

## Lista popularnych daemonów

| **Daemon** | **Opis** |
| [alsa](/index.php/Alsa "Alsa") | Advanced Linux Sound Architecture; udostępnia sterowniki dla kart dźwiękowych. |
| [avahi-daemon](/index.php/Avahi "Avahi") |
| [avahi-dnsconfd](/index.php/Avahi "Avahi") |
| crond | Uruchamia zadania o określonym czasie. |
| [cups](/index.php/CUPS "CUPS") | Powszechny Uniksowy system drukowania. |
| [dbus](/index.php/D-Bus "D-Bus") | Prosty system komunikacji międzyprocesowej dla aplikacji softwarowych. |
| [fam](/index.php/FAM "FAM") | Monitor zmian na plikach. |
| gensplash |
| [hal](/index.php/HAL "HAL") | Warstwa abstrakcji sprzętowej. |
| [mpd](/index.php/MPD "MPD") | Demon odtwarzacza muzyki. |
| [mysqld](/index.php/MySQL "MySQL") | Serwer bazy daanych MySQL. |
| netfs | Montuje sieciowe systemy plików. |
| network |
| networkmanager |
| [ntpd](/index.php/NTPD "NTPD") | Usługa udostępniająca protokół synchronizacji czasu (klient i serwer). |
| [openntpd](/index.php/OpenNTP "OpenNTP") | Alternatywa dla NTPD (klient i serwer). |
| [pure-ftpd](/index.php?title=Pure-FTPD&action=edit&redlink=1 "Pure-FTPD (page does not exist)") | Serwer FTP. |
| [rsyslogd](/index.php/Rsyslog "Rsyslog") | Najnowsza wersja programu prowadzącego logi systemowe. |
| [samba](/index.php/Samba "Samba") | System udostępniania plików i drukarek dla klientów sieci Microsoft Windows (SMB). |
| sensors | Monitoring sprzętu (temperatury, wiatraki itd.). |
| [sshd](/index.php/OpenSSH "OpenSSH") | System komunikacji OpenSSH. |
| stbd | Demon, który był w starszych wersjach wymagany przez gnome-system-tools. Nikt nie wie do czego służy, ale na szczęście od wersji gnome-tools 2.28 nie jest dłużej wymagany. |
| syslogd | Jest to starszy i podstawowy system logujący. |
| [syslog-ng](/index.php/Syslog-ng "Syslog-ng") | Logger systemowy nowej generacji. Domyślnie zainstalowany w systemie. |
| [vsftpd](/index.php/Vsftpd "Vsftpd") | Kolejny serwer FTP. |