W tym artykule omówiono wspólne techniki szyfowania dostępne w Arch Linux do kryptograficznej ochrony logicznej części dysku twardego (folder, partycja, cały dysk, ...), dzięki czemu wszystkie zapisane w nim dane są automatycznie szyfrowane i odszyfrowywane w locie po ponownym odczytaniu.

Dyski do przechowywania "w tym kontekście mogą być dyskami twardymi komputera, urządzeniami zewnętrznymi, takimi jak dyski flash USB lub dyski DVD, a także dyskami wirtualnymi, takimi jak urządzenia loop-back devices lub Chmura publiczna. (o ile Arch Linux może go adresować jako urządzenie blokowe lub system plików).

## Contents

*   [1 Po co używać szyfrowania?](#Po_co_u.C5.BCywa.C4.87_szyfrowania.3F)
*   [2 Szyfrowanie danych vs szyfrowanie systemu](#Szyfrowanie_danych_vs_szyfrowanie_systemu)
*   [3 Dostępne metody](#Dost.C4.99pne_metody)
*   [4 Ułożone szyfrowania systemu plików](#U.C5.82o.C5.BCone_szyfrowania_systemu_plik.C3.B3w)
    *   [4.1 blokowe szyfrowanie dysków](#blokowe_szyfrowanie_dysk.C3.B3w)
    *   [4.2 Tabela porównawcza](#Tabela_por.C3.B3wnawcza)
        *   [4.2.1 Podsumowanie](#Podsumowanie)
        *   [4.2.2 Podstawowa klasyfikacja](#Podstawowa_klasyfikacja)
        *   [4.2.3 praktyczne implikacje](#praktyczne_implikacje)
        *   [4.2.4 Usability features](#Usability_features)
        *   [4.2.5 Funkcje zabezpieczeń](#Funkcje_zabezpiecze.C5.84)
        *   [4.2.6 Funkcje wydajności](#Funkcje_wydajno.C5.9Bci)
        *   [4.2.7 Block device encryption specific](#Block_device_encryption_specific)
        *   [4.2.8 Skumulowane szyfrowanie systemu plików](#Skumulowane_szyfrowanie_systemu_plik.C3.B3w)
        *   [4.2.9 Zgodność i rozpowszechnienie](#Zgodno.C5.9B.C4.87_i_rozpowszechnienie)
*   [5 Przygotowanie](#Przygotowanie)
    *   [5.1 Wybór konfiguracji](#Wyb.C3.B3r_konfiguracji)
    *   [5.2 Przykłady](#Przyk.C5.82ady)
    *   [5.3 Wybieranie silnego hasła](#Wybieranie_silnego_has.C5.82a)
    *   [5.4 Przygotowanie dysku](#Przygotowanie_dysku)
*   [6 Jak działa szyfrowanie](#Jak_dzia.C5.82a_szyfrowanie)
    *   [6.1 Podstawowa zasada](#Podstawowa_zasada)
    *   [6.2 Klucze, pliki kluczy i hasła](#Klucze.2C_pliki_kluczy_i_has.C5.82a)
    *   [6.3 Kryptograficzne metadane](#Kryptograficzne_metadane)
    *   [6.4 Szyfry i tryby działania](#Szyfry_i_tryby_dzia.C5.82ania)

## Po co używać szyfrowania?

Szyfrowanie dysku zapewnia, że pliki są zawsze przechowywane na dysku w postaci zaszyfrowanej. Pliki będą dostępne tylko dla systemu operacyjnego i aplikacji w czytelnej formie, podczas gdy system jest uruchomiony i odblokowane przez zaufanego użytkownika. Nieautoryzowana osoba, patrząc bezpośrednio na zawartość dysku, znajdzie tylko losowo wyglądające dane zamiast rzeczywistych plików.

Na przykład może to zapobiec nieautoryzowanemu przeglądaniu danych, gdy komputer lub dysk twardy jest:

*   znajduje się w miejscu, do którego niezaufani ludzie mogą uzyskać dostęp, gdy jesteś nieobecny
*   zgubione lub skradzione, tak jak w przypadku laptopów, netbooków lub zewnętrznych urządzeń pamięci masowej
*   w warsztacie naprawczym
*   wyrzucony po zakończeniu eksploatacji

Ponadto szyfrowanie dysku może również służyć do zabezpieczenia przed nieautoryzowanymi próbami manipulowania systemem operacyjnym - na przykład instalowaniem keyloggerów lub koni trojańskich przez atakujących, którzy mogą uzyskać fizyczny dostęp do systemu, gdy jesteś nieobecny.

**Warning:** Szyfrowanie dysku nie chroni danych przed wszystkimi zagrożeniami.

Nadal będziesz narażony na:

*   Atakujący, którzy mogą włamać się do twojego systemu (np. Przez Internet) podczas jego działania i po odblokowaniu i zamontowaniu zaszyfrowanych części dysku.
*   Atakujący, którzy mogą uzyskać fizyczny dostęp do komputera podczas jego pracy (nawet jeśli używasz screenlockera) lub bardzo krótko po jego uruchomieniu, jeśli mają zasoby do wykonania
*   Podmiot rządowy, który ma nie tylko zasoby do łatwego zlikwidowania powyższych ataków, ale może również po prostu zmusić cię do oddania kluczy / haseł przy użyciu różnych technik przymusu. W większości krajów nie-demokratycznych na świecie, a także w Stanach Zjednoczonych i Wielkiej Brytanii, organy odpowiedzialne za egzekwowanie prawa mogą być zgodne z prawem, jeśli mają podejrzenia, że możesz ukrywać coś interesującego.

Bardzo silna konfiguracja szyfrowania dysku (np. Pełne szyfrowanie systemu z weryfikacją autentyczności i brak partycji rozruchowej tekstowej) jest niezbędna, aby mieć szansę przed profesjonalnymi atakującymi, którzy mogą manipulować systemem przed jego użyciem. I nawet wtedy wątpliwe jest, czy naprawdę może zapobiec wszelkim manipulacjom (np. Keyloggerom sprzętowym).

**Warning:** Szyfrowanie dysku również nie chroni przed uszkodzeniem dysku. Zalecane są regularne kopie zapasowe, aby zapewnić bezpieczeństwo danych.

## Szyfrowanie danych vs szyfrowanie systemu

	Szyfrowanie danych

	Zdefiniowane jako szyfrujące tylko same dane użytkownika (często znajdujące się w katalogu / home lub na nośnikach wymiennych, takich jak płyty DVD z danymi), szyfrowanie danych jest najprostszym i najmniej inwazyjnym zastosowaniem szyfrowania dysku, ale ma pewne znaczące wady.

	W nowoczesnych systemach komputerowych istnieje wiele procesów w tle, które mogą przechowywać informacje o danych użytkownika lub częściach danych w niezabezpieczonych obszarach dysku twardego, takie jak:

*   partycje wymiany
    *   (potencjalne środki zaradcze: wyłączyć wymianę lub skorzystać z szyfrowanej wymiany)

*   `/tmp` (pliki tymczasowe utworzone przez aplikacje użytkowników)
    *   potencjalne środki zaradcze: unikaj takich wniosków; mount / tmp wewnątrz ramdyska

*   `/var` (pliki dzienników i bazy danych i takie, na przykład mlocate przechowuje indeks wszystkich nazw plików w `/var/lib/mlocate/mlocate.db`)

	Ponadto zwykłe szyfrowanie danych pozostawia zagrożenie atakom manipulacyjnym w systemie offline (np. Ktoś instalujący ukryty program, który rejestruje hasła używane do odblokowania zaszyfrowanych danych lub oczekuje na jego odblokowanie, a następnie potajemnie kopiuje / wysyła niektóre dane do miejsca, w którym osoba atakująca może ją pobrać).

	Szyfrowanie systemu

	Zdefiniowane jako szyfrowanie danych systemu operacyjnego i danych użytkownika, szyfrowanie systemu pomaga rozwiązać niektóre niedociągnięcia szyfrowania danych.

	Korzyści:

*   zapobiega nieautoryzowanemu fizycznemu dostępowi do plików systemu operacyjnego (i manipulowaniu nimi) (ale patrz ostrzeżenie powyżej)
*   zapobiega nieautoryzowanemu dostępowi fizycznemu do prywatnych danych, które mogą być przechowywane w pamięci podręcznej przez system

	Niedogodności:

*   odblokowanie zaszyfrowanych części dysku może się nie zdarzyć w trakcie logowania użytkownika lub po nim; to musi się teraz zdarzyć w czasie rozruchu

W praktyce nie zawsze jest jasna granica między szyfrowaniem danych a szyfrowaniem systemu, a wiele różnych kompromisów i dostosowanych ustawień są możliwe.

W każdym razie szyfrowanie dysku powinno być postrzegane jedynie jako uzupełnienie istniejących mechanizmów bezpieczeństwa systemu operacyjnego - skoncentrowane na zabezpieczeniu fizycznego dostępu w trybie offline, przy jednoczesnym wykorzystaniu "innych" elementów systemu w celu zapewnienia bezpieczeństwa sieci i kontrolą dostępu użytkowników.

Zobacz też [Wikipedia:Disk encryption](https://en.wikipedia.org/wiki/Disk_encryption "wikipedia:Disk encryption").

## Dostępne metody

Wszystkie metody szyfrowania dysków działają w taki sposób, że nawet jeśli dysk ma rzeczywiście zaszyfrowane dane, system operacyjny i aplikacje "widzą" go jako odpowiednie, czytelne dane, o ile kontener kryptograficzny (tj. Logiczna część dysku, zaszyfrowane dane) został "odblokowany" i zamontowany.

W tym celu należy podać "informacje tajne" (zwykle w postaci pliku z kluczami i / lub hasła), z którego można uzyskać klucz szyfrujący (i przechowywane w kluczu jądra na czas trwania sesji).

Jeśli nie jesteś całkowicie obeznany z tego rodzaju operacją, przeczytaj również część #Jak działa sekcja szyfrowania poniżej.

Dostępne metody szyfrowania dysków można rozdzielić na dwa typy:

## Ułożone szyfrowania systemu plików

Ujednolicone rozwiązania szyfrowania plików są implementowane jako warstwa, która układa się na wierzchu istniejącego systemu plików, powodując, że wszystkie pliki zapisane w folderze z włączoną szyfrowaniem mają być szyfrowane w locie przed podstawowym systemem plików zapisywanym na dysku i odszyfrowywane w każdym przypadku, gdy system plików odczytuje je z dysku. W ten sposób pliki są przechowywane w systemie plików hostów w zaszyfrowanej formie (co oznacza, że ich zawartość, a zwykle również ich nazwy plików / folderów, zastępuje się losowo wyglądającymi danymi o przybliżonej długości), ale inne niż to, które wciąż istnieją w tym systemie plików, bez szyfrowania, jako zwykłe pliki / symlink / hardlinks / etc.

Sposób, w jaki jest zaimplementowany, polega na tym, że aby odblokować folder przechowujący surowe zaszyfrowane pliki w systemie plików hosta ("katalog dolny"), jest on montowany (za pomocą specjalnego stosowego pseudo-systemu plików) na sobie lub opcjonalnie w innej lokalizacji ("górny katalog"), gdzie te same pliki pojawiają się w czytelnej formie - dopóki nie zostanie odmontowany ponownie lub system zostanie wyłączony.

Dostępne rozwiązania w tej kategorii to:

### blokowe szyfrowanie dysków

Z drugiej strony, metody szyfrowania urządzeń blokowych działają pod warstwą systemu plików i zapewniają, że wszystko zapisane na określonym urządzeniu blokowym (np. Cały dysk, partycja lub plik działający jako urządzenie z pętlą zwrotną) jest zaszyfrowane . Oznacza to, że podczas gdy urządzenie blokowe jest w trybie offline, cała jego zawartość wygląda na dużą porcję danych losowych, bez możliwości określenia, jaki rodzaj systemu plików i danych zawiera. Uzyskanie dostępu do danych odbywa się ponownie poprzez zamontowanie zabezpieczonego kontenera (w tym przypadku urządzenia blokowego) w dowolnym miejscu w specjalny sposób.

Następujące "szyfrowanie urządzeń blokowych" są dostępne w Arch Linux:

	loop-AES

	jest potomkiem cryptoloop i jest bezpiecznym i szybkim rozwiązaniem do szyfrowania systemu. Jednak pętla AES jest uważana za mniej przyjazną dla użytkownika niż inne opcje, ponieważ wymaga niestandardowego wsparcia jądra.

	dm-crypt

	dm-crypt to standardowa funkcja szyfrowania urządzenia-odwzorowania dostarczana przez jądro Linux. Może być używany bezpośrednio przez tych, którzy lubią mieć pełną kontrolę nad wszystkimi aspektami partycjonowania i zarządzania kluczami. Zarządzanie dm-crypt odbywa się za pomocą narzędzia przestrzeni użytkownika cryptsetup. Może być używany do następujących typów szyfrowania urządzeń blokowych: LUKS (domyślnie), zwykły i ma ograniczone funkcje dla urządzeń loopAES i Truecrypt.

LUKS, used by default, is an additional convenience layer which stores all of the needed setup information for dm-crypt on the disk itself and abstracts partition and key management in an attempt to improve ease of use and cryptographic security.

*   Dodatkowym udogodnieniem jest LUKS, używane domyślnie, która w celu zwiększenia łatwości obsługi i bezpieczeństwa kryptograficznego zapisuje wszystkie informacje potrzebne do konfiguracji dm-crypt na samej partycji dysku i zarządzania w celu poprawy łatwości obsługi i bezpieczeństwa kryptograficznego.

*   zwykły tryb dm-crypt, będący oryginalną funkcjonalnością jądra, nie wykorzystuje warstwy wygody. Trudniej jest zastosować taką samą siłę kryptograficzną. W ten sposób powstają dłuższe klucze (hasła lub pliki kluczy). Ma jednak inne zalety, opisane w poniższej tabeli porównawczej.

	TrueCrypt

Należy zauważyć, że twórcy TrueCrypt zakończyła wsparcie dla niego w maju 2014 r.

Dla praktycznych implikacji wybranej warstwy działania, patrz tabela porównania poniżej, a także ogólny zapis do eCryptfs. Zobacz Kategoria: Szyfrowanie w celu uzyskania dostępnej zawartości omawianych metod, a także innych narzędzi nieuwzględnionych w tabeli.

### Tabela porównawcza

Kolumna "dm-crypt +/- LUKS" oznacza funkcje cryptu dm dla LUKS ("+") i zwykłych ("-") trybów szyfrowania. Jeśli określona funkcja wymaga użycia LUKS, oznacza to "(z LUKS)". Podobnie "(bez LUKS)" wskazuje, że użycie LUKS jest przeciwny do osiągnięcia tej funkcji i powinien używać trybu zwykłego.

| 

##### Podsumowanie

 | Loop-AES | dm-crypt +/- LUKS | Truecrypt | eCryptfs | EncFs |
| Rodzaj | block device encryption | block device encryption | block device encryption | stacked filesystem encryption | stacked filesystem encryption |
| Główne zalety | longest-existing one; possibly the fastest; works on legacy systems | de-facto standard for block device encryption on Linux; very flexible | very portable, well-polished, self-contained solution | slightly faster than EncFS; individual encrypted files portable between systems | easiest one to use; supports non-root administration |
| Dostępność w Arch Linux | musi ręcznie skompilować niestandardowe jądro | *kernel modules:* already shipped with default kernel; *tools:* [device-mapper](https://www.archlinux.org/packages/?name=device-mapper), [cryptsetup](https://www.archlinux.org/packages/?name=cryptsetup) [core] | [truecrypt 7.1a-2](https://projects.archlinux.org/svntogit/packages.git/commit/trunk?h=packages/truecrypt&id=efe03070990f9e3554508bd982b1bd5a654aa095) [extra] (read-only features in later versions) | *kernel module:* already shipped with default kernel; *tools:* [ecryptfs-utils](https://www.archlinux.org/packages/?name=ecryptfs-utils) [community] | [encfs](https://www.archlinux.org/packages/?name=encfs) [community] |
| Licencja | GPL | GPL | custom
[[1](#See_also)] | GPL | GPL |
| 

##### Podstawowa klasyfikacja

 | Loop-AES | dm-crypt +/- LUKS | Truecrypt | eCryptfs | EncFs |
| Szyfruje | całe urządzenia blokowe | całe urządzenia blokowe | całe urządzenia blokowe | pliki | pliki |
| Pojemnik do szyfrowania danych może być ... | partycja dysku lub dysk / plik działający jako partycja wirtualna | partycja dysku lub dysk / plik działający jako partycja wirtualna | partycja dysku lub dysk / plik działający jako partycja wirtualna | katalog w istniejącym systemie plików | katalog w istniejącym systemie plików |
| Odniesienie do systemu plików | działa pod warstwą systemu plików: nie obchodzi, czy zawartość zaszyfrowanego urządzenia blokowego to system plików, tabela partycji, konfiguracja LVM lub cokolwiek innego | działa pod warstwą systemu plików: nie obchodzi, czy zawartość zaszyfrowanego urządzenia blokowego to system plików, tabela partycji, konfiguracja LVM lub cokolwiek innego | działa pod warstwą systemu plików: nie obchodzi, czy zawartość zaszyfrowanego urządzenia blokowego to system plików, tabela partycji, konfiguracja LVM lub cokolwiek innego | dodaje dodatkową warstwę do istniejącego systemu plików, aby automatycznie szyfrować / deszyfrować pliki | dodaje dodatkową warstwę do istniejącego systemu plików, aby automatycznie szyfrować / deszyfrować pliki |
| Szyfrowanie zaimplementowane w... | w przestrzeni jądra | w przestrzeni jądra | w przestrzeni jądra | w przestrzeni jądra | w przestrzeni użytkownika (za pomocą FUSE) |
| Metadane kryptograficzne przechowywane w... |  ? | w LUKS: LUKS Header | begin/end of (decrypted) device ([format](http://www.truecrypt.org/docs/volume-format-specification)) | nagłówek każdego zaszyfrowanego pliku | plik kontrolny na najwyższym poziomie każdego kontenera EncF |
| klucz do szyfrowania przechowywany w. |  ? | w LUKS: LUKS header | begin/end of (decrypted) device ([format](http://www.truecrypt.org/docs/volume-format-specification)) | kluczowy plik, który może być przechowywany w dowolnym miejscu | kluczowy plik, który może być przechowywany w dowolnym miejscu

[[1]](https://github.com/rfjakob/encfs/blob/next/encfs/encfs.pod#environment-variables)[[2]](https://github.com/vgough/encfs/issues/48#issuecomment-69301831)

 |
| 

##### praktyczne implikacje

 | Loop-AES | dm-crypt +/- LUKS | Truecrypt | eCryptfs | EncFs |
| Metadane pliku (liczba plików, struktura dir, rozmiary plików, uprawnienia, mtimes itp.) Są szyfrowane | ✔ | ✔ | ✔ | ✖
(nazwy plików i katalogów można zaszyfrować) | ✖
(nazwy plików i katalogów można zaszyfrować |
| Może być używany do szyfrowania całego dysku twardego (w tym tablic partycji) | ✔ | ✔ | ✔ | ✖ | ✖ |
| Może być używany do szyfrowania przestrzeni wymiany | ✔ | ✔ | ✔ | ✖ | ✖ |
| Może być używany bez wcześniejszego przydzielenia określonej ilości miejsca dla zaszyfrowanego kontenera danych | ✖ | ✖ | ✖ | ✔ | ✔ |
| Może być używany do ochrony istniejących systemów plików bez blokowania dostępu do urządzenia, np. NFS lub Samba, przechowywanie w chmurze itp. | ✖
[[2](#See_also)] | ✖ | ✖ | ✔ | ✔ |
| Umożliwia kopie zapasowe zaszyfrowanego pliku w trybie offline | ✖ | ✖ | ✖ | ✔ | ✔ |
| 

##### Usability features

 | Loop-AES | dm-crypt +/- LUKS | Truecrypt | eCryptfs | EncFs |
| Wsparcie dla automatyzacji podczas logowania |  ? | ✔ |  ? | ✔ | ✔ |
| Obsługa automatycznego odmontowania w przypadku braku aktywności |  ? |  ? |  ? |  ? | ✔ |
| Użytkownicy niebędący administratorami mogą tworzyć / usuwać kontenery w celu szyfrowania danych | ✖ | ✖ | ✖ | limited | ✔ |
| Zapewnia GUI | ✖ | ✖ | ✔ | ✖ | ✔

[[3]](http://www.libertyzero.com/GEncfsM/)[[4]](https://launchpad.net/gencfsm)

 |
| 

##### Funkcje zabezpieczeń

 | Loop-AES | dm-crypt +/- LUKS | Truecrypt | eCryptfs | EncFs |
| Obsługiwane szyfry | AES | AES, Anubis, CAST5/6, Twofish, Serpent, Camellia, Blowfish,… (every cipher the kernel Crypto API offers) | AES, Twofish, Serpent | AES, Blowfish, Twofish... | AES, Blowfish, Twofish, and any other ciphers available on the system |
| Wsparcie dla solenia |  ? | ✔
(with LUKS) | ✔ | ✔ |  ? |
| Obsługa kaskadowania wielu szyfrów |  ? | Not in one device, but blockdevices can be cascaded | ✔ |  ? | ✖ |
| Wsparcie dla dyfuzji kluczy |  ? | ✔
(with LUKS) |  ? |  ? |  ? |
| Ochrona przed key scrubbing | ✔ | ✔
(without LUKS) |  ? |  ? |  ? |
| Support for multiple (independently revocable) keys for the same encrypted data |  ? | ✔
(with LUKS) |  ? |  ? | ✖ |
| 

##### Funkcje wydajności

 | Loop-AES | dm-crypt +/- LUKS | Truecrypt | eCryptfs | EncFs |
| Obsługa wielowątkowości |  ? | ✔
[[8](#See_also)] | ✔ |  ? |  ? |
| wsparcie szyfrowania sprzętowa akceleracja | ✔ | ✔ | ✔ | ✔ | ✔
[[13](#See_also)] |
| 

##### Block device encryption specific

 | Loop-AES | dm-crypt +/- LUKS | Truecrypt |
| Obsługa ręcznej zmiany rozmiaru zaszyfrowanego urządzenia blokowego w miejscu |  ? | ✔ | ✖ |
| 

##### Skumulowane szyfrowanie systemu plików

 | eCryptfs | EncFs |
| Obsługiwane systemy plików | ext3, ext4, xfs (with caveats), jfs, nfs... | ext3, ext4, xfs (with caveats), jfs, nfs, cifs...

[[5]](https://github.com/vgough/encfs)

 |
| Możliwość szyfrowania nazw plików | ✔ | ✔ |
| Możliwość "nie" szyfrowania nazw plików | ✔ | ✔ |
| Zoptymalizowana obsługa niewielkich plików | ✖ | ✔ |
| 

##### Zgodność i rozpowszechnienie

 | Loop-AES | dm-crypt +/- LUKS | Truecrypt | eCryptfs | EncFs |
| Obsługiwane wersje jądra Linux | 2.0 lub nowszy | CBC-mode since 2.6.4, ESSIV 2.6.10, LRW 2.6.20, XTS 2.6.24 |  ? |  ? | 2.4 lub nowszy |
| Szyfrowane dane można również uzyskać z poziomu systemu Windows | ✔
(with [[3](#See_also)], [[14](#See_also)]) | ?
(with [[4](#See_also)], [[14](#See_also)]) | ✔ |  ? |  ?
[[9](#See_also)] |
| Zaszyfrowane dane można również uzyskać z systemu Mac OS X. |  ? |  ? | ✔ |  ? | ✔
[[5](#See_also)] |
| Szyfrowane dane można również uzyskać z FreeBSD |  ? |  ? | ✖ |  ? | ✔
[[6](#See_also)] |
| Używany przez |  ? | Debian/Instalator Ubuntu (szyfrowanie systemu)
Instalator Fedory |  ? | Instalator Ubuntu (home dir encryption)
Chromium OS (encryption of cached user data [[7](#See_also)]) |  ? |

## Przygotowanie

### Wybór konfiguracji

Która konfiguracja szyfrowania dysków jest odpowiednia, ponieważ zależy to od swoich celów (przeczytaj [#Po co używać szyfrowania?](#Po_co_u.C5.BCywa.C4.87_szyfrowania.3F) Powyżej i parametrów systemu.

Między innymi będziesz musiał odpowiedzieć na następujące pytania:

	Jakiego "napastnika" chcesz chronić?

*   Dorywczo użytkownik komputera śledzi twój dysk, gdy twój system jest wyłączony / skradziony / itp.
*   Profesjonalny kryptolog, który może uzyskać wielokrotne odczytywanie / zapisywanie dostępu do systemu przed i po jego użyciu
*   Coś pomiędzy nimi

	Jaką strategię szyfrowania należy zastosować?

*   Szyfrowanie danych
*   Szyfrowanie systemu
*   Coś między nimi

	Jak należy się troszczyć o swap, / tmp, itd.?

*   Ignorować i mam nadzieję, żadne dane nie wyciekły
*   Wyłącz lub zamontuj jako ramdisk
*   Szyfruj (jako część pełnego szyfrowania dysku lub osobno)

	Jak powinny być odblokowane szyfrowane części dysku?

*   Hasło (takie samo jak hasło logowania lub oddzielne)
*   Plik Keyfile (np. Na pendrive'ie USB, przechowywany w bezpiecznym miejscu lub nosić ze sobą)
*   Obie

	Kiedy należy odblokować zaszyfrowane części dysku?

*   Przed startem
*   Podczas rozruchu
*   Przy logowaniu
*   Ręcznie na żądanie (po zalogowaniu)

	Jak powinno się pomieścić wielu użytkowników?

*   Ani trochę
*   Korzystanie ze wspólnego hasła / klucza
*   Niezależnie wydane i odwołane hasła / klucze do tej samej szyfrowanej części dysku
*   Oddzielne zaszyfrowane części dysku dla różnych użytkowników

	Następnie możesz przejść do dokonania wymaganych wyborów technicznych (patrz #Dostępne metody powyżej i #Jak szyfrowanie działa poniżej), dotyczące

*   ułożone szyfrowanie systemu plików a szyfrowanie blokowe
*   zarządzanie kluczami
*   szyfr i tryb pracy
*   przechowywanie metadanych
*   lokalizacja "niższego katalogu" (w przypadku ułożonego szyfrowania systemu plików)

### Przykłady

W praktyce mogłoby się okazać, że coś takiego:

	Przykład 1

	Proste szyfrowanie danych (wewnętrzny dysk twardy) za pomocą folderu wirtualnego o nazwie `~/Private` w katalogu domowym użytkownika szyfrowanym EncFS
└──> zaszyfrowane wersje plików przechowywanych na dysku w `~/.Private`
└──> odblokowywane na żądanie z dedykowanym hasłem

	Przykład 2

	Częściowe szyfrowanie systemu za pomocą katalogu domowego każdego użytkownika zaszyfrowanego za pomocą ECryptfs
└──> odblokowany przy logowaniu użytkownika, używając hasła logowania
└──> `swap` i `/tmp` partycje szyfrowane z Dm-crypt z LUKS, używając automatycznie generowanego klucza na sesję
└──> indeksowanie / buforowanie zawartości `home` przez slocate (i podobne aplikacje) są wyłączone.

	Przykład 3

	Szyfrowanie systemu - cały dysk twardy z wyjątkiem partycji rozruchowej (jednak / boot może być szyfrowany przez GRUB) zaszyfrowane za pomocą Dm-crypt z LUKS
└──> odblokowany podczas ładowania, używając haseł lub pamieci USB z plikami kluczowymi
└──> Może różne hasła / klucze na użytkownika - niezależnie odwołalne
└──> Może szyfrowanie obejmujące wiele dysków lub elastyczność układu partycji z LUKS na LVM

	Przykład 4

	Ukryte / zwykłe szyfrowanie systemu - cały dysk twardy zaszyfrowany zwykłą dm-crypt
└──> USB-boot, używając dedykowanych haseł i pamięci USB z plikiem kluczowym
└──> integralność danych sprawdzona przed montowaniem
└──> `boot` partycja znajduje się na wspomnianej pamięci USB

Oczywiście możliwe jest wiele innych kombinacji. Należy dokładnie zaplanować, jaki rodzaj instalacji będzie odpowiedni dla twojego systemu.

### Wybieranie silnego hasła

Zobacz [Security#Passwords](/index.php/Security#Passwords "Security").

### Przygotowanie dysku

Przed skonfigurowaniem szyfrowania dysku na dysku (częściowym) należy najpierw najpierw wyczyścić dysk. Składa się z nadpisania całego dysku lub partycji strumieniem zero bajtów lub bajtów losowych i jest wykonywany z jednego lub obu z następujących powodów:

	Zapobieganie odzyskiwaniu wcześniej zapisanych danych

Szyfrowanie dysków nie zmienia faktu, że poszczególne sektory są zastępowane tylko na żądanie, gdy system plików tworzy lub modyfikuje dane, które poszczególne sektory posiadają (zobacz [#How the encryption works](#How_the_encryption_works) poniżej). Sektory, które system plików uważa za "nie aktualnie używane", nie są dotykane i mogą zawierać resztki danych z poprzednich systemów plików. Jedynym sposobem, aby upewnić się, że wszystkie dane, które zostały wcześniej zapisane na dysku nie można odzyskać ma to ręcznie usunąć. W tym celu nie ma znaczenia, czy użyto zero bajtów czy losowych bajtów (chociaż przecieranie zerowymi bajtami będzie znacznie szybsze).

	Zapobiegaj ujawnianiu wzorców użytkowania na zaszyfrowanym dysku

ajlepiej byłoby, gdyby cała zaszyfrowana część dysku była nieodróżnialna od jednolicie losowych danych. W ten sposób żadna nieuprawniona osoba nie może wiedzieć, która i ile sektorów rzeczywiście zawiera zaszyfrowane dane - co może być pożądanym celem samym w sobie (w ramach prawdziwej poufności), a także służy jako dodatkowa bariera dla napastników próbujących złamać szyfrowanie. Aby osiągnąć ten cel, ważne jest wyczyszczenie dysku za pomocą wysokiej jakości losowych bajtów.

Drugi cel ma sens tylko w połączeniu z szyfrowaniem urządzeń blokowych, ponieważ w przypadku stosowego szyfrowania systemu plików zaszyfrowane dane mogą być łatwo zlokalizowane (w postaci odrębnych zaszyfrowanych plików w systemie plików hosta). Zauważ też, że nawet jeśli chcesz zaszyfrować tylko określony folder, będziesz musiał usunąć całą partycję, jeśli chcesz pozbyć się plików, które były wcześniej przechowywane w tym folderze w formie niezaszyfrowanej (z powodu fragmentacji dysku). Jeśli na tej samej partycji znajdują się inne foldery, będziesz musiał wykonać ich kopię zapasową i przenieść później.

Po określeniu, jaki rodzaj skasowania dysku chcesz wykonać, zapoznaj się z artykułem [#Securely wipe disk](#Securely_wipe_disk) w celu uzyskania instrukcji technicznych.

**Tip:** Podejmując decyzję, która metoda ma być używana do bezpiecznego wymazywania dysku twardego, pamiętaj, że nie musi to być wykonywane więcej niż jeden raz tak długo, jak dysk jest używany jako szyfrowany dysk.

## Jak działa szyfrowanie

Ta sekcja jest przeznaczona jako wprowadzenie na wysokim poziomie do koncepcji i procesów, które są w centrum zwykłych konfiguracji szyfrowania dysku.

Nie zawiera szczegółów technicznych ani matematycznych (należy sięgnąć po odpowiednią literaturę), ale powinien zapewnić administratorowi systemu zrozumienie, w jaki sposób różne opcje konfiguracji (szczególnie w zakresie zarządzania kluczami) mogą wpływać na użyteczność i bezpieczeństwo

### Podstawowa zasada

Do celów szyfrowania dysków każda jednostka blokowa (lub pojedynczy plik w przypadku skumulowanego szyfrowania systemu plików) dzieli się na "" sektory "" o równej długości, na przykład 512 bajtów (4096 bitów). Szyfrowanie / odszyfrowywanie odbywa się wtedy w zależności od sektora, więc sektor n-tego pliku bloku / pliku na dysku przechowuje zaszyfrowaną wersję n-tego sektora oryginalnych danych.

Gdy system operacyjny lub aplikacja zażąda pewnego fragmentu danych z pliku blokowego / pliku, cały sektor (lub sektory) zawierający dane będzie odczytywany z dysku, odszyfrowany w locie i tymczasowo przechowywany w pamięci:

```
        ╔═══════╗
 sector 1 ║"???.."║
          ╠═══════╣         ╭┈┈┈┈┈╮
 sector 2 ║"???.."║         ┊ key ┊
          ╠═══════╣         ╰┈┈┬┈┈╯
          :       :            │
          ╠═══════╣            ▼             ┣┉┉┉┉┉┉┉┫
 sector n ║"???.."║━━━━━━━(decryption)━━━━━━▶┋"abc.."┋ sector n
          ╠═══════╣                          ┣┉┉┉┉┉┉┉┫
          :       :
          ╚═══════╝

          encrypted                          unencrypted
     blockdevice or                          data in RAM
       file on disk

```

Podobnie, przy każdej operacji zapisu wszystkie sektory, których dotyczy problem, muszą zostać całkowicie zaszyfrowane (podczas gdy pozostałe sektory pozostają nienaruszone).

Aby móc de / szyfrować dane, system szyfrowania dysku musi znać unikatowy "klucz" związany z tym. Kiedy ma być zamontowany zaszyfrowane urządzenie blokowe lub folder, należy podać odpowiedni klucz (zwany odtąd "kluczem głównym").

Entropia klucza ma kluczowe znaczenie dla bezpieczeństwa szyfrowania. Losowo wygenerowany ciąg bajtów o określonej długości, na przykład 32 bajtów (256 bitów) ma pożądane właściwości, ale nie jest możliwe, aby pamiętać i zastosować ręcznie podczas montowania.

Z tego powodu dwie techniki są używane jako pomocnicy. Pierwszym z nich jest zastosowanie kryptografii, aby zwiększyć entropową właściwość klucza głównego, zwykle z użyciem osobnego przyjaznego dla człowieka hasła. W przypadku różnych typów szyfrowania tabela #Comparison zawiera listę odpowiednich funkcji. Druga metoda polega na utworzeniu pliku klucza o wysokiej entropii i przechowywaniu go na nośniku innym niż dysk danych, który ma być zaszyfrowany.

Zobacz też [Wikipedia:Authenticated encryption](https://en.wikipedia.org/wiki/Authenticated_encryption "wikipedia:Authenticated encryption").

### Klucze, pliki kluczy i hasła

Oto przykłady jak przechowywać i kryptograficznie zabezpieczyć klucz główny kluczem:

	Przechowywany w pliku kluczy w postaci zwykłego tekstu

Najprostszym rozwiązaniem jest przechowywanie klucza głównego w pliku (w formie czytelnej). Plik - nazywany "plikiem kluczowym" - może być umieszczony na pamięci USB przechowywanej w bezpiecznej lokalizacji i łączyć się tylko z komputerem, jeśli chcesz zamontować szyfrowane części dysku (np. Podczas ładowania lub logowania).

	Przechowywany w formie chronionej przed frazą w pliku klucza lub na dysku

Klucz główny (a tym samym zaszyfrowane dane) można chronić tajnym hasłem, które trzeba pamiętać i wprowadzić za każdym razem, gdy chcesz zamontować zaszyfrowane urządzenie blokowe lub folder. Aby uzyskać szczegółowe informacje, zapoznaj się z poniżej opisanych metadanych.

	Losowo generowane w locie dla każdej sesji

W niektórych przypadkach, np. podczas szyfrowania przestrzeni wymiany lub partycji a / tmp nie trzeba utrzymywać stałego klucza głównego. Nowy klucz może być generowany losowo dla każdej sesji bez konieczności interakcji z użytkownikiem. Oznacza to, że po odmontowaniu wszystkie pliki zapisane w danej partycji nigdy nie mogą być odszyfrowane przez nikogo, co w tych szczególnych przypadkach jest w porządku.

### Kryptograficzne metadane

Często techniki szyfrowania wykorzystują funkcje kryptograficzne w celu zwiększenia bezpieczeństwa samego klucza głównego. Na górze zaszyfrowanego urządzenia przekazywane jest hasło lub plik klucza, a tylko wynik może odblokować klucz główny w celu odszyfrowania danych.

Wspólną konfiguracją jest zastosowanie tzw. "Rozciągania kluczy" do hasła (za pomocą "funkcji wywolania kluczy") i użycie wynikowych poprawek jako klucza do deszyfrowania faktycznego klucza głównego (który był wcześniej przechowywany w postaci zaszyfrowanej)

```
╭┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈╮                         ╭┈┈┈┈┈┈┈┈┈┈┈╮
┊ mount passphrase ┊━━━━━⎛key derivation⎞━━━▶┊ mount key ┊
╰┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈╯ ,───⎝   function   ⎠    ╰┈┈┈┈┈┬┈┈┈┈┈╯
╭──────╮            ╱                              │
│ salt │───────────´                               │
╰──────╯                                           │
╭─────────────────────╮                            ▼         ╭┈┈┈┈┈┈┈┈┈┈┈┈╮
│ encrypted master key│━━━━━━━━━━━━━━━━━━━━━━(decryption)━━━▶┊ master key ┊
╰─────────────────────╯                                      ╰┈┈┈┈┈┈┈┈┈┈┈┈╯

```

Funkcja wyprowadzania kluczy (na przykład PBKDF2 lub szyfrowanie) jest umyślnie zwolniona (dotyczy wielu iteracji funkcji mieszania, na przykład 1000 iteracji HMAC-SHA-512), dzięki czemu ataki brutalnej siły, aby znaleźć frazę, są niewykonalne. W przypadku zwykłego użytkownika konieczne będzie tylko obliczenie raz na sesję, więc małe spowolnienie nie jest problemem. Pobiera także dodatkową blob danych, tzw. "Sól" jako argument - jest losowo generowana raz podczas konfigurowania szyfrowania dysku i przechowywana w niezabezpieczonej części metadanych kryptograficznych. Ponieważ każda konfiguracja będzie inna, to powoduje, że napastnicy przyspieszają ataki brutalnych sił, używając prekompetentów tabel do funkcji wyprowadzania kluczowych.

Zaszyfrowany klucz główny może być przechowywany na dysku razem z zaszyfrowanymi danymi. W ten sposób poufność zaszyfrowanych danych zależy całkowicie od tajnego hasła.

Zazwyczaj nie jest on używany do de / szyfrowania danych na dysku bezpośrednio. Na przykład w przypadku ułożenia szyfrowania plików każdy plik może zostać automatycznie przypisany do własnego klucza szyfrowania. Kiedy tylko plik ma być odczytany / zmodyfikowany, klucz ten musi najpierw zostać odszyfrowany przy użyciu klucza głównego, zanim będzie mógł zostać użyty do de / zaszyfrowania zawartości pliku:

```
                          ╭┈┈┈┈┈┈┈┈┈┈┈┈╮
                          ┊ master key ┊
  *file on disk:*           ╰┈┈┈┈┈┬┈┈┈┈┈┈╯
 ┌ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┐        │
 ╎╭───────────────────╮╎        ▼          ╭┈┈┈┈┈┈┈┈┈┈╮
 ╎│ encrypted file key│━━━━(decryption)━━━▶┊ file key ┊
 ╎╰───────────────────╯╎                   ╰┈┈┈┈┬┈┈┈┈┈╯
 ╎┌───────────────────┐╎                        ▼           ┌┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┐
 ╎│ encrypted file    │◀━━━━━━━━━━━━━━━━━(de/encryption)━━━▶┊ readable file ┊
 ╎│ contents          │╎                                    ┊ contents      ┊
 ╎└───────────────────┘╎                                    └┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┘
 └ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┘

```

W podobny sposób można użyć oddzielnego klucza (na przykład jednego w folderze) do szyfrowania nazw plików w przypadku skumulowanego szyfrowania systemu plików.

W przypadku szyfrowania urządzenia blokowego stosuje się jeden klucz główny na urządzenie, a zatem wszystkie dane. Niektóre metody oferują funkcje do przypisywania wielu haseł / plików kluczowych dla tego samego urządzenia, a inne nie. Niektórzy używają wyżej wymienionych funkcji, aby zabezpieczyć klucz główny, a inni zapewniają pełną kontrolę nad kluczowym zabezpieczeniem dla użytkownika. Dwa przykłady są wyjaśnione przez parametry kryptograficzne używane przez dm-crypt w trybach zwykłych lub LUKS.

Porównując parametry używane przez oba tryby, zauważymy, że tryb zwykłego trybu kryptograficznego dm-crypt zawiera parametry odnoszące się do lokalizacji pliku kluczy

Dodatkowe zabezpieczenia można osiągnąć, zamiast tego przechować zaszyfrowany klucz główny w pliku kluczowym, na przykład na przykład. kij USB. Zapewnia to uwierzytelnianie dwuskładnikowe: dostęp do zaszyfrowanych danych wymaga obecnie tylko jednego elementu (hasła), a dodatkowo tylko jednego (plik klucza).

Innym sposobem uzyskania uwierzytelnienia dwuskładnikowego jest rozszerzenie powyższego schematu pobierania kluczy w celu matematycznego "połączenia" hasła z danymi bajtowymi odczytanymi z jednego lub więcej plików zewnętrznych (zlokalizowanych na pendrivie USB lub podobnym), przed przekazaniem go do wyprowadzenia klucza Funkcje. Pliki, o których mowa, mogą być cokolwiek, np normalne obrazy JPEG, które mogą być korzystne dla #Nieprawdopodobnego zaprzeczenia. W tym kontekście wciąż są one nazywane "kluczowymi plikami".

Po wyprowadzeniu klucz główny jest bezpiecznie przechowywany w pamięci (na przykład w kluczu jądra), tak długo, jak jest zamontowane zaszyfrowane urządzenie blokowe lub folder. (np. `--keyfile-size`, `--keyfile-offset`). Tryb LUKS-u kryptografii nie jest potrzebny, ponieważ każda jednostka blokowa zawiera nagłówek z metadanymi kryptograficznymi na początku. Nagłówek zawiera szyfr używany, zaszyfrowany klucz główny i parametry wymagane do jego deszyfrowania. Te ostatnie parametry z kolei wynikają z opcji używanych podczas wstępnego szyfrowania klucza głównego (np. `--iter-time`, `--use-random`).

Aby zapoznać się z zaletami różnych technik, odnieś się do tabeli #Comparison lub przejrzyj poszczególne strony.

### Szyfry i tryby działania

Algorytm używany do tłumaczenia pomiędzy niezabezpieczonymi i zaszyfrowanymi danymi (tzw. "Plaintext" i "ciphertext"), które odpowiadają sobie nawzajem w odniesieniu do danego klucza szyfrującego, nazywa się "szyfrem".

Szyfrowanie dysków wykorzystuje "szyfry blokowe", które działają na blokach danych o stałej długości, np. 16 bajtów (128 bitów). W czasie pisania tego artykułu najczęściej używanymi są:

 block size | key size | comment |
| [AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard "wikipedia:Advanced Encryption Standard") | 128 bitów | 128, 192 i 256 bitów | *zatwierdzony przez NSA do ochrony informacji poufnych "SECRET" i "TOP SECRET" w USA (przy użyciu klucza o rozmiarze 192 lub 256 bitów* |
| [Blowfish](https://en.wikipedia.org/wiki/Blowfish_(cipher) | 64 bitów | 32–448 bitów | *jeden z pierwszych bezpiecznych szyfrów, które stały się publicznie dostępne, a więc bardzo dobrze rozwinięty w Linuksie* |
| [Twofish](https://en.wikipedia.org/wiki/Twofish "wikipedia:Twofish") | 128 bitów | 128, 192 i 256 bitów | *rozwinięty jako następca Blowfish, ale nie osiągnął tak powszechnego wykorzystania* |
| [Serpent](https://en.wikipedia.org/wiki/Serpent_(cipher) | 128 bitów | 128, 192 i 256 bitów | Uważany za najbardziej bezpieczny z pięciu finalistów konkursu AES[[10](#See_also)][[11](#See_also)][[12](#See_also)]. |

Szyfrowanie / odszyfrowywanie sektora (patrz wyżej) uzyskuje się przez podzielenie go na małe bloki odpowiadające rozmiarowi bloku szyfru i po pewnym zestawie reguł (tak zwanym "trybie działania"), jak nałożyć kolejno szyfr na poszczególne bloki

Po prostu zastosowanie go do każdego bloku osobno, bez modyfikacji (nazwanego trybem "elektroniczna książka kodowa (ECB)") nie byłoby bezpieczne, ponieważ jeśli te same 16 bajtów tekstu jawnego zawsze generuje te same 16 bajtów tekstu zaszyfrowanego, osoba atakująca może łatwo rozpoznać wzorzec w tekstu zaszyfrowanego na przechowywanym dysku.

Najbardziej podstawowym (i wspólnym) trybem działania w praktyce jest "szyfrowanie łańcucha (CBC)". Podczas szyfrowania sektora w tym trybie każdy blok danych prostokątnych łączy się w sposób matematyczny z szyfrem z poprzednim blokiem, przed szyfrowaniem za pomocą szyfru. W pierwszym bloku, ponieważ nie ma poprzedniego szyfrogramu, używany jest specjalny wstępnie wygenerowany blok danych przechowywany w metadanych kryptograficznych sektora i nazywany "wektorem inicjującym (IV)":

```
                                  ╭──────────────╮
                                  │initialization│
                                  │vector        │
                                  ╰────────┬─────╯
          ╭  ╠══════════╣        ╭─key     │      ┣┉┉┉┉┉┉┉┉┉┉┫        
          │  ║          ║        ▼         ▼      ┋          ┋         . START
          ┴  ║"????????"║◀━━━━(cipher)━━━━(+)━━━━━┋"Hello, W"┋ block  ╱╰────┐
    sector n ║          ║                         ┋          ┋ 1      ╲╭────┘
  of file or ║          ║──────────────────╮      ┋          ┋         ' 
 blockdevice ╟──────────╢        ╭─key     │      ┠┈┈┈┈┈┈┈┈┈┈┨
          ┬  ║          ║        ▼         ▼      ┋          ┋
          │  ║"????????"║◀━━━━(cipher)━━━━(+)━━━━━┋"orld !!!"┋ block
          │  ║          ║                         ┋          ┋ 2
          │  ║          ║──────────────────╮      ┋          ┋
          │  ╟──────────╢                  │      ┠┈┈┈┈┈┈┈┈┈┈┨
          │  ║          ║                  ▼      ┋          ┋
          :  :   ...    :        ...      ...     :   ...    : ...

               ciphertext                         plaintext
                  on disk                         in RAM

```

Podczas odszyfrowywania procedura jest odwracana analogicznie.

Warto zwrócić uwagę na generowanie unikalnego wektora inicjalizacyjnego dla każdego sektora. Najprostszym wyborem jest obliczenie go w przewidywalny sposób z łatwo dostępnej wartości, takiej jak numer sektora. Może to jednak umożliwić osobie atakującej wielokrotny dostęp do systemu w celu przeprowadzenia tak zwanego ataku znaku wodnego. Aby temu zapobiec, można użyć metody o nazwie "Zaszyfrowany wektor inicjalizacji sektora soli (ESSIV)" w celu wygenerowania wektorów inicjalizacji w sposób, który sprawia, że wyglądają zupełnie losowo na potencjalnego napastnika.

Istnieje również wiele innych, bardziej skomplikowanych trybów operacji dostępnych dla szyfrowania dysku, które już zapewniają wbudowane zabezpieczenia przed takimi atakami (a więc nie wymagają ESSIV). Niektóre mogą dodatkowo gwarantować autentyczność zaszyfrowanych danych (tj. Potwierdzić, że nie zostały zmodyfikowane / uszkodzone przez osobę, która nie ma dostępu do klucza).