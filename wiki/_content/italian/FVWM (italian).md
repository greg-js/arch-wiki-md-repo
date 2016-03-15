FVWM è stabile, potente, efficiente e basato su standard ICCCM e con supporto a multipli desktop virtuali per il sistema X Window. Si richiede un certo sforzo per imparare ad usarlo bene, dato che è quasi interamente configurato modificando file di configurazione con un editor di testo, ma coloro che persistono finiscono con un ambiente desktop che funziona esattamente come vogliono farlo funzionare. Lo sviluppo è attivo, e il supporto è eccellente. E per coloro che se lo chiedono, FVWM significa Feeble virtuale Gestione Window.

## Contents

*   [1 Installazione di FVWM](#Installazione_di_FVWM)
*   [2 Avviare FVWM](#Avviare_FVWM)
*   [3 Far emergere la sua Potenza](#Far_emergere_la_sua_Potenza)
*   [4 Riferimenti](#Riferimenti)

## Installazione di FVWM

[Installare](/index.php/Pacman_(Italiano) "Pacman (Italiano)") il pacchetto [fvwm](https://www.archlinux.org/packages/?name=fvwm) reperibile nei [repository ufficiali](/index.php/Official_Repositories_(Italiano) "Official Repositories (Italiano)").

Si può installare una versione pacthata [fvwm-patched](https://aur.archlinux.org/packages/fvwm-patched/) da [AUR](/index.php/Arch_User_Repository_(Italiano) "Arch User Repository (Italiano)") o se avete aggiunto il repositorio archlinuxfr (vedere [Unofficial user repositories](/index.php/Unofficial_user_repositories "Unofficial user repositories")) al vostro `/etc/pacman.conf`, è possibile installarlo regolarmente tramite [pacman](/index.php/Pacman_(Italiano) "Pacman (Italiano)").

```
# pacman -S fvwm-patched

```

## Avviare FVWM

FVWM verrà automaticamente aggiunto nella lista delle sessioni dei menu di kdm/gdm. Altrimenti aggiungere

```
exec fvwm2 

```

o

```
exec fvwm

```

al proprio `.xinitrc`.

Si veda [xinitrc](/index.php/Xinitrc_(Italiano) "Xinitrc (Italiano)") per i dettagli, come ad esempio la conservazione della sessione logind (e/o consolekit).

## Far emergere la sua Potenza

Al primo avvio di fvwm, ci si troverà con una configurazione inesistente, un desktop nero. Con un click sinistro sul desktop si sarà in grado di selezionare una configurazione di base di FVWM. Scegliere i moduli desiderati e procedere. Si vorrà senz'altro fare di più per creare il proprio desktop, quindi ecco alcuni consigli:

*   Anche se è superata, il guida per principianti Zensites FVWM [[1]](http://zensites.net/fvwm/guide/), aiuta a capire come funziona FVWM e come costruire la **vostra** configurazione di base.

*   La Wiki di Gentoo Linux ha una utile guida alla configurazione.[[2]](http://en.gentoo-wiki.com/wiki/FVWM/Configuration)

*   La homepage FVWM[[3]](http://fvwm.org/) include una documentazione[[4]](http://fvwm.org/documentation/), una FAQ [[5]](http://fvwm.org/documentation/faq/), collegamenti a un Wiki[[6]](http://fvwmwiki.xteddy.org/)) e al forum di FVWM [[7]](http://www.fvwmforums.org).

*   Il modo migliore per ottenere con il desktop che si desidera, è probabilmente quello di controllare le configurazioni del forum di FVWM [[8]](http://www.fvwmforums.org/phpBB3/viewforum.php?f=39&sid=468469f95f9a2a90cd9d5a0819d26eec) o su Box-Look.org,[[9]](http://www.box-look.org), dove si può scegliete quello che vi piace, installarlo, e modificarlo a piacere.

*   Per come lavorare sulle configurazioni che gli altri hanno fatto, può essere utile guardare i suggerimenti sui file di configurazione di Thomas Adam, lo sviluppatore FVWM più attivo.[[10]](http://www.fvwmforums.org/phpBB3/viewtopic.php?f=40&t=1505)

*   La pagina [[11]](http://web.archive.org/web/20070912061152/abdn.ac.uk/~u15dm4/fvwm/) sull'[Archivio Internet Archive](http://archive.org/) è obsoleta, ma sembra essere l'unica documentazione significativa online per fvwm-patched.

*   [FVWM-Crystal](/index.php?title=FVWM-Crystal&action=edit&redlink=1 "FVWM-Crystal (page does not exist)"), che è anche nei [repository di Arch](https://www.archlinux.org/packages/extra/any/fvwm-crystal/), è un add-on che rende FVWM molto più facile da configurare, anche se una configurazione più semplice incide su una flessibilità molto più limitata rispetto ad una di modifica diretta dei file di configurazione.

*   [XdgMenu](/index.php/XdgMenu "XdgMenu") è un programma utile per generare menu.

*   Fvwm funziona bene con [xcompmgr](/index.php/Xcompmgr "Xcompmgr") per ottenere semplici effetti di compositing.

*   Applicazioni utili sono simili a quelle suggerite per [Openbox](/index.php/Openbox_(Italiano) "Openbox (Italiano)") o [Fluxbox](/index.php/Fluxbox_(Italiano) "Fluxbox (Italiano)").

## Riferimenti

Links usati in questo tutorial:

1.  Zensites [FVWM guida per principianti](http://zensites.net/fvwm/guide/).
2.  Gentoo Wiki [guida di configurazione](http://en.gentoo-wiki.com/wiki/FVWM/Configuration).
3.  [FVWM Homepage](http://fvwm.org/).
4.  FVWM Homepage [documentazione](http://fvwm.org/documentation/).
5.  FVWM Homepage [FAQ](http://fvwm.org/documentation/faq/).
6.  [FVWM Wiki](http://fvwmwiki.xteddy.org/).
7.  [FVWM Forums](http://www.fvwmforums.org).
8.  [Configurazioni](http://www.fvwmforums.org/phpBB3/viewforum.php?f=39&sid=468469f95f9a2a90cd9d5a0819d26eec) presenti nel forum di FVWM.
9.  [Box-Look](http://www.box-look.org/).
10.  Thomas Adam su [errori comuni nella configurazione dei file](http://www.fvwmforums.org/phpBB3/viewtopic.php?f=40&t=1505).
11.  [Fvwm Patches](http://web.archive.org/web/20070912061152/abdn.ac.uk/~u15dm4/fvwm/) nell'[Archivio Internet](http://archive.org/).