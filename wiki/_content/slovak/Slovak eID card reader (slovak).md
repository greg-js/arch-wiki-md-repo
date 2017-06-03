Táto stránka popisuje postup rozbehania čítačky a aplikácie eID klient pre [Občiansky preukaz SR s čipom (eID)](https://portal.minv.sk/wps/wcm/connect/sk/site/main/obciansky-preukaz-s-cipom/) v Arch linuxe.

## Contents

*   [1 Testované a funkčné čítačky](#Testovan.C3.A9_a_funk.C4.8Dn.C3.A9_.C4.8D.C3.ADta.C4.8Dky)
*   [2 Inštalácia](#In.C5.A1tal.C3.A1cia)
*   [3 Oficiálna príručka](#Ofici.C3.A1lna_pr.C3.ADru.C4.8Dka)
*   [4 Používanie](#Pou.C5.BE.C3.ADvanie)
    *   [4.1 Prvé spustenie](#Prv.C3.A9_spustenie)
    *   [4.2 Povolenie automatického spúšťania eID klienta](#Povolenie_automatick.C3.A9ho_sp.C3.BA.C5.A1.C5.A5ania_eID_klienta)
    *   [4.3 Kontrola čítačky](#Kontrola_.C4.8D.C3.ADta.C4.8Dky)
    *   [4.4 "Čítačka IDBridge CT30 nie je podporovaná vo virtualizovanom prostredí pre OS Linux."](#.22.C4.8C.C3.ADta.C4.8Dka_IDBridge_CT30_nie_je_podporovan.C3.A1_vo_virtualizovanom_prostred.C3.AD_pre_OS_Linux..22)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 DEBTAP: gzip: /var/cache/debtap/ubuntu-packages-files.gz: unexpected end of file; Synchronization failed. Exiting...](#DEBTAP:_gzip:_.2Fvar.2Fcache.2Fdebtap.2Fubuntu-packages-files.gz:_unexpected_end_of_file.3B_Synchronization_failed._Exiting...)

## Testované a funkčné čítačky

| Model čítačky | lsusb | eID klient |
| IDBridge CT30 | Gemalto (was Gemplus) GemPC Twin SmartCard Reader | Gemalto PC Twin Reader |
| Bit4id - miniLector EVO | Advanced Card Systems, Ltd ACR38 SmartCard Reader | ACS ACR 38U-CCID |

## Inštalácia

1\. Balíčky zo štandardných repozitárov [glibc](https://www.archlinux.org/packages/?name=glibc), [chrpath](https://www.archlinux.org/packages/?name=chrpath), [openssl](https://www.archlinux.org/packages/?name=openssl), [qt4](https://www.archlinux.org/packages/?name=qt4), [pcsclite](https://www.archlinux.org/packages/?name=pcsclite), [pcsc-tools](https://www.archlinux.org/packages/?name=pcsc-tools), [openssl](https://www.archlinux.org/packages/?name=openssl), [xterm](https://www.archlinux.org/packages/?name=xterm), [qt5-imageformats](https://www.archlinux.org/packages/?name=qt5-imageformats), [ccid](https://www.archlinux.org/packages/?name=ccid):

```
sudo pacman -S glibc chrpath openssl qt4 pcsclite pcsc-tools openssl xterm qt5-imageformats ccid

```

2\. AUR balíček [debtap](https://aur.archlinux.org/packages/debtap/):

```
yaourt debtap

```

3\. Aktualizácia debtap databázy:

```
sudo debtap -u

```

4\. eID klient aplikáciu stiahnuť zo stránky [Min. vnútra SR](https://eidas.minv.sk/TCTokenService/download/) - [balíček Debian 7.0 32-bit](https://eidas.minv.sk/TCTokenService/download/linux/debian/eidklient_i386_debian.tar.gz) alebo [balíček Debian 7.0 64-bit](https://eidas.minv.sk/TCTokenService/download/linux/debian/eidklient_amd64_debian.tar.gz)

5\. Prekonfigurovanie stiahnutého DEB balíčka na Arch linux kompatibilný formát a jeho inštalácia:

```
tar -zxf eidklient_*_debian.tar.gz
cd eID_klient/
debtap eidklient_*_debian.deb     `**# akékoľvek otázky pri spustení tohto príkazu stačí iba odklepnúť enterom**`
sudo pacman -U eidklient-*.pkg.tar.xz

```

6\. Oprava symbolických liniek na knižnice:

```
sudo ln -sf /usr/lib/qt/plugins/imageformats/libqtga.so /usr/lib/eidklient/
sudo ln -sf /usr/lib/qt4/plugins/imageformats/libqgif.so /usr/lib/eidklient/
sudo ln -sf /usr/lib/qt4/plugins/imageformats/libqico.so /usr/lib/eidklient/
sudo ln -sf /usr/lib/qt4/plugins/imageformats/libqjpeg.so /usr/lib/eidklient/
sudo ln -sf /usr/lib/qt4/plugins/imageformats/libqmng.so /usr/lib/eidklient/
sudo ln -sf /usr/lib/qt4/plugins/imageformats/libqsvg.so /usr/lib/eidklient/
sudo ln -sf /usr/lib/qt4/plugins/imageformats/libqtiff.so /usr/lib/eidklient/

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
cp /usr/lib/eidklient/*.desktop ~/Desktop

```

## Oficiálna príručka

Na stánkach [Min. vnútra SR](https://eidas.minv.sk/TCTokenService/download/) alebo [slovensko.sk](https://www.slovensko.sk/sk/na-stiahnutie)

## Používanie

### Prvé spustenie

```
eIdKlient

```

### Povolenie automatického spúšťania eID klienta

*   V prostredí aplikácie: dá sa povoliť pri prvom spustení aplikácie, alebo následne vo "Všeobecných nastaveniach".
*   Manuálne cez príkazový riadok: `cp /usr/lib/eidklient/startup/aplikacia-pre-autentifikaciu-el-dokladmi.desktop ~/.config/autostart/`

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