## Contents

*   [1 Algemeen](#Algemeen)
*   [2 Gebruik](#Gebruik)
    *   [2.1 Installeren en verwijderen van pakketten](#Installeren_en_verwijderen_van_pakketten)
    *   [2.2 Het systeem upgraden](#Het_systeem_upgraden)
    *   [2.3 De pakketten-lijst doorzoeken](#De_pakketten-lijst_doorzoeken)
    *   [2.4 Ander gebruik](#Ander_gebruik)
    *   [2.5 Configuratie](#Configuratie)
    *   [2.6 Repositories](#Repositories)
*   [3 Gerelateerde links](#Gerelateerde_links)

## Algemeen

Pacman is een van de hoogtepunten van Arch Linux. Het combineert een simpel binair pakket formaat met een eenvoudig te gebruiken bouwsysteem (zie ook [ABS](/index.php/ABS "ABS")). Pacman maakt het mogelijk om pakketten gemakkelijk te beheren en te veranderen. Het repository systeem maakt het gebruikers mogelijk om hun eigen repositories te maken, dit moedigt groei van de gemeenschap en meewerken aan (zie ook [AUR](/index.php/AUR "AUR")).

Pacman kan een systeem up-to-date houden door de pakkettenlijst te synchroniseren met de hoofdserver, zo is het voor een systeemadministrator gemakkelijk om het systeem te beheren. Het server/client model maakt het ook mogelijk om pakketten te downloaden en te installeren met een simpel commando, compleet met alle vereisten (vergelijkbaar met Debian's apt-get).

## Gebruik

Pacman is zowel een binaire als een broncode pakketten-tool. Het combineert verschillende ideeen van FreeBSD, Debian en Slackware om één veelzijdige maar toch gebruiksvriendelijke pakkettenbeheer-tool te maken. Pacman kan pakketten downloaden, installeren en upgraden, vanuit lokale en niet-lokale repositories en regelt daarbij de vereisten. Ook heeft het handige tools om zelf pakketten te maken.

### Installeren en verwijderen van pakketten

Voordat we beginnen met het installeren en upgraden van pakketten is het een goed idee om the lokale pakketten-database te synchroniseren met de niet-lokale repositories.

```
pacman -Sy

```

Om een pakket of een groep pakketten te installeren (met alle vereisten), gebruikt men het volgende commando.

```
pacman -S pakket_naam1 pakket_naam2

```

Soms zijn er meerdere versies van een pakket in verschillende repositories (bijvoorbeeld extra en testing). Men kan zelf specificeren welke te installeren

```
pacman -S extra/pakket_naam
pacman -S testing/pakket_naam

```

Om één pakket te verwijderen, en alle vereisten achter te laten:

```
pacman -R pakket_naam

```

Om ook alle vereisten te verwijderen, mits ze niet gebruikt worden door andere pakketten

```
pacman -Rs pakket_naam

```

### Het systeem upgraden

Pacman kan alle pakketten op het systeem updaten met één commando. Dit zal echter wel lang duren afhangend van hoe up-to-date het systeem is.

```
pacman -Su

```

NB: Het is ook mogelijk de repositories gelijk te synchroniseren

```
pacman -Syu

```

### De pakketten-lijst doorzoeken

Pacman kan de pakketten-lijst doorzoeken voor een lijst pakketten.

```
pacman -Ss pakketnaam

```

Om alleen geinstalleerde pakketten te doorzoeken:

```
pacman -Qs pakketnaam

```

Als het pakket gevonden is, is het mogelijk om er informatie over te weergeven.

```
pacman -Si pakketnaam
pacman -Qi pakketnaam

```

Om een lijst van bestanden binnen een pakket te weergeven:

```
pacman -Ql pakketnaam

```

Het is ook mogelijk om te kijken bij welk pakket een bestand hoort:

```
pacman -Qo /pad/naar/het/bestand

```

### Ander gebruik

Pacman kan ook nog andere dingen. Een pakket downloaden maar niet installeren:

```
pacman -Sw pakket-naam

```

Een lokaal pakket installeren

```
pacman -A /pad/naar/pakket/pakket_name-versie.pkg.tar.gz

```

De cache van pacman legen (/var/cache/pacman/pkg):

```
pacman -Scc

```

Voor verdere info kan men de commando **pacman --help** of **man pacman** gebruiken.

### Configuratie

De algemene opties staan in de [options] sectie. Hier kan gespecificeerd worden welke pakketten niet geupgrade moeten worden. Dit is handig voor belangrijke systeembestanden. De syntax is vrij simpel.

```
NoUpgrade   = etc/passwd etc/group etc/shadow etc/sudoers
NoUpgrade   = etc/fstab etc/raidtab etc/ld.so.conf
NoUpgrade   = etc/rc.conf etc/rc.local
NoUpgrade   = etc/modprobe.d/modprobe.conf etc/modules.conf
NoUpgrade   = etc/lilo.conf boot/grub/menu.lst

```

Een andere handige optie is IgnorePkg. Als men bijvoorbeeld een pakket heeft veranderd of gepatched kan met IngorePkg ervoor gezorgd worden dat Pacman deze niet upgrade wanneer een nieuwere versie beschikbaar is. Deze optie kan ook gebruik woorden voor grote pakketten om veel downloaden te voorkomen.

### Repositories

In deze sectie kan men instellen welke repositories gebruikt moeten worden. Deze kunnen direct gespecificeerd worden of uit een bestand worden gehaald. The laatste is handig voor repositories met veel mirrors.

```
[repository-name]
Server = [ftp://server.net/repo](ftp://server.net/repo)
[current]
# Add your preferred servers here, they will be used first
Include = /etc/pacman.d/current

```

Zie voor meer infomratie 'man pacman'

## Gerelateerde links

*   [Boost Pacman](/index.php/Boost_Pacman "Boost Pacman")
*   [Colored Pacman output](/index.php/Colored_Pacman_output "Colored Pacman output")
*   [Downgrade packages](/index.php/Downgrade_packages "Downgrade packages")
*   [Redownloading all installed packages](/index.php/Redownloading_all_installed_packages "Redownloading all installed packages")
*   [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository")
*   [Local repository HOW-TO](/index.php/Local_repository_HOW-TO "Local repository HOW-TO")
*   [Custom local repository with ABS and gensync](/index.php/Custom_local_repository_with_ABS_and_gensync "Custom local repository with ABS and gensync")
*   [Howto Upgrade via Home Network](/index.php/Howto_Upgrade_via_Home_Network "Howto Upgrade via Home Network")
*   [Pacman GUI Frontends](/index.php/Pacman_GUI_Frontends "Pacman GUI Frontends")