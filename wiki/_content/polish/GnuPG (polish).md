Według [official website](https://www.gnupg.org/):

	GnuPG to pełna i darmowa implementacja [OpenPGP](http://openpgp.org/about/) standard zdefiniowany przez [RFC4880](https://tools.ietf.org/html/rfc4880) (znany również jako PGP). GnuPG pozwala na szyfrowanie i podpisywanie danych i komunikacji. Posiada wszechstronny system zarządzania kluczami, a także moduły dostępu do wszystkich rodzajów katalogów kluczy publicznych. GnuPG, znany również jako GPG, to narzędzie linii poleceń z funkcjami ułatwiającymi integrację z innymi aplikacjami. Dostępnych jest wiele aplikacji i bibliotek frontendowych. Wersja 2 GnuPG zapewnia także obsługę S/MIME i Secure Shell (ssh).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalacja](#Instalacja)
*   [2 Konfiguracja](#Konfiguracja)
    *   [2.1 Lokalizacja katalogu](#Lokalizacja_katalogu)
    *   [2.2 Pliki konfiguracyjne](#Pliki_konfiguracyjne)
    *   [2.3 Domyślne opcje dla nowych użytkowników](#Domyślne_opcje_dla_nowych_użytkowników)
*   [3 Używanie](#Używanie)
    *   [3.1 Utwórz parę kluczy](#Utwórz_parę_kluczy)
    *   [3.2 Lista kluczy](#Lista_kluczy)
    *   [3.3 Wyeksportuj swój klucz publiczny](#Wyeksportuj_swój_klucz_publiczny)
    *   [3.4 Zaimportuj klucz publiczny](#Zaimportuj_klucz_publiczny)
    *   [3.5 Użyj serwera kluczy](#Użyj_serwera_kluczy)
    *   [3.6 Szyfrowanie i odszyfrowanie](#Szyfrowanie_i_odszyfrowanie)
        *   [3.6.1 Asymetryczne](#Asymetryczne)
        *   [3.6.2 Symetryczne](#Symetryczne)
*   [4 Konserwacja kluczy](#Konserwacja_kluczy)
    *   [4.1 Zrób kopię swojego klucza prywatnego](#Zrób_kopię_swojego_klucza_prywatnego)
    *   [4.2 Edytuj swój klucz](#Edytuj_swój_klucz)
    *   [4.3 Eksportowanie podklucza](#Eksportowanie_podklucza)
    *   [4.4 Rotating subkeys](#Rotating_subkeys)
*   [5 Podpisy](#Podpisy)
    *   [5.1 Utwórz podpis](#Utwórz_podpis)
        *   [5.1.1 Zarejestruj plik](#Zarejestruj_plik)
        *   [5.1.2 Clearsign a file or message](#Clearsign_a_file_or_message)
        *   [5.1.3 Utwórz oddzielny podpis](#Utwórz_oddzielny_podpis)
    *   [5.2 Zweryfikuj podpis](#Zweryfikuj_podpis)
*   [6 gpg-agent](#gpg-agent)
    *   [6.1 Konfiguracja](#Konfiguracja_2)
    *   [6.2 Załaduj ponownie agenta](#Załaduj_ponownie_agenta)
    *   [6.3 pinentry](#pinentry)
    *   [6.4 Bezobsługowe hasło](#Bezobsługowe_hasło)
    *   [6.5 SSH agent](#SSH_agent)
        *   [6.5.1 Set SSH_AUTH_SOCK](#Set_SSH_AUTH_SOCK)
        *   [6.5.2 Skonfiguruj pinentry, aby użyć prawidłowego TTY](#Skonfiguruj_pinentry,_aby_użyć_prawidłowego_TTY)
        *   [6.5.3 Dodaj klucze SSH](#Dodaj_klucze_SSH)
        *   [6.5.4 Użyj klucza GPG jako klucza SSH](#Użyj_klucza_GPG_jako_klucza_SSH)
*   [7 Smartcards](#Smartcards)
    *   [7.1 GnuPG only setups](#GnuPG_only_setups)
    *   [7.2 GnuPG z pcscd (PCSC Lite)](#GnuPG_z_pcscd_(PCSC_Lite))
        *   [7.2.1 Zawsze używaj pcscd](#Zawsze_używaj_pcscd)
*   [8 Porady i wskazówki](#Porady_i_wskazówki)
    *   [8.1 Inny algorytm](#Inny_algorytm)
    *   [8.2 Zaszyfruj hasło](#Zaszyfruj_hasło)
    *   [8.3 Odwoływanie klucza](#Odwoływanie_klucza)
    *   [8.4 Change trust model](#Change_trust_model)
    *   [8.5 Ukryj wszystkie identyfikatory odbiorców](#Ukryj_wszystkie_identyfikatory_odbiorców)
    *   [8.6 Używanie caff do wysyłania kluczy partiami](#Używanie_caff_do_wysyłania_kluczy_partiami)
    *   [8.7 Zawsze pokazuj długie identyfikatory i odciski palca](#Zawsze_pokazuj_długie_identyfikatory_i_odciski_palca)
    *   [8.8 Niestandardowe funkcje](#Niestandardowe_funkcje)
    *   [8.9 Cache passwords](#Cache_passwords)
*   [9 Rozwiązywanie problemów:](#Rozwiązywanie_problemów:)
    *   [9.1 Nie ma wystarczającej liczby losowych bajtów](#Nie_ma_wystarczającej_liczby_losowych_bajtów)
    *   [9.2 su](#su)
    *   [9.3 Agent complains end of file](#Agent_complains_end_of_file)
    *   [9.4 KGpg configuration permissions](#KGpg_configuration_permissions)
    *   [9.5 GNOME na Wayland zastępuje gniazdo agenta SSH](#GNOME_na_Wayland_zastępuje_gniazdo_agenta_SSH)
    *   [9.6 mutt](#mutt)
    *   [9.7 "Utracone" klucze, aktualizacja do wersji 2.1 Gnupg](#"Utracone"_klucze,_aktualizacja_do_wersji_2.1_Gnupg)
    *   [9.8 gpg zawiesza się dla wszystkich serwerów kluczy (podczas próby odebrania kluczy)](#gpg_zawiesza_się_dla_wszystkich_serwerów_kluczy_(podczas_próby_odebrania_kluczy))
    *   [9.9 Nie wykryto SmartCard](#Nie_wykryto_SmartCard)
    *   [9.10 gpg: WARNING: server 'gpg-agent' is older than us (x < y)](#gpg:_WARNING:_server_'gpg-agent'_is_older_than_us_(x_<_y))
    *   [9.11 gpg: ..., IPC connect call failed](#gpg:_...,_IPC_connect_call_failed)
*   [10 Zobacz też](#Zobacz_też)

## Instalacja

[Install](/index.php/Install "Install") the [gnupg](https://www.archlinux.org/packages/?name=gnupg) package.

This will also install [pinentry](https://www.archlinux.org/packages/?name=pinentry), a collection of simple PIN or passphrase entry dialogs which GnuPG uses for passphrase entry. Which *pinentry* dialog is used is determined by the symbolic link `/usr/bin/pinentry`, which by default points to `/usr/bin/pinentry-gtk-2`.

If you want to use a graphical frontend or program that integrates with GnuPG, see [List of applications/Security#Encryption, signing, steganography](/index.php/List_of_applications/Security#Encryption,_signing,_steganography "List of applications/Security").

## Konfiguracja

### Lokalizacja katalogu

`$GNUPGHOME` jest używany przez GnuPG do wskazywania katalogu, w którym przechowywane są jego pliki konfiguracyjne. Domyślnie `$GNUPGHOME`nie jest ustawione i twoje `$HOME` jest używany zamiast; w ten sposób znajdziesz `~/.gnupg` katalog zaraz po instalacji.

Aby zmienić domyślną lokalizację, uruchom gpg w ten sposób `$ gpg --homedir *path/to/file*` lub ustaw `GNUPGHOME` [environment variable](/index.php/Environment_variable "Environment variable").

### Pliki konfiguracyjne

Domyślne pliki konfiguracyjne to `~/.gnupg/gpg.conf` i `~/.gnupg/dirmngr.conf`.

Domyślnie katalog gnupg ma ustawione uprawnienia do `700` , a pliki, które zawiera, mają ustawione uprawnienia do `600`. Tylko właściciel katalogu ma uprawnienia do odczytu, zapisu i uzyskiwania dostępu do plików. Jest to ze względów bezpieczeństwa i nie należy go zmieniać. W przypadku, gdy ten katalog lub jakikolwiek inny plik wewnątrz niego nie jest zgodny z tą miarą bezpieczeństwa, otrzymasz ostrzeżenia o niebezpiecznych uprawnieniach do plików i katalogu domowego.

Dołącz do tych plików dowolne długie opcje, które chcesz. Nie zapisuj dwóch kresek, ale po prostu nazwę opcji i wymagane argumenty. Znajdziesz pliki szkieletów w `/usr/share/gnupg`. Pliki te są kopiowane do `~/.gnupg` przy pierwszym uruchomieniu gpg, jeśli tam nie istnieją. Inne przykłady można znaleźć w [#See also](#See_also).

Dodatkowo [pacman](/index.php/Pacman "Pacman") używa innego zestawu plików konfiguracyjnych do weryfikacji podpisów paczek. Zobacz [Pacman/Package signing](/index.php/Pacman/Package_signing "Pacman/Package signing") dla szczegółów.

### Domyślne opcje dla nowych użytkowników

Jeśli chcesz ustawić domyślne opcje dla nowych użytkowników, umieść pliki konfiguracyjne w `/etc/skel/.gnupg/`. Po dodaniu nowego użytkownika w systemie pliki z tego katalogu zostaną skopiowane do katalogu domowego GnuPG. Istnieje również prosty skrypt o nazwie "addgnupghome", który można wykorzystać do stworzenia nowych katalogów domowych GnuPG dla istniejących użytkowników:

```
# addgnupghome user1 user2

```

To doda odpowiednie `/home/user1/.gnupg` i `/home/user2/.gnupg` i skopiuj do niego pliki z katalogu szkieletu. Użytkownicy z istniejącym katalogiem macierzystym GnuPG są po prostu pomijani.

## Używanie

**Note:** Kiedy *`user-id`* jest wymagany w poleceniu, można go określić za pomocą identyfikatora klucza, odcisku palca, części imienia i nazwiska lub adresu e-mail itp. GnuPG jest elastyczny w tym zakresie..

### Utwórz parę kluczy

Wygeneruj parę kluczy, wpisując terminal:

```
$ gpg --full-gen-key

```

**Tip:** Użyj `--expert` możliwość uzyskania alternatywnych szyfrów [ECC](https://en.wikipedia.org/wiki/Elliptic_curve_cryptography "wikipedia:Elliptic curve cryptography").

Polecenie spowoduje wyświetlenie odpowiedzi na kilka pytań. Do ogólnego użytku większość ludzi będzie chciała:

*   klucz RSA (tylko podpis) i klucz RSA (tylko szyfrowanie).
*   klucz do domyślnej wartości (2048). Większy klucz 4096 "daje nam prawie nic, a kosztuje nas sporo"[[1]](https://www.gnupg.org/faq/gnupg-faq.html#no_default_of_rsa4096).
*   data wygaśnięcia. Okres roku jest wystarczająco dobry dla przeciętnego użytkownika. W ten sposób, nawet jeśli dojdzie do utraty dostępu do kluczy, pozwoli to innym dowiedzieć się, że nie jest już ważny. Później, jeśli to konieczne, data wygaśnięcia może zostać przedłużona bez konieczności ponownego wydania nowego klucza.
*   twoje imię i adres e-mail. Możesz dodać wiele tożsamości do tego samego klucza później ("', jeśli masz wiele adresów e-mail, które chcesz powiązać z tym kluczem).
*   'komentarz "nie". Ponieważ semantyka pola komentarza to [not well-defined](https://lists.gnupg.org/pipermail/gnupg-devel/2015-July/030150.html), ma ograniczoną wartość do identyfikacji.
*   [a secure passphrase](/index.php/Security#Choosing_secure_passwords "Security").

**Note:** Nazwa i adres e-mail, który tu wpiszesz, będą widoczne dla każdego, kto importuje twój klucz.

### Lista kluczy

Aby wyświetlić listę kluczy w swoim publicznym key ring:

```
$ gpg --list-keys

```

Aby wyświetlić sekretną listę kluczy key ring:

```
$ gpg --list-secret-keys

```

### Wyeksportuj swój klucz publiczny

Głównym zastosowaniem gpg jest zapewnienie poufności wymienianych wiadomości za pośrednictwem kryptografii z kluczem publicznym. Dzięki niemu każdy użytkownik dystrybuuje klucz publiczny swojego klucza, który może być używany przez innych do szyfrowania wiadomości do użytkownika. Klucz prywatny musi być zawsze "prywatny", w przeciwnym razie dochodzi do złamania poufności. Zobacz w [w:Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography "w:Public-key cryptography") przykłady wymiany wiadomości.

Tak więc, aby inni mogli wysyłać zaszyfrowane wiadomości, potrzebują Twojego publicznego klucza.

By wygenerować wersję ASCII klucza publicznego do pliku `*public.key*` (np. do dystrybucji poprzez e-mail):

```
$ gpg --output *public.key* --armor --export *user-id*

```

Alternatywnie lub dodatkowo możesz zobaczyć sekcję [#Użyj serwera kluczy](#Użyj_serwera_kluczy) by podzielić się swoim kluczem.

**Tip:** Dodaj `--no-emit-version` aby uniknąć drukowania numeru wersji lub dodać odpowiednie ustawienie do pliku konfiguracyjnego.

### Zaimportuj klucz publiczny

Aby szyfrować wiadomości innym osobom, a także weryfikować ich podpisy, potrzebujesz ich klucza publicznego. Aby zaimportować klucz publiczny z nazwą pliku `*public.key*` do twojego publicznego breloczka

```
$ gpg --import *public.key*

```

Alternatywnie, [#Use a keyserver](#Use_a_keyserver) znaleźć klucz publiczny.

### Użyj serwera kluczy

Możesz zarejestrować swój klucz za pomocą publicznego serwera kluczy PGP, aby inni mogli odzyskać klucz bez konieczności bezpośredniego kontaktu z Tobą:

```
$ gpg --send-keys *user-id*

```

**Warning:** Po przesłaniu klucza do serwera kluczy nie można go usunąć z serwera.[[2]](https://pgp.mit.edu/faq.html)

Aby poznać szczegóły klucza na serwerze kluczy, bez importowania go, wykonaj następujące czynności:

```
$ gpg --search-keys *user-id*

```

Aby zaimportować klucz z serwera kluczy:

```
$ gpg --recv-keys *key-id*

```

**Warning:**

*   Powinieneś zweryfikować autentyczność pobranego klucza publicznego, porównując jego odcisk palca z tym, który właściciel opublikował w niezależnym źródle (np. Kontaktując się bezpośrednio z osobą). Zobacz [Wikipedia:Public key fingerprint](https://en.wikipedia.org/wiki/Public_key_fingerprint "wikipedia:Public key fingerprint") po więcej informacji.
*   Używanie krótkiego ID może napotkać na kolizje. Wszystkie klucze zostaną zaimportowane z krótkim identyfikatorem. Aby tego uniknąć, należy użyć pełnego identyfikatora odcisku palca lub długiego identyfikatora klucza podczas odbierania klucza. [[3]](https://lkml.org/lkml/2016/8/15/445)

**Tip:**

*   Dodanie `keyserver-options auto-key-retrieve` do `gpg.conf` automatycznie pobierze klucze z serwera kluczy w razie potrzeby.
*   Alternatywny serwer kluczy to `pool.sks-keyservers.net` i można go określić za pomocą `keyserver` w `dirmngr.conf`; Zobacz też [wikipedia:Key server (cryptographic)#Keyserver examples](https://en.wikipedia.org/wiki/Key_server_(cryptographic)#Keyserver_examples "wikipedia:Key server (cryptographic)").
*   Jeśli twoja sieć blokuje porty używane dla hkp / hkps, być może musisz podać port 80, tzn. `pool.sks-keyservers.net:80`
*   Możesz połączyć się z serwerem kluczy przez [Tor](/index.php/Tor "Tor") używając `--use-tor`. Zobacz [GnuPG blog post](https://gnupg.org/blog/20151224-gnupg-in-november-and-december.html) po więcej informacji.
*   Możesz połączyć się z serwerem kluczy za pomocą serwera proxy, ustawiając opcję `http_proxy` Zmienna i ustawienie środowiska `honor-http-proxy` w `dirmngr.conf`. Ewentualnie ustaw `http-proxy *host[:port]*` w `dirmngr.conf`, przesłonięte `http_proxy`Zmienna środowiskowa.
*   Jeśli chcesz zaimportować identyfikator klucza, aby zainstalować konkretny pakiet Arch Linux, Zobacz [pacman/Package signing#Managing the keyring](/index.php/Pacman/Package_signing#Managing_the_keyring "Pacman/Package signing") i [Makepkg#Signature checking](/index.php/Makepkg#Signature_checking "Makepkg").

### Szyfrowanie i odszyfrowanie

#### Asymetryczne

Musisz [zaimportować klucz publiczny](#Zaimportuj_klucz_publiczny) użytkownika przed szyfrowaniem (opcje `--encrypt` or `-e`) pliku lub wiadomości do danego odbiorcy (opcje `--recipient` or `-r`). Dodatkowo musisz [Utworzyć parę kluczy](#Utwórz_parę_kluczy) jeśli jeszcze tego nie zrobiłeś.

Aby zaszyfrować plik o nazwie "doc", użyj:

```
$ gpg --recipient *user-id* --encrypt *doc*

```

Aby odszyfrować (opcja `--decrypt` lub `-d`) zaszyfrowany kluczem prywatnym plik o nazwie *doc* .gpg za pomocą klucza publicznego, użyj:

```
$ gpg --output *doc* --decrypt *doc*.gpg

```

*gpg* poprosi cię o podanie hasła, a następnie odszyfruje i zapisze dane z *doc* . gpg do *doc* . Jeśli pominiesz `-o` (`--output`) opcje, *gpg* zapisze odszyfrowane dane na standardowe wyjście.

**Tip:**

*   Dodaj `--armor` zaszyfrować plik przy użyciu zbroi ASCII (nadaje się do kopiowania i wklejania wiadomości w formacie tekstowym)
*   Używająć `-R *user-id*` lub `--hidden-recipient *user-id*` zamiast `-r` nie umieszczać identyfikatorów kluczy odbiorców w zaszyfrowanej wiadomości. Pomaga to ukryć odbiorców wiadomości i stanowi ograniczony środek zaradczy przeciwko analizie ruchu.
*   Dodaj `--no-emit-version` aby uniknąć drukowania numeru wersji lub dodać odpowiednie ustawienie do pliku konfiguracyjnego.
*   Możesz użyć gnupg do zaszyfrowania poufnych dokumentów za pomocą własnego identyfikatora użytkownika jako odbiorcy lub używając `--default-recipient-self` zamiast tego flaga; można jednak wykonać tylko ten jeden plik naraz, chociaż zawsze można zarchiwizować różne pliki, a następnie zaszyfrować plik tar. Zobacz też [Disk encryption#Available methods](/index.php/Disk_encryption#Available_methods "Disk encryption") jeśli chcesz zaszyfrować katalogi lub cały system plików.

#### Symetryczne

Szyfrowanie symetryczne nie wymaga generowania pary kluczy i może być używane do prostego szyfrowania danych za pomocą hasła. Po prostu użyj `--symmetric` lub `-c` aby wykonać szyfrowanie symetryczne:

```
$ gpg -c *doc*

```

Poniższy przykład:

*   Szyfruje `*doc*` z symetrycznym szyfrem za pomocą hasła
*   Używa algorytmu szyfrowania AES-256 do szyfrowania hasła
*   Korzysta z algorytmu skrótu SHA-512, aby zmapować hasło
*   Obejmuje hasło dla 65536 iteracje

```
$ gpg -c --s2k-cipher-algo AES256 --s2k-digest-algo SHA512 --s2k-count 65536 *doc*

```

Aby odszyfrować symetrycznie zaszyfrowany `*doc*.gpg` za pomocą hasła i wypakować odszyfrowane treści do tego samego katalogu, co `*doc*`:

```
$ gpg --output *doc* --decrypt *doc*.gpg

```

## Konserwacja kluczy

### Zrób kopię swojego klucza prywatnego

Aby wykonać kopię zapasową klucza prywatnego, wykonaj następujące czynności:

```
$ gpg --export-secret-keys --armor *<user-id>* > *privkey.asc*

```

Zwróć uwagę, że "gpg" wersja 2.1 zmieniła domyślne zachowanie, więc powyższe polecenie wymusza ochronę hasłem, nawet jeśli świadomie zdecydowałeś się nie używać go przy tworzeniu klucza. Jest tak, ponieważ w przeciwnym razie każdy, kto uzyska dostęp do powyższego wyeksportowanego pliku, będzie mógł szyfrować i podpisywać dokumenty tak, jakby były "bez", które wymagają znajomości hasła.

**Warning:** Hasło jest zwykle najsłabszym ogniwem chroniącym twój tajny klucz. Umieść klucz prywatny w bezpiecznym miejscu w innym systemie / urządzeniu, takim jak zamknięty pojemnik lub zaszyfrowany dysk. Jest to jedyne bezpieczeństwo, które musisz odzyskać na swoim kluczyku w przypadku, na przykład, awarii napędu, kradzieży lub gorszych.

Aby zaimportować kopię zapasową klucza prywatnego:

```
$ gpg --import *privkey.asc*

```

### Edytuj swój klucz

Uruchomienie `gpg --edit-key *<user-id>*` Polecenie wyświetli menu, które pozwoli ci wykonać większość kluczowych zadań związanych z zarządzaniem.

Kilka przydatnych poleceń w podmenu edycji kluczy:

```
> passwd       # change the passphrase
> clean        # compact any user ID that is no longer usable (e.g revoked or expired)
> revkey       # revoke a key
> addkey       # add a subkey to this key
> expire       # change the key expiration time

```

Typ `help` w podmenu edycji kluczy, aby uzyskać więcej poleceń.

**Tip:** Jeśli masz wiele kont e-mail, możesz dodać każdą z nich jako tożsamość, używając `adduid` komenda. Możesz wtedy ustawić swój ulubiony jako `primary`.

### Eksportowanie podklucza

Jeśli zamierzasz używać tego samego klucza na wielu urządzeniach, możesz usunąć klucz główny i przechowywać tylko minimalny podklucz szyfrowany na mniej bezpiecznych systemach.

Najpierw sprawdź, który podklucz chcesz wyeksportować.

```
$ gpg -K

```

Wybierz tylko ten podklucz do eksportu.

```
$ gpg -a --export-secret-subkeys [subkey id]! > /tmp/subkey.gpg

```

**Warning:** Jeśli zapomnisz dodać!, Wszystkie twoje podklucze zostaną wyeksportowane.

W tym momencie możesz przestać, ale najprawdopodobniej dobrze jest również zmienić hasło. Zaimportuj klucz do folderu tymczasowego.

```
$ gpg --homedir /tmp/gpg --import /tmp/subkey.gpg
$ gpg --homedir /tmp/gpg --edit-key *<user-id>*
> passwd
> save
$ gpg --homedir /tmp/gpg -a --export-secret-subkeys [subkey id]! > /tmp/subkey.altpass.gpg

```

**Note:** Otrzymasz ostrzeżenie, że klucz główny nie był dostępny, a hasło nie zostało zmienione, ale można je bezpiecznie zignorować, tak jak hasło podklucza.

W tym momencie możesz teraz użyć `/tmp/subkey.altpass.gpg` na innych urządzeniach.

### Rotating subkeys

**Warning:** **Nigdy** nie usuwaj podkluczów z wygasłymi lub cofniętymi, chyba że masz dobry powód. Spowoduje to utratę możliwości odszyfrowywania plików zaszyfrowanych przy użyciu starego podklucza. Usuwaj **tylko** klucze wygasłe lub unieważnione od innych użytkowników w celu wyczyszczenia kluczy.

Jeśli ustawiłeś podklucze, aby wygasły po określonym czasie, możesz utworzyć nowe. Zrób to z kilkutygodniowym wyprzedzeniem, aby inni mogli zaktualizować swoją bazę kluczy.

**Tip:** Nie musisz tworzyć nowego klucza tylko dlatego, że wygasł. Możesz przedłużyć datę wygaśnięcia.

Utwórz nowy podklucz (powtórz dla podpisu i klucza szyfrowania)

```
$ gpg --edit-key *<user-id>*
> addkey

```

I odpowiedz na następujące pytania, które prosi (patrz[#Create key pair](#Create_key_pair) dla sugerowanych ustawień).

Zapisz zmiany

```
> save

```

Zaktualizuj go do serwera kluczy.

```
$ gpg --keyserver pgp.mit.edu --send-keys *<user-id>*

```

**Tip:** Odwołanie wygasłych podkluczy jest niepotrzebną i prawdopodobnie złą formą. Jeśli stale odnawiasz klucze, może to spowodować, że inni nie będą mieli do ciebie zaufania.

## Podpisy

Dokumenty poświadczające i sygnatury czasowe podpisów. Jeśli dokument zostanie zmodyfikowany, weryfikacja podpisu nie powiedzie się. W przeciwieństwie do szyfrowania, które wykorzystuje klucze publiczne do szyfrowania dokumentu, podpisy tworzone są za pomocą klucza prywatnego użytkownika. Odbiorca podpisanego dokumentu sprawdza następnie podpis za pomocą klucza publicznego nadawcy.

### Utwórz podpis

#### Zarejestruj plik

Aby podpisać plik, użyj `--sign` lub `-s` flaga:

```
 $ gpg --output *doc*.sig --sign *doc*

```

`*doc*.sig` zawiera zarówno skompresowaną zawartość oryginalnego pliku `*doc*`, jak i podpis w formacie binarnym, ale plik nie jest zaszyfrowany. możesz łączyć podpisywanie z [szyfrowaniem](#Szyfrowanie_i_odszyfrowanie)

#### Clearsign a file or message

Aby podpisać plik bez kompresowania go do formatu binarnego użyj:

```
 $ gpg --output *doc*.sig --clearsign *doc*

```

Tutaj zarówno zawartość oryginalnej dokumentacji `*doc*`, jak i podpis są przechowywane w formie czytelnej dla człowieka w pliku `*doc*.sig`.

#### Utwórz oddzielny podpis

Aby utworzyć oddzielny plik podpisu, który ma być dystrybuowany oddzielnie od samego dokumentu lub pliku, użyj flagi `--detach-sig`

```
 $ gpg --output *doc*.sig --detach-sig *doc*

```

Tutaj podpis jest przechowywany w `*doc*.sig`, ale zawartość `*doc*` nie jest w nim zapisana. Ta metoda jest często używana w dystrybucji oprogramowania, aby umożliwić użytkownikom sprawdzenie, czy program nie został zmodyfikowany przez stronę trzecią.

### Zweryfikuj podpis

Aby zweryfikować podpis, użyj flagi `--verify`

```
 $ gpg --verify *doc*.sig

```

gdzie `*doc*.sig` to podpisany plik zawierający podpis, który chcesz zweryfikować.

Jeśli sprawdzasz odłączony podpis, zarówno podpisany plik danych, jak i plik podpisu muszą być obecne podczas weryfikacji. Na przykład, aby sprawdzić najnowszą wersję iso Arch Linux, wykonaj:

```
 $ gpg --verify archlinux-*version*.iso.sig

```

gdzie `archlinux-*version*.iso` musi znajdować się w tym samym katalogu.

Można również określić podpisany plik danych z drugim argumentem:

```
 $ gpg --verify archlinux-*version*.iso.sig */path/to/*archlinux-*version*.iso

```

Jeśli plik został zaszyfrowany, oprócz podpisu, po prostu [odszyfruje](#Szyfrowanie_i_odszyfrowanie) plik i jego podpis również zostaną zweryfikowane.

## gpg-agent

*gpg-agent* jest najczęściej używany jako demon do żądania i buforowania hasła dla pęku kluczy. Jest to przydatne, jeśli GnuPG jest używany z zewnętrznego programu, takiego jak klient poczty [gnupg](https://www.archlinux.org/packages/?name=gnupg) przychodzi z [systemd user](/index.php/Systemd/User "Systemd/User") gniazda, które są domyślnie włączone. Te gniazda są `gpg-agent.socket`, `gpg-agent-extra.socket`, `gpg-agent-browser.socket`, `gpg-agent-ssh.socket`, i `dirmngr.socket`.

*   Główny `gpg-agent.socket` jest używany przez *gpg* do łączenia się z demonem *gpg-agent.*
*   Celem użycia `gpg-agent-extra.socket` w systemie lokalnym jest skonfigurowanie przekazywania domeny unixowej z systemu zdalnego. Umożliwia to używanie *gpg* w systemie zdalnym bez narażania kluczy prywatnych w systemie zdalnym. Aby uzyskać szczegółowe informacje, patrz [gpg-agent(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gpg-agent.1).
*   `gpg-agent-ssh.socket` może być używany przez [SSH](/index.php/SSH "SSH") do buforowania [kluczy SSH](/index.php/SSH_keys "SSH keys") dodanych przez program *ssh-add*. Zobacz [#SSH agent](#SSH_agent) dla potrzebnej konfiguracji.
*   `dirmngr.socket` uruchamia demona GnuPG obsługującego połączenia z serwerami kluczy.

**Note:** Jeśli używasz innej niż domyślna lokalizacji GnuPG [#Lokalizacja katalogu](#Lokalizacja_katalogu), będziesz musiał edytować wszystkie pliki gniazd, aby użyć wartości `gpgconf --list-dirs`.
.

### Konfiguracja

gpg-agent można skonfigurować za pomocą pliku `~/.gnupg/gpg-agent.conf`. Opcje konfiguracji są wymienione w [gpg-agent(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gpg-agent.1). Na przykład możesz zmienić podręczne cache dla nieużywanych kluczy:

 `~/.gnupg/gpg-agent.conf` 
```
default-cache-ttl 3600

```

**Tip:** Aby zapisać w pamięci podręcznej hasło dla całej sesji, uruchom następujące polecenie:
```
$ /usr/lib/gnupg/gpg-preset-passphrase --preset XXXXXX

```

gdzie XXXX jest kluczem. Możesz uzyskać jego wartość podczas uruchamiania `gpg --with-keygrip -K`. Hasło zostanie zapisane, dopóki `gpg-agent` nie zostanie zrestartowany. Jeśli ustawisz wartość `default-cache-ttl`, będzie ona miała pierwszeństwo.

### Załaduj ponownie agenta

Po zmianie konfiguracji, ponownie załaduj agenta za pomocą *gpg-connect-agent*:

```
$ gpg-connect-agent reloadagent /bye

```

Polecenie powinno wyświetlić `OK`.

Jednak w niektórych przypadkach tylko ponowne uruchomienie może nie być wystarczające, np. Gdy `keep-screen` został dodany do konfiguracji agenta. W takim przypadku najpierw musisz zabić trwający proces gpg-agent, a następnie możesz go ponownie uruchomić, jak wyjaśniono powyżej.

### pinentry

Wreszcie, agent musi wiedzieć, jak poprosić użytkownika o hasło. Można to ustawić w pliku konfiguracyjnym gpg-agent.

Domyślne używa okna dialogowego gtk. Dostępne są inne opcje - patrz informacja o pinentry. Aby zmienić konfigurację okna dialogowego, ustaw konfigurację programu `pinentry-program`:

 `~/.gnupg/gpg-agent.conf` 
```

# PIN entry program
# pinentry-program /usr/bin/pinentry-curses
# pinentry-program /usr/bin/pinentry-qt
# pinentry-program /usr/bin/pinentry-kwallet

pinentry-program /usr/bin/pinentry-gtk-2

```

**Tip:** Aby użyć `/usr/bin/pinentry-kwallet`, musisz zainstalować pakiet [kwalletcli](https://aur.archlinux.org/packages/kwalletcli/) pakiet.

Po wprowadzeniu tej zmiany, ponownie załaduj gpg-agent.

### Bezobsługowe hasło

Począwszy od GnuPG 2.1.0, wymagane jest użycie gpg-agent i pinentry, co może przełamać kompatybilność wsteczną dla haseł wprowadzanych przez STDIN za pomocą opcji `--passphrase-fd 0`. Aby mieć ten sam typ funkcjonalności co starsze wersje, należy zrobić dwie rzeczy:

Najpierw edytuj konfigurację gpg-agent, aby umożliwić tryb pracy z *loopback*

 `~/.gnupg/gpg-agent.conf`  `allow-loopback-pinentry` 

Zrestartuj proces gpg-agent, jeśli jest uruchomiony, aby zmiana zaczęła obowiązywać.

Po drugie, albo aplikacja musi zostać zaktualizowana, aby zawierała parametr wiersza poleceń, aby użyć trybu pętli zwrotnej, jak na przykład:

```
$ gpg --pinentry-mode loopback ...

```

...lub jeśli nie jest to możliwe, dodaj opcję do konfiguracji:

 `~/.gnupg/gpg.conf`  `pinentry-mode loopback` 
**Note:** The upstream author indicates setting `pinentry-mode loopback` in `gpg.conf` may break other usage, using the commandline option should be preferred if at all possible. [[4]](https://bugs.g10code.com/gnupg/issue1772)

### SSH agent

*gpg-agent* ma emulację agenta OpenSSH. Jeśli już korzystasz z pakietu GnuPG, możesz rozważyć użycie jego agenta do buforowania [SSH keys](/index.php/SSH_keys "SSH keys") Ponadto niektórzy użytkownicy mogą preferować okno dialogowe wprowadzania kodu PIN, które zapewnia agent GnuPG w ramach zarządzania hasłami.

#### Set SSH_AUTH_SOCK

Musisz ustawić `SSH_AUTH_SOCK`, aby SSH używał *gpg-agent* zamiast *ssh-agent*. Aby upewnić się, że każdy proces może znaleźć Twoją instancję gpg-agent niezależnie od np. typ powłoki jest dzieckiem użytkowania [pam_env](/index.php/Environment_variables#Using_pam_env "Environment variables").

 `~/.pam_environment` 
```
SSH_AGENT_PID	DEFAULT=
SSH_AUTH_SOCK	DEFAULT="${XDG_RUNTIME_DIR}/gnupg/S.gpg-agent.ssh"
```

**Note:** Jeśli ustawisz `SSH_AUTH_SOCK` ręcznie (na przykład w tym przykładzie pam_env), pamiętaj, że lokalizacja gniazda może być inna, jeśli używasz niestandardowego `GNUPGHOME`. Możesz użyć poniższego przykładu bash lub zmienić `SSH_AUTH_SOCK` na wartość `gpgconf --list-dirs agent-ssh-socket`.

Ewentualnie zależą od Bash. Działa to również w przypadku niestandardowych lokalizacji gniazd:

 `~/.bashrc` 
```
unset SSH_AGENT_PID
if [ "${gnupg_SSH_AUTH_SOCK_by:-0}" -ne $$ ]; then
  export SSH_AUTH_SOCK="$(gpgconf --list-dirs agent-ssh-socket)"
fi
```

**Note:** The test involving the `gnupg_SSH_AUTH_SOCK_by` variable is for the case where the agent is started as `gpg-agent --daemon /bin/sh`, in which case the shell inherits the `SSH_AUTH_SOCK` variable from the parent, *gpg-agent* [[5]](http://git.gnupg.org/cgi-bin/gitweb.cgi?p=gnupg.git;a=blob;f=agent/gpg-agent.c;hb=7bca3be65e510eda40572327b87922834ebe07eb#l1307).

#### Skonfiguruj pinentry, aby użyć prawidłowego TTY

Ustaw również GPG_TTY i odśwież TTY, jeśli użytkownik przełączył się w sesję X, jak podano w [gpg-agent(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gpg-agent.1). Na przykład:

 `~/.bashrc` 
```
# Set GPG TTY
export GPG_TTY=$(tty)

# Refresh gpg-agent tty in case user switches into an X session
gpg-connect-agent updatestartuptty /bye >/dev/null

```

#### Dodaj klucze SSH

Po uruchomieniu *gpg-agent* możesz użyć *ssh-add* do zatwierdzenia kluczy, wykonując te same kroki, co dla [ssh-agent](/index.php/SSH_keys#ssh-agent "SSH keys"). Lista zatwierdzonych kluczy przechowywana jest w pliku `~/.gnupg/sshcontrol`.

Po zatwierdzeniu klucza, za każdym razem, gdy potrzebne jest hasło, otrzymasz okno dialogowe z danymi. Możesz kontrolować buforowanie hasła w pliku `~/.gnupg/gpg-agent.conf`. W poniższym przykładzie *gpg-agent* będzie przechowywać klucze w pamięci podręcznej przez 3 godziny:

 `~/.gnupg/gpg-agent.conf` 
```
default-cache-ttl-ssh 10800
max-cache-ttl-ssh 10800

```

#### Użyj klucza GPG jako klucza SSH

Jeśli używasz *gpg-agent* jako agent SSH, możesz użyć swojego klucza GnuPG jako klucza SSH. Zmniejsza to kluczową konserwację i możesz przechowywać klucz SSH na karcie dostępu. Musisz utworzyć klucz z funkcją uwierzytelniania (patrz [#Custom capabilities](#Custom_capabilities)). GnuPG automatycznie użyje tego klucza, jeśli będzie to konieczne. Aby sprawdzić, czy klucz został dodany, uruchom:

```
$ ssh-add -l

```

Komentarz do klucza powinien wyglądać tak: `openpgp:*key-id*` `cardno:*card-id*`*.*

**Note:** GnuPG może nie dodać twojego klucza GnuPG do $ `$GNUPGHOME/sshcontrol`, gdzie znajdują się "normalne" klucze SSH.

## Smartcards

GnuPG używa scdaemona jako interfejsu do czytnika kart inteligentnych. Szczegółowe informacje znajdują się w [man page](/index.php/Man_page "Man page")

### GnuPG only setups

**Note:** Aby umożliwić scdaemonowi bezpośredni dostęp do czytników kart USB smar, musi być zainstalowana opcjonalna zależność [libusb-compat](https://www.archlinux.org/packages/?name=libusb-compat).

Jeśli nie planujesz używać innych kart oprócz tych opartych na GnuPG, powinieneś sprawdzić parametr port-czytnika w `~/.gnupg/scdaemon.conf`. Wartość "0" odnosi się do pierwszego dostępnego czytnika portów szeregowych, a wartość "32768" (domyślnie) odnosi się do pierwszego czytnika USB.

### GnuPG z pcscd (PCSC Lite)

**Note:** Należy zainstalować [pcsclite](https://www.archlinux.org/packages/?name=pcsclite) i [ccid](https://www.archlinux.org/packages/?name=ccid) a zawarta usługa [systemd](/index.php/Systemd#Using_units "Systemd") `pcscd.service` musi być uruchomiona, lub gniazdo pcscd.socket musi nasłuchiwać.

pcscd to demon, który obsługuje dostęp do karty inteligentnej (SCard API). Jeśli scduemon GnuPG nie połączy bezpośrednio karty inteligentnej (np. Za pomocą zintegrowanej obsługi CCID), będzie się starał znaleźć kartę elektroniczną za pomocą sterownika PCSC Lite.

#### Zawsze używaj pcscd

Jeśli używasz jakiejkolwiek karty inteligentnej ze sterownikiem opensc (np .: karty identyfikacyjne z niektórych krajów) powinieneś zwrócić uwagę na konfigurację GnuPG. Po wyjęciu z pudełka możesz otrzymać wiadomość podobną do tej, gdy używasz `gpg --card-status`

```
gpg: selecting openpgp failed: ec=6.108

```

Domyślnie scdaemon będzie próbował łączyć się bezpośrednio z urządzeniem. To połączenie zakończy się niepowodzeniem, jeśli czytnik będzie używany przez inny proces. Na przykład: demon pcscd używany przez OpenSC. Aby poradzić sobie z tą sytuacją, powinniśmy użyć tego samego sterownika, co opensc, aby mogli dobrze współpracować. W celu wskazania scdaemona do użycia pcscd powinieneś usunąć `reader-port` z `~/.gnupg/scdaemon.conf`, określić lokalizację biblioteki `libpcsclite.so` i wyłączyć ccid, abyśmy upewnili się, że używamy pcscd:

 `~/.gnupg/scdaemon.conf` 
```
pcsc-driver /usr/lib/libpcsclite.so
card-timeout 5
disable-ccid

```

Sprawdź [scdaemon(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/scdaemon.1), jeśli nie korzystasz z OpenSC.

## Porady i wskazówki

### Inny algorytm

Możesz użyć silniejszych algorytmów:

 `~/.gnupg/gpg.conf` 
```
...

personal-digest-preferences SHA512
cert-digest-algo SHA512
default-preference-list SHA512 SHA384 SHA256 SHA224 AES256 AES192 AES CAST5 ZLIB BZIP2 ZIP Uncompressed
personal-cipher-preferences TWOFISH CAMELLIA256 AES 3DES

```

W najnowszej wersji GnuPG domyślnymi algorytmami są SHA256 i AES, które są wystarczająco bezpieczne dla większości ludzi. Jeśli jednak używasz wersji GnuPG starszej niż 2.1 lub chcesz uzyskać jeszcze wyższy poziom bezpieczeństwa, wykonaj powyższy krok.

### Zaszyfruj hasło

Przydaje się szyfrowanie hasła, więc nie będzie ono zapisane w pliku konfiguracyjnym. Dobrym przykładem jest twoje hasło e-mail.

Najpierw utwórz plik z hasłem. Po podaniu hasła musisz zostawić jedną pustą linię, w przeciwnym razie gpg zwróci komunikat o błędzie podczas oceniania pliku.

Następnie uruchom:

```
$ gpg -e -a -r *<user-id>* *your_password_file*

```

`-e` is for encrypt, `-a` for armor (ASCII output), `-r` for recipient user ID.

Zostaniesz z nowym plikiem `*your_password_file*.asc`

**Tip:** [pass](/index.php/Pass "Pass") automatyzuje ten proces.

### Odwoływanie klucza

**Warning:**

*   Każdy, kto ma dostęp do Twojego certyfikatu unieważnienia, może odwołać klucz, czyniąc go bezużytecznym.
*   Odwołanie klucza powinno być wykonywane tylko w przypadku złamania lub zgubienia klucza, lub zapomnienia hasła.

Certyfikaty unieważnienia są generowane automatycznie dla nowo wygenerowanych kluczy, chociaż jeden z nich może zostać wygenerowany ręcznie przez użytkownika później. Są one zlokalizowane w `~/.gnupg/openpgp-revocs.d/`. Nazwa pliku certyfikatu to odcisk palca klucza, który zostanie odwołany.

Aby unieważnić klucz, wystarczy zaimportować certyfikat unieważnienia:

```
$ gpg --import *<fingerprint>*.rev

```

Teraz zaktualizuj serwer kluczy:

```
$ gpg --keyserver subkeys.pgp.net --send-keys *<userid>*

```

### Change trust model

By default GnuPG uses the [Web of Trust](https://en.wikipedia.org/wiki/Web_of_Trust "wikipedia:Web of Trust") as the trust model. You can change this to [Trust on first use](https://en.wikipedia.org/wiki/Trust_on_first_use "wikipedia:Trust on first use") by adding `--trust-model=tofu` when adding a key or adding this option to your GnuPG configuration file. More details are in [this email to the GnuPG list](https://lists.gnupg.org/pipermail/gnupg-devel/2015-October/030341.html).

### Ukryj wszystkie identyfikatory odbiorców

Domyślnie identyfikator klucza odbiorcy znajduje się w zaszyfrowanej wiadomości. Można go usunąć w czasie szyfrowania dla odbiorcy za pomocą ukrytego odbiorcy `hidden-recipient *<user-id>*`. Aby usunąć go dla wszystkich odbiorców, dodaj `throw-keyids` do pliku konfiguracyjnego. Pomaga to ukryć odbiorców wiadomości i stanowi ograniczony środek zaradczy przeciwko analizie ruchu. (Korzystając z małej inżynierii społecznej, każdy, kto potrafi odszyfrować wiadomość, może sprawdzić, czy jeden z pozostałych odbiorców jest tym, kogo podejrzewa.) Po stronie odbierającej może spowolnić proces deszyfrowania, ponieważ wszystkie dostępne klucze tajne muszą zostać wypróbowane ( np. z `--try-secret-key *<user-id>*`).

### Używanie caff do wysyłania kluczy partiami

Aby umożliwić użytkownikom sprawdzanie poprawności kluczy w serwerach kluczy iw ich plikach kluczy (to znaczy upewnić się, że pochodzą od kogo się podają), PGP/GPG korzysta z [Web of Trust](https://en.wikipedia.org/wiki/Web_of_Trust "wikipedia:Web of Trust"). Strony z kluczami pozwalają użytkownikom zebrać się w fizycznej lokalizacji, aby sprawdzić klucze. Protokół podpisywania kluczy [Zimmermann-Sassaman](https://en.wikipedia.org/wiki/Zimmermann%E2%80%93Sassaman_key-signing_protocol "wikipedia:Zimmermann–Sassaman key-signing protocol") jest sposobem na uczynienie ich bardzo skutecznymi. Tutaj znajdziesz artykuł z instrukcjami.

Aby ułatwić proces podpisywania kluczy i wysyłania podpisów do właścicieli po keysigning party możesz użyć narzędzia caff. Można go zainstalować z AUR z pakietem [caff-svn](https://aur.archlinux.org/packages/caff-svn/).

Aby wysłać podpisy do ich właścicieli, potrzebujesz działającego [MTA](https://en.wikipedia.org/wiki/Message_transfer_agent "wikipedia:Message transfer agent"). Jeśli jeszcze go nie masz, zainstaluj [msmtp](/index.php/Msmtp "Msmtp").

### Zawsze pokazuj długie identyfikatory i odciski palca

Aby zawsze wyświetlać długie identyfikatory klucza, dodaj plik `keyid-format 0xlong` do pliku konfiguracyjnego. Aby zawsze wyświetlać pełne `with-fingerprint` do pliku konfiguracyjnego.

### Niestandardowe funkcje

W celu dalszego dostosowania można również ustawić niestandardowe możliwości do kluczy. Dostępne są następujące możliwości:

*   Certify (tylko dla kluczy głównych) - pozwala kluczowi tworzyć podklucze, obowiązkowe dla kluczy głównych.
*   Sign - pozwala kluczowi tworzyć podpisy kryptograficzne, które inni mogą zweryfikować za pomocą klucza publicznego.
*   Encrypt - umożliwia każdemu szyfrowanie danych za pomocą klucza publicznego, który tylko klucz prywatny może odszyfrować.
*   Authenticate - umożliwia uwierzytelnianie klucza za pomocą różnych programów innych niż GnuPG. Klucz może być użyty jako np. klucz SSH.

Możliwe jest określenie możliwości klucza głównego, uruchamiając:

```
$ gpg --full-generate-key --expert

```

Wybierz opcję, która pozwala ustawić własne możliwości.

Comparably, to specify custom capabilities for subkeys, add the `--expert` flag to `gpg --edit-key`, see [#Edit your key](#Edit_your_key) for more information.

Porównywalnie, aby określić niestandardowe możliwości dla podkluczy, dodaj `--expert` flag to `gpg --edit-key` zobacz [#Edit your key](#Edit_your_key), aby uzyskać więcej informacji.

### Cache passwords

Aby otrzymać hasło do GnuPG tylko raz na sesję, ustaw `max-cache-ttl` i `default-cache-ttl` na coś bardzo wysokiego, na przykład:

 `gpg-agent.conf` 
```
max-cache-ttl 60480000
default-cache-ttl 60480000

```

Zobacz [#gpg-agent](#gpg-agent).

## Rozwiązywanie problemów:

### Nie ma wystarczającej liczby losowych bajtów

Podczas generowania klucza, gpg można napotkać ten błąd:

```
Not enough random bytes available. Please do some other work to give the OS a chance to collect more entropy!

```

Aby sprawdzić dostępną entropię, sprawdź parametry jądra:

```
cat /proc/sys/kernel/random/entropy_avail

```

Zdrowy system linuksowy z dużą dostępną entropią powróci do pełnej liczby 4096 bitów entropii. Jeśli wartość zwracana jest mniejsza niż 200, systemu zaczyna brakować entropii.

Aby go rozwiązać, pamiętaj, że często nie trzeba tworzyć kluczy, a najlepiej robić to, co sugeruje komunikat (np. Tworzyć aktywność na dysku, poruszać myszą, edytować wiki - wszystko stworzy entropię). Jeśli to nie pomoże, sprawdź, która usługa wykorzystuje entropię i zastanów się, czy nie zatrzymać jej na czas. Jeśli to nie jest alternatywa, zobacz [Random number generation#Alternatives](/index.php/Random_number_generation#Alternatives "Random number generation").

### su

Podczas używania `pinentry` musisz mieć odpowiednie uprawnienia urządzenia końcowego (np. `/dev/tty1`) w użyciu. Jednak w przypadku *su* (lub *sudo*) własność pozostaje z oryginalnym użytkownikiem, a nie nowym. Oznacza to, że pinentry zawiedzie, nawet jako root. Poprawka polega na zmianie uprawnień urządzenia w pewnym momencie przed użyciem pinentry (tj. Za pomocą gpg z agentem). Jeśli robisz gpg jako root, po prostu zmień właściciela na root przed użyciem gpg:

```
# chown root /dev/ttyN  # where N is the current tty

```

a następnie zmienić go po użyciu gpg po raz pierwszy. Odpowiednik ten prawdopodobnie będzie true w `/dev/pts/`.

**Note:** Właściciel tty musi być zgodny z użytkownikiem, dla którego działa pinentry. Bycie częścią grupy `tty` **nie** wystarczy.

**Tip:** Jeśli uruchomisz gpg ze `script`, użyje on nowego tty z poprawną wartością:
```
# script -q -c "gpg --gen-key" /dev/null

```

### Agent complains end of file

Domyślnym programem pinentry jest pinentry-gtk-2, który do prawidłowego działania potrzebuje magistrali sesji DBus. Zobacz [General troubleshooting#Session permissions](/index.php/General_troubleshooting#Session_permissions "General troubleshooting") szczegółowe informacje.

Alternatywnie możesz użyć `pinentry-qt`. Zobacz [#pinentry](#pinentry).

### KGpg configuration permissions

Pojawiły się problemy z [kgpg](https://www.archlinux.org/packages/?name=kgpg) możliwością uzyskania dostępu do pliku `~/.gnupg/` options. Jeden problem może być wynikiem przestarzałego pliku opcji, zobacz raport o błędzie [bug](https://bugs.kde.org/show_bug.cgi?id=290221) report.

### GNOME na Wayland zastępuje gniazdo agenta SSH

W przypadku sesji Wayland, `gnome-session` ustawia SSH_AUTH_SOCK na standardowe gniazdo gnome-keyring, $ `$XDG_RUNTIME_DIR/keyring/ssh`. To przesłoni wszelkie wartości ustawione w `~/.pam_environmment` lub systemd jednostek jednostkowych.

Aby wyłączyć to zachowanie, ustaw zmienną `GSM_SKIP_AGENT_WORKAROUND`:

 `~/.pam_environment` 
```
SSH_AGENT_PID	DEFAULT=
SSH_AUTH_SOCK	DEFAULT="${XDG_RUNTIME_DIR}/gnupg/S.gpg-agent.ssh"
GSM_SKIP_SSH_AGENT_WORKAROUND	DEFAULT="true"
```

### mutt

Mutt może nie używać poprawnie *gpg-agent*, musisz ustawić zmienną środowiskową `GPG_AGENT_INFO` (treść nie ma znaczenia) podczas uruchamiania mutt. Upewnij się także, czy poprawnie buforujesz hasła, patrz [#Cache passwords](#Cache_passwords).

Zobacz [this forum thread](https://bbs.archlinux.org/viewtopic.php?pid=1490821#p1490821)

### "Utracone" klucze, aktualizacja do wersji 2.1 Gnupg

Kiedy gpg `gpg --list-keys` nie pokazuje kluczy, które były tam wcześniej, a aplikacje narzekają na brakujące lub nieprawidłowe klucze, niektóre klucze mogły nie zostać zmigrowane do nowego formatu.

Przeczytaj [http://jo-ke.name/wp/?p=111](http://jo-ke.name/wp/?p=111) GnuPG invalid packet workaround] Zasadniczo jest napisane, że istnieje błąd związany z kluczami w starych plikach `pubring.gpg` i `secring.gpg`, które zostały zastąpione nowym plikiem `pubring.kbx` oraz podkatalogiem `private-keys-v1.d/` i plikami. Twoje brakujące klucze można odzyskać za pomocą następujących komend:

```
$ cd
$ cp -r .gnupg gnupgOLD
$ gpg --export-ownertrust > otrust.txt
$ gpg --import .gnupg/pubring.gpg
$ gpg --import-ownertrust otrust.txt
$ gpg --list-keys

```

### gpg zawiesza się dla wszystkich serwerów kluczy (podczas próby odebrania kluczy)

Jeśli gpg zawieszi się z określonym serwerem kluczy podczas próby odebrania kluczy, być może trzeba zabić dirmngr, aby uzyskać dostęp do innych serwerów kluczy, które faktycznie działają, w przeciwnym razie może zachowywać zawieszenie dla nich wszystkich.

### Nie wykryto SmartCard

Twój użytkownik może nie mieć uprawnień dostępu do karty elektronicznej, co powoduje `card error` , mimo że karta jest poprawnie skonfigurowana i włożona.

Jednym z możliwych rozwiązań jest dodanie nowego `scard` grupy, w tym użytkowników, którzy potrzebują dostępu do smartcard.

Następnie użyj reguły [udev](/index.php/Udev#Writing_udev_rules "Udev") , podobnej do następującej:

 `/etc/udev/rules.d/71-gnupg-ccid.rules` 
```
ACTION=="add", SUBSYSTEM=="usb", ENV{ID_VENDOR_ID}=="1050", ENV{ID_MODEL_ID}=="0116|0111", MODE="660", GROUP="scard"

```

Trzeba dostosować VENDOR i MODEL zgodnie z wyjściem `lsusb`, powyższy przykład dotyczy YubikeyNEO.

### gpg: WARNING: server 'gpg-agent' is older than us (x < y)

To ostrzeżenie pojawia się, gdy `gnupg`jest uaktualniony, a stary gpg-agent nadal działa. [Zrestartuj](/index.php/Restart "Restart") `gpg-agent.socket` użytkownika (tj. Użyj flagi `--user` podczas ponownego uruchamiania).

### gpg: ..., IPC connect call failed

Upewnij się, że `gpg-agent` i `dirmngr` nie działają z `killall gpg-agent dirmngr`, a folder `$GNUPGHOME/crls.d/` ma uprawnienia ustawione na `700`.

Jeśli twoj keyring jest przechowywana na systemie plików vFat (np. Dysku USB), `gpg-agent` nie będzie w stanie utworzyć wymaganych gniazd (vFat nie obsługuje gniazd), możesz utworzyć przekierowania do lokalizacji, która obsługuje gniazda, np. `/dev/shm`:

```
# export GNUPGHOME=/custom/gpg/home
# printf '%%Assuan%%
socket=/dev/shm/S.gpg-agent
' > $GNUPGHOME/S.gpg-agent
# printf '%%Assuan%%
socket=/dev/shm/S.gpg-agent.browser
' > $GNUPGHOME/S.gpg-agent.browser
# printf '%%Assuan%%
socket=/dev/shm/S.gpg-agent.extra
' > $GNUPGHOME/S.gpg-agent.extra
# printf '%%Assuan%%
socket=/dev/shm/S.gpg-agent.ssh
' > $GNUPGHOME/S.gpg-agent.ssh

```

Sprawdź, czy gpg-agent uruchamia się pomyślnie z `gpg-agent --daemon`.

## Zobacz też

*   [GNU Privacy Guard Homepage](https://gnupg.org/)
*   [RFC4880 "OpenPGP Message Format"](https://tools.ietf.org/html/rfc4880)
*   [Creating GPG Keys (Fedora)](https://fedoraproject.org/wiki/Creating_GPG_Keys)
*   [OpenPGP subkeys in Debian](https://wiki.debian.org/Subkeys)
*   [A more comprehensive gpg Tutorial](https://sanctum.geek.nz/arabesque/series/gnu-linux-crypto/)
*   [gpg.conf recommendations and best practices](https://help.riseup.net/en/security/message-security/openpgp/gpg-best-practices)
*   [Torbirdy gpg.conf](https://github.com/ioerror/torbirdy/blob/master/gpg.conf)
*   [/r/GPGpractice - a subreddit to practice using GnuPG.](https://www.reddit.com/r/GPGpractice/)
*   [Protecting code integrity with PGP](https://github.com/lfit/itpol/blob/master/protecting-code-integrity.md)