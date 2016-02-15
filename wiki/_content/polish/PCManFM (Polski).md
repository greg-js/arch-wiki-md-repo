## Contents

*   [1 Wstęp](#Wst.C4.99p)
*   [2 Instalacja](#Instalacja)
*   [3 Zarządzanie dyskami](#Zarz.C4.85dzanie_dyskami)
    *   [3.1 Montowanie z udisks](#Montowanie_z_udisks)
    *   [3.2 Montowanie z gvfs](#Montowanie_z_gvfs)
    *   [3.3 Montowanie jako normalny użytkownik](#Montowanie_jako_normalny_u.C5.BCytkownik)
*   [4 Wsparcie NTFS](#Wsparcie_NTFS)
*   [5 Informacje końcowe](#Informacje_ko.C5.84cowe)
*   [6 Zobacz również](#Zobacz_r.C3.B3wnie.C5.BC)

## Wstęp

PCManFM to menedżer plików, który w zamyśle ma być zastępstwem takich menedżerów jak Nautilus z GNOME czy Konqueror z KDE. Wydany jest na licencji GNU General Public License, PCManFM jest wolnym oprogramowaniem.

## Instalacja

```
# pacman -Sy pcmanfm

```

Wymagany jest demon FAM:

```
# pacman -S fam

```

Następnie edytujemy `/etc/rc.conf` i dodajemy go do DAEMONS:

 `/etc/rc.conf`  `DAEMONS=(... fam ...)` 

Istenieje możliwość zainstalowania pakietu `gamin`, który nie wymaga wpisu do pliku `/etc/rc.conf`:

```
# pacman -S gamin

```

## Zarządzanie dyskami

PCManFM umożliwa montowanie i odmontowywanie urządzeń, zarówno manualnie jak i automatycznie. To udogodnienie jest oferowane jako alternatywa dla konsolowych narzędzi takich jak [pmount](https://aur.archlinux.org/packages/pmount/). Istnieje kilka wersji PCManFM, możliwe jest także wybranie różnych sposobów zarządzania dyskami.

**Note:** Musisz posiadać folder `/media`.

### Montowanie z udisks

Obecne wydanie PCManFM umożliwia montowanie poprzez udisks. Jeżeli chcesz z tego korzystać, upewnij się czy daemon D-Bus jest zainstalowany i uruchomiony.

### Montowanie z gvfs

Jeżeli przeferujesz Gnome Virtual FileSystem, procedura jest taka sama, ale wymagane są dodatkowe pakiety:

*   [gvfs](/index.php/Gvfs "Gvfs") (i zależonści);
*   (opcjonalnie) gvfs-smb, gvfs-obexftp, gvfs-afc, itp. w celu uzyskania dodatkowych możliwości.

### Montowanie jako normalny użytkownik

Aby umożliwić montowanie urządzeń takich jak dyski USB, pendrive'y czy dyski DVD jako normalny użytkownik wymagany jest poprawnie skonfigurowany zestaw [PolicyKit](/index.php/PolicyKit "PolicyKit"). Pliki konfiguracyjne można znaleźć w podfolderach `/etc/polkit-1`. Dalej pokazane jest jak skonfigurować PolicyKit aby zezwolić użytkownikom z grupy "storage" montowanie urządzeń wymiennych.

**Note:** Obecnie PolicyKit skonfigurowany jest aby domyślnie zezwalać użytkownikom z grupy _storage_ na (od)montowanie. Dlatego ten krok nie jest niezbędny.

Jako root utwórz plik `/etc/polkit-1/localauthority/50-local.d/55-myconf.pkla` (lub inny kończący się .pkla) zawierający:

```
 [Storage Permissions]
 Identity=unix-group:storage
 Action=org.freedesktop.udisks.filesystem-mount;org.freedesktop.udisks.drive-eject;org.freedesktop.udisks.drive-detach;org.freedesktop.udisks.luks-unlock;org.freedesktop.udisks.inhibit-polling;org.freedesktop.udisks.drive-set-spindown
 ResultAny=yes
 ResultActive=yes
 ResultInactive=no

```

PolicyKit zauważy zmiany i wprowadzi je bez potrzeby żadnej akcji z twojej strony. Następnie należy każdego użytkownika któremu umożliwamy montowanie dodać do grupy _storage_:

```
# usermod -a -G storage 'nazwa użytkownika'

```

## Wsparcie NTFS

Należy zainstalować pakiet `ntfs-3g` (Zobacz [NTFS-3G](/index.php/NTFS-3G "NTFS-3G")):

```
# pacman -S ntfs-3g

```

## Informacje końcowe

Aby dowiedzieć się więcej o tym menedżerze, przejdź do angielskojęzycznego artykułu [PCManFM](/index.php/PCManFM "PCManFM").

## Zobacz również

*   [Strona projektu](http://pcmanfm.sourceforge.net/)