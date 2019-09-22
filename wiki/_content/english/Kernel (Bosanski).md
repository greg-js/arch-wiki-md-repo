Related articles

*   [Kernel modules](/index.php/Kernel_modules "Kernel modules")
*   [Compile kernel module](/index.php/Compile_kernel_module "Compile kernel module")
*   [Kernel Panics](/index.php/Kernel_Panics "Kernel Panics")
*   [sysctl](/index.php/Sysctl "Sysctl")

Prema Wikipedia-i:

	[Linux kernel](https://en.wikipedia.org/wiki/Linux_kernel nalik na UNIX.

[Arch Linux](/index.php/Arch_Linux_(Bosanski) "Arch Linux (Bosanski)") je baziran na Linux kernelu. Postoje razni alternativni Linux kerneli za Arch Linux pored zadnjeg stabilnog kernela. Ovaj članak opisuje opcije dostupne u repository-ima. Također, tu je i opis patcheva koji se mogu primijeniti na kernel. Članak se završava se pregledom kompilacije custom kernela sa linkovima za razne metode.

Kernel paketi se [instaliraju](/index.php/Install "Install") na filesystem pod `/boot/`. Da se kernel može bootati, [boot loader (Bosanski)](/index.php/Boot_loader_(Bosanski) "Boot loader (Bosanski)") mora biti ispravno konfigurisan.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Oficijalno podržani kerneli](#Oficijalno_podržani_kerneli)
*   [2 Kompajliranje](#Kompajliranje)
*   [3 kernel.org kerneli](#kernel.org_kerneli)
*   [4 Patchevi i patchset-ovi](#Patchevi_i_patchset-ovi)
    *   [4.1 Major patchsetovi](#Major_patchsetovi)
    *   [4.2 Drugi patchsets](#Drugi_patchsets)
*   [5 Vidi i](#Vidi_i)

## Oficijalno podržani kerneli

*   **Stable** — Vanilla Linux kernel i moduli sa nekoliko patcheva primjenjenih.

	[https://www.kernel.org/](https://www.kernel.org/) || [linux](https://www.archlinux.org/packages/?name=linux)

*   **Hardened** — Linux kernel sa fokusom na sigurnost sa setom patcheva da se mitigiraju kernel i userspace exploiti. Također, omogućava više upstream kernel hardening feature-a nego [linux](https://www.archlinux.org/packages/?name=linux).

	[https://github.com/anthraxx/linux-hardened](https://github.com/anthraxx/linux-hardened) || [linux-hardened](https://www.archlinux.org/packages/?name=linux-hardened)

*   **Longterm** — Long-term support (LTS) (Podrška na dugo vrijeme) Linux kernel i moduli.

	[https://www.kernel.org/](https://www.kernel.org/) || [linux-lts](https://www.archlinux.org/packages/?name=linux-lts)

*   **Zen Kernel** — Rezultat kolaboracije kernel hakera da se pruži najbolji mogući Linux kernel za svakodnevnu upotrebu. Vidi više detalja na [https://liquorix.net](https://liquorix.net) (koji ima kernel binary-e bazirane na Zen-u za Debianw).

	[https://github.com/zen-kernel/zen-kernel](https://github.com/zen-kernel/zen-kernel) || [linux-zen](https://www.archlinux.org/packages/?name=linux-zen)

## Kompajliranje

Arch Linux pruža dvije metode kompajliranja kernela.

	[/Arch Build System](/index.php?title=Kernel_(Bosanski)/Arch_Build_System&action=edit&redlink=1 "Kernel (Bosanski)/Arch Build System (page does not exist)")

	Iskorištava prednosti visoko kvalitetnog [linux](https://www.archlinux.org/packages/?name=linux) [PKGBUILD](/index.php/PKGBUILD "PKGBUILD")-a i prednosti [paket menadžmenta](https://en.wikipedia.org/wiki/Package_management_system "wikipedia:Package management system").

	[/Traditional compilation](/index.php?title=Kernel_(Bosanski)/Traditional_compilation&action=edit&redlink=1 "Kernel (Bosanski)/Traditional compilation (page does not exist)")

	Uključuje manuelno download-ovanje source tarball-a, kompajliranje u home folderu kao običan korisnik.

## kernel.org kerneli

*   **Git** — Linux kernel i moduli buildani koristeći source iz Git repository-a Linus Torvaldsa

	[https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git) || [linux-git](https://aur.archlinux.org/packages/linux-git/)

*   **Mainline** — Kernel gdje su svi novi feature-i uvedeni, release-an svako 2-3 mjeseca.

	[https://www.kernel.org/](https://www.kernel.org/) || [linux-mainline](https://aur.archlinux.org/packages/linux-mainline/)

*   **Next** — Bleeding edge kerneli sa feature-ima koji čekaju da se merge-aju u sljedeći mainline kernel.

	[https://www.kernel.org/doc/man-pages/linux-next.html](https://www.kernel.org/doc/man-pages/linux-next.html) || [linux-next-git](https://aur.archlinux.org/packages/linux-next-git/)

*   **Longterm 3.16** — Long-term support (LTS) Linux 3.16 kernel i moduli.

	[https://www.kernel.org/](https://www.kernel.org/) || [linux-lts316](https://aur.archlinux.org/packages/linux-lts316/)

*   **Longterm 4.4** — Long-term support (LTS) Linux 4.4 kernel i moduli.

	[https://www.kernel.org/](https://www.kernel.org/) || [linux-lts44](https://aur.archlinux.org/packages/linux-lts44/)

*   **Longterm 4.9** — Long-term support (LTS) Linux 4.9 kernel i moduli.

	[https://www.kernel.org/](https://www.kernel.org/) || [linux-lts49](https://aur.archlinux.org/packages/linux-lts49/)

*   **Longterm 4.14** — Long-term support (LTS) Linux 4.14 kernel i moduli.

	[https://www.kernel.org/](https://www.kernel.org/) || [linux-lts414](https://aur.archlinux.org/packages/linux-lts414/)

## Patchevi i patchset-ovi

Postoji mnogo razloga za patchovanje kernela, glavni su performanse ili podrška za feature koji nisu u mainline, poput [reiser4](/index.php/Reiser4 "Reiser4") file system podrške. Drugi razlozi mogu biti čisto radi zabave i da se vidi kako se to radi i šta su prednosti toga.

Važno je napomenuti da je najbolji način da se ubrza sistem jeste da se prvo kernel prilagodi sistemu, posebno arhitekturi i tipu procesora. Iz ovog razloga, korištenje pre-packaged verzija custom kernela sa generičkom arhitekturom nije preporučeno ili vrijedno toga. Drugi benefit jeste taj što se može smanjiti veličina kernela (ujedno i build time) isključivanjem podrške za stvari koje nemate ili ih ne koristite. Npr, možete početi sa stock kernel config-om kada je nova verzija release-ana i ukloniti podršku za stvari poput bluetooth, video4linux, 1000Mbit ethernet, itd; funkcionalnosti za koje znate da nisu potrebne za vašu mašinu. Iako ova stranica nije za customiziranje kernel configa, preporučena je kao prvi korak prije korištenja patchsetova kada su savladane osnove.

Config fajlovi za Arch Linux mogu biti korišteni kao početna tačka. Oni su Arch paket source fajlovima, npr. [[1]](https://projects.archlinux.org/svntogit/packages.git/tree/trunk?h=packages/linux) linkovani iz [linux](https://www.archlinux.org/packages/?name=linux). Config fajl vašeg trenutnog kernela može biti dostupan u file systemu na `/proc/config.gz` ako je `CONFIG_IKCONFIG_PROC` kernel opcija uključena.

Ukoliko niste prije patchovali ili customizirali kernel ranije, nije teško i postoje razni PKGBUILD-ovi na forumu za individualne patchsetova. Preporučeno je da se počne ispočetka sa malo istraživanja o prednostima svakog patchseta umjesto da se samo naslijepo odabere patchset. Na ovaj način, naučit ćete više o tome šta radite umjesto da samo odaberete kernel na startup-u i onda se pitate šta u stvari radi.

**Warning:** Patchsetovi su razvijani od raznih vrsta ljudi. Neki od tih ljudih su uključeni u produkciju linux kernel i drugi iz hobija, koje može da se odrazi na nivo pouzdanosti i stabilnosti samog patchseta.

### Major patchsetovi

*   **[Linux-ck](/index.php/Linux-ck "Linux-ck")** — Sadrži patchove od strane Con Kolivasa dezijnirane da se poboljšava responsiveness sa naglaskom na desktop, ali odgovarajući za bilo koji workload.

	[http://ck.kolivas.org/](http://ck.kolivas.org/) || [linux-ck](https://aur.archlinux.org/packages/linux-ck/)

*   **pf-kernel** — Pruža razne super feature koji nisu merge-ani u mainline. Baziran nije na vec postojećem Linux forku niti patchset, iako neko neoficijalni portovi mogu biti korišteni ukoliko potrebni patchsetovi nisu release-ani oficijalno. Najistaknutiji patchovi iz linux-pf su PDS CPU scheduler i UKSM.

	[https://gitlab.com/post-factum/pf-kernel/wikis/README](https://gitlab.com/post-factum/pf-kernel/wikis/README) || Paketi:

*   [Repository](/index.php/Unofficial_user_repositories#post-factum_kernels "Unofficial user repositories") od pf-kernel developer, [post-factum](https://aur.archlinux.org/account/post-factum)
*   [Repository](/index.php/Unofficial_user_repositories#home-thaodan "Unofficial user repositories"), [linux-pf](https://aur.archlinux.org/packages/linux-pf/), [linux-pf-preset-default](https://aur.archlinux.org/packages/linux-pf-preset-default/), [linux-pf-lts](https://aur.archlinux.org/packages/linux-pf-lts/) od pf-kernel fork developer, [Thaodan](https://aur.archlinux.org/account/Thaodan)

*   **[Realtime kernel](/index.php/Realtime_kernel "Realtime kernel")** — Održavano od male grupe core developera, koje vodi Ingo Molnar. Ovaj patch omogućava skoro svakom kernelu da bude preempted(naći odgovarajući prevod), sa izuzetkom malih regiona koda ("raw_spinlock critical regions"). Ovo je urađeno sa zamjenjivanjem većine kernel spinlocka sa mutex-ima koji podržavaju nasljeđivanje prioriteta, kao i prebacivanje svih interrupt-a i software interrupt-a u kernel thread.

	[https://wiki.linuxfoundation.org/realtime/start](https://wiki.linuxfoundation.org/realtime/start) || [linux-rt](https://aur.archlinux.org/packages/linux-rt/), [linux-rt-lts](https://aur.archlinux.org/packages/linux-rt-lts/)

### Drugi patchsets

Neki od izlistanih paketa mogu biti dostupni kao binary paketi preko [Neoficijalnih korisničkih repository-a](/index.php/Unofficial_user_repositories "Unofficial user repositories").

*   **[AppArmor](/index.php/AppArmor "AppArmor")** — [Mandatory Access Control](https://en.wikipedia.org/wiki/Mandatory_access_control "wikipedia:Mandatory access control") (MAC) sistem, sprovedeno na [Linux Security Modules](https://en.wikipedia.org/wiki/Linux_Security_Modules "wikipedia:Linux Security Modules") (LSM). Dok [linux](https://www.archlinux.org/packages/?name=linux) podržava apparmor, ovaj kernel ima potrebne [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") uključne po defaultu.

	[https://gitlab.com/apparmor/apparmor/wikis/About](https://gitlab.com/apparmor/apparmor/wikis/About) || [linux-apparmor](https://aur.archlinux.org/packages/linux-apparmor/)

*   **Aufs** — aufs kompatibilni linux kernel i moduli, korisno kada se koristi [docker](/index.php/Docker "Docker").

	[http://aufs.sourceforge.net/](http://aufs.sourceforge.net/) || [linux-aufs](https://aur.archlinux.org/packages/linux-aufs/)

*   **Clear** — Patchevi iz Intelovog Clear Linux projekta. Pruža optimizacije za performanse i sigurnost. [WireGuard](/index.php/WireGuard "WireGuard") modul.

	[https://github.com/clearlinux-pkgs/linux](https://github.com/clearlinux-pkgs/linux) || [linux-clear](https://aur.archlinux.org/packages/linux-clear/)

*   **Libre** — Linux kernel bez "binary blobova".

	[https://www.fsfla.org/ikiwiki/selibre/linux-libre/](https://www.fsfla.org/ikiwiki/selibre/linux-libre/) || [linux-libre](https://aur.archlinux.org/packages/linux-libre/)

*   **Liquorix** — Kernel zamjena napravljena koristeći konfiguraciju ciljanu za Debian i Zen kernel source-ove. Dezijaniran za desktop, multimediju i gaming workloade, često je korišten kao Debian Linux zamjena za performanse. Danebtz, maintainer Liquorix patchseta je ujedno i developer za Zen patchset.

	[https://liquorix.net](https://liquorix.net) || [linux-lqx](https://aur.archlinux.org/packages/linux-lqx/)

*   **MultiPath TCP** — Linux Kernel i moduli sa Multipath TCP podrškom.

	[https://multipath-tcp.org/](https://multipath-tcp.org/) || [linux-mptcp](https://aur.archlinux.org/packages/linux-mptcp/)

*   **[Reiser4](/index.php/Reiser4 "Reiser4")** — Nasljednik file systema za ReiserFS, razvijen od početka od strane Namesysa i Hans Reisera.

	[https://sourceforge.net/projects/reiser4/files/](https://sourceforge.net/projects/reiser4/files/) ||

*   **VFIO** — Linux kernel i nekoliko patchec pisani od strane Alex Williamsona (acs override i i915) da se enable mogućnost za rad PCI Passthrough as KVM-om na nekim mašinama.

	[https://lwn.net/Articles/499240/](https://lwn.net/Articles/499240/) || [linux-vfio](https://aur.archlinux.org/packages/linux-vfio/), [linux-vfio-lts](https://aur.archlinux.org/packages/linux-vfio-lts/)

*   **XanMod** — Ciljano da se u potpunosti iskoristi prednost workstationa sa viskom performansama, gaming desktopima, media centrima i drugima je napravljena da pruži više čvrsto, responsive i smooth desktop iskustvo. Ovaj kernel koristi scheduler, BFQ I/O scheduler, UKSM realtime memory data deduplication, YeAH TCP kontrola zagušenja, x86_64 podršku za napredni set instrukcija i druge defaultne promjene.

	[https://xanmod.org/](https://xanmod.org/) || [linux-xanmod](https://aur.archlinux.org/packages/linux-xanmod/)

## Vidi i

*   [O'Reilly - Linux Kernel in a Nutshell](http://www.kroah.com/lkn/) (besplatna ebook)
*   [Koji stabilni kernel bih trebao koristiti?](http://kroah.com/log/blog/2018/08/24/what-stable-kernel-should-i-use/) od Greg Kroah-Hartman