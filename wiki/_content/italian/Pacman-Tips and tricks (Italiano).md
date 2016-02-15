Per visualizzare i pacchetti e le dipendenze non più necessarie:

```
pacman -Qdtq

```

Per rimuoverle, dopo il comando precedente o direttamente, diamo:

```
# pacman -R $(pacman -Qdtq)

```

Per rimuovere gli orfani (ricorsivamente; **fare attenzione!**):

```
# pacman -Rs $(pacman -Qtdq)

```

*   Per reinstallare tutti i pacchetti del vostro sistema (se disponibili in un repository attivo):

```
#pacman -S $(pacman -Qq | grep -v "$(pacman -Qmq)")

```

## Salvataggio e recupero di una lista dei pacchetti installati per un ripristino veloce del software

È buona abitudine tenere un backup periodico di tutti i pacchetti installati con pacman. Se si è vittima di un crash che rende il sistema irrecuperabile, pacman può reinstallare i medesimi pacchetti in una nuova installazione senza difficoltà.

Per prima cosa, fare un backup dei pacchetti:

```
pacman -Qqe > pkglist

```

Salvare il file pkglist in una chiavetta USB o in un altro supporto.

Copiare il file pkglist nella nuova installazione e posizionarsi nella directory che lo contiene.

Digitare il comando seguente:

```
# pacman -S $(cat pkglist)

```

## Creare repository locali

[Pacman](/index.php/Pacman_(Italiano) "Pacman (Italiano)") 3 introduce un nuovo script chiamato **repo-add** che permette di generare i propri repository molto più facilmente. Utilizzare **repo-add --help** per ulteriori dettagli sul suo utilizzo.

Questo script è molto facile da utilizzare, anche per mantenere il proprio DB aggiornato. É sufficiente che conserviate tutti i pacchetti che volete nel vostro repository in una directory, ed eseguiate il seguente comando.

```
repo-add /percorso/al/repo.db.tar.gz *.pkg.tar.gz

```

Dove 'repo' è il nome del vostro repository personalizzato. L'ultimo parametro aggiungerà tutti i file pkg.tar.gz al vostro repository, quindi state attenti: se disponete di più versioni di un pacchetto nella directory, non è chiaro chi avrà la precedenza e finirà nel repository.

Per aggiungere un nuovo pacchetto (e rimuovere quello vecchio in caso esistesse), semplicemente eseguite

```
repo-add /percorso/al/repo.db.tar.gz pacchettodaaggiungere-1.0-1-i686.pkg.tar.gz

```

Se c'è un pacchetto che non volete più nel vostro repository, leggete di **repo-remove**

Una volta che avete creato il vostro repository locale, aggiungetelo al vostro **pacman.conf**. Il nome del vostro file db.tar.gz è il nome del repository. Potete fare riferimento ad esso direttamente utilizzando un indirizzo **file://**, o accedendo via ftp usando **[ftp://localhost/percorso/alla/directory](ftp://localhost/percorso/alla/directory)**.

Se possibile e sei disposto, aggiungi il tuo repository-personale alla nostra [lista di repository-personali non ufficiali](/index.php/Unofficial_user_repositories "Unofficial user repositories"), così che tutti gli altri utenti possano trovare ed installare i tuoi pacchetti.