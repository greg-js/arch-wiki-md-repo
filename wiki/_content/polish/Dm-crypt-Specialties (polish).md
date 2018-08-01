## Contents

*   [1 Zabezpieczanie niezaszyfrowanej partycji rozruchowej](#Zabezpieczanie_niezaszyfrowanej_partycji_rozruchowej)
    *   [1.1 Uruchamianie z urządzenia wymiennego](#Uruchamianie_z_urz.C4.85dzenia_wymiennego)
    *   [1.2 chkboot](#chkboot)
    *   [1.3 mkinitcpio-chkcryptoboot](#mkinitcpio-chkcryptoboot)
        *   [1.3.1 Instalacja](#Instalacja)
        *   [1.3.2 Technical Overview](#Technical_Overview)
    *   [1.4 Inne metody](#Inne_metody)
*   [2 Używanie zaszyfrowanych plików kluczy GPG, LUKS lub OpenSSL](#U.C5.BCywanie_zaszyfrowanych_plik.C3.B3w_kluczy_GPG.2C_LUKS_lub_OpenSSL)
*   [3 Zdalne odblokowanie partycji root (lub innej)](#Zdalne_odblokowanie_partycji_root_.28lub_innej.29)
    *   [3.1 Zdalne odblokowanie (haki: systemd, systemd-tool)](#Zdalne_odblokowanie_.28haki:_systemd.2C_systemd-tool.29)
    *   [3.2 Zdalne odblokowanie (haki: netconf, dropbear, tinyssh, ppp)](#Zdalne_odblokowanie_.28haki:_netconf.2C_dropbear.2C_tinyssh.2C_ppp.29)
    *   [3.3 Zdalne odblokowanie przez Wi-Fi (haki: buduj własne)](#Zdalne_odblokowanie_przez_Wi-Fi_.28haki:_buduj_w.C5.82asne.29)
*   [4 Obsługa Discard / TRIM dla dysków półprzewodnikowych (SSD)](#Obs.C5.82uga_Discard_.2F_TRIM_dla_dysk.C3.B3w_p.C3.B3.C5.82przewodnikowych_.28SSD.29)
*   [5 Szyfrowanie hakiem i wiele dysków](#Szyfrowanie_hakiem_i_wiele_dysk.C3.B3w)
    *   [5.1 Rozszerzanie LVM na wielu dyskach](#Rozszerzanie_LVM_na_wielu_dyskach)
        *   [5.1.1 Dodanie nowego dysku](#Dodanie_nowego_dysku)
        *   [5.1.2 Rozszerzanie woluminu logicznego](#Rozszerzanie_woluminu_logicznego)
    *   [5.2 Modyfikowanie haków szyfrowania dla wielu partycji](#Modyfikowanie_hak.C3.B3w_szyfrowania_dla_wielu_partycji)
        *   [5.2.1 Główny system plików obejmujący wiele partycji](#G.C5.82.C3.B3wny_system_plik.C3.B3w_obejmuj.C4.85cy_wiele_partycji)
        *   [5.2.2 Wiele partycji innych niż root](#Wiele_partycji_innych_ni.C5.BC_root)
*   [6 Szyfrowany system za pomocą oddzielnego nagłówka LUKS](#Szyfrowany_system_za_pomoc.C4.85_oddzielnego_nag.C5.82.C3.B3wka_LUKS)
    *   [6.1 Używanie haka systemd](#U.C5.BCywanie_haka_systemd)
    *   [6.2 Modyfikowanie haka szyfrowania](#Modyfikowanie_haka_szyfrowania)
*   [7 Szyfrowanie /boot i odłączony nagłówek LUKS na USB](#Szyfrowanie_.2Fboot_i_od.C5.82.C4.85czony_nag.C5.82.C3.B3wek_LUKS_na_USB)
    *   [7.1 Przygotowywanie urządzeń dyskowych](#Przygotowywanie_urz.C4.85dze.C5.84_dyskowych)
        *   [7.1.1 Przygotowanie klucza USB](#Przygotowanie_klucza_USB)
        *   [7.1.2 Główny napęd](#G.C5.82.C3.B3wny_nap.C4.99d)
    *   [7.2 Procedura instalacji i niestandardowe szyfrowanie hook](#Procedura_instalacji_i_niestandardowe_szyfrowanie_hook)
        *   [7.2.1 Boot Loader](#Boot_Loader)
    *   [7.3 Zmiana pliku klucza LUKS](#Zmiana_pliku_klucza_LUKS)

## Zabezpieczanie niezaszyfrowanej partycji rozruchowej

Partycja `/boot` i [Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record") to dwa obszary dysku, które nie są zaszyfrowane, nawet w [encrypted root](/index.php/Dm-crypt/Encrypting_an_entire_system "Dm-crypt/Encrypting an entire system"). Zwykle nie można ich zaszyfrować, ponieważ [boot loader](/index.php/Boot_loader "Boot loader") i BIOS (odpowiednio) nie mogą odblokować kontenera dm-crypt, aby kontynuować proces uruchamiania. Wyjątkiem jest [GRUB](/index.php/GRUB "GRUB"), który uzyskał funkcję odblokowania LUKSa zaszyfrowanego `/boot` - patrz [dm-crypt/Encrypting an entire system#Encrypted boot partition (GRUB)](/index.php/Dm-crypt/Encrypting_an_entire_system#Encrypted_boot_partition_.28GRUB.29 "Dm-crypt/Encrypting an entire system").

W tej sekcji opisano kroki, które można podjąć w celu zwiększenia bezpieczeństwa procesu rozruchu.

**Warning:** Należy pamiętać, że zabezpieczenie partycji `/boot` i MBR może złagodzić liczne ataki podczas rozruchu, ale systemy skonfigurowane w ten sposób mogą nadal być podatne na sabotaż BIOS/UEFI/firmware, sprzętowe keyloggery, zimne ataki rozruchowe i wiele innych zagrożeń, które są poza zakresem tego artykułu. Omówienie problemów związanych z zaufaniem systemu oraz ich związek z szyfrowaniem na pełnym dysku można znaleźć na stronie [[1]](http://www.youtube.com/watch?v=pKeiKYA03eE).

### Uruchamianie z urządzenia wymiennego

**Warning:** Systemd wersja 230 generatora cryptsetup emituje `RequiresMountsFor` dla pliku kluczy crypto. Dlatego też, gdy system plików przechowujący ten plik zostanie odłączony, zatrzymuje również usługę cryptsetup. Takie zachowanie jest niepoprawne, ponieważ system plików i kryptokey są wymagane tylko raz, gdy kontener kryptograficzny jest początkowo skonfigurowany. Zobacz [systemd issue 3816](https://github.com/systemd/systemd/issues/3816).

Używanie nośnika wymienego do uruchamiania systemu jest dość prostą procedurą i oferuje znaczną poprawę bezpieczeństwa przed niektórymi rodzajami ataków. Dwie wrażliwe części systemu wykorzystujące [zaszyfrowany system plików root](/index.php/Dm-crypt/Encrypting_an_entire_system_(Polski) "Dm-crypt/Encrypting an entire system (Polski)") to

*   [Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record"), i
*   partycja `/boot`

Te muszą być przechowywane niezaszyfrowane w celu uruchomienia systemu. Aby zabezpieczyć je przed manipulacją, zaleca się przechowywanie ich na wymiennym nośniku, takim jak dysk USB, i uruchamianie z tego dysku zamiast dysku twardego. Tak długo, jak utrzymujesz dysk ze sobą przez cały czas, możesz mieć pewność, że te komponenty nie zostały zmodyfikowane, dzięki czemu uwierzytelnianie będzie o wiele bezpieczniejsze podczas odblokowywania systemu.

Zakłada się, że masz już skonfigurowany system z dedykowaną partycją zamontowaną w `/boot`. Jeśli nie, wykonaj kroki opisane w [dm-crypt/System configuration#Boot loader](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration"), zastępując dysk twardy dyskiem wymiennym.

**Note:** Musisz upewnić się, że twój system obsługuje uruchamianie z wybranego nośnika, czy to dysku USB, zewnętrznego dysku twardego, karty SD, czy cokolwiek innego.

Przygotuj dysk wymienny (`/dev/sdx`).

```
# gdisk /dev/sdx #format if necessary. Alternatively, cgdisk, fdisk, cfdisk, gparted...
# mkfs.ext2 /dev/sdx1
# mount /dev/sdx1 /mnt

```

Copy your existing `/boot` contents to the new one.

Skopiuj istniejącą zawartość `/boot` na nową.

```
# cp -ai /boot/* /mnt/

```

Zainstaluj nową partycję. Nie zapomnij zaktualizować pliku [[fstab].

```
# umount /boot
# umount /mnt
# mount /dev/sdx1 /boot
# genfstab -p -U / > /etc/fstab

```

Zaktualizuj [GRUB](/index.php/GRUB "GRUB"). `grub-mkconfig` powinien automatycznie wykryć nowy identyfikator UUID partycji, ale niestandardowe wpisy menu mogą wymagać ręcznej aktualizacji.

```
# grub-mkconfig -o /boot/grub/grub.cfg
# grub-install /dev/sdx #install to the removable device, not the hard disk.

```

Uruchom ponownie i przetestuj nową konfigurację. Pamiętaj, aby odpowiednio ustawić kolejność uruchamiania urządzenia w systemie BIOS lub [UEFI](/index.php/UEFI "UEFI"). Jeśli uruchomienie systemu nie powiedzie się, nadal można uruchomić komputer z dysku twardego, aby rozwiązać problem.

### chkboot

**Warning:** chkboot makes a `/boot` partition **tamper-evident**, not **tamper-proof**. By the time the chkboot script is run, you have already typed your password into a potentially compromised boot loader, kernel, or initrd. If your system fails the chkboot integrity test, no assumptions can be made about the security of your data.

Odnosząc się do artykułu z magazynu ct (wydanie 3/12, strona 146, 01.16.2012, [[2]](http://www.heise.de/ct/inhalt/2012/03/6/)) poniższy skrypt sprawdza pliki w katalogu / boot pod kątem zmian sumy kontrolnej SHA-1, i-węzła i zajętych bloków na dysku twardym. Sprawdza także główny rekord rozruchowy. Skrypt nie może zapobiec pewnym typom ataków, ale wiele z nich jest trudniejszych. Konfiguracja samego skryptu nie jest przechowywana w niezaszyfrowanej partycji `/boot`. Z zablokowanym / wyłączonym zaszyfrowanym systemem, utrudnia to niektórym napastnikom, ponieważ nie jest oczywiste, że automatyczne porównywanie sumy kontrolnej partycji jest wykonywane po starcie systemu. Jednak osoba atakująca, która przewiduje takie środki ostrożności, może manipulować oprogramowaniem układowym, aby uruchomić własny kod nad jądrem i przechwycić dostęp do systemu plików, np. do rozruchu i przedstawienia niezakodowanych plików. Ogólnie rzecz biorąc, żadne środki bezpieczeństwa poniżej poziomu oprogramowania układowego nie są w stanie zagwarantować zaufania i fałszowania dowodów.

Dostępny jest skrypt z instrukcją [instalacji](ftp://ftp.heise.de/pub/ct/listings/1203-146.zip)(autor: Juergen Schmidt, ju at heisec.de; Licencja: GPLv2). Istnieje również pakiet [chkboot](https://aur.archlinux.org/packages/chkboot/) do zainstalowania.

Po instalacji dodaj plik usługi (pakiet zawiera jeden oparty na następujących elementach) i włącz go:

```
[Unit]
Description=Check that boot is what we want
Requires=basic.target
After=basic.target

[Service]
Type=oneshot
ExecStart=/usr/local/bin/chkboot.sh

[Install]
WantedBy=multi-user.target

```

Istnieje małe zastrzeżenie dla systemd. W chwili pisania tego tekstu oryginalny skrypt `chkboot.sh` zawiera puste miejsce na początku #! `#!/bin/bash` które musi zostać usunięte, aby usługa mogła pomyślnie się uruchomić.

Ponieważ `/usr/local/bin/chkboot_user.sh` musi zostać wykonany zaraz po zalogowaniu, musisz dodać go do [autostartu](/index.php/Autostart "Autostart") (np. w KDE -> *System Settings -> Startup and Shutdown -> Autostart*; GNOME 3: *gnome-session-properties*).

W Arch Linuksie zmiany w `/boot` są dość częste, na przykład po aktualizacji kerneli. Dlatego pomocne może być korzystanie ze skryptów przy każdej pełnej aktualizacji systemu. Jednym ze sposobów, aby to zrobić:

```
#!/bin/bash
#
# Note: Insert your <user>  and execute it with sudo for pacman & chkboot to work automagically
#
echo "Pacman update [1] Quickcheck before updating" & 
sudo -u <user> /usr/local/bin/chkboot_user.sh		# insert your logged on <user> 
/usr/local/bin/chkboot.sh
sync							# sync disks with any results 
sudo -u <user> /usr/local/bin/chkboot_user.sh		# insert your logged on <user> 
echo "Pacman update [2] Syncing repos for pacman" 
pacman -Syu
/usr/local/bin/chkboot.sh
sync	
sudo -u <user> /usr/local/bin/chkboot_user.sh		# insert your logged on <user>
echo "Pacman update [3] All done, let us roll on ..."

```

### mkinitcpio-chkcryptoboot

**Warning:** Ten hak nie szyfruje kodu rdzenia (MBR) [GRUB](/index.php/GRUB "GRUB")-a ani kodu pośredniczącego EFI, ani nie chroni przed sytuacjami, gdy atakujący jest w stanie zmodyfikować zachowanie bootloadera, aby złamać jądro i / lub initramfs w czasie wykonywania.

[mkinitcpio-chkcryptoboot](https://aur.archlinux.org/packages/mkinitcpio-chkcryptoboot/) jest haczykiem [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio"), który przeprowadza kontrole integralności podczas wczesnej przestrzeni użytkownika i radzi, aby użytkownik nie wprowadzał swojego hasła do partycji głównej, jeśli system wydaje się być zagrożony. Bezpieczeństwo uzyskuje się za pomocą zaszyfrowanej partycji rozruchowej, która jest odblokowywana za pomocą modułu `cryptodisk.mod` GRUB-a oraz partycji root systemu plików, która jest szyfrowana hasłem innym niż poprzednie. W ten sposób initramfs i jądro są zabezpieczone przed ingerencją w trybie offline, a partycja root może pozostać bezpieczna, nawet jeśli hasło `/boot` partycji zostało wprowadzone na zaatakowanej maszynie (pod warunkiem, że hak chkcryptoboot wykryje kompromis i samo nie zostanie naruszone podczas uruchamiania w czasie wykonywania))

Ten haczyk wymaga odblokowania wersji [grub](https://www.archlinux.org/packages/?name=grub) > = 2.00 i dedykowanej partycji zaszyfrowanej / `/boot` LUKS z własnym hasłem, aby być bezpiecznym.

#### Instalacja

Zainstaluj [mkinitcpio-chkcryptoboot](https://aur.archlinux.org/packages/mkinitcpio-chkcryptoboot/) i edytuj `/etc/default/chkcryptoboot.conf`. Jeśli chcesz wykryć, czy partycja rozruchowa została pominięta, zmodyfikuj zmienne `CMDLINE_NAME` i `CMDLINE_VALUE` , wartościami znanymi tylko Tobie. Możesz skorzystać z porady dotyczącej używania dwóch skrótów, jak sugeruje się tuż po instalacji. Należy również wprowadzić odpowiednie zmiany w [linii poleceń jądra](/index.php/Kernel_command_line "Kernel command line") w `/etc/default/grub`. Zmodyfikuj linię `HOOKS=` w pliku `/etc/mkinitcpio.conf` i hak `chkcryptoboot` przed `encrypt`. Po zakończeniu [zregeneruj initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs").

#### Technical Overview

[mkinitcpio-chkcryptoboot](https://aur.archlinux.org/packages/mkinitcpio-chkcryptoboot/) składa się z haka instalacyjnego i haka uruchomieniowego dla mkinitcpio. Hook instalacyjny uruchamia się za każdym razem, gdy initramfs jest przebudowywany i miesza skrót GRUB [EFI](/index.php/EFI "EFI") `$esp/EFI/grub_uefi/grubx64.efi`) (w przypadku systemów [UEFI](/index.php/UEFI "UEFI")) lub pierwsze 446 bajtów dysku, na którym zainstalowany jest GRUB (w przypadku systemów BIOS) i przechowuje wartości mieszania wewnątrz initramfs zlokalizowanych wewnątrz partycji zaszyfrowanej / `/boot`. Po uruchomieniu systemu GRUB pyta o hasło `/boot`, a następnie wywołuje tę samą operację skrótu i porównuje wynikowe hashy, zanim poprosi o hasło do partycji głównej. Jeśli nie pasują, hak wyświetli następujący błąd:

```
CHKCRYPTOBOOT ALERT!
CHANGES HAVE BEEN DETECTED IN YOUR BOOT LOADER EFISTUB!
YOU ARE STRONGLY ADVISED NOT TO ENTER YOUR ROOT CONTAINER PASSWORD!
Please type uppercase yes to continue:

```

Oprócz skrótu programu ładującego, hak sprawdza również parametry działającego jądra względem tych skonfigurowanych w pliku `/etc/default/chkcryptoboot.conf`. Jest to sprawdzane zarówno w czasie wykonywania, jak i po zakończeniu procesu rozruchu. Pozwala to haczykowi wykryć, czy konfiguracja GRUB-a nie została ominięta w czasie wykonywania, a następnie wykryć, czy cała partycja {ic|/boot}} nie została ominięta.

W systemach BIOS hak tworzy hash pierwszego bootloadera GRUB-a (instalowanego do pierwszych 446 bajtów urządzenia rozruchowego) w celu porównania w późniejszych procesach rozruchowych. Główny drugi etap GRUB-a bootloadera `core.img` nie jest sprawdzany.

### Inne metody

Alternatywnie do powyższych skryptów można skonfigurować za pomocą [AIDE](/index.php/AIDE "AIDE"), którą można dostosować za pomocą bardzo elastycznego pliku konfiguracyjnego.

Chociaż jedna z tych metod powinna służyć większości użytkowników, nie rozwiązuje ona wszystkich problemów związanych z bezpieczeństwem związanym z niezaszyfrowaną partycją `/boot`. Jedno podejście, które stara się zapewnić w pełni uwierzytelniony łańcuch rozruchowy, zostało opublikowane w POTTS jako praca naukowa w celu wdrożenia struktury uwierzytelniania [STARK](http://www1.informatik.uni-erlangen.de/stark).

Potwierdzenie koncepcji POTTS wykorzystuje Arch Linux jako podstawową dystrybucję i implementuje łańcuch rozruchowy systemu

*   POTTS - menu startowe dla monitu o jednorazowe potwierdzenie uwierzytelnienia
*   TrustedGrub - a implementacja [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy"), która uwierzytelnia jądro i initramfs względem rejestrów układów TPM
*   TRESOR - łatka jądra, która implementuje AES, ale utrzymuje klucz główny nie w pamięci RAM, ale w rejestrach procesora podczas pracy.

As part of the thesis [installation](http://13.tc/p/potts/manual.html) instructions based on Arch Linux (ISO as of 2013-01) have been published. If you want to try it, be aware these tools are not in standard repositories and the solution will be time consuming to maintain.

W ramach pracy zostały opublikowane instrukcje [instalacji](http://13.tc/p/potts/manual.html) oparte na Arch Linux (ISO od 2013-01). Jeśli chcesz go wypróbować, pamiętaj, że te narzędzia nie znajdują się w standardowych repozytoriach, a rozwiązanie będzie wymagało czasu.

## Używanie zaszyfrowanych plików kluczy GPG, LUKS lub OpenSSL

następujące posty na forum podają instrukcje użycia uwierzytelniania dwuetapowego, gpg lub openssl zaszyfrowanych kluczy, zamiast pliku klucza tekstowego opisanego wcześniej w tym artykule wiki [System Encryption using LUKS with GPG encrypted keys](https://bbs.archlinux.org/viewtopic.php?id=120243):

*   GnuPG: [Post regarding GPG encrypted keys](https://bbs.archlinux.org/viewtopic.php?pid=943338#p943338) Ten post zawiera ogólne instrukcje.
*   OpenSSL: [Post regarding OpenSSL encrypted keys](https://bbs.archlinux.org/viewtopic.php?pid=947805#p947805) Ten post ma tylko `ssldec` haki.
*   OpenSSL: [Post regarding OpenSSL salted bf-cbc encrypted keys](https://bbs.archlinux.org/viewtopic.php?id=155393) Ten post ma `bfkf` initcpio przechwytuje, instaluje i zaszyfrowane skrypty generujące skrypty keyfile.
*   LUKS: [Post regarding LUKS encrypted keys](https://bbs.archlinux.org/viewtopic.php?pid=1502651#p1502651) z `lukskey` hakiem initcpio. Lub [#Encrypted /boot and a detached LUKS header on USB](#Encrypted_.2Fboot_and_a_detached_LUKS_header_on_USB) poniżej z niestandardowym hakiem do szyfrowania dla initcpio.

Zauważ, że:

*   Możesz wykonać powyższe instrukcje tylko z dwiema partycjami podstawowymi, jedną partycją rozruchową (wymaganą z powodu szyfrowania) i jedną podstawową partycją LVM. Na partycji LVM możesz mieć tyle partycji, ile potrzebujesz, ale co najważniejsze powinna zawierać przynajmniej partycje woluminu root, swap i home logical wolumin. Dodatkową zaletą jest posiadanie tylko jednego pliku klucza dla wszystkich partycji oraz możliwość hibernacji komputera (zawieszenie na dysk), w którym partycja wymiany jest szyfrowana. Jeśli zdecydujesz się na to, twoje haki w `/etc/mkinitcpio.conf` powinny wyglądać tak: `HOOKS=( ... usb usbinput (etwo or ssldec) encrypt (if using openssl) lvm2 resume ... )` i powinieneś dodać

 `resume=/dev/<VolumeGroupName>/<LVNameOfSwap>` do [parametrów jądra](/index.php/Kernel_parameters "Kernel parameters").

*   Jeśli musisz tymczasowo przechowywać zaszyfrowany plik klucza gdzieś, nie przechowuj ich na niezaszyfrowanym dysku. Nawet lepiej pamiętaj o zapisaniu ich w pamięci RAM, takich jak `/dev/shm`
*   Jeśli chcesz użyć pliku klucza szyfrowanego GPG, musisz użyć statycznie skompilowanej wersji GnuPG 1.4 lub możesz edytować haki i użyć tego pakietu AUR [gnupg1](https://aur.archlinux.org/packages/gnupg1/)
*   Możliwe, że aktualizacja OpenSSL może przerwać niestandardowe `ssldec` wymienione w drugim poście na forum.

## Zdalne odblokowanie partycji root (lub innej)

Jeśli chcesz móc zdalnie ponownie uruchomić system w pełni zaszyfrowany LUKS lub uruchomić go za pomocą usługi [Wake-on-LAN](/index.php/Wake-on-LAN "Wake-on-LAN") będziesz potrzebował sposobu na wprowadzenie hasła dla partycji / woluminu root podczas uruchamiania. Można to osiągnąć, uruchamiając hak [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio"), który konfiguruje interfejs sieciowy. Niektóre pakiety wymienione poniżej udostępniają różne [konfiguracje mkinitcpio](/index.php/Mkinitcpio#Build_hooks "Mkinitcpio") w celu ułatwienia konfiguracji.

**Note:**

*   Pamiętaj, aby używać nazw urządzeń jądra dla interfejsu sieciowego (np. `eth0`)), a nie dla [udev's](/index.php/Udev "Udev") (np. `enp1s0`), ponieważ te nie będą działać.
*   Konieczne może być dodanie modułu do [karty sieciowej](/index.php/Network_configuration#Device_driver "Network configuration") do tablicy [MODULES](/index.php/Mkinitcpio#MODULES "Mkinitcpio").

### Zdalne odblokowanie (haki: systemd, systemd-tool)

AUR pakiet [mkinitcpio-systemd-tool](https://aur.archlinux.org/packages/mkinitcpio-systemd-tool/) zapewnia [systemd](https://www.archlinux.org/packages/?name=systemd)-centric mkinitcpio hook o nazwie *systemd-tool* z następującym zestawem funkcji dla systemd w initramfs:

| 

Podstawowe funkcje zapewniane przez hak:

*   ujednolicona konfiguracja systemd + mkinitcpio
*   automatyczne przydzielanie zasobów binarnych i konfiguracyjnych
*   wywoływanie skryptów mkinitcpio i funkcji wbudowanych na żądanie

 | 

Funkcje oferowane przez dołączone jednostki serwisowe:

*   initrd debugging
*   wczesna konfiguracja sieci
*   interaktywna powłoka użytkownika
*   zdalny dostęp ssh w initrd
*   cryptsetup + niestandardowy agent hasła

 |

Pakiet [mkinitcpio-systemd-tool](https://aur.archlinux.org/packages/mkinitcpio-systemd-tool/) wymaga [haka systemowego](/index.php/Mkinitcpio#Common_hooks "Mkinitcpio"). Aby uzyskać więcej informacji, zapoznaj się z plikiem [README](https://github.com/random-archer/mkinitcpio-systemd-tool/blob/master/README.md) projektu oraz dostępnymi domyślnymi [plikami jednostek usług systemowych](https://github.com/random-archer/mkinitcpio-systemd-tool), aby rozpocząć.

Zalecane haki to: `base autodetect modconf block filesystems keyboard fsck systemd systemd-tool`.

### Zdalne odblokowanie (haki: netconf, dropbear, tinyssh, ppp)

Inną kombinacją pakietów zapewniającą zdalne logowanie do initcpio jest [mkinitcpio-netconf](https://aur.archlinux.org/packages/mkinitcpio-netconf/) i [mkinitcpio-ppp](https://aur.archlinux.org/packages/mkinitcpio-ppp/) (do zdalnego odblokowania za pomocą połączenia [PPP](https://en.wikipedia.org/wiki/Point-to-Point_Protocol "wikipedia:Point-to-Point Protocol") przez Internet) along w z serwerem [SSH](/index.php/SSH "SSH"). Możesz użyć albo [mkinitcpio-dropbear](https://aur.archlinux.org/packages/mkinitcpio-dropbear/) lub [mkinitcpio-tinyssh](https://aur.archlinux.org/packages/mkinitcpio-tinyssh/). Te haki nie instalują żadnej powłoki, więc musisz także [zainstalować](/index.php/Install "Install") [mkinitcpio-utils](https://aur.archlinux.org/packages/mkinitcpio-utils/)pakiet. Poniższe instrukcje mogą być używane w dowolnej kombinacji powyższych pakietów. Gdy istnieją różne ścieżki, zostanie to odnotowane.

1.  Jeśli nie masz jeszcze pary kluczy SSH, [wygeneruj](/index.php/SSH_keys#Generating_an_SSH_key_pair "SSH keys") ją w systemie klienta (tym, który będzie używany do odblokowania zdalnego komputera). Jeśli zdecydujesz się użyć [mkinitcpio-tinyssh](https://aur.archlinux.org/packages/mkinitcpio-tinyssh/), masz możliwość użycia klawiszy [Ed25519 keys](/index.php/SSH_keys#Ed25519 "SSH keys").
2.  Wstaw swój klucz publiczny SSH (tj. Ten, który zwykle umieszczasz na hostach, abyś mógł wejść bez hasła lub tego, które właśnie utworzyłeś i który kończy się na .pub) do pliku `/etc/dropbear/root_key` lub `/etc/tinyssh/root_key`.
    **Tip:** Ta metoda może później zostać użyta do dodania innych kluczy publicznych SSH w razie potrzeby; W przypadku zwykłego skopiowania zawartości plików `~/.ssh/authorized_keys`, należy sprawdzić, czy zawiera on tylko klucze, których zamierzasz użyć do odblokowania zdalnego komputera. Dodając dodatkowe klucze, zregeneruj swój initrd również za pomocą `mkinitcpio`. Zobacz też [Secure Shell#Protection](/index.php/Secure_Shell#Protection "Secure Shell").

3.  Dodaj wszystkie trzy `<netconf and/or ppp> <dropbear lub tinyssh> encryptssh` [hooks](/index.php/Mkinitcpio#HOOKS "Mkinitcpio") przed `filesystems` w tablicy "HOOKS" w `/etc/mkinitcpio.conf` (`encryptssh` zastępuje hook `encrypt`). Następnie zregeneruj [initramfs](/index.php/Initramfs "Initramfs").
    **Note:** Hak `net` dostarczony przez [mkinitcpio-nfs-utils](https://www.archlinux.org/packages/?name=mkinitcpio-nfs-utils) nie jest potrzebny.

4.  Skonfiguruj wymagany parametr `cryptdevice=` dodaj [parametr](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration") polecenia `ip=` [parametr komendy jądra](/index.php/Kernel_parameters "Kernel parameters") do bootloadera za pomocą odpowiednich argumentów. Na przykład, jeśli serwer DHCP nie przypisuje statycznego adresu IP do systemu zdalnego, co utrudnia dostęp przez SSH po ponownym uruchomieniu, można jawnie podać adres IP, który ma być używany `ip=192.168.1.1:::::eth0:none` Alternatywnie można również określić maskę podsieci i bramę wymaganą przez sieć: `ip=192.168.1.1::192.168.1.254:255.255.255.0::eth0:none` 
    **Note:** Od wersji 0.0.4 programu [mkinitcpio-netconf](https://aur.archlinux.org/packages/mkinitcpio-netconf/) można zagnieżdżać wiele parametrów `ip=` w celu skonfigurowania wielu interfejsów. Nie można mieszać go z `ip=dhcp` (`ip=:::::eth0:dhcp`) sam. Interfejs musi zostać określony.
     `ip=ip=192.168.1.1:::::eth0:none:ip=172.16.1.1:::::eth1:none` Aby uzyskać szczegółowy opis, spójrz na odpowiednią [sekcję mkinitcpio](/index.php/Mkinitcpio#Using_net "Mkinitcpio"). Po zakończeniu zaktualizuj konfigurację swojego [bootloadera](/index.php/Bootloader "Bootloader").
5.  Na koniec zrestartuj system zdalny i spróbuj [ssh do niego](/index.php/Secure_Shell#Client_usage "Secure Shell"), **jawnie określając nazwę użytkownika "root"** (nawet jeśli konto root jest wyłączone na komputerze, ten użytkownik root jest używany tylko w initrd w celu odblokowania systemu zdalnego). Jeśli korzystasz z pakietu [mkinitcpio-dropbear](https://aur.archlinux.org/packages/mkinitcpio-dropbear/) i masz zainstalowany pakiet [openssh](https://www.archlinux.org/packages/?name=openssh), najprawdopodobniej nie otrzymasz żadnych ostrzeżeń przed zalogowaniem się, ponieważ konwertuje on i używa tych samych kluczy hosta, co używa openssh (oprócz kluczy Ed25519, ponieważ dropbear ich nie obsługuje). Jeśli używasz [mkinitcpio-tinyssh](https://aur.archlinux.org/packages/mkinitcpio-tinyssh/), masz możliwość zainstalowania [tinyssh-convert](https://aur.archlinux.org/packages/tinyssh-convert/) lub [tinyssh-convert-git](https://aur.archlinux.org/packages/tinyssh-convert-git/), dzięki czemu możesz użyć tych samych kluczy, co twoja instalacja [openssh](https://www.archlinux.org/packages/?name=openssh) (obecnie tylko klucze Ed25519). W obu przypadkach powinieneś uruchomić [[Secure_Shell#Daemon_management|demona ssh] przynajmniej raz, używając dostarczonych jednostek systemd, aby klucze mogły zostać wygenerowane jako pierwsze. Po ponownym uruchomieniu komputera pojawi się monit o podanie hasła w celu odblokowania urządzenia root. System zakończy proces uruchamiania, a następnie możesz ssh do niego, [jak zwykle](/index.php/Secure_Shell#Client_usage "Secure Shell") (z wybranym użytkownikiem zdalnym).

**Tip:** Jeśli chcesz po prostu dobre rozwiązanie do zdalnego montowania innych zaszyfrowanych partycji (takich jak `/home`), możesz zajrzeć do [[https://bbs.archlinux.org/viewtopic.php?pid=880484](https://bbs.archlinux.org/viewtopic.php?pid=880484) tego wątku na forum.

### Zdalne odblokowanie przez Wi-Fi (haki: buduj własne)

Hak sieciowy jest zwykle używany z połączeniem ethernetowym. Jeśli chcesz skonfigurować komputer tylko z siecią bezprzewodową i odblokować go przez Wi-Fi, możesz utworzyć niestandardowy hak, aby połączyć się z siecią Wi-Fi przed uruchomieniem haka sieciowego.

Poniższy przykład pokazuje konfigurację za pomocą adaptera USB, łączącego się z siecią Wi-Fi chronioną WPA2-PSK. Jeśli użyjesz na przykład WEP lub innego programu ładującego, być może będziesz musiał zmienić niektóre rzeczy.

1.  Zmodyfikuj `/etc/mkinitcpio.conf`:
    *   Dodaj potrzebny moduł jądra do konkretnego adaptera Wi-Fi
    *   Dołącz pliki binarne `wpa_passphrase` i `wpa_supplicant`.
    *   Dodaj hak `wifi` (lub nazwę do wyboru, jest to niestandardowy hak, który zostanie utworzony) przed hakiem `net`.
        ```
        MODULES=(*module*)
        BINARIES=(wpa_passphrase wpa_supplicant)
        HOOKS=(base udev autodetect ... **wifi** net ... dropbear encryptssh ...)
        ```

2.  Utwórz hak `wifi` w `/etc/initcpio/hooks/wifi`:
    ```
    run_hook ()
    {
    	# sleep a couple of seconds so wlan0 is setup by kernel
    	sleep 5

    	# set wlan0 to up
    	ip link set wlan0 up

    	# assocciate with wifi network
    	# 1\. save temp config file
    	wpa_passphrase "*network ESSID*" "*pass phrase*" > /tmp/wifi

    	# 2\. assocciate
    	wpa_supplicant -B -D nl80211,wext -i wlan0 -c /tmp/wifi

    	# sleep a couple of seconds so that wpa_supplicant finishes connecting
    	sleep 5

    	# wlan0 should now be connected and ready to be assigned an ip by the net hook
    }

    run_cleanuphook ()
    {
    	# kill wpa_supplicant running in the background
    	killall wpa_supplicant

    	# set wlan0 link down
    	ip link set wlan0 down

    	# wlan0 should now be fully disconnected from the wifi network
    }
    ```

3.  Utwórz plik instalacyjny hook w `/etc/initcpio/install/wifi`:
    ```
    build ()
    {
    	add_runscript
    }
    help ()
    {
    cat<<HELPEOF
    	Enables wifi on boot, for dropbear ssh unlocking of disk.
    HELPEOF
    }
    ```

4.  Dodaj `ip=:::::wlan0:dhcp` do [parametrów jądra](/index.php/Kernel_parameters "Kernel parameters"). Usuń `ip=:::::eth0:dhcp`, aby nie było konfliktu.
5.  Opcjonalnie utwórz dodatkowy wpis rozruchowy z parametrem jądra `ip=:::::eth0:dhcp`.
6.  [Zregenerować initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs").
7.  Update the configuration of your [boot loader](/index.php/Boot_loader "Boot loader").

Pamiętaj, aby skonfigurować [wifi](/index.php/Wifi "Wifi"), aby móc zalogować się po pełnym uruchomieniu systemu. Jeśli nie możesz połączyć się z siecią Wi-Fi, spróbuj nieco wydłużyć czas uśpienia.

## Obsługa Discard / TRIM dla dysków półprzewodnikowych (SSD)

Użytkownicy [Solid State Drive](/index.php/Solid_State_Drive "Solid State Drive") powinni mieć świadomość, że domyślnie polecenia TRIM nie są włączane przez urządzenie mapujące urządzenia, tj. Urządzenia blokowe są montowane bez opcji `discard` chyba że zastąpi się domyślną.

Opiekunowie device-mapper wyraźnie dali do zrozumienia, że obsługa TRIM nigdy nie będzie domyślnie włączona na urządzeniach dm-crypt ze względu na potencjalne konsekwencje dla bezpieczeństwa [[3]](http://www.saout.de/pipermail/dm-crypt/2011-September/002019.html)[[4]](http://www.saout.de/pipermail/dm-crypt/2012-April/002420.html) Minimalny wyciek danych w postaci uwolnionych informacji blokowych, być może wystarczających do określenia używanego systemu plików, może wystąpić na urządzeniach z włączoną obsługą TRIM. Ilustracja i omówienie problemów wynikających z aktywacji TRIM jest dostępna na [blogu](http://asalor.blogspot.de/2011/08/trim-dm-crypt-problems.html) programisty cryptsetup. Jeśli obawiasz się o takie czynniki, pamiętaj, że zagrożenia mogą się sumować: na przykład, jeśli Twoje urządzenie jest nadal szyfrowane za pomocą domyślnego szyfrowania (cryptsetup <1.6.0) `--cipher aes-cbc-essiv`, więcej informacji wyciek może nastąpić więcej wycieków informacji z przyciętej obserwacji sektora niż z bieżącą wartością [domyślną](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_LUKS_mode "Dm-crypt/Device encryption").

Można wyróżnić następujące przypadki:

*   Urządzenie jest szyfrowane za pomocą domyślnego trybu LUKS dm-crypt:
    *   Domyślnie nagłówek LUKS jest przechowywany na początku urządzenia, a użycie polecenia TRIM jest przydatne do ochrony modyfikacji nagłówka. Jeśli na przykład zhakowane hasło LUKS zostanie odwołane, bez TRIM stary nagłówek będzie ogólnie dostępny do odczytu aż do nadpisania przez inną operację; jeśli dysk zostanie skradziony w międzyczasie, atakujący mogą teoretycznie znaleźć sposób na zlokalizowanie starego nagłówka i użyć go do odszyfrowania zawartości za pomocą złamanego hasła. Zobacz [cryptsetup FAQ, section 5.19 What about SSDs, Flash and Hybrid Drives?](https://gitlab.com/cryptsetup/cryptsetup/wikis/FrequentlyAskedQuestions#5-security-aspects) i [Full disk encryption on an ssd](https://www.reddit.com/r/archlinux/comments/2f370s/full_disk_encryption_on_an_ssd/ck5p5c5).
    *   TRIM można pozostawić wyłączony, jeśli problemy bezpieczeństwa wymienione w górnej części tej sekcji są uważane za gorsze zagrożenie niż powyższy punkt.

	Zobacz też [Securely wipe disk#Flash memory](/index.php/Securely_wipe_disk#Flash_memory "Securely wipe disk").

*   Urządzenie jest szyfrowane w trybie zwykłym dm-crypt lub nagłówek LUKS jest przechowywany [osobno](#Encrypted_system_using_a_detached_LUKS_header):
    *   Jeśli wymagana wiarygodność jest wymagana, TRIM **nigdy** nie powinien być używany ze względu na rozważania u góry tej sekcji lub użycie szyfrowania zostanie podane.
    *   Jeśli wiarygodna zaprzeczalność nie jest wymagana, TRIM może być wykorzystany do zwiększenia wydajności, pod warunkiem, że zagrożenia bezpieczeństwa opisane na początku tej sekcji nie budzą obaw.

**Warning:** Przed włączeniem TRIM na dysku upewnij się, że urządzenie w pełni obsługuje polecenia TRIM lub może nastąpić utrata danych. Zobacz [Solid State Drives#TRIM](/index.php/Solid_State_Drives#TRIM "Solid State Drives").

W [linux](https://www.archlinux.org/packages/?name=linux) 3.1 i nowszych, obsługa przejścia tranzytowego TRM w dm-crypt może być przełączana podczas tworzenia urządzenia lub montowania za pomocą polecenia dmsetup. Obsługa tej opcji istnieje również w wersji [cryptsetup](https://www.archlinux.org/packages/?name=cryptsetup) 1.4.0 i nowszych. Aby dodać obsługę podczas rozruchu, musisz dodać: `:allow-discards` do opcji `cryptdevice`. Opcja TRIM może wyglądać następująco:

```
cryptdevice=/dev/sdaX:root:allow-discards

```

Dla głównych opcji konfiguracyjnych `cryptdevice` przed: `:allow-discards` zobacz [Dm-crypt/System configuration](/index.php/Dm-crypt/System_configuration "Dm-crypt/System configuration").

Jeśli używasz initrd opartego na systemd, musisz przekazać:

```
rd.luks.options=discard

```

**Note:** Opcja `rd.luks.options=discard` kernel nie ma żadnego wpływu na urządzenia zawarte w pliku `/etc/crypttab` pliku obrazu initramfs (`/etc/crypttab.initramfs` na prawdziwym root). Musisz podać opcję `discard` w `/etc/crypttab.initramfs`.

Oprócz opcji jądra, wymagane jest również okresowe uruchamianie `fstrim` lub montowanie systemu plików (np. `/dev/mapper/root` w tym przykładzie) z opcją `discard` w `/etc/fstab`. Szczegółowe informacje można znaleźć na stronie [TRIM](/index.php/TRIM "TRIM").

Dla urządzeń LUKS odblokowanych przez `/etc/crypttab` użyj opcji `discard`, np .:

 `/etc/crypttab`  `luks-123abcdef-etc UUID=123abcdef-etc none discard` 

Gdy odblokowujesz ręcznie urządzenia na konsoli, użyj `--allow-discards`.

W LUKS2 możesz ustawić opcję `allow-discards` jako flagę domyślną dla urządzenia, otwierając ją raz z opcją `--persistent`:

```
# cryptsetup --allow-discards --persistent open --type luks2 /dev/sdaX root

```

Możesz potwierdzić, że flaga jest ustawiona trwale w nagłówku LUKS2, patrząc na wynik `cryptsetup luksDump`:

 `# cryptsetup luksDump /dev/sdaX | grep Flags` 
```
Flags:          allow-discards

```

W każdym przypadku możesz sprawdzić, czy urządzenie faktycznie zostało otwarte z odrzutami, sprawdzając wynik `dmsetup table`:

 `# dmsetup table` 
```
luks-123abcdef-etc: 0 1234567 crypt aes-xts-plain64 000etc000 0 8:2 4096 1 allow_discards

```

## Szyfrowanie hakiem i wiele dysków

**Tip:** `sd-encrypt` hook obsługuje odblokowywanie wielu urządzeń. Można je podać w wierszu komend jądra lub w `/etc/crypttab.initramfs`. Zobacz [dm-crypt/System configuration#Using sd-encrypt hook](/index.php/Dm-crypt/System_configuration#Using_sd-encrypt_hook "Dm-crypt/System configuration").

Szyfrowanie pozwala tylko na pojedynczy wpis `cryptdevice=` [FS#23182](https://bugs.archlinux.org/task/23182)). W konfiguracjach systemowych z wieloma napędami może to być ograniczenie, ponieważ *dm-crypt* nie ma funkcji, która mogłaby przekroczyć fizyczne urządzenie. Na przykład w "LVM na LUKS": Cała LVM istnieje wewnątrz LUKS mapper. Jest to całkowicie w porządku dla systemu z jednym napędem, ponieważ istnieje tylko jedno urządzenie do odszyfrowania. Ale co się stanie, gdy chcesz zwiększyć rozmiar LVM? Nie możesz, przynajmniej nie bez modyfikowania haka `encrypt`.

W poniższych sekcjach krótko pokazano alternatywne rozwiązania, aby przezwyciężyć ograniczenie. Pierwszy dotyczy sposobu rozszerzenia [LUKS na instalację LVM](/index.php/Dm-crypt/Encrypting_an_entire_system_(Polski)#LUKS_na_LVM "Dm-crypt/Encrypting an entire system (Polski)") na nowy dysk. Drugi z modyfikowaniem haka `encrypt` w celu odblokowania wielu dysków w konfiguracjach LUKS bez LVM.

### Rozszerzanie LVM na wielu dyskach

Zarządzanie wieloma dyskami jest podstawową funkcją [LVM](/index.php/LVM "LVM") i główną przyczyną elastyczności partycjonowania. Może być również używany z *dm-crypt*, ale tylko wtedy, gdy LVM jest używany jako pierwszy element odwzorowujący. W takich [LUKS na instalacji LVM](/index.php/Dm-crypt/Encrypting_an_entire_system_(Polski)#LUKS_na_LVM "Dm-crypt/Encrypting an entire system (Polski)") LVM zaszyfrowane urządzenia są tworzone wewnątrz woluminów logicznych (z oddzielnym hasłem/kluczem na wolumin). Poniżej opisano kroki mające na celu rozszerzenie tej konfiguracji na inny dysk.

**Warning:** Utworzyć kopię zapasową! Chociaż zmiana rozmiaru systemów plików może być standardowa, należy pamiętać, że operacje mogą się nie udać, a poniższe mogą nie mieć zastosowania w konkretnej instalacji. Ogólnie rzecz biorąc, rozszerzenie systemu plików na wolne miejsce na dysku jest mniej problematyczne niż jego zmniejszenie. Dotyczy to w szczególności, gdy używane są ułożone elementy odwzorowujące, jak to ma miejsce w następnym przykładzie.

#### Dodanie nowego dysku

Po pierwsze, może być pożądane przygotowanie nowego dysku zgodnie z przygotowaniem [dm-crypt/Drive preparation (Polski)](/index.php/Dm-crypt/Drive_preparation_(Polski) "Dm-crypt/Drive preparation (Polski)"). Po drugie, jest podzielony na partycje jako LVM, np. cała przestrzeń jest przydzielona do `/dev/sdY1` z typem partycji `8E00` (Linux LVM). Po trzecie, nowy dysk/partycja jest dołączona do istniejącej grupy woluminów LVM, np.:

```
# pvcreate /dev/sdY1
# vgextend MyStorage /dev/sdY1

```

#### Rozszerzanie woluminu logicznego

W kolejnym kroku, przydział nowej przestrzeni dyskowej, wolumin logiczny, który ma zostać rozszerzony, musi zostać odłączony. Można go wykonać dla partycji root `cryptdevice` ale w tym przypadku procedurę należy wykonać z poziomu Arch Install ISO.

W tym przykładzie zakłada się, że wolumin logiczny dla `/home` ((lv-name `homevol`) zostanie rozszerzony o świeżą przestrzeń dyskową:

```
# umount /home
# fsck /dev/mapper/home
# cryptsetup luksClose /dev/mapper/home
# lvextend -l +100%FREE MyStorage/homevol

```

Teraz wolumen logiczny jest rozszerzony, a kontener LUKS jest następny:

```
# cryptsetup open /dev/MyStorage/homevol home
# umount /home      # as a safety, in case it was automatically remounted
# cryptsetup --verbose resize home

```

Wreszcie, sam system plików jest zmieniany:

```
# e2fsck -f /dev/mapper/home
# resize2fs /dev/mapper/home

```

Gotowe! Jeśli poszedł do planu, `/home` można ponownie złożyć i obejmuje teraz zakres na nowy dysk:

```
# mount /dev/mapper/home /home

```

Zauważ, że zmiana `cryptsetup resize` nie wpływa na klucze szyfrowania, a te nie uległy zmianie.

### Modyfikowanie haków szyfrowania dla wielu partycji

#### Główny system plików obejmujący wiele partycji

Możliwe jest zmodyfikowanie haka szyfrowania, aby umożliwić odszyfrowanie root'a (`/`) podczas startu systemu. Jeden sposób:

```
# cp /usr/lib/initcpio/install/encrypt /etc/initcpio/install/encrypt2
# cp /usr/lib/initcpio/hooks/encrypt  /etc/initcpio/hooks/encrypt2
# sed -i "s/cryptdevice/cryptdevice2/" /etc/initcpio/hooks/encrypt2
# sed -i "s/cryptkey/cryptkey2/" /etc/initcpio/hooks/encrypt2

```

Dodaj `cryptdevice2=` do swoich opcji rozruchowych (i `cryptkey2=` w razie potrzeby), i dodaj hook `encrypt2` do swojego pliku [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf") przed jego odbudowaniem. Zobacz [dm-crypt/System configuration](/index.php/Dm-crypt/System_configuration "Dm-crypt/System configuration").

#### Wiele partycji innych niż root

Być może masz wymóg korzystania z `encrypt` przechwytywania na partycji innej niż root. Arch nie obsługuje tego z pudełka, ale możesz łatwo zmienić wartości cryptdev i cryptname w `/lib/initcpio/hooks/encrypt` (pierwszy na partycję `/dev/sd*`, drugi na nazwę, którą chcesz przypisywać). To powinno wystarczyć.

Dużą zaletą jest to, że możesz mieć wszystko zautomatyzowane, podczas gdy konfiguracja `/etc/crypttab` z zewnętrznym plikiem klucza (np. Plik klucza nie znajduje się na żadnej wewnętrznej partycji dysku twardego) może być uciążliwa - musisz upewnić się, że USB/FireWire / ... urządzenie zostanie zamontowane przed zaszyfrowaną partycją, co oznacza, że musisz zmienić kolejność `/etc/fstab` (przynajmniej).

Oczywiście, jeśli pakiet [cryptsetup](https://www.archlinux.org/packages/?name=cryptsetup) zostanie uaktualniony, będziesz musiał ponownie zmienić ten skrypt. W przeciwieństwie do `/etc/crypttab`, obsługiwana jest tylko jedna partycja, ale z kilkoma dalszymi włamaniami powinno być możliwe odblokowanie wielu partycji.

Jeśli chcesz to zrobić na partycji programowego RAID, musisz jeszcze zrobić jeszcze jedną rzecz. Samo ustawienie urządzenia `/dev/mdX` w `/lib/initcpio/hooks/encrypt` nie wystarcza; hak `encrypt` nie uda się znaleźć klucza z jakiegoś powodu i nie poprosi o podanie hasła. Wygląda na to, że urządzenia RAID nie są przywoływane aż do uruchomienia haka `encrypt`. Możesz rozwiązać ten problem, umieszczając macierz RAID w katalogu `/boot/grub/menu.lst`, np.

```
kernel /boot/vmlinuz-linux md=1,/dev/hda5,/dev/hdb5

```

Jeśli skonfigurujesz partycję root jako RAID, zauważysz podobieństwa z tą konfiguracją. [GRUB](/index.php/GRUB "GRUB") radzi sobie z wieloma definicjami tablic:

```
kernel /boot/vmlinuz-linux root=/dev/md0 ro md=0,/dev/sda1,/dev/sdb1 md=1,/dev/sda5,/dev/sdb5,/dev/sdc5

```

## Szyfrowany system za pomocą oddzielnego nagłówka LUKS

Ten przykład jest zgodny z tym samym ustawieniem, co w [dm-crypt/Encrypting an entire system (Polski)#Zwykły dm-crypt](/index.php/Dm-crypt/Encrypting_an_entire_system_(Polski)#Zwyk.C5.82y_dm-crypt "Dm-crypt/Encrypting an entire system (Polski)"), które należy przeczytać najpierw przed wykonaniem tego przewodnika.

Używając oddzielnego nagłówka, zaszyfrowane urządzenie blokowe przenosi tylko zaszyfrowane dane, co daje [dyskretne szyfrowanie](https://en.wikipedia.org/wiki/Deniable_encryption "wikipedia:Deniable encryption"), o ile istnienie nagłówka nie jest znane atakującym. Jest podobne do używania [Zwykły dm-crypt](/index.php/Dm-crypt/Encrypting_an_entire_system_(Polski)#Zwyk.C5.82y_dm-crypt "Dm-crypt/Encrypting an entire system (Polski)"), ale z zaletami LUKS, takimi jak wielokrotne hasła dla klucza głównego i pochodnej klucza.Co więcej, użycie oddzielnego nagłówka oferuje formę uwierzytelniania dwuskładnikowego z łatwiejszą konfiguracją niż [przy użyciu zaszyfrowanych plików kluczy GPG lub OpenSSL](#Using_GPG.2C_LUKS.2C_or_OpenSSL_Encrypted_Keyfiles), a jednocześnie ma wbudowane zapytanie o hasło dla wielokrotnych prób. Zobacz [Disk encryption#Cryptographic metadata](/index.php/Disk_encryption#Cryptographic_metadata "Disk encryption") po więcej informacji.

Zobacz [dm-crypt/Device encryption (Polski)#Opcje szyfrowania dla trybu LUKS](/index.php/Dm-crypt/Device_encryption_(Polski)#Opcje_szyfrowania_dla_trybu_LUKS "Dm-crypt/Device encryption (Polski)") dla opcji szyfrowania przed wykonaniem pierwszego kroku, aby skonfigurować zaszyfrowaną partycję systemową i utworzyć plik nagłówkowy do użycia z `cryptsetup`:

```
# dd if=/dev/zero of=header.img bs=4M count=1 conv=notrunc
# cryptsetup luksFormat --type luks2 /dev/sdX --align-payload 8192 --header header.img

```

**Tip:** Używając opcji `--header`, `--align-payload` pozwala określić początek zaszyfrowanych danych na urządzeniu. Rezerwując miejsce na początku urządzenia, możesz później ponownie [podłączyć nagłówek LUKS](/index.php/Dm-crypt/Device_encryption#Restore_using_cryptsetup "Dm-crypt/Device encryption") Zobacz [cryptsetup(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cryptsetup.8) dla wartości obsługiwanych przez `--align-payload`.

Otwórz kontener:

```
# cryptsetup open --header header.img /dev/sdX enc

```

Teraz postępuj zgodnie z [LVM na konfiguracji LUKS](/index.php/Dm-crypt/Encrypting_an_entire_system_(Polski)#Przygotowywanie_partycji.2C_kt.C3.B3re_nie_s.C4.85_uruchomione "Dm-crypt/Encrypting an entire system (Polski)") do swoich wymagań. To samo dotyczy [przygotowywania partycji rozruchowej](/index.php/Dm-crypt/Encrypting_an_entire_system_(Polski)#Przygotowanie_partycji_rozruchowej_4 "Dm-crypt/Encrypting an entire system (Polski)") na urządzeniu wymiennym (ponieważ w przeciwnym razie nie ma sensu posiadanie oddzielnego pliku nagłówkowego do odblokowania zaszyfrowanego dysku). Następnie przenieś plik `header.img`:

```
# mv header.img /mnt/boot

```

Postępuj zgodnie z procedurą instalacji aż do kroku mkinitcpio (powinieneś już być `arch-chroot` wewnątrz zaszyfrowanego systemu).

**Tip:** Zauważysz, że ponieważ partycja systemowa ma tylko "losowe" dane, nie ma ona tablicy partycji, a przez to `UUID` ani `LABEL`.. Ale nadal możesz mieć spójne mapowanie za pomocą [Persistent block device naming#by-id and by-path](/index.php/Persistent_block_device_naming#by-id_and_by-path "Persistent block device naming"). Na przykład. używanie identyfikatora dysku `/dev/disk/by-id/`.

Istnieją dwie opcje dla initramfs do obsługi odłączonego nagłówka LUKS.

### Używanie haka systemd

Najpierw utwórz `/etc/crypttab.initramfs` i dodaj do niego zaszyfrowane urządzenie. Składnia jest zdefiniowana w [crypttab(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/crypttab.5)

 `/etc/crypttab.initramfs`  `enc	/dev/disk/by-id/*your-disk_id*	none	header=/boot/header.img` 

Zmodyfikuj plik `/etc/mkinitcpio.conf` , aby [Mkinitcpio#Common_hooks|używał systemd]] i dodaj nagłówek do `FILES`.

 `/etc/mkinitcpio.conf` 
```
...
FILES=(**/boot/header.img**)
...
HOOKS=(base **systemd** autodetect **keyboard** **sd-vconsole** modconf block **sd-encrypt** **sd-lvm2** filesystems fsck)
...
```

[Zregeneruj initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs") i gotowe.

**Note:** Żadne parametry cryptsetup nie muszą być przekazywane do wiersza poleceń jądra, ponieważ `/etc/crypttab.initramfs` zostanie dodane jako `/etc/crypttab` do initramfs. Jeśli chcesz je określić w wierszu komend jądra, zobacz [dm-crypt/System configuration#Using sd-encrypt hookdla](/index.php/Dm-crypt/System_configuration#Using_sd-encrypt_hook "Dm-crypt/System configuration") obsługiwanych opcji.

### Modyfikowanie haka szyfrowania

Ta metoda pokazuje, jak zmodyfikować hak `encrypt`, aby użyć oddzielnego nagłówka LUKS. Teraz `encrypt` hak musi zostać zmodyfikowany, aby umożliwić `cryptsetup` użycie osobnego nagłówka (([FS#42851](https://bugs.archlinux.org/task/42851); podstawowe źródło i pomysł dla tych zmian opublikowanych w BBS). Utwórz kopię, aby nie została nadpisana w aktualizacji mkinitcpio:

```
# cp /usr/lib/initcpio/hooks/encrypt /etc/initcpio/hooks/encrypt2
# cp /usr/lib/initcpio/install/encrypt /etc/initcpio/install/encrypt2

```
 `/etc/initcpio/hooks/encrypt2 (around line 52)` 
```
warn_deprecated() {
    echo "The syntax 'root=${root}' where '${root}' is an encrypted volume is deprecated"
    echo "Use 'cryptdevice=${root}:root root=/dev/mapper/root' instead."
}

**local headerFlag=false**
for cryptopt in ${cryptoptions//,/ }; do
    case ${cryptopt} in
        allow-discards)
            cryptargs="${cryptargs} --allow-discards"
            ;;  
        **header)
            cryptargs="${cryptargs} --header /boot/header.img"
            headerFlag=true
            ;;**
        *)  
            echo "Encryption option '${cryptopt}' not known, ignoring." >&2 
            ;;  
    esac
done

if resolved=$(resolve_device "${cryptdev}" ${rootdelay}); then
    if **$headerFlag ||** cryptsetup isLuks ${resolved} >/dev/null 2>&1; then
        [ ${DEPRECATED_CRYPT} -eq 1 ] && warn_deprecated
        dopassphrase=1
```

Teraz zmodyfikuj plik [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf"), aby dodać haki `encrypt2` i `lvm2`, `header.img` do `FILES` i `loop` do MODULES, oprócz innych konfiguracji system wymaga:

 `/etc/mkinitcpio.conf` 
```
...
MODULES=(**loop**)
...
FILES=(**/boot/header.img**)
...
HOOKS=(base udev autodetect **keyboard** **keymap** consolefont modconf block **encrypt2** **lvm2** filesystems fsck)
...
```

Jest to wymagane, aby nagłówek LUKS był dostępny podczas rozruchu, umożliwiając odszyfrowanie systemu, zwalniając nas z bardziej skomplikowanej konfiguracji, aby zamontować inne oddzielne urządzenie USB w celu uzyskania dostępu do nagłówka. Po tej konfiguracji tworzony jest [initramfs](/index.php/Mkinitcpio#Image_creation_and_activation "Mkinitcpio").

Następnie [bootlader](/index.php/Dm-crypt/Encrypting_an_entire_system#Configuring_the_boot_loader_4 "Dm-crypt/Encrypting an entire system") jest skonfigurowany tak, aby określał `cryptdevice=` również przekazywanie nowej opcji `header` dla tej instalacji:

```
cryptdevice=/dev/disk/by-id/*your-disk_id*:enc:header

```

Aby zakończyć, wykonaj [dm-crypt/Encrypting an entire system (Polski)#Po instalacji](/index.php/Dm-crypt/Encrypting_an_entire_system_(Polski)#Po_instalacji "Dm-crypt/Encrypting an entire system (Polski)") jest szczególnie przydatny w przypadku partycji `/boot` na nośniku USB.

## Szyfrowanie /boot i odłączony nagłówek LUKS na USB

Zamiast osadzać plik `header.img` i keyfile w obrazie [initramfs](/index.php/Initramfs "Initramfs"), ta konfiguracja sprawi, że twój system będzie całkowicie zależny od klucza USB, a nie tylko obrazu boot i od zaszyfrowanego pliku klucza wewnątrz zaszyfrowanej partycji rozruchowej. Ponieważ nagłówek i plik klucza nie są zawarte w obrazie initramfs, a niestandardowy zaszyfrowanie jest przeznaczone specjalnie dla identyfikatora USB, dosłownie potrzebujesz klucza USB do rozruchu. Ponieważ nagłówek i plik klucza nie są zawarte w obrazie [initramfs](/index.php/Initramfs "Initramfs"), a niestandardowy zaszyfrowanie jest przeznaczone specjalnie dla identyfikatora USB [by-id](/index.php/Persistent_block_device_naming#by-id_and_by-path "Persistent block device naming"), dosłownie potrzebujesz klucza USB do rozruchu.

W przypadku dysku USB, ponieważ szyfrujesz dysk i plik klucza w środku, najlepiej jest kaskadować szyfry, aby nie używać tego samego dwa razy. To, czy atak typu [meet-in-the-middle](https://en.wikipedia.org/wiki/Meet-in-the-middle_attack "wikipedia:Meet-in-the-middle attack") będzie faktycznie wykonalny, jest dyskusyjne. Możesz użyć twofish-serpent lub serpent-twofish.

### Przygotowywanie urządzeń dyskowych

Zakłada się, że `sdb` będzie napędem USB, a `sda` będzie głównym dyskiem twardym.

Przygotuj urządzenia zgodnie z [dm-crypt/Drive preparation (Polski)](/index.php/Dm-crypt/Drive_preparation_(Polski) "Dm-crypt/Drive preparation (Polski)").

#### Przygotowanie klucza USB

Użyj [gdisk](/index.php/Fdisk#gdisk "Fdisk"), aby podzielić dysk na partycje zgodnie z [pokazanym tu układem](/index.php/Dm-crypt/Encrypting_an_entire_system_(Polski)#Przygotowanie_dysku_5 "Dm-crypt/Encrypting an entire system (Polski)"), z tym wyjątkiem, że powinien zawierać tylko pierwsze dwie partycje. Oto, co następuje:

 `# gdisk /dev/sdb` 
```
Number  Start (sector)    End (sector)  Size       Code  Name
   1            2048         1050623   512.0 MiB   EF00  EFI System
   2         1050624         1460223   200.0 MiB   8300  Linux filesystem

```

Przed uruchomieniem `cryptsetup` najpierw sprawdź [opcje Szyfrowania dla LUKS](/index.php/Dm-crypt/Device_encryption_(Polski)#Opcje_szyfrowania_dla_trybu_LUKS "Dm-crypt/Device encryption (Polski)") i [Szyfrów oraz tryby działania](/index.php/Disk_encryption_(Polski)#Szyfry_i_tryby_dzia.C5.82ania "Disk encryption (Polski)"), aby wybrać pożądane ustawienia.

[Przygotuj partycję rozruchową](/index.php/Dm-crypt/Encrypting_an_entire_system#Preparing_the_boot_partition_5 "Dm-crypt/Encrypting an entire system"), ale nie `mount` jeszcze żadnej partycji i [sformatuj partycję systemową EFI](/index.php/EFI_system_partition#Format_the_partition "EFI system partition").

```
# mount /dev/mapper/cryptboot /mnt
# dd if=/dev/urandom of=/mnt/key.img bs=*filesize* count=1
# cryptsetup --align-payload=1 luksFormat /mnt/key.img
# cryptsetup open /mnt/key.img lukskey

```

*filesize* jest w bajtach, ale może być poprzedzone przyrostkiem takim jak `M`. Zbyt mały plik sprawi, że będziesz nieprzyjemny `Requested offset is beyond real size of device /dev/loop0` error. Jako przybliżone odniesienie, utworzenie pliku 4M spowoduje jego pomyślne zaszyfrowanie. Powinieneś uczynić plik większym, niż potrzeba, ponieważ zaszyfrowane urządzenie będzie trochę mniejsze niż rozmiar pliku.

Przy dużym pliku możesz użyć opcji `--keyfile-offset=*offset*` i `--keyfile-size=*size*` aby przejść do właściwej pozycji. [[5]](https://wiki.gentoo.org/wiki/Custom_Initramfs#Encrypted_keyfile)

Teraz powinieneś mieć `lukskey` otwarty w urządzeniu pętlowym (pod spodem `/dev/loop1`) zmapowane jako `/dev/mapper/lukskey`.

#### Główny napęd

```
# truncate -s 2M /mnt/header.img
# cryptsetup --key-file=/dev/mapper/lukskey --keyfile-offset=*offset* --keyfile-size=*size* luksFormat /dev/sda --align-payload 4096 --header /mnt/header.img

```

Wybierz *offset* i rozmiar w bajtach (8192 bajty to maksymalny rozmiar pliku klucza dla `cryptsetup`)

```
# cryptsetup open --header /mnt/header.img --key-file=/dev/mapper/lukskey --keyfile-offset=*offset* --keyfile-size=*size* /dev/sda enc 
# cryptsetup close lukskey
# umount /mnt

```

Wykonaj czynności [Przygotowywanie woluminów logicznych](/index.php/Dm-crypt/Encrypting_an_entire_system_(Polski)#Przygotowywanie_wolumin.C3.B3w_logicznych "Dm-crypt/Encrypting an entire system (Polski)") w celu skonfigurowania LVM na LUKS.

Zobacz [Partitioning#Discrete partitions](/index.php/Partitioning#Discrete_partitions "Partitioning") dla zaleceń dotyczących rozmiaru twoich partycji.

Po zamontowaniu partycji root `mount` zaszyfrowaną partycję rozruchową jako `/mnt/boot` i partycję ESP lub EFI jako `/mnt/boot/efi`.

### Procedura instalacji i niestandardowe szyfrowanie hook

Postępuj zgodnie z [instrukcją instalacji](/index.php/Installation_guide "Installation guide") aż do kroku `mkinitcpio`, ale nie rób jeszcze tego, a następnie pomiń procedury partycjonowania, formatowania i motowania, ponieważ zostały już wykonane.

Aby zaszyfrować konfigurację, musisz zbudować własny hak, który jest na szczęście łatwy do zrobienia i tutaj jest kod, którego potrzebujesz. Będziesz musiał postępować zgodnie z [Persistent block device naming#by-id and by-path](/index.php/Persistent_block_device_naming#by-id_and_by-path "Persistent block device naming") aby obliczyć własne wartości `by-id` dla dysku USB i głównego dysku twardego (są one połączone -> do `sda` lub `sdb`)).

Powinieneś używać `by-id` pomocniczego zamiast tylko `sda` lub `sdb`, ponieważ `sdX` może się zmienić, to gwarantuje, że jest to właściwe urządzenie.

Możesz nazywać `customencrypthook`, co tylko chcesz, a niestandardowe haki do budowania można umieszczać w `hooks` i instalować foldery w `/etc/initcpio`. Zachowaj kopię zapasową obu plików (przenieś je do partycji `/home` lub katalogu `/home` / home po jej utworzeniu). `/usr/bin/ash` to nie literówka.

 `/etc/initcpio/hooks/customencrypthook` 
```
#!/usr/bin/ash

run_hook() {
    modprobe -a -q dm-crypt >/dev/null 2>&1
    modprobe loop
    [ "${quiet}" = "y" ] && CSQUIET=">/dev/null"

    while [ ! -L '/dev/disk/by-id/*usbdrive*-part2' ]; do
     echo 'Waiting for USB'
     sleep 1
    done

    cryptsetup open /dev/disk/by-id/*usbdrive*-part2 cryptboot
    mkdir -p /mnt
    mount /dev/mapper/cryptboot /mnt
    cryptsetup open /mnt/key.img lukskey
    cryptsetup --header /mnt/header.img --key-file=/dev/mapper/lukskey --keyfile-offset=''offset'' --keyfile-size=''size'' open /dev/disk/by-id/*harddrive* enc
    cryptsetup close lukskey
    umount /mnt
}

```

Dysk `*usbdrive*` to Twój `by-id` napędu USB, a `*harddrive*` jest twoim głównym dyskiem twardym.

**Tip:** Można również zamknąć `cryptboot` przy użyciu `cryptsetup close`, ale jego otwarcie ułatwia instalowanie aktualizacji systemu za pomocą Pacmana i regenerację initramfs za pomocą [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio"). Partycja `/boot` musi być zamontowana dla aktualizacji wpływających na [kernel](/index.php/Kernel "Kernel") lub [Initramfs](/index.php/Initramfs "Initramfs"), a initramfs będzie automatycznie generowany ponownie po tych aktualizacjach.

```
# cp /usr/lib/initcpio/install/encrypt /etc/initpcio/install/customencrypthook

```

Teraz edytuj skopiowany plik i usuń sekcję `help()`, ponieważ nie jest to konieczne.

 `/etc/mkinitcpio.conf (edit this only do not replace it, these are just excerpts of the necessary parts)` 
```
MODULES=(loop)
...
HOOKS=(base udev autodetect modconf block customencrypthook lvm2 filesystems keyboard fsck)
```

`files=()` i `binaries=()` są puste i nie powinieneś zastępować tablicy `HOOKS=(...)` całkowicie po prostu edytuj w `customencrypthook lvm2` po `block` i przed `filesystems` i upewnij się, że `systemd`, `sd-lvm2`, i `encrypt` są usunięte.

#### Boot Loader

Zakończ [Podręcznik instalacji](/index.php/Installation_guide#Initramfs "Installation guide") od kroku `mkinitcpio` Do rozruchu potrzebny jest [GRUB](/index.php/GRUB "GRUB") lub [efibootmgr](/index.php/Efibootmgr "Efibootmgr"). Uwaga: możesz użyć [GRUB](/index.php/GRUB "GRUB")-a do obsługi zaszyfrowanych dysków, [konfigurując program ładujący](/index.php/Dm-crypt/Encrypting_an_entire_system#Configuring_the_boot_loader_6 "Dm-crypt/Encrypting an entire system"), ale edycja `GRUB_CMDLINE_LINUX` nie jest konieczna dla tej konfiguracji.

Lub użyj bezpośredniego UEFI Secure boot, generując klucze za pomocą [cryptboot](https://aur.archlinux.org/packages/cryptboot/), a następnie podpisując initramfs i jądro i tworząc startowy plik .efi dla twojego katalogu `/boot/efi` z [sbupdate-git](https://aur.archlinux.org/packages/sbupdate-git/). Przed użyciem cryptboot lub sbupdate zanotuj ten fragment z [Secure Boot#Using your own keys](/index.php/Secure_Boot#Using_your_own_keys "Secure Boot"):

**Tip:** Zauważ, że [cryptboot](https://aur.archlinux.org/packages/cryptboot/) wymaga, aby zaszyfrowana partycja rozruchowa była określona w `/etc/crypttab`przed uruchomieniem, a jeśli używasz go w połączeniu z [sbupdate-git](https://aur.archlinux.org/packages/sbupdate-git/), sbupdate oczekuje, że pliki `/boot/efikeys/db.*` utworzone przez cryptboot będą pisane wielkimi literami jak `DB.*` chyba, że skonfigurowano inaczej w `/etc/default/sbupdate`. Użytkownicy, którzy nie używają systemd do obsługi szyfrowania, mogą nie mieć niczego w swoim pliku `/etc/crypttab` i musieliby utworzyć wpis.

```
# efibootmgr -c -d /dev/*device* -p *partition_number* -L "Arch Linux Signed" -l "EFI\Arch\linux-signed.efi"

```

Zobacz [efibootmgr(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/efibootmgr.8), aby uzyskać wyjaśnienie opcji.

Upewnij się, że porządek rozruchowy stawia `Arch Linux Signed` jako pierwszy. Jeśli nie, zmień go za pomocą `efibootmgr -o XXXX,YYYY,ZZZZ`.

### Zmiana pliku klucza LUKS

```
# cryptsetup --header /boot/header.img --key-file=/dev/mapper/lukskey --keyfile-offset=*offset* --keyfile-size=*size* luksChangeKey /dev/mapper/enc /dev/mapper/lukskey2 --new-keyfile-size=*newsize* --new-keyfile-offset=*newoffset*

```

Następnie `cryptsetup close lukskey` i [shred](/index.php/Securely_wipe_disk#shred "Securely wipe disk") lub [dd](/index.php/Securely_wipe_disk#dd "Securely wipe disk") stary plik klucza z losowymi danymi przed usunięciem, a następnie upewnij się, że nowy plik klucza ma zmienioną nazwę na starą: `key.img` lub inną nazwę.