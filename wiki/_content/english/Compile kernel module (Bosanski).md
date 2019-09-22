Related articles

*   [Kernel (Bosanski)](/index.php/Kernel_(Bosanski) "Kernel (Bosanski)")
*   [Kernel modules](/index.php/Kernel_modules "Kernel modules")

Nekad možda poželiš kompajlirati Linux [kernel modul](/index.php/Kernel_module "Kernel module") bez da rekompajliras cijeli kernel.

**Note:** Možeš zamijeniti postojeći modul samo ukoliko je kompajliran kao modul(M) i nije builtin (y) u kernel.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Build okruženje](#Build_okruženje)
*   [2 Source konfiguracija](#Source_konfiguracija)
*   [3 Kompajliranje module](#Kompajliranje_module)
*   [4 out-of-tree kompajliranje module](#out-of-tree_kompajliranje_module)
*   [5 Instaliranje module](#Instaliranje_module)
*   [6 mogući errori](#mogući_errori)
*   [7 Vidi i](#Vidi_i)

## Build okruženje

Prvo moraš instalirati potrebne build dependency-e poput kompajlera([base-devel](https://www.archlinux.org/groups/x86_64/base-devel/)) i [linux-headers](https://www.archlinux.org/packages/?name=linux-headers).

Sljedeće moraš preuzeti source code kernela kojeg koristiš. Možeš pokušati noviji kernel nego što koristiš ali su velike šanse da se module neće loadati.

Pronađi kernel verziju sa

```
$ uname -r

```

Onda preuzmi potrebne source codove, vidi [Kernels/Traditional compilation#Download the kernel source](/index.php/Kernels/Traditional_compilation#Download_the_kernel_source "Kernels/Traditional compilation"). Ukoliko skineš zadnji source koristeći [Git](/index.php/Git "Git"), potrebno je checkout potrebnu verziju koristeći tag (npr. v4.1).

## Source konfiguracija

Kada imaš source code, uđi u taj folder i clean ga sa (pobrisat će .config.old i promijeniti naziv .config u .config.old)

```
$ make mrproper

```

Zatim je potrebno kopirati .config trenutnog kernel u ovaj folder koristeći

```
$ cp /usr/lib/modules/$(uname -r)/build/.config ./
$ cp /usr/lib/modules/$(uname -r)/build/Module.symvers ./

```

Zatim, pobrini se da je konfiguracija podešena za kernel source-ove (ako koristiš kernel source za tačnu verziju, onda ne bi trebalo ništa da pita, ali noviji source-ovi nego trenutni kernel mogu pitati za nove opcije)

Također, ukoliko modul koji želiš da kompajliraš ima neke kompilacijske opcije poput debug build možeš ih podesiti sa bilo kojim alatom od make config/menuconfig/xconfig (vidi README)

```
$ make oldconfig

```

## Kompajliranje module

Da bi se modul učitao propisno, morate naći tačnu verziju EXTRAVERSION komponente trenutne verzije kernela da biste mogli matchati tačne verzije u kernel source-u. EXTRAVERSION je variabla koja je smještena na vrhu Makefile, ali Makefile u vanilla kernelu će EXTRAVERSION biti prazna; podešena je u dijelu Arch kernel build procesa. Vrijednost EXTRAVERSION trenutnog kernela (obično `-1`) može se naći na jedan od dva načina:

1.  Na vrhu `/usr/lib/modules/$(uname -r)/build/Makefile` fajla
2.  Ukucaj `uname -r` i pogledaj između trećeg broja verzije i `-ARCH` (Arch specifično podešenje LOCALVERSION podešeno u .config fajlu). Npr, sa kernel verzijom `4.9.65-1-ARCH`, EXTRAVERSION je `-1`.

Nakon što je EXTRAVERSION poznat, pripremimo source za kompajlirano modula:

```
$ make EXTRAVERSION=<TVOJA EXTRAVERSION OVDJE> modules_prepare

```

Primjer:

```
$ make EXTRAVERSION=-1 modules_prepare

```

Alternativno, ako sretni da učitate module sa modprobe koristeći `--force-vermagic` opciju da se ignoriše nepoklapanje u verziji kernela, možete jednostavno pokrenuti:

```
$make modules_prepare

```

**Note:** Iako Makefile na `/usr/lib/modules/$(uname -r)/build/Makefile` se može kopirati preko Makefile u kernel source da se izbjegne manuelna specifikacija EXTRAVERSION na cli, to može prouzrokovati da se dogodi nepoklapanje kernel verzije. Ako je kernel source dobijen koristeći version control alat, poput git-a, jednostavno kopiranje Makefile-a bi učinilo da working kopija bude dirty, koji će kernel build proces prepoznati, te će appendati `+` u LOCALVERSION konfiguracijsku varijablue. Npr. `4.9.65-1-ARCH+`.

Na kraju, kompajlirajte željeni module time što navedete njegov folder. (Možete pronaći lokaciju modula koristeći modinfo ili find)

```
$ make M=fs/btrfs

```

## out-of-tree kompajliranje module

preuzmi oficijalni source code trenutnog linux kernela kao što je opisano u [Kernel/Arch Build System](/index.php/Kernel/Arch_Build_System "Kernel/Arch Build System"):

```
$ cd && mkdir build
$ asp update linux
$ asp checkout linux

```

zatim usmjeri na checkirani source prilikom kompajliranja modula:

```
$ cd build/mymod
$ make -C ~/build/linux/trunk/src/archlinux-linux M=$PWD modules

```

## Instaliranje module

Sada, nakon uspješnog kompajliranja module samo morate gzip i kopirati u svoj trenutni kernel.

Ukoliko zamjenjujete neki već postojeći module, morate ga prepisati (zapamtite da reinstaliranje [linux](https://www.archlinux.org/packages/?name=linux) će ga zamijeniti sa defaultnim modulom)

```
$ xz fs/btrfs/btrfs.ko
# cp -f fs/btrfs/btrfs.ko.xz /usr/lib/modules/`uname -r`/kernel/fs/btrfs/

```

Alternativno, možete staviti update-ovani module u updates folder (kreirajte ga ukoliko ne postoji).

```
$ cp fs/btrfs/btrfs.ko.xz /usr/lib/modules/`uname -r`/updates

```

Ako dodajete novi modul, možete ga samo kopirati u extramodules (note, ovo je samo primjer jer se btrfs neće loadati odavde)

```
# cp fs/btrfs/btrfs.ko.xz /usr/lib/modules/`uname -r`/extramodules/

```

Ako kompajlirate module za rani boot (npr. updated modul) koji je kopirati u [Initramfs](/index.php/Initramfs "Initramfs") onda morate regenerisati sa njim (u suprotnom, module se neće loadati). Dalje, ukoliko koristite "updates" folder metodu, možda ćete morati rebuildati modul dependency tree sa "depmod" prije regenerisanja [Initramfs](/index.php/Initramfs "Initramfs").

```
# mkinitcpio -p linux

```

## mogući errori

Ako EXTRAVERSION nije ispravno podešena, sljedeći error se mogu pojaviti

```
# insmod mymod.ko
insmod: ERROR: could not insert module mymod.ko: Invalid module format
# modprobe mymod
modprobe: ERROR: could not insert 'mymod': Exec format error

```

dodavanje force-vermagic ignoriše mismatch verzije

```
modprobe mymod --force-vermagic

```

## Vidi i

*   [Linux Kernel Newbies](https://kernelnewbies.org/)
*   [The Linux Kernel Module Programming Guide](http://www.tldp.org/LDP/lkmpg/2.6/html/)