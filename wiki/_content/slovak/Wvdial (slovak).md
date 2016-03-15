Existuje zopár spôsobov ako dať regulárnym používateľom možnosť používať <tt>wvdial</tt> na vytáčanie ppp pripojenia. Tento dokument popisuje tri rozličné spôsoby, navzájom sa líšiace obtiažnosťou nastavenia a dôsledkami na bezpečnosť.

Tento dokument predpokladá, že už máte <tt>wvdial</tt> správne nakonfigurovaný. Všetka nižšie-uvedená konfigurácia sa musí robiť ako <tt>root</tt>.

## Použitie <tt>suid</tt>

Toto je nepochybne najľahšie nastavenie, ale má obrovský dopad na bezpečnosť systému, keďže znamená, že *každý používateľ vie spúšťať wvdial ako root*. Zvážte prosím, či namiesto toho nepoužiť radšej jedno z ostatných riešení.

Nakoľko normálni pužívatelia nemôžu defaultne používať wvdial na vytáčanie ppp pripojenia, potrebujete zmeniť povolenia:

```
chmod u+s /usr/bin/wvdial

```

Mali by ste vidieť nasledujúce povolenia:

```
ls -l /usr/bin/wvdial
-rwsr-xr-x  1 root root 114368 2005-12-07 19:21 /usr/bin/wvdial

```

## Použitie skupiny <tt>dialout</tt>

Ďalší, trošku bezpečnejší spôsob, je vytvoriť skupinu nazvanú <tt>dialout</tt> (názov skupiny môže byť samozrejme aj iný) a dať členom tejto skupiny povolenie spúšťať <tt>wvdial</tt> ako root.

Najprv vytvorte skupinu a pridajte do nej používateľov:

```
groupadd dialout
gpasswd -a myuser dialout

```

Potom nastavte skupinu a povolenia na <tt>wvdial</tt>:

```
chgrp dialout /usr/bin/wvdial
chmod u+s,o= /usr/bin/wvdial

```

Mali by ste vidieť nasledujúce povolenia:

```
ls -l /usr/bin/wvdial
-rwsr-x---  1 root dialout 114368 2005-12-07 19:21 /usr/bin/wvdial

```

## Použitie <tt>sudo</tt>

<tt>sudo</tt> nepochybne ponúka najbezpečnejšiu možnosť, aby mohli regulárni používatelia zriadiť dial-up pripojenia použitím <tt>wvdial</tt>. Použiť sa to môže na udelenie povolenia pre celú skupinu alebo len jednotlivým používateľom. Ďalšou výhodou použitia <tt>sudo</tt> je, že potrebujete utrobiť nastavenie len raz, kdežto oba predošlé riešenia budú "od-urobené" keď sa nainštaluje nový balíček <tt>wvdial</tt>.

Tento dokument sa nebude púšťať do takých vecí, že čo všetko vie <tt>sudo</tt> ponúknuť, na to si prosím prečítajte návodové stránky (<tt>sudo</tt>, <tt>sudoers</tt>, <tt>visudo</tt>).

Použite <tt>visudo</tt> na úpravu súboru <tt>/etc/sudoers</tt>:

```
visudo

```

Ak chcete dať konkrétnemu používateľovi povolenie na spúšťanie <tt>wvdial</tt> ako root, pridajte nasledujúci riadok (samozrejme zmeňte meno používateľa):

```
myuser localhost = /usr/bin/wvdial

```

Ak chcete dať rovnaké povolenie všetkým členom skupiny (<tt>dialout</tt>):

```
%dialout localhost = /usr/bin/wvdial

```