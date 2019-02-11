Táto stránka popisuje postup rozbehania čítačky a aplikácie eID klient pre [Občiansky preukaz SR s čipom (eID)](https://portal.minv.sk/wps/wcm/connect/sk/site/main/obciansky-preukaz-s-cipom/) v Arch linuxe.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Testované a funkčné čítačky](#Testované_a_funkčné_čítačky)
*   [2 Inštalácia](#Inštalácia)
*   [3 Oficiálna príručka](#Oficiálna_príručka)
*   [4 Používanie](#Používanie)
    *   [4.1 Prvé spustenie](#Prvé_spustenie)
    *   [4.2 Povolenie automatického spúšťania eID klienta](#Povolenie_automatického_spúšťania_eID_klienta)
    *   [4.3 Kontrola čítačky](#Kontrola_čítačky)
    *   [4.4 "Čítačka IDBridge CT30 nie je podporovaná vo virtualizovanom prostredí pre OS Linux."](#"Čítačka_IDBridge_CT30_nie_je_podporovaná_vo_virtualizovanom_prostredí_pre_OS_Linux.")
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 DEBTAP: gzip: /var/cache/debtap/ubuntu-packages-files.gz: unexpected end of file; Synchronization failed. Exiting...](#DEBTAP:_gzip:_/var/cache/debtap/ubuntu-packages-files.gz:_unexpected_end_of_file;_Synchronization_failed._Exiting...)

## Testované a funkčné čítačky

| Model čítačky | lsusb | eID klient |
| IDBridge CT30 | Gemalto (was Gemplus) GemPC Twin SmartCard Reader | Gemalto PC Twin Reader |
| Bit4id - miniLector EVO | Advanced Card Systems, Ltd ACR38 SmartCard Reader | ACS ACR 38U-CCID |
| AU9560 - USB Smart Card Reader Controller | Alcor Micro Corp. AU9540 Smartcard Reader | Alcor Micro AU9560 |

## Inštalácia

1\. Balíčky zo štandardných repozitárov [glibc](https://www.archlinux.org/packages/?name=glibc), [chrpath](https://www.archlinux.org/packages/?name=chrpath), [openssl](https://www.archlinux.org/packages/?name=openssl), [qt4](https://www.archlinux.org/packages/?name=qt4), [pcsclite](https://www.archlinux.org/packages/?name=pcsclite), [pcsc-tools](https://www.archlinux.org/packages/?name=pcsc-tools), [openssl](https://www.archlinux.org/packages/?name=openssl), [xterm](https://www.archlinux.org/packages/?name=xterm), [qt5-imageformats](https://www.archlinux.org/packages/?name=qt5-imageformats), [ccid](https://www.archlinux.org/packages/?name=ccid), [openssl-1.0](https://www.archlinux.org/packages/?name=openssl-1.0), [libcurl-compat](https://www.archlinux.org/packages/?name=libcurl-compat):

```
sudo pacman -S glibc chrpath openssl qt4 pcsclite pcsc-tools openssl xterm qt5-imageformats ccid openssl-1.0 libcurl-compat

```

2\. AUR balíček [debtap](https://aur.archlinux.org/packages/debtap/), [libcurl-openssl-1.0](https://aur.archlinux.org/packages/libcurl-openssl-1.0/):

```
yaourt debtap
yaourt libcurl-openssl-1.0

```

3\. Aktualizácia debtap databázy:

```
sudo debtap -u

```

4\. eID klient aplikáciu stiahnuť zo stránky [Min. vnútra SR](https://eidas.minv.sk/TCTokenService/download/) - [balíček Debian 8/9 32-bit](https://eidas.minv.sk/TCTokenService/download/linux/debian/Aplikacia_pre_eID_i386_debian.tar.gz) alebo [balíček Debian 8/9 64-bit](https://eidas.minv.sk/TCTokenService/download/linux/debian/Aplikacia_pre_eID_amd64_debian.tar.gz)

5\. Prekonfigurovanie stiahnutého DEB balíčka na Arch linux kompatibilný formát a jeho inštalácia:

```
tar -zxf Aplikacia_pre_eID_*_debian.tar.gz
sudo debtap -u
debtap Aplikacia_pre_eID_*_debian.deb
                 `**# Prve dve otázky pri spustení tohto príkazu stačí odklepnúť enterom.**`
                 `**# Následne je potreba upraviť ".PKGINFO":**`
                                   `**# V default vygenerovanom ".PKGINFO" sa objaví min. 6x "Carriage return" (^M), ktorý je potrebné odstrániť zo všetkých riadkov.**`
                                   `**# Taktiež doporučujem opraviť "pkgname = eac-mw-klient" na "pkgname = eidklient".**`
                                   `**# Následne ".PKGINFO" uložiť a preskociť dalšie zmeny v zostávajucich súboroch.**`
sudo pacman -U eidklient*.pkg.tar.xz

```

6\. Oprava symbolických liniek na knižnice:

```
sudo ln -sf /usr/lib/qt/plugins/imageformats/libqtga.so /usr/lib/eac_mw_klient/
sudo ln -sf /usr/lib/qt4/plugins/imageformats/libqgif.so /usr/lib/eac_mw_klient/
sudo ln -sf /usr/lib/qt4/plugins/imageformats/libqico.so /usr/lib/eac_mw_klient/
sudo ln -sf /usr/lib/qt4/plugins/imageformats/libqjpeg.so /usr/lib/eac_mw_klient/
sudo ln -sf /usr/lib/qt4/plugins/imageformats/libqmng.so /usr/lib/eac_mw_klient/
sudo ln -sf /usr/lib/qt4/plugins/imageformats/libqsvg.so /usr/lib/eac_mw_klient/
sudo ln -sf /usr/lib/qt4/plugins/imageformats/libqtiff.so /usr/lib/eac_mw_klient/

```

7\. Naštartovať PC/SC Smart Card daemona:

```
sudo systemctl start pcscd.service

```

Podľa potreby zapnúť štartovanie daemona ihneď po štarte OS:

```
sudo systemctl enable pcscd.service

```

8\. Umiestnenie aplikačných odkazov na plochu:

```
cp /usr/lib/eac_mw_klient/*.desktop ~/Desktop

```

9\. eIDklient verzia 3 disig-web-designer (pre online nahrávanie certifikátov na občianske preukazy s čipom) [balíček Debian 8/9 32-bit](https://download.disigcdn.sk/cdn/products/websigner/disig-web-signer-1-0-7_1.1.5-1.debian_i386.deb) alebo [balíček Debian 8/9 64-bit](https://download.disigcdn.sk/cdn/products/websigner/disig-web-signer-1-0-7_1.1.5-1.debian_amd64.deb)

```
debtap disig-web-signer-*.debian_amd64.deb
                 `**# Prve dve otázky pri spustení tohto príkazu stačí odklepnúť enterom.**`
                 `**# Následne je potreba upraviť ".PKGINFO":**`
                                   `**# Úplne vymazať riadok obsahujúci "depend = gdebi".**`
                                   `**# Riadok obsahujúci "depend = libgl1-mesa-glx" možno nahradiť nasledujúcim "depend = mesa".**`
                                   `**# Následne ".PKGINFO" uložiť a preskociť dalšie zmeny v zostávajucich súboroch.**`
sudo pacman -U disig-web-signer*.pkg.tar.xz

```

## Oficiálna príručka

Na stánkach [Min. vnútra SR](https://eidas.minv.sk/TCTokenService/download/) alebo [slovensko.sk](https://www.slovensko.sk/sk/na-stiahnutie)

## Používanie

### Prvé spustenie

```
LD_PRELOAD=/usr/lib/libcurl-openssl-1.0.so EAC_MW_klient

```

### Povolenie automatického spúšťania eID klienta

*   V prostredí aplikácie: dá sa povoliť pri prvom spustení aplikácie, alebo následne vo "Všeobecných nastaveniach".
*   Manuálne cez príkazový riadok: `cp /usr/lib/eac_mw_klient/startup/aplikacia-pre-eid.desktop ~/.config/autostart/`

### Kontrola čítačky

Prostredníctvom balíčka [pcsc-tools](https://www.archlinux.org/packages/?name=pcsc-tools) pribudli v systéme okrem iného utilitky `pcsc_scan`, `scriptor` alebo `gscriptor`.

### "Čítačka IDBridge CT30 nie je podporovaná vo virtualizovanom prostredí pre OS Linux."

Napriek tomuto upozorneniu no stránkach [Min. vnútra SR](https://eidas.minv.sk/TCTokenService/download/) alebo [slovensko.sk](https://www.slovensko.sk/sk/na-stiahnutie), fungovanie čítačiek vo VirtualBox VM fungovalo bez akýchkoľvek problémov.

## Troubleshooting

### DEBTAP: gzip: /var/cache/debtap/ubuntu-packages-files.gz: unexpected end of file; Synchronization failed. Exiting...

V prípade chyby (aktuálne k verzii 2.8-1):

```
curl: (22) The requested URL returned error: 404 Not Found
gzip: /var/cache/debtap/ubuntu-packages-files.gz: unexpected end of file
Synchronization failed. Exiting...

```

stačí v scripte `/usr/bin/debtap` opraviť `**http**://packages.ubuntu.com` za **https** a príkaz spustiť znova.

Jednoduchý príkaz ktorý to celé opraví:

```
sudo sed '/ubuntu_latest_stable_version/s/http:\/\/packages.ubuntu.com/https:\/\/packages.ubuntu.com/' -i /usr/bin/debtap

```