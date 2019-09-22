Related articles

*   [Boot debugging](/index.php/Boot_debugging "Boot debugging")
*   [Kernels](/index.php/Kernels "Kernels")
*   [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters")
*   [Compile kernel module (Bosanski)](/index.php/Compile_kernel_module_(Bosanski) "Compile kernel module (Bosanski)")

[Kernel moduli](https://en.wikipedia.org/wiki/Loadable_kernel_module "wikipedia:Loadable kernel module") su dio koda koji može se loadati i unloadati iz kernela na zahtjev. Oni produžuju funkcionalnost kernela bez rebootanja sistema.

Da kreirate kernel module, možete pročitati [The Linux Kernel Module Programming Guide](http://tldp.org/LDP/lkmpg/2.6/html/index.html). Module može biti konfigurisan kao built-in ili loadable. Da dinamično učitate ili uklonite modul, mora biti konfigurisan kao loadable modul u kernel konfiguraciji (linija povezana sa modulom će pokazati slovo `M`).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Dohvaćanja informacija](#Dohvaćanja_informacija)
*   [2 Automatsko loadanje module sa systemd](#Automatsko_loadanje_module_sa_systemd)
*   [3 Manuelno održavanje modula](#Manuelno_održavanje_modula)
*   [4 Podešavanje opcija modula](#Podešavanje_opcija_modula)
    *   [4.1 Manauelno prilikom loadanja sa modprobe](#Manauelno_prilikom_loadanja_sa_modprobe)
    *   [4.2 Koristeći fajlove u /etc/modprobe.d/](#Koristeći_fajlove_u_/etc/modprobe.d/)
    *   [4.3 Koristeći kernel command line](#Koristeći_kernel_command_line)
*   [5 Podešavanja aliasa](#Podešavanja_aliasa)
*   [6 Blacklistanje](#Blacklistanje)
    *   [6.1 Korištenje fajlova u /etc/modprobe.d/](#Korištenje_fajlova_u_/etc/modprobe.d/)
    *   [6.2 Korištenje kernel command line](#Korištenje_kernel_command_line)
*   [7 Troubleshooting](#Troubleshooting)
    *   [7.1 Moduli se ne loadaju](#Moduli_se_ne_loadaju)
*   [8 Vidi i](#Vidi_i)

## Dohvaćanja informacija

Moduli su smješteni u `/usr/lib/modules/*kernel_release*`. Možete koristiti `uname -r` da vidite svoju trenutnu kernel verziju.

**Note:** Imena modula često imaju `_` ili `-`; ovi simboli se mogu smjenjivati kada se koristi `modprobe` komanda i u konfiguracijskom fajlu u `/etc/modprobe.d/`.

Da vidite trenutno loadane module u kernel:

```
$ lsmod

```

Da vidite informacije u modulu:

```
$ modinfo *module_name*

```

Da vidite listu opcija za modul:

```
$ systool -v -m *module_name*

```

Da izlistate veliku konfiguraciju svih modula:

```
$ modprobe -c | less

```

Da prikažete konfiguraciju određenog modula::

```
$ modprobe -c | grep *module_name*

```

Izlistajte dependency-e modula (ili aliasa), uključujući i sami modul:

```
$ modprobe --show-depends *module_name*

```

## Automatsko loadanje module sa systemd

Danas, svo potrebno loadanje module automatski radi [udev](/index.php/Udev "Udev"), tako da ukoliko ne koristite out-of-tree kernel modul, nema potrebe da stavljate module koji će se bootati u bootu u konfiguracijski fajl. Ipak, postoje slučajevu gdje možda želite loadati dodatni modul tokom boot procesa ili blacklistati drugi za ispravno funkcionisanje računara.

Kernel moduli se mogu eksplicitino izlistati u fajlovima pod `/etc/modules-load.d/` za systemd da ih loada tokom boot-a. Svaki konfiguracijski fajl ja imenovan kao `/etc/modules-load.d/<program>.conf`. Konfiguracijski fajlovi jednostavno sadrže listu kernel modula koji će se loadati, odvojeni novom linijom. Prazne linije i linije čiji prvo non-whitespace karakter je `#` ili `;` su ignorisane.

 `/etc/modules-load.d/virtio-net.conf` 
```
# Load virtio_net.ko tokom boota
virtio_net
```

Vidi [modules-load.d(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/modules-load.d.5) za više detalja.

## Manuelno održavanje modula

Upravljanje kernel modulima vrši se sa alatima iz [kmod](https://www.archlinux.org/packages/?name=kmod) paketa. Možete manuelno koristiti ove alate.

**Note:** Ake ste upgrade kernel, ali niste još uvijek rebootali sistem, *modprobe* će failati bez error poruke i sa exit kodom 1 jer putanja `/usr/lib/modules/$(uname -r)` više ne psotoji. Provjerite manuelno da li putanja postoji kada *modprobe* faila da vidite da li je to slučaj.

Da loadate module:

```
# modprobe *ime_modula*

```

Da loadate modul na osnovu imena (oni koji nisu instalirani u `/usr/lib/modules/$(uname -r)/`):

```
# insmod naziv_fajla [argumenti]

```

Da unloadate modul:

```
# modprobe -r *module_name*

```

Ili:

```
# rmmod *module_name*

```

## Podešavanje opcija modula

Da proslijedite parametar kernel modulu, možete ih proslijediti manuelno sa modprobe ili osigurati da određeni parametri su uvijek primijenjeni korištenjem modprobe konfiguracijskog fajla ili koristeći kernel command line.

### Manauelno prilikom loadanja sa modprobe

Osnovni način prosljeđivanja parametara modulu je korištenjem modprobe komadne. Parametri su navedeni na command line koristeći jednostavne `*ključ=vrijednost*` dodjele:

```
# modprobe *ime_module ime_parametra=vrijednost_parametra*

```

### Koristeći fajlove u /etc/modprobe.d/

Fajlovi u `/etc/modprobe.d/` folderu mogu biti korišteni da se postave podešavanja za modul za [udev](/index.php/Udev "Udev"), koji će koristiti `modprobe` da upravlja loadanjem module tokom bootanja. Konfiguracijski fajlovi u ovom folderu mogu imati bilo kakvo ime, ali moraju završavati sa `.conf` ekstenzijom. Sintaksa je:

 `/etc/modprobe.d/myfilename.conf`  `options *module_name parameter_name=parameter_value*` 

Npr:

 `/etc/modprobe.d/thinkfan.conf` 
```
# Na ThinkPadima, ovo omogućava 'thinkfan' daemon da kontroliše brzinu ventilatora
options thinkpad_acpi fan_control=1
```

**Note:** Ukoliko je bilo koji od zahvaćenih modula učitan iz initramfs-a, onda se mora dodati odgovarajući {{ic}.conf}} u `FILES` u [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf") ili koristiti `modconf` [hook](/index.php/Mkinitcpio.conf#HOOKS "Mkinitcpio.conf") tako da bude uključen u initramfs. Da vidite sadržaj initramfs-a, koristite `lsinitcpio /boot/initramfs-linux.img`.

### Koristeći kernel command line

Ukoliko je modul buildan u kernel, možete proslijediti opcije modulu koristeći kernel comamnd line. Za sve česte bootloadere, sljedeća sintaksa je tačna:

```
*ime_modula.ime_parametra=vrijednost_parametra*

```

Npr:

```
thinkpad_acpi.fan_control=1

```

Jednostavno dodate ovo u bootloader kernel liniju, ako što je opisano u [Kernel parametrima](/index.php/Kernel_parameters "Kernel parameters").

## Podešavanja aliasa

Aliasi su alternativna imena za module. Npr: `alias my-mod dugi_naziv_modula` znači da možete koristiti `modprobe my-mod` umjesto `modprobe dugi_naziv_modula`. Možete također koristiti shell-like wildcarde, tako da `alias my-mod* dugi_naziv_modula` znači da `modprobe my-mod-something` ima isti efekat. Kreiranje aliasa:

 `/etc/modprobe.d/mojalias.conf`  `alias mymod dugi_naziv_modula` 

Neki moduli imaju aliase koji su korišteni automatski da se loadaju kada ih aplikacija treba. Isključivanje ovih aliasa može spriječiti automatsko loadanje, ali će i dalje dozvoljati manuelno loadanje modula.

 `/etc/modprobe.d/modprobe.conf` 
```
# Spriječi Bluetooth autoload
alias net-pf-31 off
```

## Blacklistanje

Blacklistanje, u kontekstu kernel modula, je mehanizam spriječavanja kernel modula da se automatski loadaju. Ovo može biti korisno ako npr. asocirani hardware nije potreban ili ako loadanje tog modula izaziva probleme: npr mogu biti dva kernel modula koja pokušavaju da kontrolišu isti dio hardware-a i loadanje oba može prouzrokovati konflikt.

Neki module su loadani kao dio [initramfs](/index.php/Initramfs "Initramfs")-a. `mkinitcpio -M` će ispisati sve automatski detektovane module: da spriječite initramfs da ne loada automatski neke od tih, blacklistajte ih u *.conf* fajlu unutar `/etc/modprobe.d` i bit će dodano tokom `modconf` hookanja tokom generisanja image-a. Pokretanjem `mkinitcpio -v` će izlistati sve pullane module za različitim hookovima (npr. `filesystems` hook, `block` hook itd.). Zapamtite da dodate *.conf* fajl u `FILES` niz u `/etc/mkinitcpio.conf` ako nemate `modconf` hook u vašem `HOOKS` nizu (npr. odudarate od defaultne konfiguracije), i nakon što ste blacklistali module, [regenerišite initramfs](/index.php?title=Regenereate_the_initramfs&action=edit&redlink=1 "Regenereate the initramfs (page does not exist)") i rebootajte iza toga.

### Korištenje fajlova u /etc/modprobe.d/

Kreirajte `.conf` fajl unutar `/etc/modprobe.d/` i dodajte liniju za svaki modul koji želite blacklistati koristeći `blacklist` ključnu riječ. Ako npr. želite spriječiti `pcspkr` module da se loada:

 `/etc/modprobe.d/nobeep.conf` 
```
# Ne loadaj 'pcspkr' modul tokom boota.
blacklist pcspkr
```

**Note:** `blacklist` komanda će blacklistati modul da se automatski loada, ali modul se može loadati od strane drugog neblacklistanog module ako taj module osivi o tom modul ili ako se loada automatski.

Ipak, postoji workaround za ovo ponašanja; `install` komanda govori modprobe da pokrene custom komandu umjesto loadanja modula u kernel uobičajeno, tako da možete forsirati da modul uvijek faila sa:

 `/etc/modprobe.d/blacklist.conf` 
```
...
install *ime_modula* /bin/true
...
```
Ovo će efikasno blacklistati taj modul i bilo koji drugi koji ovisi o njemu.

### Korištenje kernel command line

**Tip:** Ovo može biti korisno ukoliko broken modul onemogućava bootanje sistema.

Mozete također blacklistati module iz bootloadera.

Jednostavno dodajte `module_blacklist=modname1,modname2,modname3` u kernel line bootloadera, kao što je opisano u [Kernel parametrima](/index.php/Kernel_parameters "Kernel parameters").

**Note:** Kada blacklistati više od jednog modula, uzmite u obzir da se razdvajaju zarezom. Razmak ili bilo koji drugi sistem može breakati sintaksu.

## Troubleshooting

### Moduli se ne loadaju

U slučaju kada se određeni moduli ne loada i boot log (dostupan sa `journalctl -b`) kaže da je modul blacklista, ali ne postoji entry unutar `/etc/modprobe.d`, provjerite drugi modprobe source folder na `/usr/lib/modprobe.d` za blacklistane module.

Modul se neće loadati ukoliko "vermagic" string unutar kernel modula se ne poklapa sa vrijednošću trenutnog kernela na vašem sistemu. Ukoliko je poznato da je modul kompatibilan sa trenutnim kernel, "vermagic" provjera se može ignorisati sa `modprobe --force-vermagic`.

**Warning:** Ignorisanje provjere verzije za kernel modul može prouzrokovati da se kernel crasha ili da sistem ima nedefinisano ponašanje zbog nekompatibilnosti. Koristite `--force-vermagic` sa maksimalnom dozom opreza.

## Vidi i

*   [Disable PC speaker beep](/index.php/Disable_PC_speaker_beep "Disable PC speaker beep")
*   [Pisanje WMI drivera](https://lwn.net/Articles/391230/)