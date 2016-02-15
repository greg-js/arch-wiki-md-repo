Vim yra pažengusių vartotojų tekstinis redaktorius, kuris suteikia UNIX `vi` tekstinio redaktoriaus galią su daug geriau įgyvendintu įrankių sprendimu. Vim nėra toks paprastas tekstinis redaktorius, kaip nano ar pico. Jis reikalauja tam tikro laiko, norint jo išmokti ir žymiai daugiau laiko, norint išmokti profesionaliai dirbti su vim.

Vim yra suprojektuotas, norint sumažinti darbo krūvį pirštams ir riešams. Taip pat dirbant - visiškai nenaudoti pelytės. Tai gali pasirodyti keista, tačiau, kai tik susipažinsit artimiau su vim - suprasite, jog tai didelis pranašumas.

## Contents

*   [1 Ypatybės](#Ypatyb.C4.97s)
*   [2 Įdiegimas](#.C4.AEdiegimas)
*   [3 Naudojimas](#Naudojimas)
    *   [3.1 Redagavimo pagrindai](#Redagavimo_pagrindai)
    *   [3.2 Vaikštom aplinkui](#Vaik.C5.A1tom_aplinkui)
    *   [3.3 Komandų pakartojimas](#Komand.C5.B3_pakartojimas)
    *   [3.4 Trinimas](#Trinimas)

## Ypatybės

*   Vim yra labai galingas sunkioms redagavimo užduotims
*   Lankstus konfigūravimas
*   Paprastos ir tvirtos klavišų santrumpos
*   Sintaksės žymėjimas

## Įdiegimas

Jeigu norite turėti tik komandinės eilutės sąsają:

```
# pacman -S vim

```

Jeigu norite turėti ir GUI sąsają:

```
# pacman -S gvim

```

## Naudojimas

Pateiksime pačius pagrindus, kaip naudotis vim. Norint tęsti gilesnį pažinimą, galite naudoti `vimtutor`. Vim turi keturias skirtingas būsenas:

*   Command mode: klavišai yra interpretuojami kaip komandos.
*   Insert mode: klavišai yra tiesiogei vedami į bylą.
*   Visual mode: klaviškai pažymi, iškerpa arba kopijuoją tekstą.
*   Ex mode: papildomų komandų įvedimas ( pvz.: bylos išsaugojimas, teksto apkeitimas ir t.t. )

### Redagavimo pagrindai

Jeigu paleisite vim taip:

```
$ vim somefile.txt

```

pamatysite tuščią dokumentą ( turint omenyje, jog somefile.txt neegzistuoja. Jeigu jis egzistuoja - pamatysite kas jame ). Jūs negalėsite failo redaguoti iškarto - šiuo metu Jūs esate Command mode. Šioje būsenoje Jūs galite valdyti vim klavišų pagalba.

**Note:** Vim yra geras UNIX stiliaus produkto pavyzdys. Tai reiškia, jog jis nėra žibantis ir jis nelaikys Jūsų už rankos. Jis neateina kartu su įdiegtais segtukais ar žaidimais. Jis leis padaryti darbą, ir dar jį padaryti greitai. Verta prisiminti, jog yra skirtumas įvedant komandą didžiosiomis ir mažosiomis raidėmis. Kai kada didžiosiomis raidėmis įvestos komandos yra "pagerinos" mažųjų versijos (**s** pakeis raidę, **S** pakeis eilutę), kitais atvėjais - visiškai skirtingos komandos (**j** nuleis žymeklį žemyn, **J** sujungs dvi eilutes ).

Norint įvesti tekstą, paspauskite **i** mygtuką. **I** ( didžioji **i** ) įves tekstą į eilutės pradžią. Norint pridėti tekstą, paspauskite **a** mygtuką. **A** pastatys kursorių eilutės gale.

Grįžti į command mode galima bet kada ir iš bet kur, tereikia tik paspausti **Esc**.

### Vaikštom aplinkui

Norint Vim redaktoriuje perkelti kursorių dokumente galima naudoti krypties klavišus, tačiau tai nėra **vim way**. Toks sprendimas reikalauja patraukti dešinę ranką iš standartinės rašymo pozicijos link krypties klavišų. Kuomet perkelimas baigtas, dešinė ranka turi grįžti į rašymo poziciją. Tai tikrai nėra smagu..

Vim redaktoriuje, norint perkelti kursorių į apačią, tereikia paspausti raidę **j**. Kadangi raidė "j" karo į apačią - tai jinai ir perkelia kursorių į apačią. Norint perkelti kursorių atgal į viršų, reikia paspausti **k**. Kairė yra **h**, o dešinė yra **l** ( mažoji **L**).

**^** padės kursorių eilutės pradžioje, o **$** padės kursorių pabaigoje.

**Note:** **^** ir **$** yra plačiai naudojami reguliarių reiškinių išraiškose, norint pažymėti eilutės pradžią ir pabaigą. Reguliarios išraiškos yra labai galingos ir jos dažnai naudojamos *nix aplinkose, galbūt šiuo metu viskas gali pasirodyti šiek tiek per sudėtinga, tačiau vėliau pastebėsite, kas už visko slypi.

Norint peršokti vieną žodį, paspauskite klavišą **w**. **W** peršoks ten, kur jis mano esant žodžio pabaiga ( pavyzdžiui pabraukimo brūkšniai ar brūkšnys yra žodžio dalis ). Norint peršokti vienu žodžiu atgal, naudojamas **b**. Vėl gi, **B** peršoks ten, kur jis mano esant žodžio pabaigai. Norint peršokti į žodžio pabaigą, naudojami **e**, **E** įtraukia daugiau simbolių.

Norint peršokti vieną sakinį, naudojamas **(** simbolis. **(** darys tą patį, tik į kitą atgal. Norint peršokti visą paragrafą, naudojamas **{**, **}** darys viską tą patį tik atgal. (**Pastaba**: čia naudojami skliaustai yra komandos ( kaip **w** arba **e** ) - ne tos pačios, kurios yra naudojamos tekste ).

Norint perstumti ekraną į antraštę yra naudojamas **H**. **M _perstums ekraną iki vidurio, o_ **_L **iki apačios.** gg **perkels į bylos pradžią,** G_ perkels į pabaigą. **<ctrl>D** leis peržiūrėti bylą pagal puslapius.

### Komandų pakartojimas

Jeigu komandos pradžioje yra parašomas kažkoks skaičius - toji komanda bus vykdoma tiek kartų, koks skaičius buvo parašytas prieš tą komandą. Pavyzdžiui **3i**, tuomet "Help! " ir **Esc** spauzdins "Help! Help! Help!". O tarkim **2}** perkels Jus dviems paragrafais. Tokie komandų pakartojimai yra ypač naudingi tokioms komandoms, kurias tuojaus aptarsime.

### Trinimas

Raidė **x** tiesiog ištrins simbolį esantį po žymekliu. **X** ištrins visą žodį, esantį po žymekliu. Štai čia ir ateina smagumas kartojant komandas. **6x** ištrins šešis simbolius. **.** ( taškas ) pakartos prieš tai įvestą komandą. Tarkim, turite žodį "foobar" šešiuose vietose, tačiau gerai pagalvoję, nusprendžiate palikti tik "foo". Perkelkite savo žymekli iki "b" raidės ir įveskite **3x**, tuomet prie kito žodžio ir įveskite **.** ( taškas ).

Raidė **d** pasakys vim, kad ruošiatės kažką ištrinti. Po **d** įvedimo, reikia pasakyti vim'ui ką norite ištrinti. Štai čia galima pradėti naudoti judėjimo komandas. **dW** ištrins viską iki kito žodžio. **d^** ištrins viską iki eilutės pradžios. Komandų kartojimas gerai veikia ir su trinimo komanda: **3dW** ištrins tris sekančius žodžius. **D** ( didžioji ) yra **d$** sutrumpinimas, kuris ištrins viską iki eilutės pabaigos. **dd** ištrins visą eilutę.

Norint pakeisti esantį žodį, perkelkite savo žymeklį ant žodžio ir įveskite **cw** komandą. Tokia komanda ištrins žodį ir vim pereis į insert mode. Norint pakeisti tik vieną raidę, naudokite **r**.