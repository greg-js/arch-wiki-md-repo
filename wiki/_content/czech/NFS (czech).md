## Contents

*   [1 Cíl tohoto návodu](#C.C3.ADl_tohoto_n.C3.A1vodu)
*   [2 Potřebné balíčky](#Pot.C5.99ebn.C3.A9_bal.C3.AD.C4.8Dky)
*   [3 Nastavení serveru](#Nastaven.C3.AD_serveru)
    *   [3.1 Soubory](#Soubory)
        *   [3.1.1 /etc/exports](#.2Fetc.2Fexports)
        *   [3.1.2 /etc/conf.d/nfs](#.2Fetc.2Fconf.d.2Fnfs)
        *   [3.1.3 /etc/hosts.allow](#.2Fetc.2Fhosts.allow)
    *   [3.2 Démoni](#D.C3.A9moni)
*   [4 Nastavení klienta](#Nastaven.C3.AD_klienta)
    *   [4.1 Soubory](#Soubory_2)
        *   [4.1.1 /etc/conf.d/nfs](#.2Fetc.2Fconf.d.2Fnfs_2)
    *   [4.2 Démoni](#D.C3.A9moni_2)
    *   [4.3 Automatické připojení při startu](#Automatick.C3.A9_p.C5.99ipojen.C3.AD_p.C5.99i_startu)
*   [5 Problémy](#Probl.C3.A9my)
    *   [5.1 Špatný výkon, pomalý přenos dat a/nebo vysoké zatížení serveru při používání NFS a gigabitu](#.C5.A0patn.C3.BD_v.C3.BDkon.2C_pomal.C3.BD_p.C5.99enos_dat_a.2Fnebo_vysok.C3.A9_zat.C3.AD.C5.BEen.C3.AD_serveru_p.C5.99i_pou.C5.BE.C3.ADv.C3.A1n.C3.AD_NFS_a_gigabitu)
    *   [5.2 Démon portmap selže při spouštění](#D.C3.A9mon_portmap_sel.C5.BEe_p.C5.99i_spou.C5.A1t.C4.9Bn.C3.AD)
*   [6 Odkazy](#Odkazy)

## Cíl tohoto návodu

Cílem tohoto článku je nastavení NFS serveru pro sdílení souborů přes síť. Pokusím se to popsat všechno co nejjednodušeji. **Poznámka: pro informace o NFSv4 se podívejte na článek [NFSv4](/index.php/NFSv4 "NFSv4")**

Portmap byl nahrazen rpcbind

## Potřebné balíčky

Pro server i klienta nám postačí jen pár balíčků. Základní podpora NFS je zkompilována v distribučním jádře.
Nainstalujte:

*   core/portmap
*   core/nfs-utils

Oba balíčky jsou v repozitáři [core] a měly by být součástí nové instalace ArchLinuxu

## Nastavení serveru

Nyní je nunté provést konfiguraci a spustit démony. Pro provedení následujících akcí potřebujete práva roota (nebo sudo).

### Soubory

#### /etc/exports

Tento soubor (/etc/exports) určuje, které adresáře nebo soubory na NFS serveru budou sdílené a nastavuje různá oprávnění.
Pár příkladů:

```
/soubory *(ro,sync) ; Přístup pro kohokoliv, pouze pro čtení
/soubory 192.168.0.100(rw,sync) ; RW přístup pro klienta s IP 192.168.0.100
/soubory 192.168.1.1/24(rw,sync) ;  RW přístup pro klienty s rozsahem IP 192.168.1.1 až 192.168.1.255

```

Pokud uděláte změny v /etc/exports po startu démonů, můžete tyto změny snadno aplikovat následujícím příkazem (bez nutnosti restartovat démona):

```
exportfs -r

```

Pokud se rozhodnete zpřístupnit veřejně NFS server pro čtení i zápis, můžete použít all_squash v kombinaci s anonuid a anongid. Například, pro nastavení oprávnění pro uživatele nobody ze skupiny nobody, můžete použít následující:

```
; Přístup čtení-zápis pro klienta s IP 192.168.0.100 s RW přístupem pro uživatele 99 s GID 99
/files 192.168.0.100(rw,sync,all_squash,anonuid=99,anongid=99))

```

To také znamená, že pokud chcete RW přístup do této složky, musí jí vlastnit nobody.nobody:

```
chown -R nobody.nobody /soubory

```

Další detaily o souboru exports najdete v manuálu k exports.

#### /etc/conf.d/nfs

Nastavením toho souboru ovlivňujete běh nfsd, mountd, statd a sm-notify. Výchozí Archlinuxový NFS skript požaduje pro statd zapnutou volbu --no-notify:

```
STATD_OPTS="--no-notify"

```

Ostatní nastavení můžete nechat jak je, nebo ho upravit dle požadavků. Více informací najdete v manuálu.

#### /etc/hosts.allow

Pro povolení přístupu na NFS server je nutné upravit /etc/hosts.allow.
Následující nastavení umožňuje přístup na NFS komukoliv:

```
 nfsd: ALL
 portmap: ALL
 mountd:ALL

```

Pro lepší nastavení se podívejte na hosts_access(5) v man.

### Démoni

Nyní můžete spustit server následujícími příkazy:

```
/etc/rc.d/portmap start
/etc/rc.d/nfslock start
/etc/rc.d/nfsd start

```

Pořadí spouštěných démonu mustí být zachováno!
Pro spuštění serveru při bootu, vložte tyto démony (tak jak jdou za sebou) do /etc/rc.conf.

## Nastavení klienta

### Soubory

#### /etc/conf.d/nfs

Pro klienta stačí nastavit pouze statd, ostatní volby se týkají serveru. NEPOUŽÍVEJTE v klientovi volbu --no-notify, pokud si nejste plně vědomi následků!!!

Více informací opět nalezneté v manuálových stránkách statd.

### Démoni

Nahoďte démony portmap a nfslock:

```
/etc/rc.d/portmap start
/etc/rc.d/nfslock start

```

Nezapomeňte, že je musíte spouštět v tomto pořadí.
Pro spuštění těchto démonů při bootu je přidejte do pole DAEMONS v /etc/rc.conf.

Pak připojte adresář jako obvykle:

```
mount server:/soubory /mnt/soubory

```

### Automatické připojení při startu

Pokud chcete síťové adresáře připojit při startu ujistěte se, že netfs je v DAEMONS v /etc/rc.conf a přidejte do **/etc/fstab** tyto řádky:

```
server:/soubory /mnt/soubory nfs defaults 0 0

```

Pokud chcete nastavit ručně velikost čtecích a zápisových paketů, můžete to také ovlivnit v fstabu. Hodnoty uvedené níže jsou výchozí hodnoty, pokud nejsou stanoveny jiné:

```
server:/soubory /mnt/soubory nfs rsize=32768,wsize=32768 0 0

```

Podívejte se do nfs man stránek, zde naleznete více informací, včetně všech možných volbách mountu.

## Problémy

### Špatný výkon, pomalý přenos dat a/nebo vysoké zatížení serveru při používání NFS a gigabitu

Tento problém je dán velikostí paketů používaných NFS, který způsobuje znatelnou fragmentaci na gigabitové síti. Můžete upravit chování pomocí mount parametrů rsize a wsize. Použití hodnot rsize=32768,wsize=32768 by mělo stačit. Tento problém nenastává na 100Mb sítích (a pomalejších) díky pomalejšímu přenosu paketů. Poznámka: výchozí hodnoty u NFSv4 jsou 32768\. Maximum je 65536\. Zvyšujte postupně hodnoty po 1024 dokud nedosáhnete maximální rychlosti přenosu.

### Démon portmap selže při spouštění

Ujistěte se, že v poli DAEMONS v /etc/rc.conf máte portmap PŘED netfs!

## Odkazy

[Velmi užitečné informace](http://publib.boulder.ibm.com/infocenter/pseries/v5r3/index.jsp?topic=/com.ibm.aix.prftungd/doc/prftungd/nfs_perf.htm)