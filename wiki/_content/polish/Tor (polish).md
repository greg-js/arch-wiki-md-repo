**Tor** ([ang.](/index.php?title=J%C4%99zyk_angielski&action=edit&redlink=1 "Język angielski (page does not exist)") **The Onion Router**) – wirtualna sieć komputerowa implementująca trasowanie cebulowe drugiej generacji. Sieć zapobiega analizie ruchu sieciowego i w konsekwencji zapewnia użytkownikom prawie anonimowy dostęp do zasobów Internet

## Contents

*   [1 Wprowadzenie](#Wprowadzenie)
*   [2 Instalacja](#Instalacja)
*   [3 Konfiguracja](#Konfiguracja)
*   [4 komunikatory](#komunikatory)
    *   [4.1 Pidgin](#Pidgin)

## Wprowadzenie

Użytkownicy sieci Tor uruchamiają serwer proxy na swoim komputerze. Oprogramowanie to łączy się z siecią Tor, okresowo negocjuje obwód wirtualny przez sieć Tor. Tor wykorzystuje kryptografię w sposób warstwowy podobnie do warstw cebuli zapewniając idealną tajemnicę między routerami. Oprogramowanie proxy tora posiada też interfejs SOCKS dla swoich klientów. Aplikacje SOCKS-aware mogą być skierowane do sieci Tor, który następnie przepuszcza ruch przez wirtualny obwód Tora. Dzięki temu tor daje anonimowość użytkownika końcowego.

anonimowość jest uzyskana dzięki szyfrowaniu ruchu, tor wysyła zaszyfrowane pakiety przez inne węzły sieci i odszyfrowuje je na ostatnim węźle, aby odebrać ruch przed przekazaniem go do określonego serwera.

Jednym z wyzwań, które należy wykonać dla anonimowości Tor, jest to, że może to być znacznie wolniejsze niż bezpośrednie połączenie ze względu na dużą liczbę ponownych trasowania ruchu

Dodatkowo, chociaż Tor zapewnia ochronę przed analizą ruchu, nie może zapobiec potwierdzeniu ruchu na granicy sieci Tora (tj. Ruchu wchodzącego i wychodzącego z sieci).

## Instalacja

## Konfiguracja

Domyślnie Tor czyta konfiguracje z pliku `/etc/tor/torrc` Opcje konfiguracji są wyjaśnione [tor(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/tor.1) [Strona Tor](https://torproject.org/docs/tor-manual.html.en). Domyślna konfiguracja powinna działać prawidłowo dla większości użytkowników Tora.

Istnieją potencjalne konflikty między konfiguracjami w `torrc` a `tor.service`.

*   W `torrc`, `RunAsDaemon` Powinno, jako domyślnie, być ustawione na `0`, since `Type=simple` Jest ustawiony w `[Service]` Sekcji w `tor.service`.
*   W `torrc`, `User` Nie powinien być ustawiony, chyba że `User=` jest ustawione na `root` w `[Service]` Sekcji w `tor.service`.

## komunikatory

Aby korzystać z komunikatora internetowego, nie potrzebujemy proxy http, takiego jak [polipo](/index.php/Polipo "Polipo")/[privoxy](/index.php/Privoxy "Privoxy"). Będziemy używać demona tor'a bezpośrednio, który domyślnie nasłuchuje na porcie 9050.

### Pidgin

Możesz skonfigurować Pidgin do korzystania z Tora globalnie lub na konto. Aby używać Tora globalnie, przejdź do Narzędzia -> Preferencje -> Proxy. Aby używać Tora dla określonych kont, przejdź do sekcji "Konta> Zarządzaj kontami", wybierz żądane konto, kliknij przycisk Modyfikuj, a następnie przejdź do karty Proxy. Ustawienia serwera proxy są następujące:

```
Proxy type SOCKS5
Host 127.0.0.1
Port 9150

```