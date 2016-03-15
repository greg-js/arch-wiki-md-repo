Za [listą dyskusyjną systemd](http://lists.freedesktop.org/archives/systemd-devel/2014-May/019537.html):

	*systemd-timesyncd* jest usługą, która została dodana by synchronizować czas między komputerami w sieci. Implementuje klienta SNTP. W porównaniu do usług takich jak chrony lub serwer NTP, jest jedynie klientem i nie zawiera w sobie całej złożoności protokołu NTP, skupia się jedynie na pobieraniu i ustawianiu zegara. Jeżeli nie zamierzasz serwować do sieci czasu ze swojego lokalnego zegara, powinien być więcej niż wystarczający. Usługa uruchamiana jest z minimalnymi uprawnieniami i została powiązana z networkd aby działać tylko gdy jest dostępny internet. Usługa zapisuje stan zegara na dysk zanim ustawi korektę, w ten sposób ustala o ile przesuwać zegar na bardzo wczesnym etapie startu systemu tak aby urządzenia bez lub ze słabym RTC postępowały operując na w miarę właściwie ustawionym zegarze. Aby użyć tej usługi, grupa i użytkownik "systemd-timesync" muszą być utworzone.

**Note:** Przekłąd a oryginalny tekst, mogą się nieznacznie różnić.

## Instalacja

Usługa *systemd-timesyncd* dostarczona jest wraz z [systemd](https://www.archlinux.org/packages/?name=systemd) >= 213\. Aby [uruchomić i włączyć](/index.php/Systemd#Basic_systemctl_usage "Systemd"):

```
# timedatectl set-ntp true 

```

**Tip:** Przed systemd w wersji 216 *systemd-timesyncd* do uruchomienia wymagał [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd"), obecnie potrafi również współpracować z [dhcpcd](/index.php/Dhcpcd "Dhcpcd") i [NetworkManager](/index.php/NetworkManager "NetworkManager"), lecz dalej polega na zewnętrznych narzędziach.

## Konfiguracja

Przy uruchamianiu *systemd-timesyncd* wczyta plik `/etc/systemd/timesyncd.conf`. Począwszy od [systemd](/index.php/Systemd "Systemd") 217 wygląda on tak:

 `/etc/systemd/timesyncd.conf` 
```
[Time]
#NTP=
#FallbackNTP=0.arch.pool.ntp.org 1.arch.pool.ntp.org 2.arch.pool.ntp.org 3.arch.pool.ntp.org
```

Aby dodać lub zmienić [serwery czasu](/index.php/Network_Time_Protocol_daemon#Configuring_connection_to_NTP_servers "Network Time Protocol daemon"), odkomentuj linie odnoszące się do nich. Każdy adres serwera rozdzielony jest spacją, listę dostępnych serwerów otrzymasz na [stronie basenu projektu NTP](http://www.pool.ntp.org/) lub [te domyślne Archa](https://projects.archlinux.org/svntogit/packages.git/commit/trunk?h=packages/ntp&id=1b485f87c9e1384eaf069d031e415515e8ead92d) (również dostarczane przez serwery basenu NTP).

 `/etc/systemd/timesyncd.conf` 
```
[Time]
NTP=0.arch.pool.ntp.org 1.arch.pool.ntp.org 2.arch.pool.ntp.org 3.arch.pool.ntp.org
FallbackNTP=0.pool.ntp.org 1.pool.ntp.org 0.fr.pool.ntp.org
```

Od wersji 216 można również dodawać serwery za pomocą `NTP=` bezpośrednio w plikach konfiguracyjnych [systemd-networkd](/index.php/Systemd-networkd#.5BNetwork.5D_section "Systemd-networkd").

Reguły kolejności użycia serwerów NTP:

*   Z plików konfiguracyjnych per-interfejs `systemd-networkd.service(8)`.
*   Serwery z pliku `/etc/systemd/timesyncd.conf` będą dołączone jako kolejne.
*   Jeżeli serwery nie będą odpowiadać, użyte zostaną kolejne zdefiniowane w `FallbackNTP=`.

## Zobacz takze

*   [Forum: systemd-timesyncd is not syncing time](https://bbs.archlinux.org/viewtopic.php?id=182600)
*   [Forum: Using systemd-timesync instead of NTP](https://bbs.archlinux.org/viewtopic.php?id=182172)