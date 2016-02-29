Čia papasakosiu, kaip greitai įsidiegti Arch linux (toliau Arch) į kompiuterį. Kol kas remiuosi tik [angliška](/index.php/Quick_Archlinux_Install "Quick Archlinux Install") šio puslapio versija.

## Contents

*   [1 Įžanga](#.C4.AE.C5.BEanga)
*   [2 Būtina](#B.C5.ABtina)
*   [3 Įdiegimas iš Arch kompaktinio disko](#.C4.AEdiegimas_i.C5.A1_Arch_kompaktinio_disko)
    *   [3.1 Standžiojo disko dalijimas](#Stand.C5.BEiojo_disko_dalijimas)
    *   [3.2 Nustatykite skirsnių prijungimo vietas](#Nustatykite_skirsni.C5.B3_prijungimo_vietas)
    *   [3.3 Pasirinkite programas](#Pasirinkite_programas)
    *   [3.4 Įdiekite programas](#.C4.AEdiekite_programas)
    *   [3.5 Įdiekite sistemos branduolį](#.C4.AEdiekite_sistemos_branduol.C4.AF)
    *   [3.6 Pritaikykite konfigūraciją](#Pritaikykite_konfig.C5.ABracij.C4.85)
    *   [3.7 Įdiekite operacinės sistemos įkrovos programą](#.C4.AEdiekite_operacin.C4.97s_sistemos_.C4.AFkrovos_program.C4.85)
    *   [3.8 Ready to reboot](#Ready_to_reboot)
*   [4 Alternative Installing Methods](#Alternative_Installing_Methods)
*   [5 Pirmi žingsniai naujoje sistemoje](#Pirmi_.C5.BEingsniai_naujoje_sistemoje)

## Įžanga

Šis vadovėlis skirtas tiems, kurie dar nežino, kas yra Arch bei kokios jo galimybės. Tinka tiems, kurie jau turi savo kompiuteryje įdiegtą Windows OS ir nori įdiegti Arch nepažeisdami jos.

Microsoft Windows operacinė sistema turėtų būti įdiegta į pirmą disko skirsnį, nes kitaip grub nesugebės jo rasti.

## Būtina

*   Bazinis arba pilnas Arch įdiegimo kompaktinis diskas. [Siųskitės iš čia](https://www.archlinux.org/download/).
*   Nors vienas laisvas standusis diskas arba laisva vieta esamame skirsnyje. Su papildomais įrankiais (Windows Disk Management, Partition Magic ir t.t.), jūs galėsite sukurti atskirą skirsnį Arch

## Įdiegimas iš Arch kompaktinio disko

*   Įdėkite kompaktinį diską į jam skirtą vietą, perkraukite kompiuterį, ir nustatykite, kad kompiuterio pirmiausia krautųsi iš kompaktinių diskų įrenginio
*   Dar turėtumėt pamatyti [įprastą Arch įkrovos vaizdą](http://home.arcor.de/Langeland/1.png)
*   Paspauskite `Enter`
*   Pasibaigus įkrovos procesui, parašykite:

```
/arch/setup

```

Jūs dabar diegsite iš kompaktinio disko, todėl interneto prieiga nebūtina.

[Pagrindinis meniu](http://home.arcor.de/Langeland/6.png) atrodo taip.

### Standžiojo disko dalijimas

Jeigu turite tuščią kietą diską, galite iš karto pereiti prie automatinio dalinimo. Žinokite, kad tai ištrins visus jūsų standžiojo disko skirsnius! Jeigu norite išsaugoti esamus skirsnius, sekite nurodymus:

*   Pasirinkite paruošti standųjį diską (Prepare Hard-Drive)
*   Pasirinkite padalyti standųjį diską (Partition Hard-Drive)
*   Pasirinkite diską, kur norite įdiegti Arch
*   Su disko dalijimo programa cfdisk jūs galėsite sukurti naujus skirsnius standžiajame diske. Baziniam Arch įdiegimui reikalingi nors du skirsniai:

```
 * vienas swap skirsnis
 * vienas duomenų skirsnis

```

*   Jei jūsų Windows sistema įdiegta į pirmą skirsnį ir naudojama [ntfs](https://en.wikipedia.org/wiki/Ntfs "wikipedia:Ntfs") failų sistema, vaizdas turėtų atrodyti [taip](http://home.arcor.de/Langeland/9.png).

cfdisk

*   Jokiu būdu nelieskite ntfs (arba [vfat](https://en.wikipedia.org/wiki/Vfat "wikipedia:Vfat")) skirsnio, nes prarasite Windows skirsnį.
*   Skirsnio swap tipas žymimas numeriu 82.
*   Jei norite išeiti iš cfdisk nepalikdami jokių pakeitimų, pasirinkite quit, o norėdami išsaugoti - write.
*   Po dalijimo su cfdisk turėtumėte matyti tokį [skirsnių išdėstymą](http://home.arcor.de/Langeland/10.png).

### Nustatykite skirsnių prijungimo vietas

*   Parinkite 3 punktą: nustatyti failų sistemos prijungimo vietas
*   Pasirinkite skirsnį, kurį pažymėjote kaip swap
*   Pasirinkite kitą failų sistemą į kurią rašysite Arch (prijungimo vieta /)
*   Failų sistemą [ext3](https://en.wikipedia.org/wiki/Ext3 "wikipedia:Ext3")
*   Pasirinkite atlikta (done)

*Nepamirškite pasirinkt atlikta (done), nes kitaip nebūs atlikti jokie pakeitimai.*

### Pasirinkite programas

*   Pasirinkite kompaktinį diską
*   Dabar turėtumėte matyti [programų kategorijas](http://home.arcor.de/Langeland/11.png)
*   Pasirinkite Base kategoriją
*   Pagal nutylėjimą (default) pažymėti visus
*   Ok.

### Įdiekite programas

*   Tai labai paprasta: tiesiog paspauskite įdiegti (install), gerai ir visi pasirinkti paketai bus perkelti iš kompaktinio disko į failų sistemą kompiuteryje.

### Įdiekite sistemos branduolį

*   Pasirinkite "Kernel 2.6.x for IDE/SCSI systems".

### Pritaikykite konfigūraciją

*   Pasirinkite nano redaktorių keisti konfigūraciniams failams

**Paredaguokite /etc/rc.conf** jei norite pakeisti klaviatūros išdėstymą, pvz. lt yra lietuvių.

*   Jei naudojate maršrutizatorių, tai taip pat nurodykite faile /etc/rc.conf:

```
# Maršrutizatoriaus adresas
gateway="default gw 192.168.0.1"
ROUTES=(gateway) #Pašalinkite ! prie gateway

```

*   faile /etc/resolf.conf nurodykite savo naudojamą vardų serverį (dns)

```
nameserver 192.168.0.1

```

*   nano paprasta naudotis: Ctrl-o išsaugo pakeitimus, Ctrl-x išsaugo ir uždaro redaktorių.

**Paredaguokite** menu.lst*.

*   Čia nurodysite operacinių sistemų sąrašą, kurias galėsite įkrauti įjungę kompiuterį
*   Turėtumėte matyti [Menu.lst](http://home.arcor.de/Langeland/13.png)

*   Arch konfigūracijos dalis turėtų būti suderinta, o norėdami įkrauti Windows, pridėkite šias eilutes:

```
title Windows
rootnoverify (hd0,0)
chainloader +1

```

*   hd0,0 reiškia pirmą standųjį diską ir pirmą skirsnį, nenustebkite, nes skaičiuojama nuo 0, o ne nuo 1

Paspauskite Ctrl-O, Ctrl-X ir viską išsaugokite.

### Įdiekite operacinės sistemos įkrovos programą

*   Pasirinkite grub.
*   Choose the entry on top of the list.

### Ready to reboot

*   Exit the main menu, type reboot and the computer should reboot.
*   Remove the CD
*   You can choose between windows and arch, default is arch

## Alternative Installing Methods

*   [Fast Arch Install from existing Linux System](/index.php/Fast_Arch_Install_from_existing_Linux_System "Fast Arch Install from existing Linux System")
*   [The Official Arch Linux Installation Guide](https://www.archlinux.org/static/docs/arch-install-guide.html)

## Pirmi žingsniai naujoje sistemoje

*   Prisijunkite kaip naudotojas root.
*   Komanda `passwd` nustatykite root naudotojo slaptažodį.

```
# passwd

```

*   Kasdieniam naudojimui susikurkite naudotojo paskyrą, kuri neturi administratoriaus ar kitų svarbių sistemos procesų teisių (taip jūs, tyčia ar netyčia, negalėsite pažeisti ar kitaip sutrikdyti sistemos darbo). Naudotojo sukūrimui naudojama komanda adduser.

```
# adduser

```

Liko įdiegti jums reikalingas programas su Pacman. Mėgaukitės!