[Midori](http://midoribrowser.org) je odlehčený internetový prohlížeč postavený na jádře webkit, který vyvíjí Christian Dywan. Midori je součástí projektu Goodies v rámci [Xfce](/index.php/Xfce "Xfce").

Mezi jeho hlavní přednosti patří:

*   Plná integrace do [GTK+](/index.php/GTK%2B "GTK+") 2 a GTK+ 3.
*   Rychlé vykreslování díky [WebKitGTK+](https://en.wikipedia.org/wiki/WebKit "wikipedia:WebKit") jádru.
*   Panely, okna a **správce sezení**.
*   Přizpůsobitelné a plně konfigurovatelné vyhledávání.
*   **Uživatelské skripty a styly**.
*   Intuitivní **správa záložek**.
*   Upravitelné a rozšiřitelné rozhraní.
*   Podpora **rozšíření** jako je AdBlock, Speed dial, atd.

## Contents

*   [1 Instalace](#Instalace)
*   [2 Rozšíření](#Roz.C5.A1.C3.AD.C5.99en.C3.AD)
    *   [2.1 AdBlock](#AdBlock)
    *   [2.2 Vyhledávání](#Vyhled.C3.A1v.C3.A1n.C3.AD)
    *   [2.3 Uživatelské skripty](#U.C5.BEivatelsk.C3.A9_skripty)
    *   [2.4 Flash plugin](#Flash_plugin)
*   [3 Tipy a Triky](#Tipy_a_Triky)
    *   [3.1 Flash Block](#Flash_Block)
    *   [3.2 Osobní filtry pro rozšíření AdBlock](#Osobn.C3.AD_filtry_pro_roz.C5.A1.C3.AD.C5.99en.C3.AD_AdBlock)
*   [4 Další informace](#Dal.C5.A1.C3.AD_informace)

## Instalace

GTK+ 2 verze prohlížeče Midori může být [nainstalována](/index.php/Pacman "Pacman") pomocí balíčku [midori](https://www.archlinux.org/packages/?name=midori), dostupného v [Official repositories (Česky)](/index.php/Official_repositories_(%C4%8Cesky) "Official repositories (Česky)").

Vývojové verze jsou k dispozici v uživatelském repozitáři [AUR](/index.php/AUR "AUR"):

*   [midori-gtk2-bzr](https://aur.archlinux.org/packages/midori-gtk2-bzr/) - pro GTK+ 2 verzi.
*   [midori-bzr](https://aur.archlinux.org/packages/midori-bzr/) - pro GTK+ 3 a na Webkitu založenou verzi.

## Rozšíření

### AdBlock

Pro povolení doplňku AdBlock jděte do **Menu > Nastavení > Rozšíření** a zaškrtněte volbu **Blokování reklamy**.

Rozšíření AdBlock pro prohlížeč Midori využívá stejné seznamy filtrů jako AdBlock pro prohlížeč Mozilla Firefox, tudíž můžete nalézt další seznamy filtrů na stránce [AdBlock Plus](http://easylist.adblockplus.org/en/). Lze také blokovat typově podobné obrázky na různých stránkách tak, že kliknete na daný obrázek pravým tlačítkem mysí a zvolíte "'Blokovat obrázek**.**

### Vyhledávání

Prohlížeč Midori podporuje vyhledávácí nástroje, tak oblíbené v ostatních prohlížečích. Jednotlivé vyhledávací nástroje mají své klávesové zkratky, takže je můžete jednoduše vyvolat v adresním řádku. Pro jejich úpravu klikněte pravý tlačítkem myši v adresním řádku a zvolte **Nastavit vyhledávací nástroje**.

Samozřejmostí je možnost přidat zkratky pro různé webové stránky. Například je možné nastavit aby po zadání zkratky **arch** do vyhledávacího pole a jejím potvrzení, se otevřela domovská stránka Archlinux.org. Jednoduše otevřete dialog **Nastavit vyhledávací nástroje**, zvolte **přidat** a vyplňte jednotlivá políčka (url je potřeba zadat ve tvaru [http://xx.xx](http://xx.xx)).

### Uživatelské skripty

Pro povolení uživatelských skriptů jděte do *Menu > Nastavení > Rozšíření* a zaškrtněte volbu *User addons*. Uživatelské skripty prohlížeče Midori jsou kompatibilní se skripty v rozšíření [Greasemonkey](https://addons.mozilla.org/en-US/firefox/addon/greasemonkey/) pro Mozillu Firefox. Obsáhlý přehled skriptů lze nalézt na stránce [userscripts.org](http://userscripts.org/).

Pro ruční instalaci je zapotřebí vytvořit adresář `~/.local/share/midori/scripts` a zkopírivat do něj Vaše skripty. Midori při svém spuštění kontroluje obsah tohoto adresáře a načte dostupné skripty.

### Flash plugin

Pro zprovoznění Flash pluginu nainstalujte [midori-flash](https://aur.archlinux.org/packages/midori-flash/) balíček z [AUR](/index.php/AUR "AUR") nebo postupujte dle návodu pro prohlížeč [Epiphany](/index.php/Epiphany "Epiphany").

## Tipy a Triky

### Flash Block

You can also get the common FlashBlock extension in the form of a user script either from [userscripts.org](http://userscripts.org/scripts/show/46673) or by using the [FlashBlock WannaBe script](http://rightfootin.blogspot.fr/2009/04/flashblock-wannabe.html), this script has to be installed in `~/.local/share/midori/scripts` and `~/.local/share/midori/styles`, for the JavaScript file and the CSS file, respectively.

### Osobní filtry pro rozšíření AdBlock

Jejich podpora v prohlížeči Midori je prozatím zákadní, můžete využít pouze předpřipravené seznamy nebo blokovat některé obrázky. Toto omezení lze obejít, tak že vytvoříte Vaše vlastní seznamy filtrů a sdělíte prohlížeči kde je má hledat.

Postup:

*   vytvořte adresář pro Vaše filtry `~/.local/share/midori/filters`
*   v tomto adresáři vytvořte nový soubor s obsahem, který chcete blokovat:

 `myadblockfilters.txt` 
```
[Adblock]
! Nadpis: Personal AdBlocker v1
! Poslední úprava: 31 Oct 2012 18:14 UTC
! Platnost: 365 days

! Komentáře jsou uvozeny vykřičníky

! Filtrovat lze určité webové prvky přímo
[http://forums.fedoraforum.org//forum/images/smilies/smile.gif](http://forums.fedoraforum.org//forum/images/smilies/smile.gif)

! Skupinu prvků lze filtrovat pomocí zástupných znaků
[http://ubuntuforums.org/images/rebrand/statusicon/subforum_*.gif](http://ubuntuforums.org/images/rebrand/statusicon/subforum_*.gif)

! Filtrovat lze také pomocí DOM tagů, id či tříd (např. CSS)
www.phoronix.com#DIV.phxcms_header_legacy
www.phoronix.com#DIV.phxcms_bar_align

```

*   jděte do *Menu > Nastavení > Rozšíření* a u rozšíření **Blokování reklamy** klikněte na ikonu nastavení a přidejte následující odkaz:

```
file://.local/share/midori/filters/myadblockfilters.txt

```

## Další informace

*   [Midori FAQ](http://wiki.xfce.org/midori/faq)