"*[cups](https://www.archlinux.org/packages/?name=cups) je open source program, který slouží ke správě tisku. Vyvíjí ho společnost Apple Inc. pro Mac OS® X další [UNIX-like](https://en.wikipedia.org/wiki/cs:UN*X "wikipedia:cs:UN*X") operační systémy.*".

Ačkoliv jsou zde jiné programy pro správu tisku a tiskáren jako například balíčky LPRNG, **C**ommon **U**nix **P**rinting **S**ystem je ze všech nejpoužívanější, protože je relativně jednoduchý na ovládání.

## Contents

*   [1 Instalace](#Instalace)
    *   [1.1 Ovladač tiskárny](#Ovlada.C4.8D_tisk.C3.A1rny)
        *   [1.1.1 Stažení souboru PPD](#Sta.C5.BEen.C3.AD_souboru_PPD)
*   [2 Konfigurace](#Konfigurace)
    *   [2.1 Jaderné moduly](#Jadern.C3.A9_moduly)
        *   [2.1.1 USB tiskárny](#USB_tisk.C3.A1rny)
        *   [2.1.2 Tiskárny s paralelním portem](#Tisk.C3.A1rny_s_paraleln.C3.ADm_portem)
        *   [2.1.3 Automatické načtení modulů](#Automatick.C3.A9_na.C4.8Dten.C3.AD_modul.C5.AF)
    *   [2.2 CUPS daemon](#CUPS_daemon)
    *   [2.3 Webové rozhraní](#Webov.C3.A9_rozhran.C3.AD)
        *   [2.3.1 Administrace systému CUPS](#Administrace_syst.C3.A9mu_CUPS)
        *   [2.3.2 Vzdálený přístup do webového rozhraní](#Vzd.C3.A1len.C3.BD_p.C5.99.C3.ADstup_do_webov.C3.A9ho_rozhran.C3.AD)
*   [3 Řešení problémů](#.C5.98e.C5.A1en.C3.AD_probl.C3.A9m.C5.AF)
    *   [3.1 Problémy po aktualizaci](#Probl.C3.A9my_po_aktualizaci)
        *   [3.1.1 CUPS přestal pracovat](#CUPS_p.C5.99estal_pracovat)
        *   [3.1.2 Chyba s gnutls](#Chyba_s_gnutls)
        *   [3.1.3 Všechny tiskové úlohy jsou "stopped" (zastaveny)](#V.C5.A1echny_tiskov.C3.A9_.C3.BAlohy_jsou_.22stopped.22_.28zastaveny.29)
        *   [3.1.4 Verze PPD není kompatibilní s gutenprint](#Verze_PPD_nen.C3.AD_kompatibiln.C3.AD_s_gutenprint)
    *   [3.2 USB printers under CUPS 1.4.x](#USB_printers_under_CUPS_1.4.x)
        *   [3.2.1 Konfigurační soubor](#Konfigura.C4.8Dn.C3.AD_soubor)
        *   [3.2.2 Zakázání usblp](#Zak.C3.A1z.C3.A1n.C3.AD_usblp)
        *   [3.2.3 Práva zařízení](#Pr.C3.A1va_za.C5.99.C3.ADzen.C3.AD)
            *   [3.2.3.1 Device node permission troubleshooting](#Device_node_permission_troubleshooting)
            *   [3.2.3.2 Loading firmware](#Loading_firmware)
    *   [3.3 Other](#Other)
        *   [3.3.1 CUPS permission errors](#CUPS_permission_errors)
        *   [3.3.2 HPLIP tiskárna vrací chybu "/usr/lib/cups/backend/hp failed"](#HPLIP_tisk.C3.A1rna_vrac.C3.AD_chybu_.22.2Fusr.2Flib.2Fcups.2Fbackend.2Fhp_failed.22)
        *   [3.3.3 hp-toolbox sends an error, "Unable to communicate with device"](#hp-toolbox_sends_an_error.2C_.22Unable_to_communicate_with_device.22)
        *   [3.3.4 CUPS returns '"foomatic-rip" not available/stopped with status 3' with a HP printer](#CUPS_returns_.27.22foomatic-rip.22_not_available.2Fstopped_with_status_3.27_with_a_HP_printer)
        *   [3.3.5 Tisk selže s chybou *unauthorised*](#Tisk_sel.C5.BEe_s_chybou_unauthorised)
        *   [3.3.6 Tlačítko Tisk v GNOME v print dialogu zešedne](#Tla.C4.8D.C3.ADtko_Tisk_v_GNOME_v_print_dialogu_ze.C5.A1edne)
        *   [3.3.7 Unknown supported format: application/postscript](#Unknown_supported_format:_application.2Fpostscript)
        *   [3.3.8 Hledání URI tiskárny běžící pod Windows](#Hled.C3.A1n.C3.AD_URI_tisk.C3.A1rny_b.C4.9B.C5.BE.C3.ADc.C3.AD_pod_Windows)
        *   [3.3.9 Print-Job client-error-document-format-not-supported](#Print-Job_client-error-document-format-not-supported)
*   [4 Appendix](#Appendix)
    *   [4.1 Alternativní rozhraní pro ovládání CUPSu](#Alternativn.C3.AD_rozhran.C3.AD_pro_ovl.C3.A1d.C3.A1n.C3.AD_CUPSu)
    *   [4.2 PDF virtuální tiskárna](#PDF_virtu.C3.A1ln.C3.AD_tisk.C3.A1rna)
        *   [4.2.1 Print to postscript: CUPS-PDF virtual printer trick](#Print_to_postscript:_CUPS-PDF_virtual_printer_trick)
            *   [4.2.1.1 Konfigurace CUPS-PDF virtualní tiskárny](#Konfigurace_CUPS-PDF_virtualn.C3.AD_tisk.C3.A1rny)
    *   [4.3 Další zdroj pro ovladač k tiskárnám](#Dal.C5.A1.C3.AD_zdroj_pro_ovlada.C4.8D_k_tisk.C3.A1rn.C3.A1m)
*   [5 Zdroje](#Zdroje)

## Instalace

Je potřeba nainstalovat tyto balíčky:

```
# pacman -S cups ghostscript gsfonts

```

*   **cups** - CUPS software
*   **ghostscript** - Interpret pro jazyk [Postscript](https://en.wikipedia.org/wiki/cs:Postscript "wikipedia:cs:Postscript")
*   **gsfonts** - Standardní GhostScript fonty
*   **hpoj** - Pokud používáte HP Officejet, měli byste nainstalovat i tento balíček a postupovat podle instrukcí, abyste předešli zbytečným problémům. Přečtěte si pro více informací [toto vlálno na launchpadu/hplip](http://answers.launchpad.net/hplip/+question/133425).

Pokud má systém využívat nějakou síťovou tiskárnu přes protokol [Samba](/index.php/Samba_(%C4%8Cesky) "Samba (Česky)") nebo pokud má být systém print serverem pro klienty s operačním systémem [Windows](https://en.wikipedia.org/wiki/cs:Windows "wikipedia:cs:Windows"), nainstalujte také Sambu:

```
# pacman -S samba

```

### Ovladač tiskárny

Zde jsou balíčky s ovladačemi pro tiskárny od různých výrobců:

*   **gutenprint** - Kolekce velmi kvalitních ovladačů pro tiskárny od výrobců Canon, Epson, Lexmark, Sony, Olympus. A dále pro použití GhostScriptu, CUPSu a [GIMPu](/index.php?title=GIMP_(%C4%8Cesky)&action=edit&redlink=1 "GIMP (Česky) (page does not exist)")
*   **foomatic-db, foomatic-db-engine, foomatic-db-nonfree a foomatic-filters** - Foomatic. Instalace foomatic-filters by měla vyřešit problémy, jestliže cups error_log ohlašuje "stopped with status 22!".
*   **hplip** - HP GNU/Linux driver. Poskytuje podporu pro DeskJet, OfficeJet, Photosmart, Business Inkjet a nějaké modely tiskáren LaserJet. Dále poskytuje podporu i pro nějaké další tiskárny.
*   **splix** - Ovladače Samsung pro SPL (Samsung Printer Language) tiskárny
*   **ufr2** - Ovladač Canon UFR2 s podporou pro LBP, iR a MF sérií tiskáren. Balíček je možné získat z [AURu](/index.php/AUR_(%C4%8Cesky) "AUR (Česky)").
*   **cups-pdf** - Balíček, který umožňuje použití tzv. virtuální PDF tiskárny, která generuje jako svůj výstup PDF soubory.

Jestliže si nejste jistí, který ovladač nainstalovat nebo vám aktuální ovladač nefunguje, může být pro vás jednodušší nainstalovat všechny z výše uvedených ovladačů.

#### Stažení souboru PPD

V závislosti na tiskárně, je tento krok volitelný a nemusí být vůbec potřeba, protože standardní instalace serveru CUPS už nějaké základní soubory PPD (Postscript Printer Description) obsahuje. Mimo to, balíčky *foomatic-filters*, *gimp-print* a *hplip* už obsahují základní soubory PPD, které CUPS detekuje automaticky.

Zde je vysvětlení toho, co to PPD soubor vlastně je z webu Linux Printing:

	"*Pro každou PostSkriptovou tiskárnu poskytuje její výrobce tzv. PPD soubor, který obsahuje všechny základní informace a daném modelu tiskárny. Například jestli tiskárna tiskne barevně nebo pouze černobíle, podporované fonty a hlavně uživatelská nastavení jako třeba velikost papíru, rozlišení apod.*

Pokud soubor PPD pro vaši tiskárnu *není* systémem CUPS nalezen, potom:

*   mrkněte do [AURu](/index.php/AUR_(%C4%8Cesky) "AUR (Česky)"), jestli zde nejsou balíčky se jménem vaší tiskárny nebo vašeho výrobce
*   navštivte stránku [OpenPrinting databáze](http://www.linuxprinting.org/printer_list.cgi) a vyberte zde výrobce a model tiskárny
*   navštivte stránku výrobce a hledejte ovladače pro operační systém [GNU/Linux](https://en.wikipedia.org/wiki/cs:GNU/Linux "wikipedia:cs:GNU/Linux")

**Note:** PPD soubory se nacházejí v adresáři `/usr/share/cups/model/`

## Konfigurace

CUPS jsme nainstalovali. Teď už zbývá jen vše nastavit. Samozřejmě máme k dispozici nastavení pomocí příkazového řádku. Stejnětak, různá desktopová prostředí jako třeba GNOME nebo KDE, mají různé programy pro správu tiskáren. Nicméně, aby byla konfigurace srozumitelná většině uživatelů, bude se tento návod věnovat nastavení přes webové rozhraní, které nám server CUPS poskytuje.

Pokud plánujete připojení k síťové tiskárně, místo přímého připojení k počítači, budete si nejspíš chtít nejdříve přečíst stránku [Sdílení tiskáren](/index.php?title=CUPS_printer_sharing_(%C4%8Cesky)&action=edit&redlink=1 "CUPS printer sharing (Česky) (page does not exist)"). Sdílení tiskáren mezi systémy GNU/Linux je poměrně jednoduché a vyžaduje velmi málo konfigurace. Narozdíl od sdílení mezi Windows a GNU/Linuxem, které už vyžaduje trochu více úsilí.

### Jaderné moduly

Před použitím webového rozhraní programu CUPS, musí být nainstalovány vhodné jaderné moduly. Následující kroky pocházejí z návodu *Gentoo Printing*.

Tato sekce není důležitá, ačkoliv závisí na jádru. Modul jádra může být automaticky načten při připojení tiskárny. Použijte příkaz `tail` (popsaný níže) pro kontrolu, jestli byla tiskárna jádrem správně detekována. Také můžete použít program `lsmod`, pro zjištění, které moduly jádra jsou právě načteny.

#### USB tiskárny

Uživatelé USB tiskáren budou pravděpodobně potřebovat vypnout modul `usblp`. Mějte na paměti, že je zde hodně [pochybností](https://bbs.archlinux.org/viewtopic.php?pid=660601) týkajících se vypnutí `usblp`. Například některé tiskárny Canon a Epson nejsou bez tohoto modulu rozpoznány. Někteří uživatelé tiskáren Samsung ohlašovali, že používání `cupsu` s vypnutým modulem `usblp` způsobovalo problémy. Řešením bylo znovuzapnutí `usblp` a instalace `cups-usblp` z [AURu](/index.php/AUR_(%C4%8Cesky) "AUR (Česky)") místo nalíčku `cups` z oficiálního repozitáře. ([https://bbs.archlinux.org/viewtopic.php?pid=778104](https://bbs.archlinux.org/viewtopic.php?pid=778104))

Pro vypnutí modulu, upravte soubor `/etc/rc.conf` následovně:

 `/etc/rc.conf`  `MODULES=(... **!usblp** ...)` 

Na některých jádrech musí uživatelé načíst vše manuálně nahráním modulu `usbcore` následovně:

```
# modprobe usbcore

```

Jakmile jsou moduly nahrané, připojte tiskárnu a zkontrolujte, jestli ji jádro detekovalo spuštěním:

```
# tail /var/log/messages.log

```

nebo

```
# dmesg

```

Pokud používáte `usblp`, výstup by nám měl říci, že byla tiskárna detekována:

```
Feb 19 20:17:11 kernel: printer.c: usblp0: USB Bidirectional
printer dev 2 if 0 alt 0 proto 2 vid 0x04E8 pid 0x300E
Feb 19 20:17:11 kernel: usb.c: usblp driver claimed interface cfef3920
Feb 19 20:17:11 kernel: printer.c: v0.13: USB Printer Device Class driver

```

Pokud jste vypnuly modul `usblp`, uvidíte něco podobného tomuto:

```
usb 3-2: new full speed USB device using uhci_hcd and address 3
usb 3-2: configuration #1 chosen from 1 choice

```

#### Tiskárny s paralelním portem

Pokud plánujete používat tiskárnu s paralelním portem, konfigurace je skoro stejná. Jediné co musíte je načíst moduly:

```
# modprobe lp
# modprobe parport
# modprobe parport_pc

```

Znovu omrkněte, jestli vše proběhlo v pořádku:

```
# tail /var/log/messages.log

```

Ve výpisu by mělo být něco podobného:

```
lp0: using parport0 (polling).

```

#### Automatické načtení modulů

Pro automatické načítání jaderných modulů vždy při startu systému musíte jména modulů přidat do svého souboru `/etc/[rc.conf](/index.php/Rc.conf "Rc.conf")` do pole `MODULES=()`. Například jako je zde:

```
MODULES=(!usbserial scsi_mod sd_mod snd-ymfpci snd-pcm-oss **lp parport parport_pc** ide-scsi)

```

### CUPS daemon

Když už máte nainstalované jaderné moduly, můžete nastartovat svého CUPS daemona. To uděláte jednoduše spuštěním:

```
# /etc/rc.d/cupsd start

```

Ještě aby se vám CUPS daemon zapínal vždy při startu počítače, musíte ho přidat do pole `DAEMONS=()` v souboru `/etc/rc.conf`. A to takto:

```
DAEMONS=(syslog-ng dbus network gdm @crond **@cupsd**)

```

### Webové rozhraní

Pokud vám daemon běží, otevřete svůj webový prohlížeč a přejděte na: [http://localhost:631](http://localhost:631) (*Řetězec **localhost** budete možná muset nahradit tím, který najdete ve svém* `/etc/hosts`).

Následně už pouze stačí proklikat průvodci a jednoduše přidat tiskárnu. Toto se provede kliknutím na *Přídávání tiskáren (Adding Printers)* a následným kliknutím na *Přidat tiskárnu (Add printer)*. Pokud se vás prohlížeč zeptá na příhlašovací jméno a heslo, přihlašte se jako root. Na jménu, které se automaticky přiřadilo tiskárně nezáleží (to samé platí i pro 'umístění (location)' a 'popis (description)'. V dalším kroku vyberte zařízení, které chcete přidat. Nakonec vyberte odpovídající ovladače pro tiskárnu a konfigurace je hotova.

Teď už pouze stačí tiskárnu otestovat. Přejděte do záložky *Správa (Maintenance)* a stiskněte *Vytisknout testovací stránku (Print Test Page)*. Pokud se stránka nevytiskla a jste přesvědčeni o správnosti konfigurace, pravděpodobně bude problém s chybějícím nebo špatně zvoleným ovladačem.

**Tip:** [GNOME](/index.php/GNOME "GNOME") users may be inclined towards installing the GNOME CUPS manager GUI frontend. See: [#Alternative CUPS interfaces](#Alternative_CUPS_interfaces)

**Note:** When setting up a USB printer, you should see your printer listed on *Add Printer* page. If you can only see a "SCSI printer" option, it probably means that CUPS has failed to recognize your printer.

#### Administrace systému CUPS

Při administraci tiskáren (přidávání a odebírání tiskáren, zastavování úloh apod.) ve webovém rozhranní po vás bude systém chtít zadat uživatelské jméno a heslo. Defaultní uživatelské jméno je přiřazené skupině *sys* nebo root (toto můžete změnit v souboru `/etc/cups/cupsd.conf` na řádku *SystemGroup*).

Pokud je účet uživatele root uzamčen a není možné se přihlásit defaultním uživatelským jménem a heslem, bude pravděpodobně potřeba změnit SystemGroup v cupsd.conf a přečíst si [tento post](https://bbs.archlinux.org/viewtopic.php?id=35567).

#### Vzdálený přístup do webového rozhraní

Defaultně je webové rozhraní serveru CUPS přístupné pouze z *localhost* (pouze z počítače, kde je CUPS nainstalován). Pro spřístupnění rozhraní musíte provést následující změny v souboru `/etc/cups/cupsd.conf`. Přepište proto řádku:

```
Listen localhost:631

```

tímto:

```
port 631

```

systém CUPS tak bude přijímat příchozí spojení.

Existují tři různé úrovně přístupu, které můžete ovlivnit

```
<Location />           #přístup k serveru
<Location /admin>	#přístup k administraci
<Location /admin/conf>	#přístup ke konfiguračním souborům

```

Aby jste umožnili vzdálenému klientovi nějaký z přístupů, udělte mu volbu `Allow`. Položka `Allow` může mít více forem:

```
Allow all
Allow host.domena.cz
Allow *.domena.cz
Allow ip-address
Allow ip-addresa/maska

```

Omezení přístupu. Například pokud budete chtít dát všem klientům v podsíti 192.168.1.0/255.255.255.0 plný přístup, soubor `/etc/cups/cupsd.conf` by měl obsahovat toto:

```
# Omezení přístupu k serveru...
# Defaultně jsou povoleny pouze připojení z localhostu
<Location />
   Order allow,deny
   Allow From localhost
   **Allow From 192.168.1.0/255.255.255.0**
</Location>

# Omezení přístupu k admin stránkám...
<Location /admin>
   # Encryption disabled by default
   #Encryption Required
   Order allow,deny
   Allow From localhost
   **Allow From 192.168.1.0/255.255.255.0**
</Location>

# Omezení přístupu ke konfiguračním souborům...
<Location /admin/conf>
   AuthType Basic
   Require user @SYSTEM
   Order allow,deny
   Allow From localhost
   **Allow From 192.168.1.0/255.255.255.0**
</Location>

```

Možná bude potřeba ještě přidat řádku:

```
DefaultEncryption Never

```

Toto by mělo odstranit chybovou hlášku: 426 - Upgrade Required when using the CUPS web interface from a remote machine.

## Řešení problémů

Pro správné odladění programu je dobré zapnout logy. Pro jejich zapnutí nastavte 'LogLevel' v souboru `/etc/cups/cupsd.conf` na:

```
LogLevel debug

```

Obsah tohoto souboru (`/var/log/cups/error_log` můžete číst následovně:

```
# tail -n 100 -f /var/log/cups/error_log

```

Znaky na levé straně výstupu znamenají:

*   D=Ladíci informace
*   E=Chyba
*   I=Informace
*   A další

Tyto soubory mohou být také užitečné:

*   `/var/log/cups/page_log` - Vypíše se do něho vždy nový záznam a každém úspěšně provedeném tisku
*   `/var/log/cups/access_log` - Vypisuje se do něho kompletní aktivita serveru cupsd cupsd http1.1

Samozřejmě, že je nezbytné znát to, jak CUPS funguje, pokud chcete řešit nějaké problémy.

1.  Aplikace odešle soubor typu .ps (v tzv. PostScriptu - skriptovací jazyk, který tiskárně říká, jak bude výsledná stránka vypadat) serveru CUPS.
2.  CUPS se pak podívá na soubor PPD (PostScript Printer Description) a vyřeší jaké je potřeba použít filtry, aby se soubor typu .ps převedl do jazyka, kterému tiskárna bude rozumět (například PJL, PCL), obvykle GhostScript
3.  GhostScript takes the input and figures out which filters it should use, then applies them and converts the .ps file to a format understood by the printer.
4.  Then it is sent to the back-end. For example, if the printer is connected to a USB port, it uses the USB back-end.

Print a document and watch `error_log` to get a more detailed and correct image of the printing process.

### Problémy po aktualizaci

*Problémy, které se objevily po aktualizaci programu*

#### CUPS přestal pracovat

Nejspíš bude kvůli nové verzi programu potřeba aktualizovat váš konfigurační soubor. Například se vám bude zobrazovat chyba "404 - stránka nenalezena" při přístupu do administrace na localhost:631.

Pro použití nového konfiguračního souboru zkopírujte /etc/cups/cupsd.conf.default do /etc/cups/cupsd.conf (samozřejmě si zazálohujte původní konfiguraci):

```
# cp /etc/cups/cupsd.conf.default /etc/cups/cupsd.conf

```

a restartujte CUPS, aby se načetl nový konfigurační soubor.

#### Chyba s gnutls

Pokud dostáváte chyby typu:

```
/usr/sbin/cupsd: error while loading shared libraries: libgnutls.so.13: cannot open shared object file: No such file or directory

```

gnutls pravděpodobně potřebuje aktualizovat:

```
# pacman -S gnutls

```

Po aktualizaci se může v `/etc/cups` objevit soubor `cupsd.conf.pacnew`. V tomto souboru je nemodifikováná originální konfigurace. Svůj starý konfigurační soubor proto s nově vzniklým porovnejte a případně doupravte tak, aby v něm nechyběla nově vydaná nastavení.

#### Všechny tiskové úlohy jsou "stopped" (zastaveny)

Pokud jsou všechny tiskové úlohy poslané na tiskárnu zastaveny (bude u nich stav "stopped"), odeberte vaši tiskárnu a znovu ji přidejte. To provedete ve [webovém rozhraní CUPSu](http://localhost:631), přejděte do sekce Printers > Delete Printer.

#### Verze PPD není kompatibilní s gutenprint

Spusťte:

```
# /usr/sbin/cups-genppdupdate

```

A restartujte CUPS.

### USB printers under CUPS 1.4.x

Nový CUPS 1.4.x přínáší plno změn:

#### Konfigurační soubor

Syntaxe konfiguračního souboru cupsd.conf se změnila. Proto začněte s novým souborem cupsd.conf založeným na /etc/cups/cupsd.conf.default.

#### Zakázání usblp

Aktuální verze CUPSu využívá místo usblp, kde se zařízení generovala jako `/dev/usb/lpX`, libusb kde se generují do `/dev/bus/usb/`. Aby vám na vašem počítači fungovaly USB tiskárny, musí se usblp modul vypnout. To lze udělat tak, že přidáte řádek "blacklist usblp" do konfiguračního souboru `/etc/modprobe.d/modprobe.conf`:

 `/etc/modprobe.d/modprobe.conf`  `blacklist usblp` 

Pokud vám tiskárna nebude fungovat stále, zkuste ji reinstalovat.

#### Práva zařízení

Aby mohl CUPS využívat USB zařízení tiskárny, je nutné, aby k tomu měl dostatečná práva. Vlastník by měl být root:lp a práva přístupu na 660\. Například:

```
$ ls -l /dev/bus/usb/003/002
crw-rw---- 1 root lp 189, 257 20\. Okt 10:32 /dev/bus/usb/003/002

```

This is supposed to be achieved by two udev rules in /lib/udev/rules.d/50-udev-default.rules:

```
# hplip and cups 1.4+ use raw USB devices, so permissions should be similar to
# the ones from the old usblp kernel module
SUBSYSTEM=="usb", ENV{DEVTYPE}=="usb_device", ENV{ID_USB_INTERFACES}=="", IMPORT{program}="usb_id --export %p"
SUBSYSTEM=="usb", ENV{DEVTYPE}=="usb_device", ENV{ID_USB_INTERFACES}==":0701*:", GROUP="lp", MODE="660"

```

However, for some devices, in particular combined printer/scanner devices, these rules either do not trigger, or are overwritten by rules of the 'sane' package. In these cases a custom udev rule needs to be added. See below.

##### Device node permission troubleshooting

Get the printer's device file and its permissions with:

```
$ lsusb
...
Bus 003 Device 002: ID 04b8:0841 Seiko Epson Corp.
$ ls -l /dev/bus/usb/003/002
crw-rw---- 1 root lp 189, 257 20\. Okt 10:32 /dev/bus/usb/003/002

```

If the permissions are not already root:lp 660, enforce it by creating a custom udev rule, e.g

```
cat /etc/udev/rules.d/10-usbprinter.rules
ATTR{idVendor}=="04b8", ATTR{idProduct}=="0841", MODE:="0660", GROUP:="lp"

```

Note that idVendor and idProduct are from the lsusb listing above.

##### Loading firmware

Some printers and drivers need to load firmware to the printer (such as HP LaserJet 10xx printers using foo2zjs) and do this by writing directly to the lp device, a functionality provided by usblp. A work around until this issue is resolved is to install the usblp module until the firmware is loaded, then remove the module to allow CUPS to work. This can be accomplished by manually running "$ modprobe usblp", waiting for the firmware to load, then "$ rmmod usblp". You can also not blacklist usblp, then put "rmmod usblp" to /etc/rc.local, allowing the firmware to be loaded on boot before rc.local is run, then removing usblp.

In case the printer is plugged in or powered on while system is already running, /etc/rc.local does not get executed and usblp module stays loaded. A workaround is to modify the /etc/udev/rules.d/11-hpj10xx.rules provided by foo2zjs so that after the add event we wait e.g. 15 seconds for the firmware to load and then automatically remove usblp. The following example is for HP LaserJet 1018\. For other models the value of ATTRS{idProduct} should be changed to match the printer model.

Locate the line matching your printer in /etc/udev/rules.d/11-hpj10xx.rules:

```
ACTION=="add", KERNEL=="lp*", SUBSYSTEM=="usb", ATTRS{idVendor}=="03f0",     \
       ATTRS{idProduct}=="4117", RUN+="/sbin/foo2zjs-loadfw 1018 $tempnode"

```

Add the following lines below it, make sure match the product and vendor IDs:

```
ACTION=="add", KERNEL=="lp*", SUBSYSTEM=="usb", ATTRS{idVendor}=="03f0",     \
       ATTRS{idProduct}=="4117", RUN+="/usr/bin/sleep 15"
ACTION=="add", KERNEL=="lp*", SUBSYSTEM=="usb", ATTRS{idVendor}=="03f0",     \
       ATTRS{idProduct}=="4117", RUN+="/sbin/rmmod usblp"

```

### Other

##### CUPS permission errors

*   Some users fixed 'NT_STATUS_ACCESS_DENIED' (Windows clients) errors by using a slightly different syntax:

```
smb://workgroup/username:password@hostname/printer_name

```

*   Sometimes, the block device has wrong permissions:

```
# ls /dev/usb/
lp0
# chgrp lp /dev/usb/lp0

```

#### HPLIP tiskárna vrací chybu "/usr/lib/cups/backend/hp failed"

Ujistěte se, že máte nainstalovaný a běžící dbus. Například spuštěním `ls /var/run/daemons`.

Pokud máte dbus spuštěný a tato chyba dále přetrvává, možná budete muset spustit daemona *avahi*.

#### hp-toolbox sends an error, "Unable to communicate with device"

If running hp-toolbox as a regular user results in:

```
# hp-toolbox
# error: Unable to communicate with device (code=12): hp:/usb/<printer id>

```

or, "`Unable to communicate with device"`", then it may be needed to add the user to the lp group by running the following command:

```
# gpasswd -a <username> lp

```

#### CUPS returns '"foomatic-rip" not available/stopped with status 3' with a HP printer

If receiving any of the following error messages in `/var/log/cups/error_log` while using a HP printer, with jobs appearing to be processed while they all end up not being completed with their status set to 'stopped':

```
Filter "foomatic-rip" for printer "<printer_name>" not available: No such file or director

```

or:

```
PID 5771 (/usr/lib/cups/filter/foomatic-rip) stopped with status 3!

```

make sure **hplip** has been installed, in addition to [the packages mentioned above](#Packages), **net-snmp** is also needed. See [this forum post](https://bbs.archlinux.org/viewtopic.php?id=65615).

```
# pacman -S hplip

```

#### Tisk selže s chybou *unauthorised*

Pokud byl uživatel přidán do skupiny *lp* a byl mu umožněn tisk (vše se nastavuje v `cups.conf`), bude nejspíše problém v souboru `/etc/cups/printers.conf`. Za vše může pravděpodobně tato řádka:

```
AuthInfoRequired negotiate

```

Zakomentujte ji a restartujte CUPS.

#### Tlačítko Tisk v GNOME v print dialogu zešedne

	*<small>Zdroj: [I can't print from gnome applications. - Arch Forums](https://bbs.archlinux.org/viewtopic.php?id=70418)</small>*

Ujistěte se, že je nainstalovaný balíček **libgnomeprint**.

Upravte `/etc/cups/cupsd.conf` a přidejte

```
# HostNameLookups Double

```

Restartujte CUPS:

```
# /etc/rc.d/cupsd restart

```

#### Unknown supported format: application/postscript

Zakomentujte řádky:

```
application/octet-stream        application/vnd.cups-raw        0      -

```

v souboru `/etc/cups/mime.convs` a:

```
application/octet-stream

```

v `/etc/cups/mime.types`.

#### Hledání URI tiskárny běžící pod Windows

Občas jsou potíže s nalezením správné URI adresy zařízení. Pokud s tím máte problémy, spusťte následující příkaz, který vám vypíše všechny dostuné adresy URI podle zadaného uživatelského jména:

```
$ smbtree -U *windows_uzivatelske_jmeno*

```

Vše bude samozřejmě fungovat jen pokud vám poběží správně [Samba](/index.php/Samba_(%C4%8Cesky) "Samba (Česky)"). Příkaz by měl vrátit něco podobného tomuto:

```
 WORKGROUP
	\\REGULATOR-PC   		
		\\REGULATOR-PC\Z              	
		\\REGULATOR-PC\Public         	
		\\REGULATOR-PC\print$         	Printer Drivers
		\\REGULATOR-PC\G              	
		\\REGULATOR-PC\EPSON Stylus CX8400 Series	EPSON Stylus CX8400 Series
```

Z výpisu nás zajímá hlavně první část posledního řádku. V druhé části řádku je popis zařízení. Takže pro tiskárnu EPSON Stylus vložte do nastavení v CUPS tuto URI:

```
smb://uzivatelske_jmeno.heslo@REGULATOR-PC/EPSON Stylus CX8400 Series

```

Všimněte si, že je v URI dovoleno používat bíle znaky, zatímco zpětná lomítka jsou nahrazeny lomítky klasickými.

#### Print-Job client-error-document-format-not-supported

Zkuste nainstalovat foomatic balíčky a použijte ovladač foomatic.

## Appendix

### Alternativní rozhraní pro ovládání CUPSu

Pokud používáte [GNOME (Česky)](/index.php/GNOME_(%C4%8Cesky) "GNOME (Česky)"), je možné spravovat a konfigurovat tiskárnu pomocí system-config-printer-gnome. Tento balíček můžete nainstalovat takto:

```
# pacman -S system-config-printer-gnome

```

Pravděpodobně budete muset spouštět system-config-printer pod uživatelem root. Případně můžete pro určité uživatele vytvořit skupinu. Pokud to chcete řešit takto, postupujte podle kroků **1-3**.

*   1\. Vytvořte skupinu a přiřaďte ji uživatelům, kterým chcete dát práva spravovat tiskárny

```
# groupadd lpadmin
# usermod -aG lpadmin <uzivatelske_jmeno>

```

*   2\. Přidejte "lpadmin" (bez uvozovek) na níže uvedený řádek v souboru `/etc/cups/cupsd.conf`

```
SystemGroup sys root <sem>

```

*   3\. Restartujte cups, odhlašte se a znovu přihlašte (nebo restartujte počítač)

```
# /etc/rc.d/cupsd restart

```

Uživatelé, kteří používají prostředí [KDE (Česky)](/index.php/KDE_(%C4%8Cesky) "KDE (Česky)") mohou tiskárny spravovat z tzv. Control Centra. Pokud potřebujete více informací o tom, jak spravovat tiskárny v těchto prostředích, koukněte do dokumentace.

Zde je také v [AURu](/index.php/AUR_(%C4%8Cesky) "AUR (Česky)") [gtklp](https://aur.archlinux.org/packages.php?ID=43505).

### PDF virtuální tiskárna

[cups-pdf](https://www.archlinux.org/packages/?name=cups-pdf) je balíček, který umožňuje nastavení tzv. virtuální tiskárny. Díky této tiskárně můžete generovat PDF soubory z toho, co na ni pošlete. Pro samotnou funkčnost CUPSu není tento balíček potřebný, ale určitě je velmi užitečný.

Vygenerované PDF dokumenty jsou umístěny v podadresáři `/var/spool/cups-pdf`. Většinou je tento podadresář pojmenovaný po uživateli, který spustil tisk.

Balíček nainstalujete následujícím příkazem:

```
# pacman -S cups-pdf

```

Po instalaci balíku tiskárnu nastavte - například prostřednictvím webového rozhranní. Jako zařízení (Device) vyberte **CUPS-PDF (Virtual PDF Printer)**; Výrobce (Make/Manufacturer), vyberte **Generic**; Ovladač (Model/Driver), vyberte **Generic postscript color printer** nebo **Generic Cups-PDF Printer**. Případně ješte můžete zvolit [tento](http://www.physik.uni-wuerzburg.de/~vrbehr/cups-pdf/cups-pdf-CURRENT/extra/CUPS-PDF.ppd) soubor PPD.

#### Print to postscript: CUPS-PDF virtual printer trick

Printing to PDF in most applications like OpenOffice is no problem; just hit the button. Yet when printing out to postscript, matters take a little more work. For applications like OpenOffice where printing to kprinter is nebulous at best, there has to be another way -- and there is. The CUPS-PDF (Virtual PDF Printer) actually creates a postscript file and then creates the PDF using the ps2pdf utility. To print to postscript, what needs to be done is capturing the intermediate postscript file created by CUPS-PDF. This is easily accomplished with by selecting the "print to file" option in the print dialog. (choose either .ps or .eps as the extension) After selecting the "print to file" checkbox simply enter the filename and click "print".

##### Konfigurace CUPS-PDF virtualní tiskárny

1\. Nainstalujte [cups](https://www.archlinux.org/packages/?name=cups) a [cups-pdf](https://www.archlinux.org/packages/?name=cups-pdf) z `[extra]`.

2\. Nastartujte cups tímto příkazem:

```
# /etc/rc.d/cupsd 

```

**Note:** Přidejte si 'cups' do pole daemonů ve svém `/etc/rc.conf`, pokud chcete, aby se zapínal při startu operačního systému.

3\. Běžte do webové administrace CUPSu přejdutím na adresu: [http://localhost:631](http://localhost:631) a vyberte:

```
Administration (Administrace) -> Add Printer (Přidat tiskárnu)
Vyberte CUPS-PDF (Virtual PDF) pro Make a Driver:
Make:	Generic
Driver:	Generic CUPS-PDF Printer

```

Teď už stačí pro vytištění postskriptu, vytisknout vše jako obvykle, akorát v print dialogu vyberte tiskárnu "CUPS-PDF". Potom zatrhněte checkbox Print to file (Vytisknout do souboru), stiskněte *Tisk* a vložtě jméno souboru, do kterého chcete vše vytisknout.

### Další zdroj pro ovladač k tiskárnám

[Turboprint](http://www.turboprint.de/english.html) je proprietární ovladač pro mnoho různých tiskáren, které ještě nejsou oficiálně podporovány operačním systémem GNU/Linux (například Canon i*). Nicméně vysoce kvalitní výtisky jsou označeny vodoznakem nebo jsou pay-only.

## Zdroje

*   [Officiální dokumentace CUPSu](http://localhost:631/help/), *instalovaná lokálně*
*   [Oficiální stránka programu CUPS](http://www.cups.org/)
*   [Linux Printing](http://www.linuxprinting.org/), *[The Linux Foundation](http://www.linuxfoundation.org)*
*   [Gentoo's Printing Guide](http://www.gentoo.org/doc/en/printing-howto.xml), *[Gentoo Documentation Resources](http://www.gentoo.org/doc/en)*
*   [Arch Linux fóra](https://bbs.archlinux.org/)

*   [Common Unix Printing System na Wikipedii](https://en.wikipedia.org/wiki/CUPS "wikipedia:CUPS")