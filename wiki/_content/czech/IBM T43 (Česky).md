Konečně jsem se dostal k tomu, abych začal pomalu sepisovat menší tutorial týkající se instalace Arch Linuxu na laptop IBM T43.

## Contents

*   [1 Instalace Arch Linuxu](#Instalace_Arch_Linuxu)
*   [2 Základní konfigurace](#Z.C3.A1kladn.C3.AD_konfigurace)
    *   [2.1 Aktualizace nástroje pacman](#Aktualizace_n.C3.A1stroje_pacman)
    *   [2.2 Nastavení firewallu](#Nastaven.C3.AD_firewallu)
*   [3 Instalace X serveru](#Instalace_X_serveru)

# Instalace Arch Linuxu

Nejprve si musíte stáhnout obraz CD, ze kterého budete systém instalovat. Osobně doporučuji stáhnout verzi **core**. Po instalaci této verze Arch Linuxu dostanete čistou instalaci, kterou si můžete následně upravit k obrazu svému. Tento postup doporučuji především pro "hračičky". Nicméně, tento článek vychází právě z instalace **core** verze Arch Linuxu.

Instalace probíhá bez vážnějších potíží. Pouze u současné verze Arch Linuxu (tj. verze 2009.08) mi instalátor nebyl schopen provést automatické rozdělení disku. Z neznámého důvodu skončil tento krok vždy s chybovým hlášením (je pravděpodobné, že to bylo způsobeno tím, že jsem Arch Linuxem přeinstalovával OS od Microsoftu). Ale to není žádný větší problém, protože instalátor nabízí možnost provést manuální rozdělení disku. Při zbývajících krocích instalace se žádné další potíže neobjevily.

Při instalaci systémového zavaděče **grub** jsem provedl první důležitou úpravu. Osobně mám rád, když už framebuffer běží v nativním rozlišení displeje na mém laptopu, což je 1400x1050 obrazových bodů. Proto je nutné upravit soubor <tt>/boot/grub/menu.lst</tt> (tuto možnost vám nabídne rovnou instalátor Arch Linuxu):

```
 $ # ...nějaké komentáře na začátku souboru
 $ 
 $ timeout   3   # 3 sekundy na výběr jiné než defaultní možnosti
 $ default   0   # defaultní možnost
 $ color light-blue/black light-cyan/blue # základní barevné schéma
 $ 
 $ # (0) Arch Linux
 $ title  Arch Linux Hi-Res
 $ root   (hd0,1)
 $ kernel /boot/vmlinuz26 root=/dev/disk/by-uid/_uid_disku_ ro **vga=835**
 $ initrd /boot/kernel26.img
 $ 
 $ # definice dalších možností v nabídce...

```

V ukázce souboru je tučným písmem vyznačena volba, díky které se framebuffer spouští v rozlišení 1400x1050.

# Základní konfigurace

## Aktualizace nástroje pacman

První věcí, kterou po čisté instalaci Arch Linuxu provedete je aktualizace aplikace **pacman**, která v této Linuxové distribuci slouží jako správce a instalátor balíčku. Aktualizaci provedete následujícími příkazy:

```
 $ pacman -S pacman
 $ pacman -Syu

```

## Nastavení firewallu

Pomocí následujících příkazů nastavíte základní pravidla do firewallu **iptables**:

```
 $ /etc/rc.d/iptables stop
 $ iptables -F
 $ 
 $ iptables -N open
 $ iptables -A INPUT -p icmp -j ACCEPT
 $ iptables -A INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT
 $ iptables -A INPUT -j open
 $ iptables -A INPUT -p tcp -j REJECT --reject-with tcp-reset
 $ iptables -A INPUT -p udp -j REJECT --reject-with icmp-port-unreachable
 $ iptables -A INPUT -s localhost -d localhost -j ACCEPT
 $ iptables -P INPUT DROP
 $ iptables -P FORWARD DROP
 $ /etc/rc.d/iptables save | start
 $ iptables -L

```

# Instalace X serveru

Instalaci X serveru provedete pomocí příkazu:

```
 $ pacman -S xorg xf86-video-ati

```