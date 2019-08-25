Related articles

*   [Desktop environment (Italiano)](/index.php/Desktop_environment_(Italiano) "Desktop environment (Italiano)")
*   [Display manager (Italiano)](/index.php/Display_manager_(Italiano) "Display manager (Italiano)")
*   [Window manager (Italiano)](/index.php/Window_manager_(Italiano) "Window manager (Italiano)")
*   [GTK+ (Italiano)](/index.php/GTK%2B_(Italiano) "GTK+ (Italiano)")

Budgie è l'interfaccia grafica di default di Solus OS, scritta da zero. Oltre a offrire un design moderno, Budgie può emulare l'aspetto del desktop di GNOME 2.

In questo momento Budgie è in sviluppo, quindi potresti trovare bug e nuove funzionalità verranno aggiunge in seguito.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installare Budgie](#Installare_Budgie)
    *   [1.1 Avviare Budgie](#Avviare_Budgie)
*   [2 Utilizzo](#Utilizzo)
*   [3 Vedere anche](#Vedere_anche)

## Installare Budgie

Installa il pacchetto [budgie-desktop](https://www.archlinux.org/packages/?name=budgie-desktop) per l'ultima versione stabile o [budgie-desktop-git](https://aur.archlinux.org/packages/budgie-desktop-git/) per l'ultima git. È raccomandato installare le dipendenze opzionali per avere una completa esperienza con Budgie. È raccomandato anche installare il gruppo [gnome](https://www.archlinux.org/groups/x86_64/gnome/), dove contengono applicazioni necessari per l'utilizzo di Budgie.

### Avviare Budgie

Selezionare *Desktop Budgie* dal proprio [display manager](/index.php/Display_manager "Display manager") scelto, oppure modificare [xinitrc](/index.php/Xinitrc "Xinitrc") per includere Budgie Desktop:

 `~/.xinitrc` 
```
export XDG_CURRENT_DESKTOP=Budgie:GNOME
exec budgie-desktop

```

## Utilizzo

Puoi vedere le notifiche, settare il volume e modificare l'aspetto del desktop con la barra laterale chiamata "Raven", ci puoi accedere con la combinazione `Super+N` o cliccando l'indicatore di stato.

## Vedere anche

*   [Sito ufficiale di Solus](https://getsol.us/)
*   [Repository git ufficiale per lo sviluppo di Solus](https://git.solus-project.com/)
*   [Stato di sviluppo di Solus](https://build.solus-project.com/)