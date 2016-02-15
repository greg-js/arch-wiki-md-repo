Gamin è un progetto che reimplementa le specifiche [FAM](/index.php/FAM "FAM") con la nuova infrastruttura [inotify](/index.php?title=Inotify&action=edit&redlink=1 "Inotify (page does not exist)"). E' un progetto nuovo e il suo sviluppo è più attivo rispetto a quello di FAM, ne mantiene la compatibilità e di conseguenza è preferibile a quest'ultimo in ogni circostanza. Fa parte di [GNOME](/index.php/GNOME_(Italiano) "GNOME (Italiano)") ma non ha nessuna dipendenza da esso.

## Installazione

Per rimpiazzare FAM con Gamin, semplicemente rimuovete il pacchetto [fam](https://aur.archlinux.org/packages/fam/), ignorando le dipendenze, e installate [gamin](https://www.archlinux.org/packages/?name=gamin):

```
# pacman -Rd fam
# pacman -S gamin

```

Togliete `fam` dalla riga `DAEMONS` nell'[rc.conf](/index.php/Rc.conf "Rc.conf") se lo stavate usando, ovviamente. Gamin non necessita di essere inserito in questa lista.

## Links Esterni

*   [Gamin](http://en.wikipedia.org/wiki/Gamin)
*   [FAM, Gamin and inotify](http://www.noah.org/wiki/FAM,_Gamin,_inotify)