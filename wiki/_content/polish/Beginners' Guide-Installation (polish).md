**Tip:** To część wielostronicowego artykułu Przewodnik Początkującego. **[Kliknij tutaj](/index.php/Beginners%27_guide_(Polski) "Beginners' guide (Polski)")** jeśli wolisz czytać przewodnik w całości.

## Contents

*   [1 Instalacja](#Instalacja)
    *   [1.1 Zmiana języka](#Zmiana_j.C4.99zyka)
    *   [1.2 Konfiguracja sieci w środowisku instalacyjnym](#Konfiguracja_sieci_w_.C5.9Brodowisku_instalacyjnym)
        *   [1.2.1 Automatyczna konfiguracja](#Automatyczna_konfiguracja)
        *   [1.2.2 Ustawienie połączenia przewodowego](#Ustawienie_po.C5.82.C4.85czenia_przewodowego)
            *   [1.2.2.1 Dynamiczne IP (DHCP)](#Dynamiczne_IP_.28DHCP.29)
            *   [1.2.2.2 Statyczne IP](#Statyczne_IP)
        *   [1.2.3 Konfiguracja sieci bezprzewodowej](#Konfiguracja_sieci_bezprzewodowej)
        *   [1.2.4 Skonfiguruj połączenie bezpośrednie z modemem](#Skonfiguruj_po.C5.82.C4.85czenie_bezpo.C5.9Brednie_z_modemem)
            *   [1.2.4.1 xDSL (PPPoE)](#xDSL_.28PPPoE.29)
            *   [1.2.4.2 Modem analogowy, ISDN](#Modem_analogowy.2C_ISDN)
        *   [1.2.5 Proxy Server](#Proxy_Server)
        *   [1.2.6 Przetestuj połączenie](#Przetestuj_po.C5.82.C4.85czenie)
    *   [1.3 Przygotowanie dysku twardego](#Przygotowanie_dysku_twardego)
        *   [1.3.1 Manualne partycjonowanie dysku twardego](#Manualne_partycjonowanie_dysku_twardego)
    *   [1.4 Konfiguracja urządzeń blokowych, systemów plików i punktów montowania](#Konfiguracja_urz.C4.85dze.C5.84_blokowych.2C_system.C3.B3w_plik.C3.B3w_i_punkt.C3.B3w_montowania)
    *   [1.5 Montowanie partycji](#Montowanie_partycji)
    *   [1.6 Wybierz serwer instalacyjny](#Wybierz_serwer_instalacyjny)
    *   [1.7 Instalacja bazowego systemu](#Instalacja_bazowego_systemu)
    *   [1.8 Generacja fstab](#Generacja_fstab)
    *   [1.9 Chroot do systemu](#Chroot_do_systemu)
    *   [1.10 Konfiguracja systemu](#Konfiguracja_systemu)
        *   [1.10.1 Nazwa hosta](#Nazwa_hosta)
        *   [1.10.2 Font terminala i układ klawiatury](#Font_terminala_i_uk.C5.82ad_klawiatury)
        *   [1.10.3 Strefa czasowa](#Strefa_czasowa)
        *   [1.10.4 Ustawienia regionalne](#Ustawienia_regionalne)
            *   [1.10.4.1 Wybranie regionu (locale)](#Wybranie_regionu_.28locale.29)
            *   [1.10.4.2 Ustawianie systemowego locale](#Ustawianie_systemowego_locale)
        *   [1.10.5 Czas zegara sprzętowego](#Czas_zegara_sprz.C4.99towego)
            *   [1.10.5.1 Ustawienie czasu przy jednoczesnym uruchamianiu Windowsa](#Ustawienie_czasu_przy_jednoczesnym_uruchamianiu_Windowsa)
        *   [1.10.6 Moduły jądra](#Modu.C5.82y_j.C4.85dra)
    *   [1.11 Konfiguracja sieci](#Konfiguracja_sieci)
        *   [1.11.1 Sieć przewodowa](#Sie.C4.87_przewodowa)
            *   [1.11.1.1 Dynamiczne IP (DHCP)](#Dynamiczne_IP_.28DHCP.29_2)
            *   [1.11.1.2 Statyczne IP](#Statyczne_IP_2)
        *   [1.11.2 Sieć bezprzewodowa](#Sie.C4.87_bezprzewodowa)
        *   [1.11.3 Połączenie bezpośrednie z modemem](#Po.C5.82.C4.85czenie_bezpo.C5.9Brednie_z_modemem)
    *   [1.12 Stwórz początkowy ramdysk](#Stw.C3.B3rz_pocz.C4.85tkowy_ramdysk)
    *   [1.13 Instalacja i konfiguracja bootloadera](#Instalacja_i_konfiguracja_bootloadera)
        *   [1.13.1 Dla płyt głównych z BIOS](#Dla_p.C5.82yt_g.C5.82.C3.B3wnych_z_BIOS)
            *   [1.13.1.1 Syslinux](#Syslinux)
            *   [1.13.1.2 GRUB](#GRUB)
        *   [1.13.2 Dla płyt głównych z UEFI](#Dla_p.C5.82yt_g.C5.82.C3.B3wnych_z_UEFI)
            *   [1.13.2.1 EFISTUB](#EFISTUB)
            *   [1.13.2.2 GRUB](#GRUB_2)
    *   [1.14 Hasło roota](#Has.C5.82o_roota)
    *   [1.15 Odmontowanie partycji i ponowne uruchomienie](#Odmontowanie_partycji_i_ponowne_uruchomienie)

## Instalacja

Po uruchomieniu, nośnik instalacyjny automatycznie loguje się jako **root** i ustawia amerykański (US) układ klawiatury.

### Zmiana języka

**Tip:** Te kroki są opcjonalne dla większości użytkowników. Mogą być jednak przydatne, gdy planujesz pisać w plikach konfiguracyjnych z wykorzystaniem swojego języka, jeżeli Twoje hasło do sieci wifi zawiera znaki niewystępujące w języku angielskim, lub jeżeli chcesz otrzymywać wiadomości systemowe (np. możliwe błędy) w swoim ojczystym języku.

Domyślnie wybranym układem klawiatury jest `us`. Jeżeli posiadasz klawiaturę z niestandardowym układem klawiszy, uruchom polecenie:

```
# loadkeys *układ*

```

...gdzie w miejsce *układu* można wstawić `fr`, `uk`, `be-latin1`, etc. "zajrzyj [tutaj](/index.php/KEYMAP#Keyboard_layouts_.28Polski.29 "KEYMAP"), by zobaczyć pełną listę.

Mapy klawiszy są dostępne dla wielu krajów i typów klawiatur. Pliki map klawiszy znajdują się w `/usr/share/kbd/keymaps/` (możesz opuścić scieżkę i rozszerzenie pliku używając `loadkeys`).

Czcionka również powinna zostać zmieniona, bo w większości języków używane jest więcej niż standardowe 26 liter obecnych w [angielskim alfabecie](https://en.wikipedia.org/wiki/English_alphabet "wikipedia:English alphabet"). W przeciwnym wypadku niektóre charakterystyczne znaki mogą zostać zastąpione przez białe kwadraciki lub inne symbole. Zauważ, że nazwa układu jest czuła na wielkość liter, więc wpisz *dokładnie* to, co widzisz:

```
# setfont Lat2-Terminus16

```

Domyślnie wybranym językiem jest angielski (US). Jeżeli chcesz zmienić język na czas procesu instalacji *(w tym przykładzie na polski)*, usuń znak `#` na początku [locale](http://www.greendesktiny.com/support/knowledgebase_detail.php?ref=EUH-483), którego chcesz używać z `/etc/locale.gen`, razem z językiem angielskim (US). Proszę wybierz wpisy `UTF-8`.

Użyj `Ctrl+X` by wyjść, a gdy zostaniesz zapytany o zachowanie zmian, naciśnij `Y` i `Enter`, by użyć tej samej nazwy pliku.

 `# nano /etc/locale.gen` 
```
en_US.UTF-8 UTF-8
pl_PL.UTF-8 UTF-8
```

```
# locale-gen
# export LANG=pl_PL.UTF-8

```

Pamiętaj, `LAlt+LShift` aktywuje i dezaktywuje mapę klawiszy.

### Konfiguracja sieci w środowisku instalacyjnym

Instalator wymaga połączenia sieciowego, aby pobrać i zainstalować wymagane pakiety. Sieć musi być więc skonfigurowana jako pierwsza.

#### Automatyczna konfiguracja

**Warning:** udev podczas nadawania nazw interfejsom sieciowym nie trzyma się już nazewnictwa zgodnego ze schematem wlanX i ethX. Jeżeli używałeś wcześniej innej dystrybucji albo instalujesz ponownie system Arch, miej na uwadze nowe nazewnictwo i nie zakładaj, że Twój interface sieci bezprzewodowej nazywa się wlan0, albo że interface sieci przewodowej nosi nazwę eth0\. Zawsze możesz użyć narzędzia "ip", by upewnić się co do nazw Twoich interface-ów.

Od wydania systemd-197 wzwyż, udev przyporządkowuje przewidywalne, stałe nazw interfejsów sieciowych, które różnią się od starego podejścia do ich nazewnictwa (wlan0, wlan1, etc.). Nowe nazwy nie zmieniają się po ponownym uruchomieniu systemu, co rozwiązuje problem nieprzewidywalności przydzielania im nazw. Jeżeli chcesz dowiedzieć się, dlaczego było to konieczne, przeczytaj [http://www.freedesktop.org/wiki/Software/systemd/PredictableNetworkInterfaceNames](http://www.freedesktop.org/wiki/Software/systemd/PredictableNetworkInterfaceNames) .

Usługa `dhcpcd` jest uruchamiana podczas startu systemu. Spróbuje ona automatycznie skonfigurować połączenie przewodowe, jeśli są dostępne. Możesz sprawdzić, czy połączenie powiodło się używając `/bin/ping`:

```
# ping -c 3 www.google.com

```

Jeśli wynik polecenia wygląda podobnie do tego:

 `# ping -c 3 www.google.com` 
```
PING www.l.google.com (74.125.132.105) 56(84) bytes of data.
64 bytes from wb-in-f105.1e100.net (74.125.132.105): icmp_req=1 ttl=50 time=17.0 ms
64 bytes from wb-in-f105.1e100.net (74.125.132.105): icmp_req=2 ttl=50 time=18.2 ms
64 bytes from wb-in-f105.1e100.net (74.125.132.105): icmp_req=3 ttl=50 time=16.6 ms

--- www.l.google.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2003ms
rtt min/avg/max/mdev = 16.660/17.320/18.254/0.678 ms
```

oznacza to, że sieć i dostęp do internetu są poprawnie skonfigurowane. Możesz przejść do [Przygotowanie dysku twardego](#Przygotowanie_dysku_twardego). Jeśli jednak otrzymujesz:

```
ping: unknown host www.google.com

```

musisz ustawić połączenie z siecią manualnie, według poniższych poleceń.

#### Ustawienie połączenia przewodowego

Postępuj według tej procedury, jeśli twój komputer podłączony jest do sieci Ethernet. W większości przypadków, będziesz mieć jeden interfejs, nazwany `eth0`. Jeśli masz więcej interfejsów (dodatkowych kart lub kart zintegrowanych z płytą główną), ich nazwy będą zgodne z sekwencją `enp2s0f0`, `enp6s0f0`, itd...

##### Dynamiczne IP (DHCP)

Zakładając przewodowe połączenie Ethernet i dostęp do serwera DHCP (np. używając routera), uruchom:

```
# dhcpcd

```

aby otrzymać adres IP. Jeśli masz kilka interfejsów (np. kilka kart Ethernet), możesz wybrać jeden z nich używając `dhcpcd <interfejs>`, przykładowo:

```
# dhcpcd enp2s0f0

```

Sprawdź swoje połączenie według [powyższego](#Automatyczna_konfiguracja) sposobu. Jeśli sieć działa, przejdź do [#Przygotowanie dysku twardego](#Przygotowanie_dysku_twardego).

##### Statyczne IP

Trzymaj się tej procedury, by ustanowić połączenie z siecią via statyczny adres IP.

Po pierwsze, zidentyfikuj nazwę Twojego interfejsu sieciowego.

 `# ip link` 
```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT 
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: enp2s0f0: <BROADCAST,MULTICAST> mtu 1500 qdisc noop state DOWN mode DEFAULT qlen 1000
    link/ether 00:11:25:31:69:20 brd ff:ff:ff:ff:ff:ff
3: wlp3s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP mode DORMANT qlen 1000
    link/ether 01:02:03:04:05:06 brd ff:ff:ff:ff:ff:ff
```

W tym przypadku, interfejs ethernet nazywa się enp2s0f0\. Jeżeli nie masz pewności, to jego nazwa prawdopodobnie zacznie się literą "e", a prawie na pewno nie będzie się nazywał "lo" lub zaczynała się literą "w". Zawsze możesz użyć iwconfig i zobaczyć, by zobaczyć które interfejsy nie są bezprzewodowe.

 `# iwconfig` 
```
enp2s0f0  no wireless extensions.
wlp3s0    IEEE 802.11bgn  ESSID:"NETGEAR97"  
          Mode:Managed  Frequency:2.427 GHz  Access Point: 2C:B0:5D:9C:72:BF   
          Bit Rate=65 Mb/s   Tx-Power=16 dBm   
          Retry  long limit:7   RTS thr:off   Fragment thr:off
          Power Management:on
          Link Quality=61/70  Signal level=-49 dBm  
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:430   Missed beacon:0
lo        no wireless extensions.
```

W tym przykładzie, ami enp2s0f0, ani urządzenie loopback nie ma rozszerzenia bezprzewodowego, co oznacza, że naszym interfejsem na pewno jest enp2s0f0.

Musisz także znać te wartości:

*   Statyczny adres IP,
*   Maska podsieci,
*   adres IP bramy domyślnej,
*   adresy IP serwerów DNS,
*   Nazwa domeny (jeśli jesteś w lokalnej sieci, możesz ją wymyślić).

Aktywuj podłączony interfejs sieciowy, np. dla `enp2s0f0`:

```
# ip link set enp2s0f0 up

```

Dodaj adres:

```
# ip addr add <adres ip>/<maska podsieci> dev <interfejs>

```

Na przykład:

```
# ip addr add 192.168.1.2/24 dev enp2s0f0

```

Po więcej informacji, zobacz: `man ip`

Dodaj bramę:

```
# ip route add default via <adres ip>

```

(Wpisz adres IP twojej bramy)

Np:

```
# ip route add default via 192.168.1.1

```

Edytuj plik `/etc/resolv.conf`, podmieniając adresy twoich serwerów DNS:

 `# nano /etc/resolv.conf` 
```
 nameserver 61.23.173.5
 nameserver 61.95.849.8
 search example.com
```

**Note:** Aktualnie możesz dołączyć maksymalnie 3 linie `nameserver`.

**Note:** Po więcej informacji dotyczących konfiguracji sieci, odwiedź [Konfigurowanie sieci](/index.php?title=Configuring_network_(Polski)&action=edit&redlink=1 "Configuring network (Polski) (page does not exist)").

**Tip:** Jeśli nie potrzebujesz konfigurować ADSL ani połączenia bezprzewodowego, przejdź do [#Przygotowanie dysku twardego](#Przygotowanie_dysku_twardego).

Powinieneś już posiadać aktywne połączenie internetowe. Jeżeli tak nie jest, odwiedź stronę [Konfigurowanie sieci](/index.php?title=Configuring_network_(Polski)&action=edit&redlink=1 "Configuring network (Polski) (page does not exist)").}}

#### Konfiguracja sieci bezprzewodowej

Postępuj według tej procedury, jeśli potrzebujesz łączności bezprzewodowej (wifi) w czasie instalacji.

Jeżeli używałeś wcześniej innej dystrybucji lub instalujesz ponownie system Arch Linux od czasu porzucenia starego modelu nazewnictwa, możesz być zaskoczony faktem, że pierwszy interfejs nie nazywa się "wlan0". Prawdę mówiąc, to żaden interfejs nie będzie już poprzedzany przedrostkiem "wlan". Nie panikuj; po prostu wykonaj polecenie `iwconfig` by dowiedzieć się jaka jest nowa nazwa Twojego interfejsu sieciowego.

Sterowniki do kart bezprzewodowych oraz niezbędne narzędzia są dostępne w środowisku uruchamianym z nośnika instalacyjnego. Wiedza o posiadanym sprzęcie będzie kluczowa dla pomyślnej konfiguracji. Pamiętaj, że następująca procedura *wykonana w tym momencie, podczas instalacji* uruchomi sieć bezprzewodową *w środowisku instalacyjnym*. Te kroki (lub inny sposób zarządzania połączeniami bezprzewodowymi) **muszą zostać powtórzone z poziomu zainstalowanego systemu po jego uruchomieniu**.

Pamiętaj także, że te kroki są opcjonalne jeśli połączenie bezprzewodowe jest niepotrzebne w tym momencie instalacji; sieć bezprzewodowa może być skonfigurowana później.

**Note:** W poniższych przykładach `wlp3s0` oznacza interfejs, a `linksys` ESSID (nazwę) sieci. Zastąp te wartości odpowiednimi dla Twojej sieci.

Podstawowa procedura wygląda następująco:

*   (opcjonalnie) Zidentyfikuj interfejs bezprzewodowy:

```
# lspci | grep -i net

```

lub jeśli używasz karty USB:

```
# lsusb

```

*   Upewnij się, że udev załadował sterownik i stworzył odpowiedni interfejs używając `iwconfig`:

**Note:** Jeśli nie widzisz wyniku podobnego do tego, twój sterownik bezprzewodowy nie został załadowany. W takim przypadku, musisz załadować sterownik manualnie. Zobacz [Konfiguracja sieci bezprzewodowej](/index.php?title=Wireless_Setup_(Polski)&action=edit&redlink=1 "Wireless Setup (Polski) (page does not exist)") po dokładne instrukcje.
 `# iwconfig` 
```
enp2s0f0  no wireless extensions.
wlp3s0    IEEE 802.11bgn  ESSID:"NETGEAR97"  
          Mode:Managed  Frequency:2.427 GHz  Access Point: 2C:B0:5D:9C:72:BF   
          Bit Rate=65 Mb/s   Tx-Power=16 dBm   
          Retry  long limit:7   RTS thr:off   Fragment thr:off
          Power Management:on
          Link Quality=61/70  Signal level=-49 dBm  
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:430   Missed beacon:0
lo        no wireless extensions.
```

`wlp3s0` to dostępny interfejs bezprzewodowy w tym przykładzie.

*   Podnieś interfejs używając:

```
# ip link set wlp3s0 up

```

Mały procent układów bezprzewodowych wymaga firmware oprócz odpowiedniego sterownika. Jeśli układ wymaga firmware, prawdopodobnie otrzymasz ten błąd przy podnoszeniu intefejsu:

 `# ip link set wlp3s0 up`  `SIOCSIFFLAGS: No such file or directory` 

W razie niepewności, użyj `dmesg` aby przejrzeć log jądra, szukając próśb o firmware od układu bezprzewodowego.

Przykładowy wynik polecenia korzystając z układu Intela, który wymaga firmware i prosi o niego jądro podczas startu systemu:

 `# dmesg | grep firmware`  `firmware: requesting iwlwifi-5000-1.ucode` 

Jeśli polecenie nic nie wypisze, najpewniej układ nie wymaga firmware.

**Warning:** Pakiety z firmware (dla kart tego wymagających) są preinstalowane w `/usr/lib/firmware` w środowisku live (na płycie/pendrivie), **ale muszą być zainstalowane w systemie po instalacji aby zapewnić łączność bezprzewodową!** Instalacja pakietów jest opisana w dalszej części tego przewodnika. Upewnij się, że zainstalowane są zarówno sterowniki, jak i firmware przed restartem! Zobacz [Konfiguracja sieci bezprzewodowych](/index.php?title=Wireless_Setup_(Polski)&action=edit&redlink=1 "Wireless Setup (Polski) (page does not exist)") jeśli nie jesteś pewny(a) co do wymogu instalacji firmware dla posiadanego układu. To bardzo częsty błąd.

Następnie użyj `wifi-menu` z pakietu [netcfg](https://aur.archlinux.org/packages/netcfg/), by połączyć się z siecią:

```
# wifi-menu wlp3s0

```

**Warning:** Na chwilę obecną wywołanie wifi-menu bez podania parametru zmusi go do szukania "wlan0". Wykonaj wifi-menu z nazwą Twojego interfejsu jako parametrem, by go użyć.

Powinieneś(aś) teraz mieć działające połączenie z Internetem. Jeśli nie masz, odwiedź bardziej szczegółową stronę [Konfiguracja sieci bezprzewodowej](/index.php?title=Wireless_Setup_(Polski)&action=edit&redlink=1 "Wireless Setup (Polski) (page does not exist)").

#### Skonfiguruj połączenie bezpośrednie z modemem

##### xDSL (PPPoE)

Podążaj według tej procedury, jeśli masz modem lub router w trybie bridge do łączenia się z twoim dostawcą Internetu.

Wywołaj:

```
# pppoe-setup

```

*   Podaj nazwę, którą dostarczył Ci dostawca usług internetowych (ISP).
*   Naciśnij `Enter` wybierając "eth0".
*   Naciśnij `Enter` wybierając "no".
*   Wpisz `server` (zazwyczaj wymaga tego konfiguracja).
*   Naciśnij `1` by wybrać firewall.
*   Wpisz hasło, które dostarczył Ci dostawca usług internetowych.
*   Naciśnij `Y` na końcu.

Jeśli wszystko jest poprawnie skonfigurowane, połącz się używając:

```
# pppoe-start

```

Możesz także skonfigurować plik `resolv.conf`:

```
# echo nameserver 8.8.8.8 > /etc/resolv.conf

```

##### Modem analogowy, ISDN

Zobacz [Direct Modem Connection_(Polski)](/index.php?title=Direct_Modem_Connection_(Polski)&action=edit&redlink=1 "Direct Modem Connection (Polski) (page does not exist)") po szczegółowe instrukcje.

#### Proxy Server

Jeśli jesteś za serwerem proxy, musisz wyeksportować zmienne środowiskowe `http_proxy` i `ftp_proxy`. **[Kliknij tutaj](/index.php?title=Proxy_(Polski)&action=edit&redlink=1 "Proxy (Polski) (page does not exist)")** po więcej informacji.

#### Przetestuj połączenie

Na koniec, upewnij się, że połączenie działa używając `/bin/ping`:

 `# ping -c 3 www.google.com` 
```
PING www.l.google.com (74.125.132.105) 56(84) bytes of data.
64 bytes from wb-in-f105.1e100.net (74.125.132.105): icmp_req=1 ttl=50 time=17.0 ms
64 bytes from wb-in-f105.1e100.net (74.125.132.105): icmp_req=2 ttl=50 time=18.2 ms
64 bytes from wb-in-f105.1e100.net (74.125.132.105): icmp_req=3 ttl=50 time=16.6 ms

--- www.l.google.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2003ms
rtt min/avg/max/mdev = 16.660/17.320/18.254/0.678 ms

```

### Przygotowanie dysku twardego

**Warning:** Partycjonowanie dysku twardego może zniszczyć dane. **Zdecydowanie** prosimy o ostrożność i sporządzenie kopii ważnych danych przed kontynuacją.

Jeżęli jesteś początkującym, zachęcamy do użycia jakiegoś graficznego narzędzia do partycjonowania. [GParted](http://gparted.sourceforge.net/download.php) jest dobrym przykładem, w dodatku jest [dostępny jako "live" CD](http://gparted.sourceforge.net/livecd.php). Jest także dostępny w większości dystrybucji Linuxa uruchamiających się w trybie "live" CD, np w [Ubuntu](https://en.wikipedia.org/wiki/Ubuntu_(operating_system) i [Linux Mint](https://en.wikipedia.org/wiki/Linux_Mint przed ponownym uruchomieniem.

**Note:** Obecny dysk instalacyjny zawiera programy **cfdisk**, **gdisk**, i **parted**.

Jeśli już wcześniej spartycjonowałeś(aś) swój dysk, sprawdź obecny układ partycji używając `/sbin/fdisk` z opcją `-l` (małe L).

W linii poleceń roota wpisz:

```
# fdisk -l

```

Zapisz nazwy dysków i/lub partycji potrzebnych do instalacji Archa. Każda partycja jest identyfikowana przez przyrostek liczbowy. Przykład: `sda1` oznacza pierwszą partycję dysku, podczas gdy `sda` oznacza cały dysk. Możesz przejść do [#Konfiguracja urządzeń blokowych, systemów plików i punktów montowania](#Konfiguracja_urz.C4.85dze.C5.84_blokowych.2C_system.C3.B3w_plik.C3.B3w_i_punkt.C3.B3w_montowania).

**Note:** Jeśli instalujesz na pamięci flash USB, zobacz [Installing Arch Linux on a USB key_(Polski)](/index.php?title=Installing_Arch_Linux_on_a_USB_key_(Polski)&action=edit&redlink=1 "Installing Arch Linux on a USB key (Polski) (page does not exist)").

**Note:** Jeśli nie będziesz używać windowsa, zaleca się użycie [GPT](/index.php?title=GPT_(Polski)&action=edit&redlink=1 "GPT (Polski) (page does not exist)") zamiast [MBR](/index.php?title=MBR_(Polski)&action=edit&redlink=1 "MBR (Polski) (page does not exist)"). Partycjonowanie GPT można wykonać tylko z **gdisk** lub **parted**. Przeczytaj [GPT](/index.php?title=GPT_(Polski)&action=edit&redlink=1 "GPT (Polski) (page does not exist)") po listę zalet.

Pozostała część tej sekcji pokazuje przykładową konfigurację dla początkujących używając programu **cfdisk**. Nie musisz używać tej konfiguracji czy tego narzędzia; jest to tylko przykład konfiguracji.

Po więcej informacji na temat partycjonowania dysku twardego, zobacz [Partycjonowanie](/index.php/Partitioning_(Polski) "Partitioning (Polski)").

Po więcej informacji o dostępnych systemach plików, zobacz [Systemy plików](/index.php/File_Systems_(Polski) "File Systems (Polski)").

Zobacz [Swap](/index.php?title=Swap_(Polski)&action=edit&redlink=1 "Swap (Polski) (page does not exist)"), by zobaczyć szczegóły ustawiania partycji lub pliku swap. Plik swap jest łatwiejszy do rozszerzenia niż partycja i może zostać utworzony w dowolnym momencie po instalacji, ale nie może być używany razem z systemem plinków BTRFS.

Jeżeli masz ten krok już za sobą, przejdź do sekcji [montowanie partycji](#Mount_the_partitions_.28Polski.29).

W przeciwnym wypadku czytaj dalej.

#### Manualne partycjonowanie dysku twardego

**Note:** Obecny nośnik instalacyjny zawiera narzędzia [cfdisk](https://en.wikipedia.org/wiki/cfdisk "wikipedia:cfdisk"), [gdisk](https://en.wikipedia.org/wiki/gdisk "wikipedia:gdisk"), i [parted](https://en.wikipedia.org/wiki/parted "wikipedia:parted"). `gdisk` wspiera tylko tablice partycji [GPT](/index.php?title=GPT_(Polski)&action=edit&redlink=1 "GPT (Polski) (page does not exist)"), `cfdisk` wspiera tylko tablice partycji [MBR](/index.php?title=MBR_(Polski)&action=edit&redlink=1 "MBR (Polski) (page does not exist)"), a `parted` wspiera obydwa rodzaje. W tym przykładzie użyty jest **cfdisk**, jednak podmieniając **gdisk** za cfdisk można tym sposobem wykonać partycjonowanie [GPT](/index.php?title=GPT_(Polski)&action=edit&redlink=1 "GPT (Polski) (page does not exist)").

**Notka dla trybu [UEFI](/index.php?title=UEFI_(Polski)&action=edit&redlink=1 "UEFI (Polski) (page does not exist)"):**

*   Jeżeli korzystasz z płyty głównej z trybem UEFI, musisz utworzyć dodatkowo [UEFI System partition](/index.php/Unified_Extensible_Firmware_Interface#Create_an_UEFI_System_Partition_in_Linux "Unified Extensible Firmware Interface").
*   Jest zalecane, by zawsze używać GPT z UEFI, ponieważ niektóre firmware UEFI nie pozwalają na uruchamianie via UEFI-MBR.

**Notka dla partycji [GPT](/index.php/GPT "GPT"):**

*   Jeżeli nie korzystasz z systemu z rodziny Windows, zalecane jest, by użyć GPT zamiast MBR. Przeczytaj [GPT](/index.php?title=GPT_(Polski)&action=edit&redlink=1 "GPT (Polski) (page does not exist)"), by dowiedzieć się o zaletach takiego rozwiązania.
*   Jeżeli używasz płyty głównej z BIOSem (lub planujesz uruchamiać system w trybie kompatybilności z BIOSem) i chcesz zainstalować GRUB na dysku korzystającym z GPT, będziesz musiał utworzyć 1007 KiB "[BIOS Boot Partition](/index.php/GRUB#GPT_specific_instructions "GRUB")". Syslinux nie potrzebuje takiego rozwiązania.
*   Niektóre systemy BIOS mogą mieć problemy z obsługą GPT. Zobacz [http://mjg59.dreamwidth.org/8035.html](http://mjg59.dreamwidth.org/8035.html) and [http://rodsbooks.com/gdisk/bios.html](http://rodsbooks.com/gdisk/bios.html) dla rozwiązań i obejść znanych problemów.

**Note:** Jeżeli instalujesz system *na* klucz USB, zobacz [Instalowanie Arch Linux na USB](/index.php?title=Installing_Arch_Linux_on_a_USB_key_(Polski)&action=edit&redlink=1 "Installing Arch Linux on a USB key (Polski) (page does not exist)").

Przykładowy system będzie posiadał 15 GB partycję root oraz partycję [home](/index.php/Partitioning#.2Fhome "Partitioning") na reszcie dostępnego miejsca. Wybierz [MBR](/index.php?title=MBR_(Polski)&action=edit&redlink=1 "MBR (Polski) (page does not exist)") lub [GPT](/index.php?title=GPT_(Polski)&action=edit&redlink=1 "GPT (Polski) (page does not exist)"), ale nie oba!

Sposób w jaki podzielisz swój dysk zależy tylko od Ciebie, poniższy przykład służy tylko do zobrazowania całego procesu. Zobacz [Partycjonowanie](/index.php/Partitioning_(Polski) "Partitioning (Polski)").

| **MBR** | `cfdisk /dev/sda` | **Root:**

*   Wybierz New (lub naciśnij `N`) – `Enter` dla Primary – wpisz "15360" – `Enter` dla Beginning – `Enter` dla Bootable.

 |
| 

**Home:**

*   Naciśnij strzałkę w dół, by zaznaczyć puste miejsce na dysku.
*   Wybierz New (lub naciśnij `N`) – `Enter` dla Primary – `Enter`, by użyć reszty dostępnego miejsca na dysku (lub możesz podać pożądany rozmiar tak jak przy poprzedniej partycji).

 |
| **GPT** | `cgdisk /dev/sda` | **Root:**

*   Wybierz New (lub naciśnij `N`) – `Enter` dla pierwszego sektora (2048) – wpisz "15G" – `Enter` dla standardowego kodu szesnastkowego (8300) – `Enter` dla pustej nazwy partycji.

 |
| **Home:**

*   Naciśnij strzałkę w dół kilka razy by zaznaczyć większą wolną część na dysku.
*   Wybierz New (lub naciśnij `N`) – `Enter` dla pierwszego sektora – `Enter`, by użyć reszty dostępnego miejsca na dysku (lub możesz podać pożądany rozmiar, np "30G") – `Enter` dla standardowego kodu szesnastkowego (8300) – `Enter` dla pustej nazwy partycji.

 |

Jeżeli wybrałeś MBR, tak powinien wyglądać teraz Twój dysk:

```
Name    Flags     Part Type    FS Type          [Label]       Size (MB)
-----------------------------------------------------------------------
sda1    Boot       Primary     Linux                             15360
sda2               Primary     Linux                             133000*

```

Jeżeli wybrałeś GPT, powinieneś otrzymać raczej coś takiego:

```
Part. #     Size        Partition Type            Partition Name
----------------------------------------------------------------
            1007.0 KiB  free space
   1        15.0 GiB    Linux filesystem
   2        123.45 GiB  Linux filesystem

```

**Warning:** Bądź świadomy(a), że to zniszczy wszystkie dane znajdujące się na twoim dysku, więc dwa razy sprawdź wszystkie polecenia i upewnij się, że jesteś zadowolony(a) z układu partycji i ich rozmiarów przed kontynuacją. Jeśli chcesz zacząć od początku, Możesz wybrać **Q**uit (**W**yjdź), aby wyjść bez zapisywania zmian i ponownie uruchomić cfdisk.

Wybierz **W**rite (**Z**apisz), aby zapisać tablicę partycji na dysk. Po zapisaniu tablicy partycji, cfdisk automatycznie zakończy działanie.

Po więcej informacji na temat partycjonowania dysku twardego, zobacz [Partycjonowanie](/index.php/Partitioning_(Polski) "Partitioning (Polski)").

**Note:** Ostatnie ulepszenia jądra Linuksa, w tym libata i modułów PATA, spowodowały, że wszystkie dyski IDE, SATA i SCSI przyjęły schemat nazw sd*x*. Jest to całkowicie normalne.

**Note:** Jeśli używasz (U)EFI, prawdopodobnie będziesz potrzebować kolejnej partycji do przechowywania UEFI System. Przeczytaj [ten artykuł](/index.php?title=Unified_Extensible_Firmware_Interface_(Polski)&action=edit&redlink=1 "Unified Extensible Firmware Interface (Polski) (page does not exist)").

### Konfiguracja urządzeń blokowych, systemów plików i punktów montowania

Spartycjonowanie dysku to nie wszystko; partycje potrzebują [systemu plików](/index.php/File_Systems_(Polski) "File Systems (Polski)"). By sformatować partycje z użüciem systemu plików EXT4:

**Warning:** Sprawdź dwa, a nawet trzy razy, że formatowane partycje (w naszym przykładzie `/dev/sda1` i `/dev/sda2`) są tymi, które chcesz sformatować.

Użyj narzędzia `mkfs` do formatowania partycji w wybranym systemie plików. W tym przykładzie używamy systemu plików ext4 zarówno dla partycji głównej, jak i {ic|/home}.

```
# mkfs.ext4 /dev/sda1
# mkfs.ext4 /dev/sda2

```

Jeżeli utworzyłeś partycję dla swapu (code 82), nie zapomnij sformatować i aktywować jej używając:

```
# mkswap /dev/sda*X*
# swapon /dev/sda*X*

```

Po więcej informacji na temat dostępnych systemów plików, zobacz [Systemy plików](/index.php/File_Systems_(Polski) "File Systems (Polski)").

### Montowanie partycji

Każda partycja jest identyfikowana przez swój suffix. Dla przykładu - `sda1` odwołuje się do pierwszej partycji na pierwszym dysku, a `sda` odwołuje się do całego dysku.

By zobaczyć obecny podział dysku:

```
# lsblk /dev/sda

```

**Note:** Nie montuj więcej niż jednej partycji do tej samej lokalizacji. Uważaj także przy montowaniu, ponieważ kolejność ma znaczenie.

Zamontuj główną partycję w `/mnt`. Dla powyższego przykładu będzie to:

```
# mount /dev/sda1 /mnt

```

Stwórz katalog dla partycji /home i zamontuj ją:

```
# mkdir /mnt/home && mount /dev/sda3 /mnt/home

```

Jeżeli posiadasz płytę główną z UEFI, zamontuj partycję UEFI:

```
# mkdir -p /mnt/boot/efi
# mount /dev/sda*X* /mnt/boot/efi

```

### Wybierz serwer instalacyjny

Przed instalacją, wyedytuj plik `/etc/pacman.d/mirrorlist` tak, aby wybrany serwer był pierwszy w kolejności. Kopia tego pliku zostanie zainstalowana w nowym systemie przez `pacstrap`, więc warto wybrać odpowiedni serwer już teraz.

**Note:** ftp.archlinux.org ma limit 50KB/s.
 `# nano /etc/pacman.d/mirrorlist` 
```
##
## Arch Linux repository mirrorlist
## Sorted by mirror score from mirror status page
## Generated on 2012-MM-DD
##

Server = http://mirror.example.xyz/archlinux/$repo/os/$arch
...
```

*   `Alt+6`, by skopiować wybraną linijkę `Server`.
*   `PageUp`, by przewinąć w górę.
*   `Ctrl+U`, by by wkleić linijkę w wybranym miejscu (w naszym przypadku na górze pliku).
*   `Ctrl+X`, by wyjść. Po zapytaniu o zachowanie zmian, naciśnij `Y` i `Enter`.

Jeżeli chcesz, w pliku możesz zostawić tylko wybrany przez siebie mirror usuwając sałą resztę wpisów (używając `Ctrl+K`), jednak zazwyczaj dobcym pomysłem jest mieć dostępnych kilka serwerów, w razie gdyby pierwszy był offline.

**Tip:**

*   Użyj [Mirrorlist Generator](https://www.archlinux.org/mirrorlist/), by otrzymać aktualną listę mirrorów dla Twojego kraju. Mirrory HTTP są szybsze niż FTP ze względu na technologię [keepalive](https://en.wikipedia.org/wiki/Keepalive "wikipedia:Keepalive"). Z użyciem FTP, pacman musi wysyłąć sygnał za każdym razem, kiedy pobiera paczkę, co objawia się krótką przerwą w pobieraniu. By poznać inne sposoby generowania listy mirrorów, zobacz [Sortowanie mirrorów](/index.php/Mirrors#Sorting_mirrors_.28Polski.29 "Mirrors") i [Reflektor](/index.php?title=Reflector_(Polski)&action=edit&redlink=1 "Reflector (Polski) (page does not exist)").
*   [Arch Linux MirrorStatus](https://archlinux.org/mirrors/status/) udostępnia szczegółowe informacje nt stanu serwerów z mirrorami, jak npproblemami z siecią, zbieraniem danych, czas ostatniej synchroniacji, etc.

**Note:**

*   Zawsze, gdy w przyszłości zmienisz listę mirrorów, pamiętaj by zmusić pacmana, by odświerzył listę pakietów za pomocą `pacman -Syy`. Jest to dobra praktyka, która w przyszłości może oszczędzić Ci problemów z systemem. Zobacz [Mirrory](/index.php?title=Mirrors_(Polski)&action=edit&redlink=1 "Mirrors (Polski) (page does not exist)"), by dowiedzieć się więcej.
*   Jeżeli instalujesz system ze starszego medium (nieaktualny obraz), Twoja lista mirrorów może być nieaktualna, co pewnie doprowadzi do problemów, gdy spróbujesz zaktualizować system (zobacz [FS#22510](https://bugs.archlinux.org/task/22510)). Zalecane jest w takim wypadku zaktualizować listę mirrorów podanym powyżej sposobem.
*   Zgłoszono pewne błędy w [Arch Linux forums](https://bbs.archlinux.org/), dotyczące problemów z siecią, które uniemożliwiają, by pacman zaktualizował repozytoria (zobacz [[1]](https://bbs.archlinux.org/viewtopic.php?id=68944) i [[2]](https://bbs.archlinux.org/viewtopic.php?id=65728)). Kiedy instalujesz Arch Linux natywnie, problemy te można rozwiązać zastępując standardowy file downloader pacmana alternatywą (zobacz [Improve Pacman Performance](/index.php?title=Improve_Pacman_Performance_(Polski)&action=edit&redlink=1 "Improve Pacman Performance (Polski) (page does not exist)")). Gdy instalujesz Arch Linux jako gość w [VirtualBoxie](/index.php/VirtualBox "VirtualBox"), problem można rozwiązać używając w jego konfiguracji "Host interface" zamiast "NAT".

**Note:** Przed aktualizacją listy mirrorów za pomocą `pacman -Syy` upewnij się, że połączenie z siecią nie zostało przerwane. W przeciwnym wypadku otrzymasz błąd o niemożlizości przeprowadzenia aktualizacji pakietów.

### Instalacja bazowego systemu

Bazowy system jest instalowany używając skryptu [pacstrap](https://github.com/falconindy/arch-install-scripts/blob/master/pacstrap.in).

Opcja `-i` może zostać pominięta, jeżeli chcesz zainstalować wszystkie pakiety z grup *base* i *base-devel* bez potwierdzenia.

```
# pacstrap -i /mnt base base-devel

```

**Note:** Jeśli pacman nie jest w stanie zweryfikować pakietów, sprawdź czas systemowy. Jeśli data jest nieodpowiednia (np. wskazuje 2010 rok), klucze podpisujące mogą być uznane za wygasłe (lub nieważne), sprawdzenie podpisów pakietów skończy się błędem i instalacja zostanie przerwana. Ustaw poprawny czas systemowy, robiąc to manualnie lub za pomocą klienta ntp, i uruchom ponownie komendę pacstrap. Na stronie [Czas](/index.php?title=Time_(Polski)&action=edit&redlink=1 "Time (Polski) (page does not exist)") znajdziesz więcej informacji o ustawianiu czasu systemowego.

**Note:** Jeżeli pacman skarży się na brak lub niepoprawne sygnatury podczas fazy pacstrapowania (*error: failed to commit transaction (invalid or corrupted package)*), wykanaj poniższą komendę.

```
# pacman-key --init && pacman-key --populate archlinux 

```

*   [base](https://www.archlinux.org/groups/x86_64/base/): Pakiety z oprogramowaniem z repozytorium [core] dostarczające minimalnego środowiska.

*   [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/): Dodatkowe narzędzia z [core] t.j. `make` i `automake`. Większość początkujących powinna je zainstalować, ponieważ mogą być potrzebne przy administracji nowym systemem. Grupa *base-devel* będzie potrzebna do instalacji oprogramowania z [AUR](/index.php/Arch_User_Repository_(Polski) "Arch User Repository (Polski)").

To zainstaluje podstawowy system Arch. Inne pakiety mogą być zainstalowane później używając [pacmana](/index.php/Pacman_(Polski) "Pacman (Polski)").

### Generacja fstab

Wygeneruj plik [fstab](/index.php?title=Fstab_(Polski)&action=edit&redlink=1 "Fstab (Polski) (page does not exist)") używając następującej komendy. Etykiehy UUID będą użyte, bo wiąże się z nimi szereg korzyści (zabacz [fstab#Identifying filesystems](/index.php/Fstab#Identifying_filesystems "Fstab")). Jeżeli nie chcesz ich używać (lub chcesz użyć labeli), zamień `-U` na `-L`.

```
# genfstab -U -p /mnt >> /mnt/etc/fstab

```

**Note:** Dobrym pomysłem jest sprawdzenie wygenerowanego pliku fstab (`/mnt/etc/fstab`) przed kontynuację. Jeśli napotkasz błędy uruchamiając komendę genfstab lub później w trakcie instalacji, **nie** uruchamiaj genfstab ponownie; po prostu wyedytuj plik fstab.

```
# nano /mnt/etc/fstab

```

**Warning:** Plik fstab zawsze powinien zostać sprawdzony po wygenerowaniu jego zawartości. Jeżeli utworzyłeś partycję EFI, to `genfstab` dodał nieprawidłową opcję do Twojego systemu partycji, co w rezultacie "ochroni" Twój komputer od uruchomienia się z danego dysku. By to naprawić, musisz usunąć wszystkie opcje z wyjątkiem `noatime`. Dla reszty partycji upewnij się, że zamieniłeś `"codepage=cp437"` na `"codepage=437"`, albo po następnym ponownym uruchomieniu komputera system się nie uruchomi i wejdzie w tryb recovery. Jądro Linux 3.8 powinno posiadać już odpowiednią łatkę.

Kilka uwag:

*   Ostatnia kolumna definiuje kolejność sprawdzania partycji przy starcie systemu: użyj `1` dla partycji root (z wyjątkiem btrfs), która powinna być sprawdzana jako pierwsza, dla reszty partycji ustaw `2` lub wyłącz sprawdzanie ustawiając `0` (zobacz [Pola pliku fstab](/index.php/Fstab#Field_definitions_.28Polski.29 "Fstab")).
*   Wszystkie partycje [Btrfs](/index.php?title=Btrfs_(Polski)&action=edit&redlink=1 "Btrfs (Polski) (page does not exist)") i *swap* powinny być ustawione na `0`.

### Chroot do systemu

Następnie [chrootujemy](/index.php?title=Chroot_(Polski)&action=edit&redlink=1 "Chroot (Polski) (page does not exist)") się do nowego systemu.

```
# arch-chroot /mnt /bin/bash

```

**Note:** Pomiń `/bin/bash` aby użyć powłoki sh.

**Tip:** Jeśli zapomniałeś(aś) zainstalować pakiety ze skryptem pacstrap, możesz je zainstalować po chroocie używając **pacman -S <package>**

### Konfiguracja systemu

**Tip:** Dokładne śledzenie i rozumienie tych kroków jest niezbędne dla poprawnej konfiguracji systemu.

Na tym etapie instalacji, skonfigurujesz podstawowe pliki konfiguracyjne bazowego systemu Arch Linux. Będziesz to robił edytując istniejące lub tworząc nowe pliki.

#### Nazwa hosta

Dodaj swoją *hostname* w `/etc/hostname`. **Przykład:**

```
# echo *mojanazwahosta* > /etc/hostname

```

Ustaw jaką chcesz nazwę. Będzie to nazwa twojego komputera.

**Note:** Nie ma potrzeby edytowania `/etc/hosts`, jednak nic nie szkodzi na przeszkodzie, jeśli chcesz to zrobić

Dodaj swoją *hostname* w `/etc/hosts`, taką samą jak w `/etc/hostname` jako alias. Powinno to wyglądać podbnie do tego:

```
127.0.0.1   localhost.localdomain   localhost **mojanazwahosta**
::1         localhost.localdomain   localhost **mojanazwahosta**

```

**Note:** ::1 to w IPv6 odpowiednik adresu 127.0.0.1

**Warning:** Ten format, **zawierający "localhost" oraz właściwą nazwę hosta**, jest wymagany dla kompatybilności. Błędy w tym pliku mogą powodować niską wydajność sieciową i/lub nieprawidłowe działanie niektórych programów.

Jeśli używasz statycznego IP, dopisz kolejną linię wg formatu: <statyczne-IP> <nazwahosta.nazwadomeny.org> <nazwahosta>, np.:

```
192.168.1.100 **mojanazwahosta**.domain.org **mojanazwahosta**

```

**Tip:** Dla wygody, możesz zdefiniować aliasy w pliku `/etc/hosts` dla hostów w twojej sieci, i/lub w Internecie, np.:
```
192.168.1.90 media
192.168.1.88 dane

```
Powyższy przykład pozwoli na dostęp do serwerów z mediami i danymi wg nazwy, bez potrzeby wpisywania ich adresów IP.

#### Font terminala i układ klawiatury

Wyedytuj `vconsole.conf`:

 `# nano /etc/vconsole.conf` 
```
KEYMAP=pl
FONT=lat2-16
FONT_MAP=8859-2
```

*   `KEYMAP` – Jeśli chcesz, możesz użyć mapy z początku instalacji: [#Zmiana układu klawiatury](#Zmiana_uk.C5.82adu_klawiatury), jednak domyślna (`us`) działa ze znakomitą większością klawiatur. Te ustawienia dotyczą tylko terminali, nie graficznych menedżerów okien czy **Xorg**.

*   `FONT` – Dostępne alternatywne fonty terminala znajdują się w `/usr/share/kbd/consolefonts/`. Domyślna wartość (pusta) jest bezpieczna.

*   `FONT_MAP` – Określa mapę konsoli ładowaną przez setfont przy starcie systemu. Dostępne mapy znajdują się w `/usr/share/kbd/consoletrans`. Domyślna wartość (pusta) jest bezpieczna.

Zobacz [Fonty](/index.php?title=Fonts_(Polski)&action=edit&redlink=1 "Fonts (Polski) (page does not exist)") i `man vconsole.conf` po więcej informacji.

#### Strefa czasowa

Dostępne strefy i podstrefy czasowe mogą być znalezione w katalogach `/usr/share/zoneinfo/<Strefa>/<Podstrefa>`.

Aby wyświetlić dostępne <Strefy>, sprawdź katalog `/usr/share/zoneinfo/`:

```
# ls /usr/share/zoneinfo/

```

Podobnie możesz sprawdzić zawartość katalogu z <Podstrefami>:

```
# ls /usr/share/zoneinfo/Europe

```

Utwórz dowiązanie symboliczne `/etc/localtime` do pliku twojej strefy `/usr/share/zoneinfo/<Strefa>/<Podstrefa>` używając tego polecenia:

```
# ln -s `/usr/share/zoneinfo/<Strefa>/<Podstrefa>` /etc/localtime

```

**Przykład:**

```
# ln -s /usr/share/zoneinfo/Europe/Warsaw /etc/localtime

```

Jeśli używasz timedated dostarczanego przez systemd, być może będziesz chciał(a) wyedytować plik `/etc/timezone` i wpisać `Strefa`/`Podstrefa`.

**Przykład:**

```
Europe/Warsaw

```

Przeczytaj `man 5 timezone` po więcej opcji.

Wymóg posiadania `/etc/timezone` może przestać obowiązywać w przyszłości [[3]](http://cgit.freedesktop.org/systemd/systemd/commit/?id=9cb48731b29f508178731b45b0643c816800c05e).

#### Ustawienia regionalne

##### Wybranie regionu (locale)

Ustawienia regionalne mogą zostać użyte przez **glibc** i każdy inny program lub bibliotekę poprawnie wyświetlając waluty, czas, datę i inne własności regionalne:

Są dwa pliki potrzebujące edycji: `locale.gen` oraz `locale.conf`.

*   Plik `locale.gen` jest domyślnie pusty (wszystko jest zakomentowane), więc musisz usunąć stosowny znak `#` na początku linii. Jeżeli chcesz odkomentować i używać kilka wartości, upewnij się, że wszytkie będą kodowane via `UTF-8`. Raz zedytowany, pozostaje on nietknięty przez system. `locale-gen` jest uruchamiane po każdym uaktualnieniu **glibc**, generując wszystkie ustawienia regionalne określone w `/etc/locale.gen`.

Wybierz odpowiednie locale poprzez usunięcie # z początku linii, np.:

 `# nano /etc/locale.gen` 
```
en_US.UTF-8 UTF-8
pl_PL.UTF-8 UTF-8
```

Następnie uruchom:

```
# locale-gen

```

##### Ustawianie systemowego locale

Ustaw odpowiednie [locale](/index.php?title=Locale_(Polski)&action=edit&redlink=1 "Locale (Polski) (page does not exist)") w `/etc/locale.conf`.

**Przykład:**

```
# echo LANG=pl_PL.UTF-8 > /etc/locale.conf

```

Ustawienie tylko `LANG` powinno wystarczyć. Będzie to służyć za domyślną wartość dla innych ustawień.

Możesz przesłonić część ustawień używając zmiennych `LC_*` – na przykład ustawienie `LC_COLLATE=C` wyłącza sortowanie według reguł języka, ale pozostawia resztę ustawień. Możesz wyświetlić wszystkie zmienne `LC_*` poleceniem `locale`.

Zmienna `LC_ALL` przesłania *wszystkie* pozostałe ustawienia. Z tego powodu nie możesz ustawić jej z poziomu `locale.conf`. Zaleca się używanie `LC_ALL` tylko w razie konieczności.

Z powodu późniejszego tworzenia początkowego ramdysku, powinieneś(aś) ustawić zmienną `LANG`. **Przykład:**

```
# export LANG=pl_PL.UTF-8

```

#### Czas zegara sprzętowego

Jest on ustawiany w `/etc/adjtime`. Ustaw czas zegara sprzętowego w ten sam sposób w każdym z posiadanych systemów operacyjnych. W przeciwnym przypadku, będą one nadpisywać czas i powodować jego przesunięcia.

Możesz wygenerować `/etc/adjtime` automatycznie używając jednej z nastepujących komend.

*   [UTC](https://en.wikipedia.org/wiki/Coordinated_Universal_Time "wikipedia:Coordinated Universal Time") (zalecany)

```
# hwclock --systohc --utc

```

**Note:** Używanie UTC w zegarze sprzętowym nie oznacza, że oprogramowanie będize wyświetlać czas UTC.

*   **localtime** (niezalecany) - Używany domyślnie przez Windows

```
# hwclock --systohc --localtime

```

**Warning:** Używanie *localtime* może prowadzić do kilku znanych i nienaprawialnych błędów. Nie ma jednak planów porzucenia wsparcia dla *localtime*.

##### Ustawienie czasu przy jednoczesnym uruchamianiu Windowsa

Jeśli używasz jednocześnie Windowsa, masz dwie możliwe ścieżki:

*   Zalecana: Ustaw Arch Linuksa i Windowsa do używania zegara UTC (szybka modyfikacja rejestru jest wymagana, zobacz [this page](https://help.ubuntu.com/community/UbuntuTime#Make_Windows_use_UTC) po instrukcje). Oprócz tego, wyłącz synchronizację czasu z Internetem w Windowsie, ponieważ to ustawi czas z powrotem na *localtime*. Jeśli potrzebujesz takiej funkcjonalności (synchronizacja czasu), użyj [ntpd](/index.php/Ntpd "Ntpd") lub [systemd-timesyncd](/index.php/Systemd-timesyncd_(Polski) "Systemd-timesyncd (Polski)") w systemie Arch Linux.

*   Niezalecana: Skonfiguruj Arch Linuksa do uźywania *localtime* i (w [#Konfiguracja systemu](#Konfiguracja_systemu)) usuń `hwclock` z sekcji `DAEMONS` w `/etc/rc.conf` (Windows zajmie się ustawianiem zegara sprzętowego).

#### Moduły jądra

**Tip:** Normalnie wszystkie potrzebne moduły są ładowane automatycznie przez udev, więc rzadko będziesz musiał(a) tutaj coś dodać. Dodaj tylko moduły, których brakuje.

W katalogu `/etc/modules-load.d/` umieść pliki, w których będą wypisane moduły, które jądro ma załadować podczas startu systemu. Każdy plik konfiguracyjny powinien być nazwany w stylu `/etc/modules-load.d/<program>.conf`. Pliki powinny zaiwerać listę modułów do załadowania, poprzedzielaną znakami nowej linii. Linie puste i zaczynające się znakami `#` lub `;` będą ignorowane. Przykład:

 `/etc/modules-load.d/virtio-net.conf` 
```
# Załaduj virtio-net.ko podczas uruchamiania
virtio-net
```

### Konfiguracja sieci

Musisz skonfigurować sieć ponownie, tym razem dla nowego systemu. Cała procedura i wymagania są podobne do tej opisanej [wyżej](#Konfiguracja_sieci_w_.C5.9Brodowisku_instalacyjnym), jednak teraz ustawienia będą permanentne i automatycznie uruchamiane podczas startu systemu.

**Note:** Po więcej dokładnych informacji o konfiguracji sieci, odwiedź [Konfigurowanie sieci](/index.php?title=Configuring_network_(Polski)&action=edit&redlink=1 "Configuring network (Polski) (page does not exist)") i [Konfiguracja sieci bezprzewodowej](/index.php?title=Wireless_Setup_(Polski)&action=edit&redlink=1 "Wireless Setup (Polski) (page does not exist)").

#### Sieć przewodowa

**Tip:** Alternatywnie ustawień tych można dokonać przy pomocy [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd"), który ma pewne dodatkowe zalety, jest lekki, świadomy zdarzeń w czasie rzeczywistym (odłączania kabla, itp) i zintegrowany z wieloma elementami [systemd](/index.php/Systemd "Systemd").

##### Dynamiczne IP (DHCP)

Jeżeli używasz pojedynczego, stałego połączenia z siecią, nie potrzebujesz usługi zarządzania sieci i możesz zwyczajnie odblokować i uruchomić usługę `dhcpcd`. Pamiętaj o podaniu jej swojej nazwy interfejsu.

```
# systemctl enable dhcpcd@<interface>.service

```

Alternatywą jest użycie `net-auto-wired` z pakietu [netcfg](https://aur.archlinux.org/packages/netcfg/), który zręcznie obsłuży dynamiczne łączenie się z nowymi sieciami.

Zainstaluj [ifplugd](https://www.archlinux.org/packages/?name=ifplugd), który jest wymagany przez `net-auto-wired`:

```
# pacman -S ifplugd

```

Edytuj `/etc/conf.d/netcfg` i zmodyfikuj nazwę interfejsu sieci na aktualną. Prawie na pewno nie jest to eth0.

 `nano /etc/conf.d/netcfg`  `WIRED_INTERFACE="<interface>"` 

Odblokuj usługę `net-auto-wired`.

```
# systemctl enable net-auto-wired.service

```

##### Statyczne IP

Skopiuj przykładowy profil z `/etc/network.d/examples` do `/etc/network.d`:

```
# cd /etc/network.d
# cp examples/ethernet-static .

```

Edytuj skopiowany profil wg własnych potrzeb (edytuj `INTERFACE`, `ADDR`, `GATEWAY` i `DNS`):

```
# nano ethernet-static

```

Edytuj `/etc/conf.d/netcfg` i dodaj nowy profil sieci do tablicy `NETWORKS`:

 `nano /etc/conf.d/netcfg`  `NETWORKS=(ethernet-static)` 

Odblokuj usługę `netcfg`:

```
# systemctl enable netcfg.service

```

#### Sieć bezprzewodowa

Będziesz musiał(a) zainstalować inny program do konfiguracji i zarządzania profilami sieci bezprzewodowych, np. [netcfg](/index.php?title=Netcfg_(Polski)&action=edit&redlink=1 "Netcfg (Polski) (page does not exist)"). [NetworkManager](/index.php?title=NetworkManager_(Polski)&action=edit&redlink=1 "NetworkManager (Polski) (page does not exist)") lub [Wicd](/index.php?title=Wicd_(Polski)&action=edit&redlink=1 "Wicd (Polski) (page does not exist)") to popularne alternatywy.

*   Zainstaluj wymagane pakiety:

```
# pacman -S wireless_tools wpa_supplicant wpa_actiond dialog

```

Jeśli twoja karta bezprzewodowa wymaga firmware (jak zostało wyjaśnione w [#Konfiguracja sieci bezprzewodowej](#Konfiguracja_sieci_bezprzewodowej) i [Wireless_Setup_(Polski)#Sterowniki_i_firmware](/index.php?title=Wireless_Setup_(Polski)&action=edit&redlink=1 "Wireless Setup (Polski) (page does not exist)")), zainstaluj pakiet zawierający odpowiednie firmware, *przykładowo*:

```
# pacman -S zd1211-firmware

```

*   Po instalacji i ponownym uruchomieniu możesz połączyć się z siecią wykonując `wifi-menu <interface>` (gdzie `<interface>` to nazwa interfejsu), co wygeneruje plik profilu w `/etc/network.d` nazwany tak samo, jak SSID wybranej sieci. Jeżeli chcesz skonfigurować wszystko ręcznie, to dostępne są szablony w `/etc/network.d/examples/`.

**Warning:** Jeżeli korzystasz z `wifi-menu`, to pozostałe kroki muszą być wykonane *po* ponownym uruchomieniu, gdy już nie jesteś chrootwany. Proces uruchomieny przez to polecenie będzie w konflikcie z tym, który działa na zewnątrz chroota. Jeżeli koniecznie chcesz już na tym etapie posiadać skonfigurowaną sieć, jesteś zmuszony skorzystać z szablonów. Pozwala to jednak w ogóle nie martwić się o użycie `wifi-menu`.

```
# wifi-menu <interface>

```

*   Odblokuj usługę `net-auto-wireless`, która w sposób automatyczny i zręczny zajmie się obsługą połączenia z siecią:

```
# systemctl enable net-auto-wireless.service

```

**Note:** [Netcfg](/index.php/Netcfg "Netcfg") dostarcza także `net-auto-wired`, który może być użyty wspólnie z `net-auto-wireless`.

*   Upewnij się, że w `/etc/conf.d/netcfg` ustawiony jest prawidłowy interfejs (np. `wlp3s0`)}}:

 `# nano /etc/conf.d/netcfg`  `WIRELESS_INTERFACE="wlp3s0"` 

Możliwe jest zdefiniowanie listy profilów sieciowych, które powinny być automatycznie łączone za pomocą zmiennej `AUTO_PROFILES` w `/etc/conf.d/netcfg`. Jeśli `AUTO_PROFILES` nie zostanie ustawione, wszystkie sieci zostaną wypróbowane.

#### Połączenie bezpośrednie z modemem

W przypadku posiadania xDSL, modemu analogowego (dial-up) lub ISDN, zobacz [Direct Modem Connection_(Polski)](/index.php?title=Direct_Modem_Connection_(Polski)&action=edit&redlink=1 "Direct Modem Connection (Polski) (page does not exist)") po dokładne instrukcje.

### Stwórz początkowy ramdysk

**Tip:** Większość użytkowników może pominąć ten krok i użyć standardowych ustawieþ dostarczonych w `mkinitcpio.conf`. Obraz initramfs (z folderu `/boot`) został już wygenerowany podczas gdy paczka [linux](https://www.archlinux.org/packages/?name=linux) (jądro Linux) była instalowana za pomocą `pacstrap`.

Tutaj możesz ustawić właściwe [hooks](/index.php/Mkinitcpio#HOOKS "Mkinitcpio"), jeżeli root został ustawiony na kluczu USB, jeżeli używasz RAID, LVM, lub jeśli `/usr` jest na osobnej partycji.

Skonfiguruj `/etc/mkinitcpio.conf` według potrzeb (zobacz [mkninitcpio](/index.php?title=Mkinitcpio_(Polski)&action=edit&redlink=1 "Mkinitcpio (Polski) (page does not exist)")) i stwórz ramdysk używając:

```
# mkinitcpio -p linux

```

{{Note|Instalacja Arch VPS na QEMU (np. używając `virt-manager`) może wymagać modułu `virtio` w `mkinitcpio.conf` by móc się uruchomić.

 `# nano /etc/mkinitcpio.conf`  `MODULES="virtio virtio_blk virtio_pci virtio_net"` }

### Instalacja i konfiguracja bootloadera

**Note:** Jeżeli na dysku, na którym zainstalowano Arch Linux jest już zainstalowany bootloader i/lub inny system operacyjny, możliwe powinno być dodanie do listy systemów Archa i uruchamianie go poprzez nowy wpis na liście. Więcej na ten temat dowiesz się w podręcznikach swoich bootloaderów. Pamiętaj o zamontowaniu dysku z systemem Arch w przypadku korzystania z automatycznych narzędzi.

#### Dla płyt głównych z BIOS

Dla płyt z BIOSem istnieją trzy bootloadery - Syslinux, GRUB, and [LILO](/index.php?title=LILO_(Polski)&action=edit&redlink=1 "LILO (Polski) (page does not exist)"). Możesz wybrać dowolny z nich wg własnych upodobań. Poniżej opisano sposób instalacji GRUB oraz Syslinux.

*   Syslinux (obecnie) jest ograniczony do wczytywania plików tylko z partycji, na której został zainstalowany. Syslinux jest uważany za prostszy w konfiguracji, ponieważ posiada tylko jeden plik konfiguracyjny. Przykładowa konfiguracja dostępna jest [tutaj](https://bbs.archlinux.org/viewtopic.php?pid=1109328#p1109328).

*   GRUB jest bogatym w funkcje i kompleksowym rozwiązaniem. Korzysta z wielu plików konfiguracyjnych, z pomocą których tworzony jest główny plik `grub.cfg`. Jego pliki konfiguracyjne wyglądem przypominają języki skryptowe, co może być utrudnieniem dla początkujących użytkowników w przypadku próby ręcznej edycji wpisów. Zalecane jest korzystanie z ręcznego generowania wpisów.

**Note:** Niektóre płyty główne z BIOSem mają problemy z GPT. Zobacz [http://mjg59.dreamwidth.org/8035.html](http://mjg59.dreamwidth.org/8035.html) oraz [http://rodsbooks.com/gdisk/bios.html](http://rodsbooks.com/gdisk/bios.html) dla rozwiązań i obejść znanych problemów.

**Note:** Jeśli posiadasz oddzielną partycję `/boot`, najpierw sprawdź, czy jest zamontowana używając `lsblk /dev/sda`. Jeśli nie widzisz punktu montowania `/boot` przy twojej partycji, powinieneś(aś) ponownie uruchomić komputer i z poziomu LiveCD Archa:

*   zamontować główną partycję `/` w `/mnt`
*   zamontować partycję `/boot` w `/mnt/boot`
*   uruchomić `arch-chroot /mnt`

następnie postępować według instrukcji poniżej.

##### Syslinux

**Note:** Jeżeli spartycjonowałeś dysk z użyciem GPT, doinstaluj paczkę [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk) używając (`pacman -S gptfdisk`). Zawiera ona `sgdisk`, które będzie użyte do ustawienia specyficznych dla GPT flag.

Zainstaluj pakiet [syslinux](https://www.archlinux.org/packages/?name=syslinux) i uruchom skrypt `syslinux-install_update`, aby *zainstalować* pliki (`-i`), oznaczyć *aktywną* partycję jako *bootowalną* (`-a`), i zainstalować kod startowy w *MBR* (`-m`):

```
# pacman -S syslinux
# syslinux-install_update -iam

```

wyedytuj plik `syslinux.cfg`, aby wskazywał na odpowiednią partycję główną. Ten krok jest niezbędny. Jeśli będzie wskazywał na niewłaściwą partycję, Arch Linux nie uruchomi się. Zmień `/dev/sda3` na twoją partycję główną (jeśli partycjonowałeś(aś) dysk jak w przykładzie, twoja partycja główna to `/dev/sda1`). To samo zrób z `LABEL archfallback`.

```
# pacman -S syslinux
# nano /boot/syslinux/syslinux.cfg
```

```
...
LABEL arch
        ...
        APPEND root=/dev/sda3 ro
        ...
```

Po więcej informacji o konfiguracji i używaniu Syslinuksa, zobacz [Syslinux](/index.php?title=Syslinux_(Polski)&action=edit&redlink=1 "Syslinux (Polski) (page does not exist)").

##### GRUB

Zainstaluj paczkę [grub-bios](https://www.archlinux.org/packages/?name=grub-bios) i wykonaj `grub-install /dev/sda`.

**Note:** Zamień `/dev/sda` na taki wpis, który odzwierciedla dysk, na którym zainstalowałeś system Arch. *Nie używaj* numerów partycji (`sda*X*`)

**Note:** Dla dysków spartycjonowanych z użüciem GPT na płytach z BIOSem, GRUB potrzebuje a "[BIOS Boot Partition](/index.php/GRUB#GPT_specific_instructions "GRUB")".

```
# pacman -S grub-bios
# grub-install --target=i386-pc --recheck /dev/sda

```

Żeby zapobiec (nieszkodliwej) informacji o błędzie podczas uruchamiania:

```
# cp /usr/share/locale/en\@quot/LC_MESSAGES/grub.mo /boot/grub/locale/en.mo

```

Możesz użyć ręcznie stworzonego `grub.cfg`, jednak dla początkujących użytkowników zalecamy skorzystanie z automatycznej generacji:

**Tip:** Żeby automatycznie wyszukać inne systemy operacyjne znajdujące się w komputerze, zainstaluj [os-prober](https://www.archlinux.org/packages/?name=os-prober) przed wpisaniem kolejnej komendy:
```
# pacman -S os-prober

```

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

Po więcej informacji o konfiguracji i używaniu GRUBa, zobacz [GRUB](/index.php?title=GRUB_(Polski)&action=edit&redlink=1 "GRUB (Polski) (page does not exist)").

#### Dla płyt głównych z UEFI

**Note:** Jeśli posiadasz płytę UEFI przeczytaj artykuł [Bootloadery UEFI](/index.php?title=UEFI_Bootloaders_(Polski)&action=edit&redlink=1 "UEFI Bootloaders (Polski) (page does not exist)").

Dla uruchomiena z UEFI, dysk musi być spartycjonowany z użüciem GPT oraz musi być obecna i zamontowana w `/boot/efi` systemowa partycja UEFI (512 MiB lub więcej, FAT32, typ `EF00`). Jeżeli śledzisz ten poradnik od początku, ten krok masz już za sobą.

Chociaż dostęrne są inne [bootloadery dla UEFI](/index.php?title=UEFI_Bootloaders_(Polski)&action=edit&redlink=1 "UEFI Bootloaders (Polski) (page does not exist)"), użüwanie EFISTUB jest zalecane. Poniżej znajdziesz instrukcje konfiguracyjne dla EFISTUB i GRUB.

**Note:** Syslinux jak dotąd nie wspiera [UEFI](/index.php?title=UEFI_(Polski)&action=edit&redlink=1 "UEFI (Polski) (page does not exist)").

##### EFISTUB

Jądro linuxa może zachować się jak swój własny bootloader korzystając z EFISTUB. Jest to metoda zalecana przez twórców UEFI and simpler compared to `grub-efi-x86_64`. Poniższe kroki ustawiają rEFInd (fork rEFIt), by wyświetlić menu dla jąder EFISTUB, jak również uruchomienia innych bootloaderów UEFI. Możesz także użyć [gummiboot](/index.php/UEFI_Bootloaders#Using_gummiboot "UEFI Bootloaders") zamiast rEFInd. Oba potrafią wykryć bootloader Windows UEFI w wypadku korzystania z dual-boot.

1\. Uruchom system z trybem UEFI i załaduj moduły `efivars` przed wykonaniem chroot:

```
# modprobe efivars

```

2\. Zamontuj partycję UEFISYS w `/mnt/boot/efi`, wykonaj chroot i [skoriuj pliki jąhra i initramfs](/index.php/UEFI_Bootloaders#Setting_up_EFISTUB "UEFI Bootloaders") tak jak pokazano poniżej.

*   Stwórz `/boot/efi/EFI/arch/`.

*   Skopiuj `/boot/vmlinuz-linux` do `/boot/efi/EFI/arch/vmlinuz-arch.efi`. Rozszerzenie `.efi` jest bardzo ważne, bo niektóre firmware UEFI odmawiają uruchomienia pliku bez tego rozszerzenia. **Ważne:** Pamiętaj, że plik nazywa się vmlinu**z**, a nie vmlinu**x**.

*   Skopiuj `/boot/initramfs-linux.img` do `/boot/efi/EFI/arch/initramfs-arch.img`.

*   Skopiuj `/boot/initramfs-linux-fallback.img` do `/boot/efi/EFI/arch/initramfs-arch-fallback.img`.

Za każdym razem, gdy jądro i pliki initramfs są aktualizowane w `/boot`, muszą być także uaktualnione w `/boot/efi/EFI/arch`. Może to zostać zautomatyzowane poprzez [użücie systemd](/index.php/UEFI_Bootloaders#Sync_EFISTUB_Kernel_in_UEFISYS_partition_using_Systemd "UEFI Bootloaders") lub [incrona](/index.php/UEFI_Bootloaders#Sync_EFISTUB_Kernel_in_UEFISYS_partition_using_Incron "UEFI Bootloaders") (dla konfiguracji bez systemd).

3\. W tym poradniku zainstalujesz GUI nazwane rEFInd. Alternatywne bootloadery mogą zostać znalezione na stronie [UEFI Bootloaders#Booting EFISTUB](/index.php/UEFI_Bootloaders#Booting_EFISTUB "UEFI Bootloaders"). Dla zalecanego bootloadera rEFInd zainstaluj następujące paczki:

```
# pacman -S refind-efi efibootmgr

```

4\. Zainstaluj rEFInd na partycji UEFISYS (zbiorczo z [UEFI Bootloaders#Using rEFInd](/index.php/UEFI_Bootloaders#Using_rEFInd "UEFI Bootloaders")):

```
# mkdir -p /boot/efi/EFI/refind
# cp /usr/share/refind/refind_x64.efi /boot/efi/EFI/refind/refind_x64.efi
# cp /usr/share/refind/refind.conf-sample /boot/efi/EFI/refind/refind.conf
# cp -r /usr/share/refind/icons /boot/efi/EFI/refind/icons

```

5\. Stwórz plik `refind_linux.conf` z poniższymi ustawieniami, które zostaną użyte przez rEFInd:

 `# nano /boot/efi/EFI/arch/refind_linux.conf` 
```
"Boot to X"          "root=/dev/sdaX ro rootfstype=ext4 systemd.unit=graphical.target"
"Boot to console"    "root=/dev/sdaX ro rootfstype=ext4 systemd.unit=multi-user.target"
```

**Note:** `refind_linux.conf` zostało skopiowane z `/boot/efi/EFI/arch/`, gdzie initramfs i jądro zostały skopiowane w kroku 2.

**Note:** W `refind_linux.conf`, sdaX odpowiada Twojemu systemowi plików root, a nie partycji boot, o ile oczywiście utworzyłeś je osobno.

6\. Dodaj rEFInd do UEFI boot menu używając [efibootmgr](/index.php/UEFI#efibootmgr "UEFI").

**Warning:** Używając `efibootmgr` na Apple Mac może zablokować firmware, przez co konieczne będzie sflashowanie pamięci ROM płyty głównej. Dla Maców użyj [mactel-boot](https://aur.archlinux.org/packages/mactel-boot/), lub "błogosławieństwa" od Mac OS X.

```
# efibootmgr -c -g -d /dev/sdX -p Y -w -L "rEFInd" -l '\EFI\refind\refind_x64.efi'

```

**Note:** W powyższym poleceniu X i Y odnoszą się do dysku i partycji UEFISYS. Dla przykładu w `/dev/sdc5`, X to "c", a Y to "5".

7\. (Opcjonalnie) Jako zabezpieczenie na wypadek, gdyby `efibootmgr` stworzyło wpis, który nie działa, skopiuj `refind_x64.efi` do `/boot/efi/EFI/boot/bootx64.efi` tak jak poniżej:

```
# cp -r /boot/efi/EFI/refind/* /boot/efi/EFI/boot/
# mv /boot/efi/EFI/boot/refind_x64.efi /boot/efi/EFI/boot/bootx64.efi

```

##### GRUB

**Note:** W rzadkich przypadkach, będziesz musiał(a) użyć `grub-efi-i386`; na przykład na starszych komputerach Mac, gdzie Apple używa pewnego rodzaju połączenia UEFI v1.x i v2.x. W takich przypadkach, GRUB będzie działać tylko z modułami 32-bitowymi, pomimo 64-bitowego procesora. Jeżeli posiadasz system z 32-bitowym EFI, jak np. w Macach sprzed 2008 roku, zainstaluj `grub-efi-i386` zamiast `grub-efi-x86_64` i użyj opcji `--target=i386-efi`.

```
# pacman -S grub-efi-x86_64 efibootmgr
# grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=arch_grub --recheck
# cp /usr/share/locale/en\@quot/LC_MESSAGES/grub.mo /boot/grub/locale/en.mo

```

Następna komenda tworzy wpisy dla GRUB w boot menu UEFI. Jako że [grub-efi-x86_64](https://www.archlinux.org/packages/?name=grub-efi-x86_64) w wersji 2.00, `grub-install` próbuje utworzyć wpisy w menu, więc wywołanie `efibootmgr` może nie być konieczne. Zobacz [UEFI#efibootmgr](/index.php/UEFI#efibootmgr "UEFI"), by dowiedzieć się więcej.

```
# efibootmgr -c -g -d /dev/sdX -p Y -w -L "Arch Linux (GRUB)" -l '\EFI\arch_grub\grubx64.efi'

```

Możesz użyć ręcznie stworzonego `grub.cfg`, jednak dla początkujących użytkowników zalecamy skorzystanie z automatycznej generacji:

**Tip:** Żeby automatycznie wyszukać inne systemy operacyjne znajdujące się w komputerze, zainstaluj [os-prober](https://www.archlinux.org/packages/?name=os-prober) przed wpisaniem kolejnej komendy:
```
# pacman -S os-prober

```

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

Po więcej informacji o konfiguracji i używaniu GRUBa, zobacz [GRUB](/index.php?title=GRUB_(Polski)&action=edit&redlink=1 "GRUB (Polski) (page does not exist)").

Możesz użyć ręcznie stworzonego `grub.cfg`, jednak dla początkujących użytkowników zalecamy skorzystanie z automatycznej generacji:

### Hasło roota

Ustaw hasło roota używając:

```
# passwd

```

### Odmontowanie partycji i ponowne uruchomienie

Wyjdź ze środowiska chroot:

```
# exit

```

Partycje są zamontowane w `/mnt`, więc użyj tego polecenia, żeby je odmontować:

```
# umount /mnt/{boot,home,}

```

Uruchom komputer ponownie:

```
# reboot

```

**Tip:** Wyjmij nośnik instalacyjny i zmień kolejność uruchamiania w BIOSie (jeśli zmieniałeś(aś) ją przed instalacją); inaczej nośnik instalacyjny może uruchomić się ponownie!