FAM o File Alteration Monitor è un demone usato dai Desktop Environments come [GNOME](/index.php/GNOME "GNOME") ed [Xfce](/index.php/Xfce "Xfce") per monitorare e notificare i cambiamenti che avvengono nel filesystem. FAM è usato inoltre dal demone Samba server. KDE non sfrutta piu' FAM, ma si basa su inotify, un altro sottosistema di monitoring del filesystem integrato nel kernel e che non richiede particolari configurazioni.

**Attenzione:** FAM oramai non è più sviluppato!!! usare se potete [Gamin](/index.php/Gamin_(Italiano) "Gamin (Italiano)"). Gamin è invece una reimplementazione delle specifiche di FAM piu' recente, piu' manutenuta e piu' semplice da configurare.

Il sistema di monitoring del filesystem è usato per:

*   Aggiornare automaticamente i menù di sistema quando nuove applicazioni vengono installate
*   Aggiornare le finestre dei diversi filemanager quando il contenuto visualizzato varia

## Contents

*   [1 Installazione di FAM](#Installazione_di_FAM)
*   [2 Configurazione](#Configurazione)
*   [3 Start/Stop Manuale](#Start/Stop_Manuale)
*   [4 Altre risorse](#Altre_risorse)

## Installazione di FAM

Come root, digitate il seguente comando da una console:

```
# pacman -S fam

```

## Configurazione

Per far si che il demone FAM sia automaticamente caricato all'avvio del sistema, deve essere aggiunto alla lista dei demoni in /etc/rc.conf. Come utente root aprite il file */etc/rc.conf* con il vostro editor preferito:

```
# nano /etc/rc.conf

```

Aggiungete **fam** alla lista DAEMONS, ad esempio:

```
DAEMONS=(syslog-ng network ... **fam** ...)

```

Salvate e chiudete l'editor. Riavviate la macchina.

## Start/Stop Manuale

Se volete avviare manualmente FAM senza dover riavviare, aprite un terminale e come utente root digitate:

```
# /etc/rc.d/fam start

```

Per fermarlo:

```
# /etc/rc.d/fam stop

```

## Altre risorse

[FAM](https://en.wikipedia.org/wiki/File_alteration_monitor "wikipedia:File alteration monitor")

[FAM, Gamin and inotify](http://www.noah.org/wiki/FAM,_Gamin,_inotify)