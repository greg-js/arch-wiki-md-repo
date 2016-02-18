[Hamachi](https://en.wikipedia.org/wiki/Hamachi_(software) je komerčný (uzavretý) VPN software. Pomocou tohto nástroja môžete prepojiť dva alebo viac počítačov. Využíva sa pri tom ich vlastná virtuálna sieť pre priamu bezpečnú komunikáciu.

## Contents

*   [1 Inštalácia](#In.C5.A1tal.C3.A1cia)
*   [2 Konfigurácia](#Konfigur.C3.A1cia)
    *   [2.1 Hamachi 2 (beta)](#Hamachi_2_.28beta.29)
        *   [2.1.1 Používanie hamachi v príkazovom riadku ako bežný užívateľ](#Pou.C5.BE.C3.ADvanie_hamachi_v_pr.C3.ADkazovom_riadku_ako_be.C5.BEn.C3.BD_u.C5.BE.C3.ADvate.C4.BE)
        *   [2.1.2 Automatické nastavenie vlastnej prezývky](#Automatick.C3.A9_nastavenie_vlastnej_prez.C3.BDvky)
*   [3 Spustenie Hamachi](#Spustenie_Hamachi)
    *   [3.1 Systemd](#Systemd)
*   [4 GUI](#GUI)
*   [5 Tiež pozrite](#Tie.C5.BE_pozrite)

## Inštalácia

Nainštalujte balíček [logmein-hamachi](https://aur.archlinux.org/packages/logmein-hamachi/) z repozitára [AUR](/index.php/Arch_User_Repository "Arch User Repository").

## Konfigurácia

### Hamachi 2 (beta)

Konfigurácia Hamachi 2 sa nachádza v `/var/lib/logmein-hamachi/h2-engine-override.cfg` (ak súbor neexistuje, vytvorte ho). Nanešťastie nie je možné nájsť kompletný zoznam konfiguračných nastavení, takže ich tu je len zopár, ktoré je možné použiť.

#### Používanie hamachi v príkazovom riadku ako bežný užívateľ

Aby bolo možné používať `hamachi` v príkazovom riadku bez privilegovaných práv, pridajte nasledujúci riadok do konfiguračného súboru:

```
Ipc.User VaseUzivatelskeMeno

```

#### Automatické nastavenie vlastnej prezývky

Hamachi bežne používa ako prezývku názov počítača(hostname). Ak chcete, aby Hamachi automaticky nastavil vlastnú prezývku po svojom štarte, pridajte nasledujúci riadok do konfiguračného súboru:

```
Setup.AutoNick VasaPrezyvka

```

Prezývku je možné taktiež nastaviť manuálne využitím príkazového riadku `hamachi`:

```
# hamachi set-nick VasaPrezyvka

```

Toto je však nutné robiť po každom spustení Hamachi, takže ak chcete používať rovnakú prezývku, automatické nastavenie (popísané vyššie) je pravdepodobne výhodnejšie.

## Spustenie Hamachi

```
# systemctl start logmein-hamachi

```

Teraz už máte k dispozícii celý balík príkazov. Nie sú zoradené v žiadnom špeciálnom poradí a ich názvy celkom dobre popisujú ich vlastnosti.

```
$hamachi set-nick bob
$hamachi login
$hamachi create my-net tajneheslo
$hamachi go-online moja-siet
$hamachi list
$hamachi go-offline moja-siet

```

Pre získanie zoznamu všetkých príkazov spustite:

```
$hamachi ?

```

**Note:** Ak chcete vykonávať akcie v sietiach, v ktorých ste, tak sa uistite, že ste v nich "online".

### Systemd

AUR balíček [logmein-hamachi](https://aur.archlinux.org/packages/logmein-hamachi/) taktiež zahŕňa pekného malého [Systemd](/index.php/Systemd "Systemd") démona.

Nasledujúcim príkazom môžete prinútiť spustienie Hamachi po každom nabootovaní pomocou Systemd:

```
# systemctl enable logmein-hamachi

```

Ak chcete ihneď spustiť démona Hamachi, použite tento príkaz:

```
# systemctl start logmein-hamachi

```

## GUI

Na repozitári AUR sa nachádzajú aj nasledujúce grafické frontendy pre Hamachi:

*   [haguichi](https://aur.archlinux.org/packages/haguichi/) (Gtk3, Vala)
*   [quamachi](https://aur.archlinux.org/packages/quamachi/) (Qt4, Python)

## Tiež pozrite

*   [Domovská stránka projektu](https://secure.logmein.com/products/hamachi/)