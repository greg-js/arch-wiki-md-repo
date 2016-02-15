**Tip:** To część wielostronicowego artykułu Przewodnik Początkującego. **[Kliknij tutaj](/index.php/Beginners%27_Guide_(Polski) "Beginners' Guide (Polski)")** jeśli wolisz czytać przewodnik w całości.

## Contents

*   [1 Przygotowanie](#Przygotowanie)
    *   [1.1 Ściągnij ostatni obraz instalacyjny](#.C5.9Aci.C4.85gnij_ostatni_obraz_instalacyjny)
        *   [1.1.1 Nagraj obraz ISO na CD/DVD lub pendrive](#Nagraj_obraz_ISO_na_CD.2FDVD_lub_pendrive)
        *   [1.1.2 Instalacja po sieci](#Instalacja_po_sieci)
        *   [1.1.3 Instalacja w maszynie wirtualnej](#Instalacja_w_maszynie_wirtualnej)
    *   [1.2 Uruchom instalator Arch Linuksa](#Uruchom_instalator_Arch_Linuksa)
        *   [1.2.1 Uruchamiane systemu w trybie UEFI](#Uruchamiane_systemu_w_trybie_UEFI)
        *   [1.2.2 Możliwe problemy z uruchomieniem instalacji](#Mo.C5.BCliwe_problemy_z_uruchomieniem_instalacji)

## Przygotowanie

**Note:** Jeśli chcesz przeprowadzić instalację z poziomu działającej dystrybucji GNU/Linux lub LiveCD, zobacz [ten artykuł](/index.php?title=Install_from_Existing_Linux_(Polski)&action=edit&redlink=1 "Install from Existing Linux (Polski) (page does not exist)") po instrukcje, jak to zrobić. Może to być przydatne przy instalacji Archa zdalnie przez [VNC](/index.php?title=VNC_(Polski)&action=edit&redlink=1 "VNC (Polski) (page does not exist)") lub [SSH](/index.php?title=SSH_(Polski)&action=edit&redlink=1 "SSH (Polski) (page does not exist)"). Ten artykuł dotyczy tradycyjnej instalacji.

### Ściągnij ostatni obraz instalacyjny

Oficjalne obrazy instalacyjne Archa możesz znaleźć [tutaj](https://archlinux.org/download/). W czasie pisania tego artykułu, ostatnią wersją jest 2013.02.01 i do niej odnosi się ten poradnik. Obrazy testowe również są dostępne i mogą zostać ściagnięte [stąd](https://releng.archlinux.org/isos/) (nie są to oficjalne wydania i nie są oficjalnie wspierane). Zauważ, że każdy obraz wspiera architekturę zarówno 32 jak i 64 bitową.

#### Nagraj obraz ISO na CD/DVD lub pendrive

*   Nagraj obraz .iso na CD lub DVD używając wybranego oprogramowania.

**Note:** Jakość napędów optycznych i samych płyt może być bardzo różna. Generalnie, polecane jest nagrywanie z niską prędkością. Niektórzy użytkownicy polecają prędkości _**tak niskie jak 4x lub 2x.**_ Jeśli doświadczasz nieprzewidzianych zachowań w trakcie instalacji, spróbuj nagrać obraz z najniższą możliwą prędkością.

*   Możesz także nagrać obraz .iso na pendrive. Dokładne instrukcje znajdziesz na stronie [USB Installation Media_(Polski)](/index.php?title=USB_Installation_Media_(Polski)&action=edit&redlink=1 "USB Installation Media (Polski) (page does not exist)").

**Note:** Jeśli posiadasz płytę główną z [UEFI](/index.php/UEFI "UEFI"), zobacz [to](/index.php/UEFI#Create_UEFI_bootable_USB_from_ISO "UEFI"), a także [to](/index.php/USB_Installation_Media#Without_overwriting_the_USB_drive "USB Installation Media").

#### Instalacja po sieci

Zamiast nagrywać obraz na płytę lub pendrive, możesz uruchomić go korzystając z sieci. Jest to dobry sposób, jeśli posiadasz już skonfigurowany serwer. Zobacz [ten artykuł](/index.php?title=Install_Arch_from_network_(via_PXE)_(Polski)&action=edit&redlink=1 "Install Arch from network (via PXE) (Polski) (page does not exist)"), potem postępuj według [Uruchom instalator Arch Linuksa](#Uruchom_instalator_Arch_Linuksa).

#### Instalacja w maszynie wirtualnej

Instalacja w [maszynie wirtualnej](https://en.wikipedia.org/wiki/Virtual_machine "wikipedia:Virtual machine") to dobry sposób na zaznajomienie się z Arch Linuksem i jego instalacją bez usuwania obecnego systemu operacyjnego i partycjonowania dysku. Pozwala także na pozostawienie Beginner's Guide otwartego w przeglądarce podczas instalacji. Część użytkowników może uważać za przydatne, posiadanie niezależnego systemu Arch Linux w maszynie wirtualnej do celów testowych.

Przykładowe programy do wirtualizacji to [VirtualBox](/index.php?title=VirtualBox_(Polski)&action=edit&redlink=1 "VirtualBox (Polski) (page does not exist)"), [VMware](/index.php?title=VMware_(Polski)&action=edit&redlink=1 "VMware (Polski) (page does not exist)"), [QEMU](/index.php?title=QEMU_(Polski)&action=edit&redlink=1 "QEMU (Polski) (page does not exist)"), [Xen](/index.php?title=Xen_(Polski)&action=edit&redlink=1 "Xen (Polski) (page does not exist)"), [Varch](/index.php?title=Varch_(Polski)&action=edit&redlink=1 "Varch (Polski) (page does not exist)"), [Parallels](/index.php?title=Parallels_(Polski)&action=edit&redlink=1 "Parallels (Polski) (page does not exist)").

Dokładny proces przygotowania maszyny wirtualnej zależy od programu, jednak generalnie następujące kroki powinny być wykonane:

1.  Stwórz obraz dysku, który będzie przechowywał system.
2.  Poprawnie skonfiguruj maszynę wirtualną.
3.  Uruchom ściągnięty obraz .iso korzystając z wirtualnego napędu CD.
4.  Postępuj według [Uruchom instalator Arch Linuksa](#Uruchom_instalator_Arch_Linuksa).

Następujące artykuły mogą być pomocne:

*   [Arch Linux VirtualBox Guest](/index.php/Arch_Linux_VirtualBox_Guest "Arch Linux VirtualBox Guest")
*   [Installing Arch Linux from VirtualBox](/index.php/Installing_Arch_Linux_from_VirtualBox "Installing Arch Linux from VirtualBox")
*   [VirtualBox Arch Linux Guest On Physical Drive](/index.php/VirtualBox_Arch_Linux_Guest_On_Physical_Drive "VirtualBox Arch Linux Guest On Physical Drive")
*   [Installing Arch Linux in VMware](/index.php/Installing_Arch_Linux_in_VMware "Installing Arch Linux in VMware")

### Uruchom instalator Arch Linuksa

Po pierwsze, możliwe, że będziesz musiał(a) zmienić kolejność uruchamiania w BIOSie komputera. Aby to zrobić, musisz nacisnąć przycisk (zwykle `Delete`, `F1`, `F2`, `F11` lub `F12`) podczas fazy POST (Power On Self-Test) uruchamiania. Następnie, wybierz "Boot Arch Linux" z menu i naciśnij `Enter` by rozpocząć instalację.

**Note:** Podstawowa instalacja wymaga 64 MB pamięci RAM.

**Note:** Użytkownicy chcący przeprowadzić instalację Arch Linuksa zdalnie poprzez połączenie [SSH](/index.php?title=SSH_(Polski)&action=edit&redlink=1 "SSH (Polski) (page does not exist)") powinni umożliwić połączenie bezpośrednio ze środowiskiem live CD. Więcej informacji znajdziesz w artykule [Instalacja przez SSH](/index.php?title=Install_from_SSH_(Polski)&action=edit&redlink=1 "Install from SSH (Polski) (page does not exist)").

Po uruchomieniu środowiska live z wybranego medium dostępną powłoką jest [Zsh](/index.php?title=Zsh_(Polski)&action=edit&redlink=1 "Zsh (Polski) (page does not exist)"); pozwala to na zaawansowane autouzupełnianie z wykorzystaniem klawisza `Tab`, jak również na dostęp do innych funkci będących częścią [grml config](http://grml.org/zsh/).

##### Uruchamiane systemu w trybie UEFI

Jeżeli posiadasz płytę główną z [UEFI](/index.php/UEFI "UEFI"), a tryb UEFI jest włączony (i używany zamiast BIOS), z CD/USB automatycznie uruchomi się jądro Arch Linux (EFISTUB via Gummiboot Boot Manager). By sprawdzić, czy wykonujesz uruchomienie z trybem UEFI, wczytaj moduł `efivars` do jądra (przed wykonaniem chroot) i sprawdź, czy pojawiły się pliki w `/sys/firmware/efi/vars/`:

```
# modprobe efivars       # przed wykonaniem chroot
# ls -1 /sys/firmware/efi/vars/

```

**Note:** Moduł jądra `efivars` wykrywa i tworzy UEFI Runtime Variables w `/sys/firmware/efi/vars`. Ten moduł **nie jest** ładowany automatycznie podczas procesu uruchamiania, a dopóki moduł jest wczytany, a system uruchomiony z wykorzystaniem UEFI **bez** parametru `noefi`, żaden plik nie istnieje w `/sys/firmware/efi/vars`. Te pliki są później używane i modyfikowane przez `efibootmgr`, by dodać wpisy bootloadera do boot menu UEFI. W trybie BIOS, modprobe nie zwróci żadnego błędu dotyczącego modułu efivars. Prawidłowym sposobem na wykrycie uruchomienia w trybie UEFI jest sprawdzenie, czy zostały utworzone pliki w `/sys/firmware/efi/vars` .

##### Możliwe problemy z uruchomieniem instalacji

*   Jeśli posiadasz chipset graficzny Intela, a obraz staje się pusty podczas uruchamiania, problemem jest prawdopodobnie Kernel Mode Setting ([KMS](/index.php?title=KMS_(Polski)&action=edit&redlink=1 "KMS (Polski) (page does not exist)")). Możliwym obejściem jest ponowne uruchomienie i naciśnięcie `Tab` nad pozycją, którą chcesz uruchomić (i686 lub x86_64). Na końcu linijki dopisz `nomodeset` i naciśnij `Enter`. Alternatywnie, dopisz `video=SVIDEO-1:d`, jednak ten parametr (jeśli zadziała), nie wyłączy Kernel Mode Setting. Zobacz artykuł [Intel](/index.php/Intel_(Polski) "Intel (Polski)") po więcej informacji.

*   Jeśli obraz _nie_ staje się pusty, a uruchamianie zatrzymuje się podczas próby ładowania jądra, naciśnij `Tab` nad odpowiednią pozycją menu, dopisz `acpi=off` na końcu linijki i naciśnij `Enter`.