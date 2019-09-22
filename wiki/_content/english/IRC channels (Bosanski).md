Related articles

*   [ArchWiki:IRC](/index.php/ArchWiki:IRC "ArchWiki:IRC")
*   [International communities (Bosanski)](/index.php/International_communities_(Bosanski) "International communities (Bosanski)")
*   [phrik](/index.php/Phrik "Phrik")

**Note:** Ne uređuj ovu stranicu ako nisi channel op u #archlinux. Dobrodošao si da učestvujes na stranici diskusije.

Da koristis [Internet Relay Char](https://en.wikipedia.org/wiki/Internet_Relay_Chat uključuje [Irssi](/index.php/Irssi "Irssi") klijenta.

Očekuje se da se upoznaš sa [Kodeksom ponašanja](/index.php?title=Code_of_conduct_(Bosanski)&action=edit&redlink=1 "Code of conduct (Bosanski) (page does not exist)") i [Kodeks ponasanja#IRC](/index.php?title=Code_of_conduct_(Bosanski)&action=edit&redlink=1 "Code of conduct (Bosanski) (page does not exist)") prije pristupanja bilo kojem od oficijalnih kanala. Za listu često korištenih skraćenica, vidi [Arch terminologija](/index.php/Arch_terminology "Arch terminology") i [IRC Žargon](http://www.ircbeginner.com/ircinfo/abbreviations.html).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Glavni kanali](#Glavni_kanali)
    *   [1.1 Registracija](#Registracija)
    *   [1.2 Operatori kanala](#Operatori_kanala)
*   [2 Drugi kanali](#Drugi_kanali)
*   [3 Internacionalni kanali](#Internacionalni_kanali)
    *   [3.1 International IRC channels](#International_IRC_channels)

## Glavni kanali

**Note:**

*   Zbog zloupotrebe gatewayi i web klijenti mogu biti banovani. Ako primjetiš problem koristi "*proper*" IRC klijent ili pitaj jednog od operatora za ban izuzetak (`+e`).
*   Statistika kanala je logovana za [#archlinux-offtopic](https://alyp.tk/stats/aotstats.html). Pričaj sa *jp/alyptik* ukoliko ne želiš da učestvuješ.

Ova sekcija je o [#archlinux](ircs://chat.freenode.net/archlinux), glavnom Arch Linux [IRC](https://en.wikipedia.org/wiki/Internet_Relay_Chat "wikipedia:Internet Relay Chat") kanalu za podršku i [#archlinux-offtopic](ircs://chat.freenode.net/archlinux-offtopic), glavni Arch Linux socijalni kanal, oba dostupni na [Freenode](https://freenode.net/) network.

Centralna tema za **#archlinux** je podrška i generalna diskusija o Arch Linuxu.

### Registracija

Da se smanji spam **#archlinux** i **#archlinux-offtopic** imaju mod kanala postavljen na `+r` i `+q $-a`. Ovo znači da moraš biti identificiras od strane `NickServ` da možeš da pristupiš ovim kanalima i da šalješ poruke. Ako nisi registrovan i identificiras, bit ćeš forwardovan u **#archlinux-unregistered**.

Da se registruješ, prati [freenode FAQ](https://freenode.net/kb/answer/registration) kao i `NickServ help` nakon konekcija na *chat.freenode.net*.

```
/query NickServ HELP REGISTER
/query NickServ HELP IDENTIFY

```

**Note:**

*   Ako `/query` ne radi u tvom IRC klijentu, možeš pokušati `/quote NickServ <command>` ili `/msg NickServ <command>`.
*   Neki IRC klijenti imaju race-condition gdje pokušavaju da se automatski povežu na kanale prije prethodne identifikacije i da se riješi ovo, moraš enable SASL. Ili pogledaj dokumentaciju svog IRC klijenta ili pogledaj na freenode [https://freenode.net/kb/answer/sasl](https://freenode.net/kb/answer/sasl) SASL page da nađeš instrukcija kako da enablaš.
*   Možeš dobiti listu ljudi koji ti mogu pomoći kucanjem `/msg ChanServ ACCESS #archlinux LIST` ili postavi pitanje u **#freenode**.

### Operatori kanala

Arch operatori su operatori i u **#archlinux** i **#archlinux-offtopic**. Vidi listu ispod ili pokreni `/msg phrik listops` na freenode-u.

Ako iz nekog razloga trebaš pomoć operator, ne budi stidljiv da `/query` ili `/msg` nas. Ovdje je lista operatora 1.11.2018\. godine:

*   alad
*   amcrae
*   falconindy
*   gehidore / man
*   grawity
*   heftig
*   jelle
*   MrElendig / Mion
*   Namarrgon
*   pid1
*   tigrmesh / tigr
*   vodik
*   wonder / ioni

## Drugi kanali

Veličina community-a je dovela do kreiranja više IRC kanala. Da dobiješ listu svih kanala na **[chat.freenode.net](ircs://chat.freenode.net)** koji sadrže `archlinux` u svom imenu, koristi komandu `/query alis list *archlinux*`.

| Kanal | Opis |
| [#archlinux64](ircs://chat.freenode.net/archlinux64) | kanal za diskusiju o x86_64, uglavnom na engleskom |
| [#archlinux-aur](ircs://chat.freenode.net/archlinux-aur) | [AUR](/index.php/AUR "AUR") generalna diskusija |
| [#archlinux-aurweb](ircs://chat.freenode.net/archlinux-aurweb) | [aurweb](https://projects.archlinux.org/aurweb.git/) development diskusija |
| [#archlinux-bugs](ircs://chat.freenode.net/archlinux-bugs) | Diskusija o bugovima |
| [#archlinux-classroom](ircs://chat.freenode.net/archlinux-classroom) | Projekat koji razvija i hosta klase za Arch Linux community |
| [#archlinux-devops](ircs://chat.freenode.net/archlinux-devops) | Arch Linux interna infrastruktura i devops diskusije. |
| [#archlinux-multilib](ircs://chat.freenode.net/archlinux-multilib) | Arch Linux Multilib Project diskusija i packaging |
| [#archlinux-newbie](ircs://chat.freenode.net/archlinux-newbie) | Mjesto za naučiti, probati nove stvari i pitati za pomoć bez straha od ismijavanja. |
| [#archlinux-pacman](ircs://chat.freenode.net/archlinux-pacman) | [Pacman](/index.php/Pacman "Pacman") development i diskusija |
| [#archlinux-projects](ircs://chat.freenode.net/archlinux-projects) | Development i diskusija o projektima (mkinitcpio, abs, dbscripts, devtools, ...) |
| [#archlinux-reproducible](ircs://chat.freenode.net/archlinux-reproducible) | Kanal za diskusiju o postizanju reproduktivnih buildova. |
| [#archlinux-security](ircs://chat.freenode.net/archlinux-security) | Kanal za diskusiju o sigurnosnim issue-ima unutar Arch paketa. |
| [#archlinux-testing](ircs://chat.freenode.net/archlinux-testing) | Kanal za diskusiju o testnim repository-ima. |
| [#archlinux-wiki](ircs://chat.freenode.net/archlinux-wiki) | Diskusija o [ArchWiki](/index.php/ArchWiki "ArchWiki"), njegovim člancima i [Arch Linux Forumi](https://bbs.archlinux.org/). |
| [#archlinux-women](ircs://chat.freenode.net/archlinux-women) | Diskusija o polovima i ravnopravnosti, uglavnom na engleskomg. |
| [#archlinux-proaudio](ircs://chat.freenode.net/archlinux-proaudio) | Diskusija o [Arch Linux Pro Audio](/index.php/Professional_audio "Professional audio"). Korisnici također u neoficijalnom #archaudio |

## Internacionalni kanali

### International IRC channels

Internacionalne diskusije su dostupne na sljedećim kanalima, također locirane na **[chat.freenode.net](ircs://chat.freenode.net)** IRC mreži, ukoliko nije navedeno drukčije.

| Kanal | Opis |
| [#archlinux-za](ircs://chat.freenode.net/archlinux-za) | Diskusija (Afrikanci, Engleski) |
| [#archlinux-br](ircs://chat.freenode.net/archlinux-br) | Diskusija (Brazilski) |
| [#archlinux-cn](ircs://chat.freenode.net/archlinux-cn) | Diskusija (Kineski); također na **[irc.oftc.net#arch-cn](ircs://irc.oftc.net/arch-cn)** |
| [#archlinux-cr](ircs://chat.freenode.net/archlinux-cr) | Diskusija (Kostarikanski) |
| [#archlinux.cz](ircs://chat.freenode.net/archlinux.cz) | Diskusija (Česki) |
| [#archlinux.dk](ircs://chat.freenode.net/archlinux.dk) | Diskusija (Danski) |
| [#archlinux.fi](ircs://chat.freenode.net/archlinux.fi) | Diskusija (Finski) |
| [#archlinux-fr](ircs://chat.freenode.net/archlinux-fr) | Diskusija (Francuski) |
| [#archlinux-gaelic](ircs://chat.freenode.net/archlinux-gaelic) | Diskusija (Gaelski) |
| [#archlinux.de](ircs://chat.freenode.net/archlinux.de) | Diskusija (Njemački) |
| [#archlinux-greece](ircs://chat.freenode.net/archlinux-greece) | Diskusija (Grčki) |
| [#archlinux-il](ircs://chat.freenode.net/archlinux-il) | Diskusija (Hebrejski) |
| [#archlinux.hu](ircs://chat.freenode.net/archlinux.hu) | Diskusija (Mađarski) |
| [#archlinux-it](ircs://chat.freenode.net/archlinux-it) | Diskusija (Talijanski); također na **[irc.azzurra.org#archlinux](irc://irc.azzurra.org/archlinux)** |
| [#archlinux-nordics](ircs://chat.freenode.net/archlinux-nordics) | Diskusija (nordijski: Danski, Finski, Norveški i Švedski) |
| [#archlinux-kr](ircs://chat.freenode.net/archlinux-kr) | Diskusija (Korejski) |
| [#archlinux-ir](ircs://chat.freenode.net/archlinux-ir) | Diskusija (Perzijski) |
| [#archlinux.org.pl](ircs://chat.freenode.net/archlinux.org.pl) | Diskusija (Poljski) |
| [#archlinux-pt](ircs://chat.freenode.net/archlinux-pt) | Diskusija (Portugalski) |
| [#archlinux.ro](ircs://chat.freenode.net/archlinux.ro) | Diskusija (Rumunski) |
| [#archlinux-tg](ircs://chat.freenode.net/archlinux-tg) | Diskusija (Ruski); most između IRC-a i Telegram grupe [Arch Linux RU](https://t.me/ArchLinuxChatRU) |
| [#archlinux-ru](ircs://chat.freenode.net/archlinux-ru) | Diskusija (Ruski); također na **[irc.mibbit.net#archlinux-ru](irc://irc.mibbit.net/archlinux-ru)** |
| [#archlinux-rs](ircs://chat.freenode.net/archlinux-rs) | Diskusija (Srbski) |
| [#archlinux-es](ircs://chat.freenode.net/archlinux-es) | Diskusija (Španski) |
| [#archlinux.se](ircs://chat.freenode.net/archlinux.se) | Diskusija (Švedski) |
| [#archlinux-tr](ircs://chat.freenode.net/archlinux-tr) | Diskusija (Turski) |
| [#archlinux-ve](ircs://chat.freenode.net/archlinux-ve) | Diskusija (Venecuelanski) |
| [#archlinuxvn](ircs://chat.freenode.net/archlinuxvn) | Diskusija (Vietnamski, Tiếng Việt) |