Related articles

*   [Desktop environment](/index.php/Desktop_environment "Desktop environment")
*   [Display manager (Česky)](/index.php/Display_manager_(%C4%8Cesky) "Display manager (Česky)")
*   [Window manager](/index.php/Window_manager "Window manager")
*   [GTK+](/index.php/GTK%2B "GTK+")

Budgie je výchozím pracovním prostředím operačního systému Solus. Kromě moderního vzhledu, může prostředí Budgie navozovat pocit práce jako v desktopovém prostředí GNOME 2.

V tuto chvíli je prostředí Budgie intenzivně vyvíjeno, takže se můžete setkat s menšími chybami spolu s tím, jak jsou přidávány nové funkce v průběhu vývoje.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalace](#Instalace)
    *   [1.1 Spuštění](#Spuštění)
*   [2 Práce s prostředím](#Práce_s_prostředím)
*   [3 Více informací](#Více_informací)

## Instalace

Nainstalujte balíček [budgie-desktop](https://www.archlinux.org/packages/?name=budgie-desktop) pro získání nejnovějšího stabilního vydání, případně [budgie-desktop-git](https://aur.archlinux.org/packages/budgie-desktop-git/) pro vývojovou verzi z GITu. Je doporučeno nainstalovat také doporučené závislosti pro získání mnohem komplexnějšího desktopového prostředí. Není na škodu doinstalovat celou skupinu balíčků [gnome](https://www.archlinux.org/groups/x86_64/gnome/), které jsou standardně součástí prostředí GNOME.

### Spuštění

Vyberte sezení *Budgie Desktop* ve Vašem oblíbeném správci přihlášení, nebo upravte nastavení v souboru [xinitrc](/index.php/Xinitrc "Xinitrc") pro zahrnutí prostředí Budgie po spuštění:

 `~/.xinitrc` 
```
export XDG_CURRENT_DESKTOP=Budgie:GNOME
exec budgie-desktop

```

## Práce s prostředím

Můžete sledovat oznamovací zprávy, upravovat hlasitost, změnit si vzhled a přizpůsobit si celkově prostředí dle Vašich potřeb pomocí postranního panelu pojmenovaného "Raven". Do panelu se lze dostat po stisknutí kláves `Super+N` nebo kliknutím na stavový aplet v hlavním panelu.

## Více informací

*   [Oficiální stránka projektu Solus](https://solus-project.com/)
*   [Oficiální GIT repozitář projektu Solus](https://git.solus-project.com/)