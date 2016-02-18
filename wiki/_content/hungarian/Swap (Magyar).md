Az az oldal a cserehely és a lapozás használatához nyújt bevezetőt GNU/Linux-on. Emellett tárgyalja a cserehelyek és a cserefájlok készítésének és aktiválásának módját.

A [All about Linux swap space (Mindent a Linux cserehelyről)](http://www.linux.com/news/software/applications/8208-all-about-linux-swap-space):

	*A Linux a fizikai RAM (random access memory) darabokra osztja, melyeket lapnak nevezünk. A virtuális memória használata, azaz "swapping" az a folyamat, amikor egy memórialap a merevlemez előre meghatározott részére kerül, melynek neve cserehely, hogy ezáltal memória szabaduljon fel- A fizikai memória és a cserehely nagyságának összege nem más, mint a virtuális memória.*

## Contents

*   [1 Cserehely](#Cserehely)
*   [2 Cserehely (külön partíció)](#Cserehely_.28k.C3.BCl.C3.B6n_part.C3.ADci.C3.B3.29)
*   [3 Cserefájl](#Cseref.C3.A1jl)
    *   [3.1 Cserefájl létrehozása](#Cseref.C3.A1jl_l.C3.A9trehoz.C3.A1sa)
    *   [3.2 Cserefájl eltávolítása](#Cseref.C3.A1jl_elt.C3.A1vol.C3.ADt.C3.A1sa)
*   [4 CSerehely USB eszközön](#CSerehely_USB_eszk.C3.B6z.C3.B6n)
*   [5 a teljesítmény hangolása](#a_teljes.C3.ADtm.C3.A9ny_hangol.C3.A1sa)
    *   [5.1 Swappiness (lapozhatóság)](#Swappiness_.28lapozhat.C3.B3s.C3.A1g.29)
    *   [5.2 Prioritás](#Priorit.C3.A1s)

## Cserehely

A cserehely leggyakrabban egy lemezpartíció, de akár egy fájl is lehet. A felhasználó az Arch Linux telepítése során, de akár később is létrehozhatja, ha szükségessé válna. A cserehely általában tanácsos az 1 GB-nál kevesebb RAM-mal rendelkező rendszereknél, de inkább személyes választás kérdése a RAM-mal bővel ellátott rendszerek esetében (bár a lemezre való felfüggesztéskor még mindig szükség van rá).

Hogy leellenőrizzük a cserehely állapotát, futtassuk ezt a parancsot:

```
$ swapon -s

```

vagy ezt:

```
$ free -m

```

**Megjegyzés:** Nincs teljesítménybeli különbség az egybefüggő cserefájl és a külön cserehely partíció közt, mindkettőt azonosként kezelhetjük.

## Cserehely (külön partíció)

A cserehely, vagy "swap" partíció létrehozható a legtöbb GNU/Linux particionáló eszközzel (mint pl.: `fdisk`, `cfdisk`). A cserehelyek típusa a**82**.

Hogy efféle partíción cserehelyet hozzunk létre (mintha fájlrendszert formáznánk), a `mkswap` parancs használandó. Például:

```
# mkswap /dev/sda2

```

**Figyelem:** A partíció minden adata el fog veszni.

A *mkswap* eszköz alapértelmezetten UUID-t is létrehoz, de ha saját UUID-t akarunk adni neki, használjuk a `-U` zászlót.:

```
# mkswap -U *saját_UUID* /dev/sda2

```

Aktiváljuk a lapozást a partíción:

```
# swapon /dev/sda2

```

Hogy rendszerindításkor hasznájuk ezt a partíciót, jegyezzük be az [fstab](/index.php/Fstab "Fstab") fájlunkba:

```
/dev/sda2 none swap defaults 0 0

```

**Megjegyzés:** Ha TRIM támogatású SSD-t használunk, a cserehelyet jelölő sorban inkább használjuk a `defaults,discard` csatolási opciókat az [fstab](/index.php/Fstab "Fstab")-ban. Ha manuálisan aktiváljuk a *swapon* paranccsal, a `-d` vagy `--discard` paraméterrel ugyanerre jutunk. Lásd a `man 8 swapon`-t a részletekért.

## Cserefájl

A teljes partíció létrehozása melletti alternatívaként a cserefájl lehetővé teszi méretének menet közbeni változtatását is, no meg persze jóval könnyebben eltávolítható. Ez rendkívül fontos lehet, ha a szabad hely az elsődleges szempont (pl. kisebb méretű SSD-knél).

**Megjegyzés:** A Btrfs fájlrendszer nem támogatja a cserefájlok használatát. Ha ezt nem vesszük figyelembe, az a fájlrendszer összeomlásához vezethet. Jegyezzük meg, hogy Btrfs-en levő cserefájl használható, ha hurok eszközön (loop device) keresztül csatoljuk. Ez persze súlyosan csökkent lapozó-teljesítményt okoz.

### Cserefájl létrehozása

Root-ként használjuk a `fallocate` parancsot a cserefájl létrehozásához, mely tetszőleges méretű lehet (M = Megabájt, G = Gigabájt). A (`dd` is használható, de jóval több időt vesz igénybe. Példaképp, ha egy 512 MB nagyságú cserefájlt akarunk létrehozni:

```
# fallocate -l 512M /swapfile
vagy
# dd if=/dev/zero of=/swapfile bs=1M count=512

```

Adjuk meg a megfelelő engedélyeket (a mindenki által olvasható cserefájl hatalmas biztonsági rés)

```
# chmod 600 /swapfile

```

Miután megfelelő mérettel létrehoztuk, hozzuk létre rajta a swap fájlrendszert:

```
# mkswap /swapfile

```

Aktiváljuk:

```
# swapon /swapfile

```

Szerkesszük az `/etc/fstab`-ot, s hozzunk létre bejegyzést a cserefájlról:

```
/swapfile none swap defaults 0 0

```

### Cserefájl eltávolítása

**Figyelem:** a cserehelyet a systemd kezeli, és bizonyos idő után újra engedélyezi.

A cserefájl eltávolításához kapcsoljuk ki rajta a lapozást:.

Root-ként:

```
# swapoff -a

```

Távolítsuk el:

```
# rm -f /swapfile

```

## CSerehely USB eszközön

Hála a Linux által kínált modularitásnak, több cserehelyet is használhatunk, akár több eszközön is. A merevlemezünk nagyon megtelt, ideiglenesen USB eszközt is használhatunk erre a célra. Ennek a módszernek nagyon komoly hátrányai vannak:

*   Az USB eszközök lassabbak, mint egy merevlemez.
*   A flash-memóriák korlátozott számú írási ciklust bírnak ki. Cserehelyként használva igen hamar tönkremennek.
*   Ha más eszközt is csatlakoztatunk, a cserehely nem használható.

Hogy cserehelyként használható legyen, az USB flash eszközt először particionáljuk cserehelyként. Ehhez grafikus és konzol alapú eszközöket egyaránt használhatunk (GParted, fdisk). Bizonyosodjunk meg róla, hogy a partíciót cserehelyként jelöltök meg, mielőtt a partíciós táblát kiírnánk.

**Figyelem:** Legyünk mindig biztosak abban, hogy a partíciót megfelelő lemezre írjuk ki!

Ezek után nyissuk meg az `/etc/fstab`-ot.

Adjunk hozzá egy új bejegyzést, a már létező "swap" bejegyzés alatt, mely a mostani cserehelyet az USB meghajtóra helyezi át

```
UUID=... none swap defaults,pri=10 0 0

```

ahol az UUID az alábbi parancs kimenetéből állapítható meg

```
ls -l /dev/disk/by-uuid/ | grep /dev/sdc1

```

Az sdc1-et helyettesítsük a fentebb létrehozott swap partíció betűjelével. `sdb1`

**Tip:** Azért használunk UUID-t, mert a rendszerhez csatolt újabb USB eszközök módosíthatják a betűjel szerinti sorrendet.

Végezetül adjuk a

```
pri=0

```

paramétert az *eredeti* swap bejegyzés mögé, hogy az fstab megtanulja: csak akkor kell használni a merevlemez eredeti cserehelyét, ha az USB eszköz megtelt.

Ez az útmutató másfajta memóriakártyákkal is működik, mint például az SD kártyák, etc.

## a teljesítmény hangolása

A cserehely értékeit hangolhatjuk, hogy nagyobb teljesítményre tegyünk szert.

### Swappiness (lapozhatóság)

A *swappiness* [sysctl](/index.php/Sysctl "Sysctl") paraméter jelképezi a rendszermag hajlandóságát, hogy használja, vagy épp kerülje a cserehelyet. Ennek értéke 0 és 100 közötti lehet. Ha alacsonyra állítjuk, csökkenti a lapozás használatát, ezzel sokszor reaktívabbá a rendszert.

 `/etc/sysctl.d/99-sysctl.conf` 
```
vm.swappiness=1
vm.vfs_cache_pressure=50
```

Hogy teszteljük, és megtanuljuk, ez miért is így működik, ebben a [cikkben](http://rudd-o.com/en/linux-and-free-software/tales-from-responsivenessland-why-linux-feels-slow-and-how-to-fix-that) nézzünk körül.

[Ez](http://askubuntu.com/questions/103915/how-do-i-configure-swappiness) pedig egy Q&A poszt, mely sokat elárul a lapozhatóságról.

### Prioritás

Ha több mint egy cserefájllal vagy partícióval dolgozunk, jobb, ha mindegyikük számára megadunk egy bizonyos prioritási értéket (0-tól 32767-ig). A rendszer elsőként a magasabb prioritási értékú cserehelyet fogja használni, s csak utána az alacsonyabbakat. Így ha például van egy gyorsabb lemezünk (`/dev/sda`) és egy lassabb (`/dev/sdb`), a magasabb értéket adjuk meg a cserehelynek, mely a gyorsabb lemezen található. Ezt az fstab-ban a `pri` paraméterrel tehetjük meg:

```
/dev/sda1 none swap defaults,pri=100 0 0
/dev/sdb2 none swap defaults,pri=10  0 0

```

Vagy a `-p` (vagy `--priority`) paraméterrel, amikor a *swapon* parancsot használjuk:

```
# swapon -p 100 /dev/sda1

```

Ha két, vagy több helynek ugyanakkor a prioritása, s ezek legmagasabb prioritású elérhető eszközök, a lapozás allokációja round-robin alapon oszlik meg köztük.