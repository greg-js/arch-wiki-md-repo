## Contents

*   [1 Arch Linux](#Arch_Linux)
*   [2 Privalumai](#Privalumai)
*   [3 Unikalus paketų tvarkymas](#Unikalus_paket.C5.B3_tvarkymas)
*   [4 Modernumas](#Modernumas)
*   [5 Paprastumas](#Paprastumas)
*   [6 Tolimesnis skaitymas](#Tolimesnis_skaitymas)

## Arch Linux

Arch Linux yra nepriklausomai kuriama i686/x86-64 bendruomeninė distribucija, paremta nuolatinio atnaujinimo (*angl. rolling-release*) modeliu, turinti dideles binarines saugyklas ir pilnavertį paketų palaikymą; tame tarpe ir tų paketų, kurie pasiekiami per portus. Ši distribucija skirta pažengusiems GNU/Linux naudotojams, o pagrindiniai jos kūrimo principai: minimalizmas, grakštumas, programinio teksto korektiškumas ir modernumas. 0.1 versija (Homer) išleista 2002 metų kovo 11 dieną.

## Privalumai

Arch sistema diegama naudojant minimalią aplinką (be grafinės vartotojo sąsajos), sukompiliuotą i686/x86-64 architektūroms. Arch yra lanksti ir paprasta UNIX tipo sistema. Jos kūrimo principai leidžia sistemą pritaikyti labai įvairiems poreikiams: nuo minimalios, valdomos per konsolę, sistemos iki pačios didžiausios ir funkcionaliausios, turinčios grafinę vartotojo sąsają, sistemos. Arch neperša nereikalingų bei nepageidaujamų paketų ir pažengusiems naudotojams suteikia galimybę patiems sukurti sistemą pagal savo poreikius. Naudotojas pats sprendžia, kokia turi būti Arch Linux sistema.

## Unikalus paketų tvarkymas

Arch yra paremta lengvai naudojama binarinių paketų sistema ([pacman](/index.php/Pacman "Pacman")), kuri leidžia atnaujinti visą sistemą naudojant tik vieną komandą. Pacman, parašyta naudojant programavimo kalbą **C**, nuo pat pradžių buvo kuriama taip, kad būtų paprasta ir labai greita. Arch taip pat teikia portų tipo paketų kūrimo sistemą ([Arch Build System](/index.php/Arch_Build_System "Arch Build System")), kuri leidžia lengvai sukurti ir įdiegti paketus naudojant pradinį programinį tekstą. Viskas daroma paprastai ir skaidriai. Dėl nuolatinio atnaujinimo modelio sistemą užtenka įdiegti tik vieną kartą ir ją nuolatos lengvai atnaujinti, neperrašinėjant visko iš naujo ir neatliekant sudėtingų naujesnės versijos patobulinimų.

## Modernumas

Arch Linux siekia palaikyti pačias naujausias stabilias programų versijas remiantis nuolatinio atnaujinimo modeliu. Šiuo metu palaikome supaprastiną pagrindinių paketų rinkinį minimalioms i686 ir x86-64 pagrindinėms sistemoms ir tūkstančius papildomų PKGBUILD programinių tekstų, skirtų sukurti ir parengti paketus naudojant pirminį programos tekstą. Arch suteikia nekeistas, "vanilines" programas (*angl. vanilla software*); paketai pateikiami nepakeisti - tokie, kokius pateikė pats autorius. Korekcijos daromos labai retai ir tik tais atvejais, kai norima išvengti labai rimtos sisteminės klaidos, kuri gali kilti dėl versijų nesiderinamumo. Arch įtraukia daugelį kitų naujovių, kurias naudoja GNU/Linux naudotojai, pavyzdžiui, šiuolaikines failų sistemas (Ext2/3/4, Reiser, XFS, JFS), LVM2/EVMS, programinį RAID masyvą, udev ir initcpio. Be to, pateikiami patys naujausi sisteminiai branduoliai (*angl. kernels*).

## Paprastumas

[The Arch Way](/index.php/The_Arch_Way "The Arch Way") yra filosofija, paremta paprastumu. Arch Linux pagrindinė sistema yra gana paprasta ir minimali, bet tuo pačiu ir funkcionali, GNU/Linux aplinka; Linux branduolys ir GNU įrankių rinkinys (*angl. toolchain*), gausybė papildomų, per komandinę eilutę pasieikiamų, įrankių, pavyzdžiui, **links** ar **Vi**. Neperkrauta, aiški ir paprasta pradinė sistema leidžia bendruomenei įvairiapusiai ją tobulinti ir plėsti.

Arch paprastos paleidimo (*angl. init*) sistemos sukūrimą labai įtakojo *BSD principas - viskas saugoma *viename faile* ([rc.conf](/index.php/Rc.conf "Rc.conf")). skirtingai nei nuo sudėtingų hierarchinių aplankų, turinčių begales sisteminių nuorodų kiekvienam eigos lygiui (*angl. run level*), struktūrų.

Sistema konfigūruojama redaguojant paprastus tekstinius failus.

## Tolimesnis skaitymas

Arch pagrindiniame tinklalapyje [https://www.archlinux.org/](https://www.archlinux.org/) galima rasti nuorodas į vartotojų forumus, oficialią dokumentaciją ir visą kitą informaciją, susijusią su Arch. Be to, siekdami geriau suprasti pagrindinius principus, galite perskaityti [The Arch Way](/index.php/The_Arch_Way "The Arch Way").