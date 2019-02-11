**Tor** ([ang.](/index.php?title=J%C4%99zyk_angielski&action=edit&redlink=1 "Język angielski (page does not exist)") **The Onion Router**) – wirtualna sieć komputerowa implementująca trasowanie cebulowe drugiej generacji. Sieć zapobiega analizie ruchu sieciowego i w konsekwencji zapewnia użytkownikom prawie anonimowy dostęp do zasobów Internet

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Wprowadzenie](#Wprowadzenie)
*   [2 Instalacja](#Instalacja)
*   [3 Konfiguracja](#Konfiguracja)
    *   [3.1 Konfiguracja przekaźnika](#Konfiguracja_przekaźnika)
*   [4 Uruchamianie Tora w Chroot](#Uruchamianie_Tora_w_Chroot)
*   [5 Uruchamianie Tora w kontenerze systemd-nspawn z wirtualnym interfejsem sieciowym](#Uruchamianie_Tora_w_kontenerze_systemd-nspawn_z_wirtualnym_interfejsem_sieciowym)
    *   [5.1 Instalacja i konfiguracja hosta](#Instalacja_i_konfiguracja_hosta)
        *   [5.1.1 Wirtualny interfejs sieciowy](#Wirtualny_interfejs_sieciowy)
        *   [5.1.2 Uruchom i włącz systemd-nspawn](#Uruchom_i_włącz_systemd-nspawn)
*   [6 Usage](#Usage)
*   [7 Web browsing](#Web_browsing)
    *   [7.1 Firefox](#Firefox)
    *   [7.2 Chromium](#Chromium)
        *   [7.2.1 Debug](#Debug)
        *   [7.2.2 Rozbudowa](#Rozbudowa)
    *   [7.3 Luakit](#Luakit)
*   [8 HTTP proxy](#HTTP_proxy)
    *   [8.1 Firefox](#Firefox_2)
    *   [8.2 Polipo](#Polipo)
    *   [8.3 Privoxy](#Privoxy)
*   [9 komunikatory](#komunikatory)
    *   [9.1 Pidgin](#Pidgin)
*   [10 Irssi](#Irssi)
*   [11 Pacman](#Pacman)
*   [12 Uruchamianie serwera Tor](#Uruchamianie_serwera_Tor)
    *   [12.1 Uruchamianie mostka Tora](#Uruchamianie_mostka_Tora)
        *   [12.1.1 Konfiguracja](#Konfiguracja_2)
    *   [12.2 Uruchamianie przekaźnika Tora](#Uruchamianie_przekaźnika_Tora)
        *   [12.2.1 Konfiguracja](#Konfiguracja_3)
    *   [12.3 Uruchomienie węzła wyjściowego Tora](#Uruchomienie_węzła_wyjściowego_Tora)
        *   [12.3.1 Konfiguracja](#Konfiguracja_4)
        *   [12.3.2 +100Mbps Exit Relay configuration example](#+100Mbps_Exit_Relay_configuration_example)
            *   [12.3.2.1 Tor](#Tor)
                *   [12.3.2.1.1 Podnieś maksymalną liczbę otwartych deskryptorów plików](#Podnieś_maksymalną_liczbę_otwartych_deskryptorów_plików)
                *   [12.3.2.1.2 Uruchom tor.service jako root, aby powiązać Tora z portami uprzywilejowanymi](#Uruchom_tor.service_jako_root,_aby_powiązać_Tora_z_portami_uprzywilejowanymi)
                *   [12.3.2.1.3 Konfiguracja Tora](#Konfiguracja_Tora)
            *   [12.3.2.2 arm](#arm)
            *   [12.3.2.3 iptables](#iptables)
            *   [12.3.2.4 Haveged](#Haveged)
            *   [12.3.2.5 pdnsd](#pdnsd)
                *   [12.3.2.5.1 Nieocenzurowany DNS](#Nieocenzurowany_DNS)
*   [13 TorDNS](#TorDNS)
    *   [13.1 Używanie TorDNS do wszystkich zapytań DNS](#Używanie_TorDNS_do_wszystkich_zapytań_DNS)
*   [14 Torsocks](#Torsocks)
*   [15 Transparent Torification](#Transparent_Torification)
*   [16 Porady i wskazówki](#Porady_i_wskazówki)
    *   [16.1 Możliwości jądra](#Możliwości_jądra)
*   [17 Rozwiązywanie problemów](#Rozwiązywanie_problemów)
    *   [17.1 Problem z wartością użytkownika](#Problem_z_wartością_użytkownika)

## Wprowadzenie

Użytkownicy sieci Tor uruchamiają serwer proxy na swoim komputerze. Oprogramowanie to łączy się z siecią Tor, okresowo negocjuje obwód wirtualny przez sieć Tor. Tor wykorzystuje kryptografię w sposób warstwowy podobnie do warstw cebuli zapewniając idealną tajemnicę między routerami. Oprogramowanie proxy tora posiada też interfejs SOCKS dla swoich klientów. Aplikacje SOCKS-aware mogą być skierowane do sieci Tor, który następnie przepuszcza ruch przez wirtualny obwód Tora. Dzięki temu tor daje anonimowość użytkownika końcowego.

anonimowość jest uzyskana dzięki szyfrowaniu ruchu, tor wysyła zaszyfrowane pakiety przez inne węzły sieci i odszyfrowuje je na ostatnim węźle, aby odebrać ruch przed przekazaniem go do określonego serwera.

Jednym z wyzwań, które należy wykonać dla anonimowości Tor, jest to, że może to być znacznie wolniejsze niż bezpośrednie połączenie ze względu na dużą liczbę ponownych trasowania ruchu

Dodatkowo, chociaż Tor zapewnia ochronę przed analizą ruchu, nie może zapobiec potwierdzeniu ruchu na granicy sieci Tora (tj. Ruchu wchodzącego i wychodzącego z sieci).

## Instalacja

## Konfiguracja

Domyślnie Tor czyta konfiguracje z pliku `/etc/tor/torrc` Opcje konfiguracji są wyjaśnione [tor(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/tor.1) [Strona Tor](https://torproject.org/docs/tor-manual.html.en). Domyślna konfiguracja powinna działać prawidłowo dla większości użytkowników Tora.

Istnieją potencjalne konflikty między konfiguracjami w `torrc` a `tor.service`.

*   W `torrc`, `RunAsDaemon` Powinno, jako domyślnie, być ustawione na `0`, since `Type=simple` Jest ustawiony w `[Service]` Sekcji w `tor.service`.
*   W `torrc`, `User` Nie powinien być ustawiony, chyba że `User=` jest ustawione na `root` w `[Service]` Sekcji w `tor.service`.

### Konfiguracja przekaźnika

Maksymalny numer deskryptora pliku, który może być otwarty przez Tora, można ustawić za pomocą `LimitNOFILE` i `tor.service` Szybkie przekaźniki mogą chcieć zwiększyć tę wartość.

Jeśli na komputerze nie jest uruchomiony serwer WWW, a Ty nie ustawiłeś `AccountingMax`, rozważ zmianę `ORPort` na `443` lub `DirPort` na `80`. Wielu użytkowników Tora utknęło za zaporami ogniowymi, które pozwalają im tylko przeglądać Internet, a ta zmiana pozwoli im dotrzeć do przekaźnika Tora. Jeśli używasz już portów `80` i `443`, inne przydatne porty to `22`, `110` i `143`. [1] Ale ponieważ są to uprzywilejowane porty, aby to zrobić, Tor musi działać jako root, ustawiając `User=root` na `tor.service` i `User tor` w `torrc`.

Możesz przejrzeć cykl życia dokumentacji nowego przekaźnika Tor.

## Uruchamianie Tora w Chroot

**Warning:** Połączenie z telnetem do lokalnego portu ControlPort wydaje się być zepsute podczas działania Tora w chroot

Ze względów bezpieczeństwa może być pożądane uruchomienie Tora w [chroot](/index.php/Chroot "Chroot"). Poniższy skrypt stworzy odpowiedni chroot w `/opt/torchroot`:

 `~/torchroot-setup.sh` 
```
#!/bin/bash
export TORCHROOT=/opt/torchroot

mkdir -p $TORCHROOT
mkdir -p $TORCHROOT/etc/tor
mkdir -p $TORCHROOT/dev
mkdir -p $TORCHROOT/usr/bin
mkdir -p $TORCHROOT/usr/lib
mkdir -p $TORCHROOT/usr/share/tor
mkdir -p $TORCHROOT/var/lib

ln -s /usr/lib  $TORCHROOT/lib
cp /etc/hosts           $TORCHROOT/etc/
cp /etc/host.conf       $TORCHROOT/etc/
cp /etc/localtime       $TORCHROOT/etc/
cp /etc/nsswitch.conf   $TORCHROOT/etc/
cp /etc/resolv.conf     $TORCHROOT/etc/
cp /etc/tor/torrc       $TORCHROOT/etc/tor/

cp /usr/bin/tor         $TORCHROOT/usr/bin/
cp /usr/share/tor/geoip* $TORCHROOT/usr/share/tor/
cp /lib/libnss* /lib/libnsl* /lib/ld-linux-*.so* /lib/libresolv* /lib/libgcc_s.so* $TORCHROOT/usr/lib/
cp $(ldd /usr/bin/tor | awk '{print $3}'|grep --color=never "^/") $TORCHROOT/usr/lib/
cp -r /var/lib/tor      $TORCHROOT/var/lib/
chown -R tor:tor $TORCHROOT/var/lib/tor

sh -c "grep --color=never ^tor /etc/passwd > $TORCHROOT/etc/passwd"
sh -c "grep --color=never ^tor /etc/group > $TORCHROOT/etc/group"

mknod -m 644 $TORCHROOT/dev/random c 1 8
mknod -m 644 $TORCHROOT/dev/urandom c 1 9
mknod -m 666 $TORCHROOT/dev/null c 1 3

if [[ "$(uname -m)" == "x86_64" ]]; then
  cp /usr/lib/ld-linux-x86-64.so* $TORCHROOT/usr/lib/.
  ln -sr /usr/lib64 $TORCHROOT/lib64
  ln -s $TORCHROOT/usr/lib ${TORCHROOT}/usr/lib64
fi

```

Po uruchomieniu skryptu jako root, Tor może zostać uruchomiony w [chroot](/index.php/Chroot "Chroot") za pomocą polecenia:

```
# chroot --userspec=tor:tor /opt/torchroot /usr/bin/tor

```

lub jeśli używasz Systemd przeładowywać usługę:

 `/etc/systemd/system/tor.service.d/chroot.conf` 
```
[Service]
User=root
ExecStart=
ExecStart=/usr/bin/sh -c "chroot --userspec=tor:tor /opt/torchroot /usr/bin/tor -f /etc/tor/torrc"
KillSignal=SIGINT
```

## Uruchamianie Tora w kontenerze systemd-nspawn z wirtualnym interfejsem sieciowym

W tym przykładzie utworzymy kontener [systemd-nspawn](/index.php/Systemd-nspawn "Systemd-nspawn") o nazwie `tor-exit` z wirtualnym interfejsem sieciowym macvlan.

Zobacz [Systemd-nspawn](/index.php/Systemd-nspawn "Systemd-nspawn") i [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd"), aby uzyskać pełną dokumentację.

### Instalacja i konfiguracja hosta

W tym przykładzie pojemnik znajdować się w `/srv/container`:

```
# mkdir /srv/container/tor-exit

```

[Install](/index.php/Install "Install") the [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts).

Install [base](https://www.archlinux.org/groups/x86_64/base/), [tor](https://www.archlinux.org/packages/?name=tor) and [arm](https://www.archlinux.org/packages/?name=arm) and deselect [linux](https://www.archlinux.org/packages/?name=linux) as per [Systemd-nspawn#Create and boot a minimal Arch Linux distribution in a container](/index.php/Systemd-nspawn#Create_and_boot_a_minimal_Arch_Linux_distribution_in_a_container "Systemd-nspawn"):

```
# pacstrap -i -c -d /srv/container/tor-exit base tor arm

```

Create directory if it does not exist:

```
# mkdir /var/lib/container

```

**Note:** Symlinks for `nspawn` are currently broken (as of 2016-02-04; see [https://github.com/systemd/systemd/issues/2001](https://github.com/systemd/systemd/issues/2001)), and will give you a "too many levels of symlinks" error. As a (possibly insecure) workaround, simply pacstrap your install to the container directory instead.

Symlink to register the container on the host, as per [Systemd-nspawn#Enable container on boot](/index.php/Systemd-nspawn#Enable_container_on_boot "Systemd-nspawn"):

```
# ln -s /srv/container/tor-exit /var/lib/container/tor-exit

```

#### Wirtualny interfejs sieciowy

Utwórz katalog DropIn dla usługi kontenera:

```
# mkdir /etc/systemd/system/systemd-nspawn@tor-exit.service.d

```
 `/etc/systemd/system/systemd-nspawn@tor-exit.service.d/tor-exit.conf` 
```
[Service]
ExecStart=
ExecStart=/usr/bin/systemd-nspawn --quiet --keep-unit --boot --link-journal=guest --network-macvlan=$INTERFACE --private-network --directory=/var/lib/container/%i
LimitNOFILE=32768
```

`--network-macvlan=$INTERFACE --private-network` automagicznie tworzy nazwę macvlan `mv-$INTERFACE` wewnątrz kontenera, który nie jest widoczny z hosta. `--private-network` jest implikowane przez `--network-macvlan=` zgodnie z [systemd-nspawn(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-nspawn.1). Jest to wskazane ze względów bezpieczeństwa, ponieważ pozwoli ci podać prywatny adres IP do kontenera i nie będzie wiedział, jakie jest IP twojego komputera. Pomoże to ukryć żądania DNS.

`LimitNOFILE=32768` per [#Raise maximum number of open file descriptors](#Raise_maximum_number_of_open_file_descriptors).

Ustaw [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") zgodnie z twoją siecią w `/srv/container/tor-exit/etc/systemd/network/mv-$INTERFACE.network`.

#### Uruchom i włącz systemd-nspawn

[Start](/index.php/Start "Start") i włącz `systemd-nspawn@tor-exit.service`.

## Usage

Uruchom / włącz `tor.service` [using systemd](/index.php/Systemd#Using_units "Systemd"). Możesz też uruchomić go przy pomocy `sudo -u tor /usr/bin/tor`.

Aby użyć programu, skonfiguruj go do użycia `127.0.0.1` lub localhost jako serwer proxy SOCKS5, z portem `9050` (zwykły tor z ustawieniami standardowymi). Aby sprawdzić, czy Tor działa poprawnie, odwiedź stronę [Tor](https://check.torproject.org/), [Harvard](http://serifos.eecs.harvard.edu/cgi-bin/ipaddr.pl?tor=1) lub [Xenobite.eu](https://torcheck.xenobite.eu/) websites.

## Web browsing

Projekt Tor obsługuje obecnie przeglądanie stron internetowych za pomocą [Tor Browser](https://aur.archlinux.org/packages/?K=tor-browser), które można pobrać z AUR. Jest on zbudowany z poprawioną wersją rozszerzonych wydań Firefoksa. Tora można również używać ze zwykłymi przeglądarkami [Firefox](/index.php/Firefox "Firefox"), [Chromium](/index.php/Chromium "Chromium") i innymi przeglądarkami.

**Warning:** Projekt Tor zdecydowanie zaleca używanie przeglądarki Tora, jeśli chcesz pozostać anonimowy [[1]](https://www.torproject.org/docs/faq.html.en#TBBOtherBrowser)

**Tip:** Aby makepkg zweryfikował podpis w archiwum źródła AUR dla TBB, zaimportuj plik [podpisywanie kluczy z projektu Tor](https://www.torproject.org/docs/signing-keys.html.en) (currently 2E1AC68ED40814E0) jak wyjaśniono w [GnuPG#Use a keyserver](/index.php/GnuPG#Use_a_keyserver "GnuPG").

### Firefox

In *Preferencje > Ogólne > Proxy sieciowe > Ustawienia* Wybierz *Ręczna konfiguracja serwerów proxy* i wprowadź host SOCKS `localhost` z portem `9050` (SOCKS v5). Aby skierować wszystkie żądania DNS poprzez Socks Proxy Tora zaznacz także *Proxy DNS podczas używania z SOCKS v5*.

**Note:** Podczas korzystania z przeglądarki Firefox 55 lub wcześniejszej (na przykład 52 ESR) ustawienia znajdują się w Preferencje> Zaawansowane> Sieć> Ustawienia.

### Chromium

Możesz po prostu uruchomić:

```
$ chromium --proxy-server="socks5://myproxy:8080" --host-resolver-rules="MAP * ~NOTFOUND , EXCLUDE myproxy"

```

The `--proxy-server="socks5://myproxy:8080"` flaga mówi Chrome, aby wysłać wszystko `http://` i `https://` Żądania URL przez serwer proxy SOCKS `"myproxy:8080"`, przy użyciu wersji 5 protokołu SOCKS. Nazwa hosta dla tych adresów URL zostanie rozwiązana przez serwer proxy, a nie lokalnie przez Chrome.

**Warning:** Proxying of `ftp://` URLs through a SOCKS proxy is not yet implemented[[2]](https://www.chromium.org/developers/design-documents/network-stack/socks-proxy).

The `--proxy-server` flaga dotyczy tylko ładowań adresów URL. Istnieją inne składniki przeglądarki Chrome, które mogą bezpośrednio rozwiązać problem DNS, a tym samym ominąć ten serwer proxy. Najbardziej znaczącym takim komponentem jest "Prefetcher DNS". W związku z tym, jeśli pobieranie z wyprzedzeniem DNS nie jest wyłączone w Chrome, nadal będą wyświetlane lokalne żądania DNS przez Chrome, mimo że określiłeś serwer proxy SOCKS v5\. Wyłączenie wstępnego pobierania DNS rozwiąże ten problem, ale jest to kruche rozwiązanie, ponieważ trzeba pamiętać o wszystkich obszarach w Chrome, które wysyłają surowe żądania DNS. Aby rozwiązać ten problem, następna flaga, `--host-resolver-rules="MAP * ~NOTFOUND , EXCLUDE myproxy"`, to wszystko, aby Chrome nie wysyłał żądań DNS przez sieć. Mówi, że wszystkie rozwiązania DNS mają być po prostu odwzorowane na (nieprawidłowy) adres `~NOTFOUND` (think of it as `0.0.0.0`). The `"EXCLUDE"` klauzula zrobić wyjątek dla `"myproxy"`, ponieważ w przeciwnym razie Chrome nie byłby w stanie rozwiązać adresu samego serwera proxy SOCKS, a wszystkie żądania musiałyby zawodzić `PROXY_CONNECTION_FAILED`.

Aby zapobiec [WebRTC leak](https://ipleak.net/#webrtcleak)możesz zainstalować rozszerzenie [WebRTC Network Limiter](https://chrome.google.com/webstore/detail/webrtc-network-limiter/npeicpdbkakmehahjeeohfdhnlpdklia).

#### Debug

Pierwszą rzeczą, którą należy sprawdzić podczas debugowania, jest karta Proxy na temat: net-internals i sprawdź, jakie są efektywne ustawienia proxy: `chrome://net-internals/#proxy`

Następnie spójrz na kartę DNS w `about:net-internals` aby upewnić się, że Chrome nie wydaje lokalnych odpowiedzi DNS: `chrome://net-internals/#dns`

#### Rozbudowa

Podobnie jak w Firefoksie, możesz skonfigurować szybki przełącznik, na przykład poprzez [Proxy SwitchySharp](https://chrome.google.com/webstore/detail/dpplabbmogkhghncfbfdeeokoefdjegm).

Po zainstalowaniu wejdź na jego stronę konfiguracji. W zakładce "Profile Proxy" dodaj nowy profil "Tor", jeśli zaznaczone, odznacz opcję "" Użyj tego samego serwera proxy dla wszystkich protokołów ", następnie dodaj" localhost "jako Host SOCKS," " 9050 *do odpowiedniego portu i wybierz "SOCKS v5".*

Opcjonalnie możesz włączyć szybkie przełączanie w zakładce "Ogólne", aby móc przełączać pomiędzy normalną nawigacją a siecią Tor, klikając lewym przyciskiem myszy ikonę Proxy SwitchySharp.

### Luakit

**Warning:** Obserwator nie będzie miał trudności z identyfikacją cię przez rzadki ciąg agenta użytkownika i mogą występować dalsze problemy z Flash, JavaScript lub podobnym.

Możesz po prostu uruchomić:

```
$ torsocks luakit

```

## HTTP proxy

Tor może być używany z proxy HTTP takim jak [Polipo](/index.php/Polipo "Polipo") lub [Privoxy](/index.php/Privoxy "Privoxy"), jednak zespół deweloperów Tor zaleca korzystanie z biblioteki SOCKS5, ponieważ przeglądarki bezpośrednio ją obsługują.

### Firefox

Dodatek FoxyProxy umożliwia określenie wielu serwerów proxy dla różnych adresów URL lub dla wszystkich przeglądanych stron. Po ponownym uruchomieniu przeglądarki Firefox ręcznie ustaw Firefoxa na port `8118` na `localhost` czyli w miejscu, gdzie działają [Polipo](/index.php/Polipo "Polipo") lub [Privoxy](/index.php/Privoxy "Privoxy"). Te ustawienia można uzyskać w opcji Dodaj> Standardowy typ proxy. Wybierz etykietę serwera proxy (np. Tor) i wprowadź port i hosta w polach Proxy HTTP i SSL Proxy. Aby sprawdzić, czy Tor działa poprawnie, odwiedź stronę Tor Check i przełącz Tor'a.

### Polipo

Projekt Tor utworzył niestandardowy [plik konfiguracyjny Polipo](https://gitweb.torproject.org/torbrowser.git/plain/build-scripts/config/polipo.conf?id=1ffcd9dafb9dd76c3a29dd686e05a71a95599fb5), aby zapobiec potencjalnym problemom z Polipo, a także zapewnić lepszą anonimowość

Pamiętaj, że Polipo nie jest wymagany, jeśli możesz użyć proxy SOCKS 5, które Tor uruchamia się automatycznie na porcie 9050\. Jeśli chcesz używać Chromium z Tor, nie potrzebujesz pakietu Polipo (patrz: [#Chromium](#Chromium)).

### Privoxy

Możesz także użyć tej konfiguracji w innych aplikacjach, takich jak przesyłanie wiadomości (np. Jabber, IRC). Aplikacje obsługujące serwery proxy HTTP, które można podłączyć do Privoxy (tj. `127.0.0.1:8118`). Aby bezpośrednio używać proxy SOCKS, możesz wskazać swoją aplikację w Tora (tj. `127.0.0.1:9050`). Problem z tą metodą polega jednak na tym, że aplikacje wykonujące DNS samodzielnie mogą powodować wyciek informacji. Rozważ użycie Socks4A (np. Z Privoxy).

## komunikatory

Aby korzystać z komunikatora internetowego, nie potrzebujemy proxy http, takiego jak [polipo](/index.php/Polipo "Polipo")/[privoxy](/index.php/Privoxy "Privoxy"). Będziemy używać demona tor'a bezpośrednio, który domyślnie nasłuchuje na porcie 9050.

### Pidgin

Możesz skonfigurować Pidgin do korzystania z Tora globalnie lub na konto. Aby używać Tora globalnie, przejdź do Narzędzia -> Preferencje -> Proxy. Aby używać Tora dla określonych kont, przejdź do sekcji "Konta> Zarządzaj kontami", wybierz żądane konto, kliknij przycisk Modyfikuj, a następnie przejdź do karty Proxy. Ustawienia serwera proxy są następujące:

```
Proxy type SOCKS5
Host 127.0.0.1
Port 9150

```

## Irssi

Freenode recommends connecting to `.onion` directly. It also requires charybdis and ircd-seven's SASL mechanism for identifying to nickserv during connection; see [Irssi#Authenticating with SASL](/index.php/Irssi#Authenticating_with_SASL "Irssi"). Start irssi:

```
$ torsocks irssi

```

Set your identification to nickserv, which will be read when connecting. Supported mechanisms are ECDSA-NIST256P-CHALLENGE (see [ecdsatool](https://github.com/atheme/ecdsatool/blob/master/cap_sasl.pl)) and PLAIN. DH-BLOWFISH is [no longer supported](https://freenode.net/sasl/sasl-irssi.shtml).

```
/sasl set *network* *username* *password* *mechanism*

```

Disable CTCP and DCC and set a different hostname to prevent information disclosure: [[3]](https://encrypteverything.ca/IRC_Anonymity_Guide)

```
/ignore * CTCPS
/ignore * DCC
/set hostname *fake_host*

```

Connect to Freenode:

```
/connect -network *network* frxleqtzgvwkv7oz.onion

```

For more information check [Accessing freenode Via Tor](http://freenode.net/irc_servers.shtml#tor), [SASL README](http://freenode.net/sasl/README.txt) or [IRC/SILC Wiki article](https://trac.torproject.org/projects/tor/wiki/doc/TorifyHOWTO/IrcSilc).

## Pacman

Operacje pobierania Pacmana (bazy danych repozytorium, pakiety i klucze publiczne) można wykonywać za pomocą sieci Tor.

Zalety:

*   Osoby atakujące, które mogą monitorować twoje połączenie internetowe i które są skierowane konkretnie do twojego komputera, nie mogą już oglądać aktualizacji i z tego powodu nie mogą wydedukować pakietów, które zainstalowałeś, jak są aktualne, kiedy i jak często je aktualizujesz. Osoba atakująca może się jeszcze dowiedzieć, jakie oprogramowanie i wersje używasz innymi metodami, na przykład podczas oglądania pakietów z serwera http lub sprawdzania, czy urządzenie pokaże, że masz zainstalowany serwer HTTP i jego wersję.
*   Jeśli zwierciadło nie jest cebulką, złośliwe węzły wyjściowe, przez które przechodzisz, mogą oglądać aktualizacje i mogą zdecydować się na atak, jednak prawdopodobnie nie będą wiedzieć, kto atakuje..
*   Atakujący próbujący sprawić, że twoja maszyna uwierzy, że nie ma żadnych nowych aktualizacji, aby uniemożliwić mu uzyskanie poprawek bezpieczeństwa, będzie miał trudniejszy czas, ponieważ nie mogą one konkretnie kierować na twoją maszynę.

Wady:

*   Dłuższe czasy aktualizacji ze względu na dłuższe opóźnienia i mniejszą przepustowość. Może to stanowić duże zagrożenie dla bezpieczeństwa, jeśli aktualizacje będą musiały być wykonane tak szybko, jak to możliwe, szczególnie na komputerach podłączonych bezpośrednio do Internetu. Tak jest w przypadku ogromnej luki w zabezpieczeniach i że błędy są szybkie do sondowania, łatwe do wykorzystania, a napastnicy już rozpoczęli atakowanie tak wielu systemów, jak tylko mogą, zanim systemy zostaną zaktualizowane.

Niezawodność z Tor:

*   Nie potrzebujesz już działającego DNS.
*   Jesteś zależny od sieci Tor i węzłów wyjściowych, które nie blokują aktualizacji.
*   Jesteś zależny od demona Tora, aby działał poprawnie. Demon Tora może nie działać, jeśli nie ma do niego więcej miejsca na dysku. "Zarezerwowane bloki gid:" w ext4, przydziałach lub w inny sposób mogą to naprawić.
*   Jeśli jesteś w kraju, w którym Tor jest zablokowany lub w ogóle nie ma żadnych użytkowników Tor, powinieneś użyć mostów.

Uwaga na GPG:

W magazynie archim, pacman ufaj tylko kluczom, które są podpisane przez ciebie (Można to zrobić za pomocą klawisza pacman -lub-klucz) lub podpisane przez 3 z 5 kluczy Arch master. Jeśli złośliwy węzeł wyjściowy zastąpi pakiety tymi, które zostały podpisane przez jego klucz, pacman nie pozwoli użytkownikowi zainstalować pakietu.

 `/etc/pacman.conf` 
```
...
XferCommand = /usr/bin/curl --socks5-hostname localhost:9050 -C - -f %u > %o
...
```

## Uruchamianie serwera Tor

Sieć Tor jest zależna od ludzi, którzy wnoszą przepustowość i konfigurują usługi. Istnieje kilka sposobów na wniesienie wkładu do sieci.

### Uruchamianie mostka Tora

Mostki Tora jest przekaźnikiem sieci Tor, który nie jest wymieniony w publicznym katalogu Tora, umożliwiając tym ludziom łączenie się z siecią Tor, gdy rządy lub dostawcy usług internetowych blokują wszystkie publiczne przekaźniki Tora.

#### Konfiguracja

Zgodnie z [https://www.torproject.org/docs/bridges](https://www.torproject.org/docs/bridges), Stwórz swój `torrc` być tylko tymi czterema liniami (Domyślnie: `/etc/tor/torrc`, i `$HOME/.torrc` jeśli ten plik nie zostanie znaleziony)

```
   SocksPort 0
   ORPort 443
   BridgeRelay 1
   Exitpolicy reject *:*

```

### Uruchamianie przekaźnika Tora

Oznacza to, że twoja maszyna będzie działać jako węzeł wejściowy lub przekaźnik przekazujący i, w przeciwieństwie do mostu, będzie wymieniony w publicznym katalogu Tora. Twój adres IP będzie publicznie widoczny w katalogu Tor, ale przekaźnik będzie przekazywał tylko do innych przekaźników lub węzłów wyjściowych Tora, a nie bezpośrednio do Internetu.

#### Konfiguracja

Powinieneś przynajmniej podzielić 20 KB / s:

```
Nickname *tornickname*
ORPort 9001                    # This TCP-Port has to be opened/forwarded in your Firewall
BandwidthRate 20 KB            # Throttle traffic to 20KB/s
BandwidthBurst 50 KB           # But allow bursts up to 50KB/s

```

Nie pozwalaj wyjść z Twojego przekaźnika:

```
ExitPolicy reject *:*

```

### Uruchomienie węzła wyjściowego Tora

Wszelkie żądania od użytkownika Tora do zwykłego Internetu oczywiście muszą gdzieś wyjść z sieci, a węzły wyjściowe zapewniają tę istotną usługę. Na dostępnym hoście, żądanie pojawi się jako pochodzące z twojego komputera. Oznacza to, że uruchomienie węzła wyjściowego jest ogólnie uważane za bardziej uciążliwe pod względem prawnym niż uruchamianie innych form przekaźników Tora. Zanim staniesz się przekaźnikiem wyjścia, możesz przeczytać [Wskazówki dotyczące uruchamiania węzła wyjściowego przy minimalnym szykanowaniu.](https://blog.torproject.org/running-exit-node).

#### Konfiguracja

Za pomocą narzędzia torrc można skonfigurować usługi, które mają być dozwolone za pośrednictwem węzła wyjściowego. Zezwalaj na cały ruch:

```
ExitPolicy accept *:*

```

Zezwalaj tylko portom irc 6660-6667 na wychodzenie z węzła:

```
ExitPolicy accept *:6660-6667,reject *:* # Allow irc ports but no more

```

Domyślnie Tor blokuje niektóre porty. Możesz użyć torrc, aby to przesłonić.

```
ExitPolicy accept *:119        # Accept nntp as well as default exit policy

```

#### +100Mbps Exit Relay configuration example

If you run a fast exit relay (+100Mbps) with `ORPort 443` and `DirPort 80` (as recommended in [Configuring a Tor relay on Debian/Ubuntu](http://www.torproject.org/docs/tor-relay-debian.html.en#after)) the following configuration changes might serve as inspiration to setup Tor alongside [iptables](/index.php/Iptables "Iptables") firewall, [Haveged](/index.php/Haveged "Haveged") to increase system entropy and [pdnsd](/index.php/Pdnsd "Pdnsd") as DNS cache. It is important to *first* read [Configuring a Tor relay on Debian/Ubuntu](http://www.torproject.org/docs/tor-relay-debian.html.en#after).

**Note:** See [#Running Tor in a systemd-nspawn container with a virtual network interface](#Running_Tor_in_a_systemd-nspawn_container_with_a_virtual_network_interface) for instructions to install Tor in a `systemd-nspawn` container. [Haveged](/index.php/Haveged "Haveged") should be installed on the container host.

##### Tor

###### Podnieś maksymalną liczbę otwartych deskryptorów plików

Aby obsłużyć więcej niż 8192 połączeń, `LimitNOFILE` można zwiększyć do 32768 w trybie [Tor FAQ](https://www.torproject.org/docs/faq.html.en#PackagedTor).

 `/etc/systemd/system/tor.service.d/increase-file-limits.conf` 
```
[Service]
LimitNOFILE=32768
```

Aby z powodzeniem podnieść `nofile` limit, możesz również dołączyć następujące elementy:

 `/etc/security/limits.conf` 
```
...
tor     soft    nofile    32768
tor     hard    nofile    32768
@tor    soft    nofile    32768
@tor    hard    nofile    32768

```

Sprawdź, czy limit `nofile` (filedescriptor) został pomyślnie podniesiony za pomocą `# sudo -u tor 'ulimit -Hn'` lub `# sudo -u tor bash` i `# ulimit -Hn`.

###### Uruchom tor.service jako root, aby powiązać Tora z portami uprzywilejowanymi

Aby powiązać Tora z portami uprzywilejowanymi, usługa musi zostać uruchomiona jako root. Proszę sprecyzuj `User tor` opcja w `/etc/tor/torrc`.

 `/etc/systemd/system/tor.service.d/start-as-root.conf` 
```
[Service]
User=root
```

###### Konfiguracja Tora

Aby nasłuchiwać na portach 80 i 443, usługa musi być uruchomiona jako `root`, jak opisano w [#Uruchom tor.service jako root, aby powiązać Tora z portami uprzywilejowanymi](#Uruchom_tor.service_jako_root,_aby_powiązać_Tora_z_portami_uprzywilejowanymi). Użyj opcji User tor w `/etc/tor/torrc`, aby właściwie zmniejszyć uprawnienia Tora.

 `/etc/tor/torrc` 
```
SocksPort 0                                       ## Pure relay configuration without local socks proxy

Log notice stdout                                 ## Default Tor behavior

ControlPort 9051                                  ## For arm connection
CookieAuthentication 1                            ## For arm connection

ORPort 443                                        ## Service must be started as root

Address $IP                                       ## IP or FQDN
Nickname $NICKNAME                                ## Nickname displayed in [Onionoo](https://onionoo.torproject.org/)

RelayBandwidthRate 500 Mbits                      ## bytes/KBytes/MBytes/GBytes/KBits/MBits/GBits
RelayBandwidthBurst 1000 MBits                    ## bytes/KBytes/MBytes/GBytes/KBits/MBits/GBits

ContactInfo $E-MAIL - $BTC-ADDRESS                ## See [OnionTip](https://oniontip.com/)

DirPort 80                                        ## Service must be started as root
DirPortFrontPage /etc/tor/tor-exit-notice.html    ## Original: [https://gitweb.torproject.org/tor.git/plain/contrib/operator-tools/tor-exit-notice.html](https://gitweb.torproject.org/tor.git/plain/contrib/operator-tools/tor-exit-notice.html)

MyFamily $($KEYID),$($KEYID)...                   ## Remember $ in front of keyid(s) ;)

ExitPolicy reject XXX.XXX.XXX.XXX/XX:*            ## Block domain of public IP in addition to std. exit policy

User tor                                          ## Return to tor user after service started as root to listen on privileged ports

DisableDebuggerAttachment 0                       ## For arm connection

### Performance related options ###
AvoidDiskWrites 1                                 ## Reduce wear on SSD
DisableAllSwap 1                                  ## Service must be started as root
HardwareAccel 1                                   ## Look for OpenSSL hardware cryptographic support
NumCPUs 2                                         ## Only start two threads
```

Ta konfiguracja jest oparta na [Tor Manual](https://www.torproject.org/docs/tor-manual.html.en).

Tor domyślnie otwiera proxy soks dla portu 9050 - nawet jeśli go nie skonfigurujesz. Ustaw `SocksPort 0`, jeśli planujesz uruchomić Tor tylko jako przekaźnik, i nie nawiązywać żadnych lokalnych połączeń aplikacji.

`Log notice stdout` zmienia logowanie na standardowe wyjście, które jest także domyślnym ustawieniem Tora. `ControlPort 9051`, `CookieAuthentication 1` i `DisableDebuggerAttachment 0` pozwala [arm](https://www.archlinux.org/packages/?name=arm) aby połączyć się z Torem i wyświetlić połączenia.

`ORPort 443` i `DirPort 80` pozwala Torowi słuchać na portach 443 i 80 oraz `DirPortFrontPage` wyświetla [tor-exit-notice.html](https://gitweb.torproject.org/tor.git/plain/contrib/operator-tools/tor-exit-notice.html) na porcie 80.

`ExitPolicy reject XXX.XXX.XXX.XXX/XX:*` powinien odzwierciedlać publiczny adres IP i maskę sieci, które można uzyskać za pomocą polecenia `# ip addr`,więc połączenia wyjściowe nie mogą łączyć się z hostem lub sąsiednimi komputerami publicznym IP i ominąć zapory ogniowe.

`AvoidDiskWrites 1` redukuje zapisy dysku i zużycie SSD. `DisableAllSwap 1` "spróbuje zablokować wszystkie obecne i przyszłe strony pamięci, aby pamięć nie mogła być stronicowana".

Jeśli `# cat /proc/cpuinfo` zwraca, że twój procesor obsługuje instrukcje AES i `# lsmod` zwraca, że moduł jest załadowany, możesz określić `HardwareAccel 1` która próbuje "użyć wbudowanej (statycznej) akceleracji sprzętowej kryptografii, gdy jest dostępna", zobacz [http://www.torservers.net/wiki/setup/server#aes-ni_crypto_acceleration](http://www.torservers.net/wiki/setup/server#aes-ni_crypto_acceleration).

`ORPort 443`, `DirPort 80` i `DisableAllSwap 1` wymaga uruchomienia usługi Tora jako `root` as described in [#Uruchom tor.service jako root, aby powiązać Tora z portami uprzywilejowanymi](#Uruchom_tor.service_jako_root,_aby_powiązać_Tora_z_portami_uprzywilejowanymi). Użyj `User tor` opcja właściwego zmniejszenia uprawnień Tora.

##### arm

Jeśli `ControlPort 9051` i `CookieAuthentication 1` jest określony w `/etc/tor/torrc`, [arm](https://www.archlinux.org/packages/?name=arm) można zacząć z `sudo -u tor arm`. Jeśli chcesz oglądać połączenia Tora w [arm](https://www.archlinux.org/packages/?name=arm) `DisableDebuggerAttachment 0` należy również określić.

##### iptables

Skonfiguruj i naucz się korzystać z [iptables](/index.php/Iptables "Iptables"). [Simple stateful firewall](/index.php/Simple_stateful_firewall "Simple stateful firewall"), w której śledzenie połączeń musiałoby śledzić tysiące połączeń w wyjściowym przekaźniku tor, ta konfiguracja zapory jest bezpaństwowa..

 `/etc/iptables/iptables.rules` 
```
*raw
-A PREROUTING -j NOTRACK
-A OUTPUT -j NOTRACK
COMMIT

*filter
:INPUT DROP [0:0]
:FORWARD DROP [0:0]
:OUTPUT ACCEPT [0:0]
-A INPUT -p tcp ! --syn -j ACCEPT
-A INPUT -p udp -j ACCEPT
-A INPUT -p icmp -j ACCEPT
-A INPUT -p tcp --dport 443 -j ACCEPT
-A INPUT -p tcp --dport 80 -j ACCEPT
-A INPUT -i lo -j ACCEPT
COMMIT
```

`-A PREROUTING -j NOTRACK` i `-A OUTPUT -j NOTRACK` wyłącza śledzenie połączeń w `raw` table.

`:INPUT DROP [0:0]` jest domyślny `INPUT` cel i opuszcza ruch wejściowy, którego nie robimy `ACCEPT`.

`:FORWARD DROP [0:0]` jest domyślny `FORWARD` cel i ma znaczenie tylko wtedy, gdy host jest normalnym routerem, a nie hostem, który jest routerem cebulowym.

`:OUTPUT ACCEPT [0:0]` jest domyślny `OUTPUT` cel i pozwala na wszystkie połączenia wychodzące.

`-A INPUT -p tcp ! --syn -j ACCEPT` zezwól na już ustanowione przychodzące połączenia TCP zgodnie z poniższymi regułami i połączeniami TCP ustanowionymi z węzła wyjściowego.

`-A INPUT -p udp -j ACCEPT` zezwól na wszystkie przychodzące połączenia UDP, ponieważ nie używamy śledzenia połączeń.

`-A INPUT -p icmp -j ACCEPT` pozwalać na [ICMP](https://en.wikipedia.org/wiki/Internet_Control_Message_Protocol "wikipedia:Internet Control Message Protocol").

`-A INPUT -p tcp --dport 443 -j ACCEPT`zezwól na połączenia przychodzące do `ORPort`.

`-A INPUT -p tcp --dport 80 -j ACCEPT` zezwól na połączenia przychodzące do `DirPort`.

`-A INPUT -i lo -j ACCEPT` Pozwala wszystkie połączenia na interfejsie loopback.

##### Haveged

Zobacz Haveged, aby zdecydować, czy twój system generuje wystarczającą entropię, aby obsłużyć wiele połączeń OpenSSL, patrz [haveged - A simple entropy daemon](http://www.issihosts.com/haveged/) i [how-to-setup-additional-entropy-for-cloud-servers-using-haveged](http://www.digitalocean.com/community/tutorials/how-to-setup-additional-entropy-for-cloud-servers-using-haveged) do dokumentacji.

##### pdnsd

**Warning:** Ta konfiguracja zakłada, że twój resolver sieciowy DNS jest zaufany (nieocenzurowany).

Możesz użyć [pdnsd](/index.php/Pdnsd "Pdnsd") do buforowania zapytań DNS lokalnie, więc przekaźnik wyjściowy może rozwiązać DNS szybciej, a przekaźnik wyjściowy nie przekazuje wszystkich zapytań DNS do zewnętrznego rekursora DNS.

 `/etc/pdnsd.conf` 
```
...
perm_cache=102400                       ## (Default value)*100 = 1MB * 100 = 100MB
...
server {
    label= "resolvconf";
    file = "/etc/pdnsd-resolv.conf";    ## Preferably do not use /etc/resolv.conf
    timeout=4;                          ## Server timeout, this may be much shorter than the global timeout option.
    uptest=query;                       ## Test availability using empty DNS queries. 
    query_test_name=".";                ## To be used if remote servers ignore empty queries.
    interval=10m;                       ## Test every 10 minutes.
    purge_cache=off;                    ## Ignore TTL.
    edns_query=yes;                     ## Use EDNS for outgoing queries to allow UDP messages larger than 512 bytes. May cause trouble with some legacy systems.
    preset=off;                         ## Assume server is down before uptest.
 }
...
```

Ten skrót konfiguracji pokazuje, jak cacheować kwerendy do twojego normalnego rekursora DNS lokalnie i zwiększać rozmiar pamięci podręcznej pdnsd do 100 MB.

###### Nieocenzurowany DNS

Jeśli twój lokalny rekursor DNS jest w jakiś sposób ocenzurowany lub ingeruje w zapytania DNS, zobacz [Resolv.conf#Alternative DNS servers](/index.php/Resolv.conf#Alternative_DNS_servers "Resolv.conf") dla alternatyw i dodaj je w oddzielnej sekcji serwera w `/etc/pdnsd.conf` zgodnie [Pdnsd#DNS servers](/index.php/Pdnsd#DNS_servers "Pdnsd").

## TorDNS

Tor 0.2.x zapewnia wbudowany forwarder DNS. Aby go włączyć dodaj następujące linie do pliku konfiguracyjnego Tora i zrestartuj demona:

 `/etc/tor/torrc` 
```
DNSPort 9053
AutomapHostsOnResolve 1
AutomapHostsSuffixes .exit,.onion

```

Umożliwi to Torowi zaakceptowanie żądań DNS (nasłuchiwanie na porcie 9053 w tym przykładzie) jak zwykłego serwera DNS i rozwiązanie domeny za pośrednictwem sieci Tor. Wadą jest to, że jest w stanie rozwiązywać zapytania DNS tylko dla rekordów A; Zapytania MX i NS nigdy nie są odbierane. Aby uzyskać więcej informacji, zobacz to [Debian-based introduction](https://techstdout.boum.org/TorDns/).

Zapytania DNS można również wykonać za pomocą interfejsu wiersza poleceń za pomocą polecenia `tor-resolve` Na przykład:

```
$ tor-resolve archlinux.org
66.211.214.131

```

### Używanie TorDNS do wszystkich zapytań DNS

Możliwe jest skonfigurowanie systemu, jeśli jest to pożądane, do korzystania z TorDNS dla wszystkich zapytań, które tworzy twój system, niezależnie od tego, czy ostatecznie użyjesz Tora do połączenia się z ostatecznym miejscem docelowym. Aby to zrobić, skonfiguruj system tak, aby używał 127.0.0.1 jako swojego serwera DNS i edytuj linię "DNSPort" w katalogu `/etc/tor/torrc`, aby wyświetlić:

```
DNSPort 53

```

Alternatywnie możesz użyć lokalnego serwera buforowania DNS, takiego jak [dnsmasq](/index.php/Dnsmasq "Dnsmasq") lub [pdnsd](/index.php/Pdnsd "Pdnsd"), który również zrekompensuje, że TorDNS jest nieco wolniejszy niż tradycyjne serwery DNS. Poniższe instrukcje pokażą, jak skonfigurować *dnsmasq* do tego celu.

Zmień ustawienie tora, aby wykryć żądanie DNS w porcie 9053 i zaistaluj [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq).

Zmodyfikuj plik konfiguracyjny tak, aby zawierał:

 `/etc/dnsmasq.conf` 
```
no-resolv
port=53
server=127.0.0.1#9053
listen-address=127.0.0.1

```

Te konfiguracje ustawiają dnsmasq, aby nasłuchiwał tylko żądań z lokalnego komputera i używał TorDNS jako jedynego dostawcy upstream. Konieczne jest edycja pliku `/etc/resolv.conf`, aby system wysyłał zapytania tylko do serwera dnsmasq.

 `/etc/resolv.conf` 
```
nameserver 127.0.0.1

```

Uruchom demona **dnsmasq**.

Finally if you use *dhcpd* you would need to change its settings to that it does not alter the resolv configuration file. Just add this line in the configuration file:

Jeśli korzystasz z dhcpd, musisz zmienić jego ustawienia, aby nie zmieniało pliku konfiguracyjnego resolv. Po prostu dodaj tę linię w pliku konfiguracyjnym:

 `/etc/dhcpcd.conf` 
```
nohook resolv.conf

```

Jeśli masz już linię *nohook*, po prostu dodaj **resolv.conf** oddzielony przecinkiem.

## Torsocks

*torsocks'* umożliwiają korzystanie z aplikacji za pośrednictwem sieci Tor bez konieczności wprowadzania zmian konfiguracji w aplikacji. Ze strony podręcznika:

'torsocks to wrapper między biblioteką torsocks a aplikacją, aby każda komunikacja internetowa przechodziła przez sieć Tor.

Przykład użycia:

```
$ torsocks elinks checkip.dyndns.org
$ torsocks wget -qO- [https://check.torproject.org/](https://check.torproject.org/) | grep -i congratulations

```

## Transparent Torification

W niektórych przypadkach bezpieczniej i często łatwiej jest w przejrzysty sposób toralizować cały system, zamiast konfigurować poszczególne aplikacje do korzystania z portu soks Tor'a, nie wspominając o zapobieganiu wyciekom DNS. Transparentną toryfikację można przeprowadzić za pomocą [iptables](/index.php/Iptables "Iptables") w taki sposób, że wszystkie pakiety wychodzące są przekierowywane przez *TransPort* Tora, z wyjątkiem ruchu samego Tora. Po zainstalowaniu aplikacje nie muszą być skonfigurowane do korzystania z Tora, przez Tor *SocksPort* będzie nadal działać. Działa to również dla DNS za pośrednictwem *DNSPort* Tora, ale zdajemy sobie sprawę, że Tor obsługuje tylko TCP, więc pakiety UDP inne niż DNS nie mogą być wysyłane przez Tora i dlatego muszą być całkowicie zablokowane, aby zapobiec wyciekom. Użycie iptables do przezroczystego toryfikowania systemu zapewnia porównywalnie silną ochronę przed wyciekami, ale nie zastępuje zwirtualizowanych aplikacji torowania, takich jak Whonix lub TorVM [[4]](https://www.whonix.org/wiki/Comparison_with_Others). Przezroczysta torifikacja również nie będzie chroniła przed atakami odcisków palców we własnym zakresie, dlatego zaleca się używanie jej w połączeniu z przeglądarką Tor (przeszukaj AUR dla wersji, którą chcesz: [https://aur.archlinux.org/packages/?K=tor-browser](https://aur.archlinux.org/packages/?K=tor-browser)) Aplikacje nadal mogą użyć się nazwy komputera, adresu MAC, numeru seryjnego, strefy czasowej itp., A te z uprawnieniami root mogą całkowicie wyłączyć zaporę. Innymi słowy, przezroczysta toryfikator z iptables chroni przed przypadkowymi połączeniami i wyciekami DNS przez źle skonfigurowane oprogramowanie, nie jest wystarczająca do ochrony przed złośliwym oprogramowaniem lub oprogramowaniem o poważnych lukach w zabezpieczeniach.

To enable transparent torification, use the following file for `iptables-restore` and `ip6tables-restore` (internally used by [systemd](/index.php/Systemd "Systemd")'s `iptables.service` and `ip6tables.service`).

**Note:**

Ten plik używa tabeli nat do wymuszania połączeń wychodzących przez TransPort lub DNSPort i blokuje wszystko, czego nie może dokonać.

*   Teraz za pomocą `--ipv6` i `--ipv4` dla zmian specyficznych dla protokołu. `iptables-restore` i `ip6tables-restore` Można teraz korzystać z tego samego pliku.
*   Gdzie --ipv6 lub --ipv4 jest jednoznacznie określone, `ip*tables-restore` zignoruje regułę, jeśli nie jest to właściwe dla protokołu.
*   `ip6tables` nie wspiera `--reject-with`. Upewnij się, że twój torrc zawiera następujące linie:

```
SocksPort 9050
DNSPort 5353
TransPort 9040

```

Zobacz [iptables(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/iptables.8).

**Note:**

Jeśli pojawi się ten błąd: `iptables-restore: unable to initialize table 'nat'`, musisz załadować odpowiednie moduły jądra:

```
# modprobe ip_tables iptable_nat ip_conntrack iptable-filter ipt_state

```

 `/etc/iptables/iptables.rules` 
```

*nat
:PREROUTING ACCEPT [6:2126]
:INPUT ACCEPT [0:0]
:OUTPUT ACCEPT [17:6239]
:POSTROUTING ACCEPT [6:408]

-A PREROUTING ! -i lo -p udp -m udp --dport 53 -j REDIRECT --to-ports 5353
-A PREROUTING ! -i lo -p tcp -m tcp --tcp-flags FIN,SYN,RST,ACK SYN -j REDIRECT --to-ports 9040
-A OUTPUT -o lo -j RETURN
--ipv4 -A OUTPUT -d 192.168.0.0/16 -j RETURN
-A OUTPUT -m owner --uid-owner "tor" -j RETURN
-A OUTPUT -p udp -m udp --dport 53 -j REDIRECT --to-ports 5353
-A OUTPUT -p tcp -m tcp --tcp-flags FIN,SYN,RST,ACK SYN -j REDIRECT --to-ports 9040
COMMIT

*filter
:INPUT DROP [0:0]
:FORWARD DROP [0:0]
:OUTPUT DROP [0:0]

-A INPUT -i lo -j ACCEPT
-A INPUT -p icmp -j ACCEPT
-A INPUT -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT
--ipv4 -A INPUT -p tcp -j REJECT --reject-with tcp-reset
--ipv4 -A INPUT -p udp -j REJECT --reject-with icmp-port-unreachable
--ipv4 -A INPUT -j REJECT --reject-with icmp-proto-unreachable
--ipv6 -A INPUT -j REJECT
--ipv4 -A OUTPUT -d 127.0.0.0/8 -j ACCEPT
--ipv4 -A OUTPUT -d 192.168.0.0/16 -j ACCEPT
--ipv6 -A OUTPUT -d ::1/8 -j ACCEPT
-A OUTPUT -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT
-A OUTPUT -m owner --uid-owner "tor" -j ACCEPT
--ipv4 -A OUTPUT -j REJECT --reject-with icmp-port-unreachable
--ipv6 -A OUTPUT -j REJECT
COMMIT

```

Ten plik działa również dla ip6tables-restore, więc możesz dowiązać symbolicznie:

```
# ln -s /etc/iptables/iptables.rules /etc/iptables/ip6tables.rules

```

Upewnij się, że Tor działa, i [start/enable](/index.php/Start/enable "Start/enable") the `iptables` i `ip6tables` systemd units.

Możesz dodać `Requires=iptables.service` i `Requires=ip6tables.service` do dowolnej jednostki systemowej loguje użytkownika (najprawdopodobniej menedżer wyświetlania), aby zapobiec uruchomieniu procesów użytkownika przed uruchomieniem zapory. Zobacz [systemd](/index.php/Systemd "Systemd").

## Porady i wskazówki

#### Możliwości jądra

Jeśli chcesz uruchomić tor jako użytkownik inny niż root i użyć portu niższego niż 1024, możesz użyć funkcji jądra, aby umożliwić {{ic|/usr/bin/tor} powiązanie z portami niższymi niż 1024:

```
# setcap CAP_NET_BIND_SERVICE=+eip /usr/bin/tor

```

**Note:** Każde uaktualnienie do pakietu tor spowoduje zresetowanie uprawnień, rozważ użycie [pacman#Hooks](/index.php/Pacman#Hooks "Pacman"), aby automatycznie ustawić uprawnienia po uaktualnieniach

Jeśli korzystasz z usługi systemd, można również użyć systemd, aby nadać procesowi odpowiednie uprawnienia. Ma to tę zaletę, że uprawnienia nie muszą być ponownie stosowane po każdej aktualizacji tor:

```
/etc/systemd/system/tor.service.d/netcap.conf

```

```
[Service]
CapabilityBoundingSet=
CapabilityBoundingSet=CAP_NET_BIND_SERVICE
AmbientCapabilities=
AmbientCapabilities=CAP_NET_BIND_SERVICE
```

Więcej informacji na stronie [superuser.com](https://superuser.com/questions/710253/allow-non-root-process-to-bind-to-port-80-and-443)

## Rozwiązywanie problemów

### Problem z wartością użytkownika

Jeśli demon **tor** nie może się uruchomić, uruchom następujące polecenie jako root (lub użyj sudo)

```
# tor

```

Jeśli pojawi się następujący błąd

```
May 23 00:27:24.624 [warn] Error setting groups to gid 43: "Operation not permitted".
May 23 00:27:24.624 [warn] If you set the "User" option, you must start Tor as root.
May 23 00:27:24.624 [warn] Failed to parse/validate config: Problem with User value. See logs for details.
May 23 00:27:24.624 [err] Reading config failed--see warnings above.

```

Oznacza to, że problem dotyczy wartości User, co prawdopodobnie oznacza, że jeden lub więcej plików lub katalogów w katalogu `/var/lib/tor` nie należy do tora. Można to ustalić za pomocą następującego polecenia find:

```
find /var/lib/tor/ ! -user tor

```

Wszystkie pliki lub katalogi wymienione w wynikach tej komendy muszą mieć zmienioną własność. Można to zrobić indywidualnie dla każdego pliku, jak na przykład:

```
chown tor:tor /var/lib/tor/filename

```

Lub, aby zmienić wszystko wymienione przez powyższy przykład find, zmodyfikuj polecenie do tego:

```
find /var/lib/tor/ ! -user tor -exec chown tor:tor {} \;

```

Tor powinien teraz poprawnie uruchomić się.

Nadal, jeśli nie możesz uruchomić usługi tor, uruchom usługę przy użyciu root'a (spowoduje to powrót do użytkownika tor). Aby to zrobić, zmień nazwę użytkownika w pliku `/etc/tor/torrc`:

```
User tor

```

Teraz zmodyfikuj plik usługi tor systemd `/usr/lib/systemd/system/tor.service` w następujący sposób

```
[Service]
User=root
Group=root
Type=simple

```

Proces zostanie uruchomiony jako użytkownik tor. W tym celu zmień identyfikator użytkownika i grupy na tor, a także zapisz go:

```
# chown -R tor:tor /var/lib/tor/
# chmod -R 755 /var/lib/tor

```

Teraz zapisz zmiany:

```
# systemctl --system daemon-reload

```

Potem [start](/index.php/Start "Start") `tor.service`.