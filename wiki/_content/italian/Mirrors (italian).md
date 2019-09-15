Articoli correlati

*   [Mirroring](/index.php/Mirroring "Mirroring")
*   [pacman (Italiano)](/index.php/Pacman_(Italiano) "Pacman (Italiano)")
*   [Reflector](/index.php/Reflector "Reflector")

Questa pagina è una guida per la selezione e la configurazione dei "mirrors", e un elenco degli attuali mirrors disponibili.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Attivazione di un mirror specifico](#Attivazione_di_un_mirror_specifico)
*   [2 Mirror status](#Mirror_status)
*   [3 Scelta e selezione dei mirrors](#Scelta_e_selezione_dei_mirrors)
    *   [3.1 Elenco per velocità](#Elenco_per_velocità)
    *   [3.2 Elenco misto in base a velocità e stato](#Elenco_misto_in_base_a_velocità_e_stato)
    *   [3.3 Script per automatizzare l'uso di Pacman Mirrorlist Generator](#Script_per_automatizzare_l'uso_di_Pacman_Mirrorlist_Generator)
    *   [3.4 Uso di reflector](#Uso_di_reflector)
*   [4 Mirror ufficiali](#Mirror_ufficiali)
    *   [4.1 IPv6-ready mirrors](#IPv6-ready_mirrors)
*   [5 Mirror non ufficiali](#Mirror_non_ufficiali)
    *   [5.1 Globali](#Globali)
    *   [5.2 TOR Network](#TOR_Network)
    *   [5.3 Singapore](#Singapore)
    *   [5.4 Bulgaria](#Bulgaria)
    *   [5.5 Vietnam](#Vietnam)
    *   [5.6 Cina](#Cina)
    *   [5.7 Francia](#Francia)
    *   [5.8 Germania](#Germania)
    *   [5.9 Indonesia](#Indonesia)
    *   [5.10 Kazakistan](#Kazakistan)
    *   [5.11 Lituania](#Lituania)
    *   [5.12 Malesia](#Malesia)
    *   [5.13 Nuova Zelanda](#Nuova_Zelanda)
    *   [5.14 Polonia](#Polonia)
    *   [5.15 Russia](#Russia)
    *   [5.16 Sud Africa](#Sud_Africa)
    *   [5.17 Stati Uniti](#Stati_Uniti)
*   [6 Risoluzioni dei problemi](#Risoluzioni_dei_problemi)
    *   [6.1 Mirror non sincronizzati: pacchetti corrotti/file non trovati](#Mirror_non_sincronizzati:_pacchetti_corrotti/file_non_trovati)
        *   [6.1.1 Usare tutti i mirror](#Usare_tutti_i_mirror)
*   [7 Vedere anche](#Vedere_anche)

## Attivazione di un mirror specifico

Per attivare i mirrors, aprire `/etc/pacman.d/mirrorlist` e individuare la propria regione geografica. Decommentare i mirrors che si desidera utilizzare.

**Nota:** La velocità di banda di ftp.archlinux.org [è limitata a 50KB/s](https://www.archlinux.org/news/throttling-ftparchlinuxorg-rsyncarchlinuxorg/)

Esempio:

```
# Any
# Server = ftp://mirrors.kernel.org/archlinux/$repo/os/i686
**Server = http://mirrors.kernel.org/archlinux/$repo/os/i686**

```

Consultare [#Mirror status](#Mirror_status) e [#Elenco per velocità](#Elenco_per_velocità) per alcuni utili strumenti che aiutano nella scelta dei mirrors.

**Tip:** Decommentare 5 mirrors di preferenza e metterli in cima al file mirrorlist. In questo modo è più facile trovarli ed eventualmente spostarli se il primo mirror della lista avesse dei problemi. Inoltre agevola gli aggiornamenti dei mirrorlist all'interno del file stesso.

È anche possibile specificare i mirrors in `/etc/pacman.conf`. Per il repository *[core]*, l'impostazione di default è:

```
[core]
Include = /etc/pacman.d/mirrorlist

```

Per usare il mirror *HostEurope* come predefinito, aggiungerlo prima della riga `Include`:

```
[core]
**Server = ftp://ftp.hosteurope.de/mirror/ftp.archlinux.org/core/os/i686**
Include = /etc/pacman.d/mirrorlist

```

pacman tenterà ora di connettersi prima a questo mirror. Procedere con la stessa impostazione per *[testing]*, *[extra]*, e *[community]*, se possibile.

**Nota:** Se i mirror sono stati indicati direttamente in `pacman.conf`, ricordarsi di utilizzare lo stesso mirror per tutti i repository. In caso contrario, potrebbero essere installati pacchetti che sono incompatibili tra di loro, come linux da *[core]* e un vecchio modulo del kernel da *[extra]*.

## Mirror status

Verificare lo stato dei mirror Arch ed il loro livello di aggiornamento visitando il sito [http://www.archlinux.de/?page=MirrorStatus](http://www.archlinux.de/?page=MirrorStatus) o [https://www.archlinux.org/mirrors/status/](https://www.archlinux.org/mirrors/status/).

Si può generare una lista aggiornata dei mirror [qui](https://www.archlinux.org/mirrorlist/) e automatizzare il processo con uno [script](#Script_per_automatizzare_l'uso_di_Pacman_Mirrorlist_Generator), oppure installare eventualmente [Reflector](/index.php/Reflector "Reflector"), una utility che genera una mirrorlist usando la lista "Mirrorcheck"; un ulteriore alternativa è controllare il livello di aggiornamento manualmente così:

1.  scegliere un server ed esplorare "extra/os/";
2.  accedere a [https://www.archlinux.org/](https://www.archlinux.org/) in un'altra scheda o finestra del browser e,
3.  confrontare la data dell'ultima modifica della cartella `i686` sul mirror *[extra]* nella pagina principale, nel box *Package Repositories* a destra.

## Scelta e selezione dei mirrors

Se non si usa [reflector](https://www.archlinux.org/packages/?name=reflector), che offre la funzionalità di ordinare i mirror sia per livello di aggiornamento che per velocità, seguire questa dimostrazione di scelta manuale dei mirror.

### Elenco per velocità

È raccomandabile, al fine di trarre il massimo vantaggio, utilizzare il mirror locale più veloce, che può essere determinato tramite lo script bash incluso `/usr/bin/rankmirrors`.

Usare `cd` per spostarsi nella cartella `/etc/pacman.d`:

```
# cd /etc/pacman.d

```

Eseguire un backup del `/etc/pacman.d/mirrorlist` esistente:

```
# cp mirrorlist mirrorlist.backup

```

Modificare `mirrorlist.backup` decommentando i mirrors testing con rankmirrors:

```
# nano mirrorlist.backup

```

Facoltativamente eseguire la seguente riga `sed` per decommentare ogni mirror:

```
# sed '/^#\S/ s|#||' -i mirrorlist.backup

```

Per ultimo, i comandi per creare la graduatoria dei mirrors. L'operando `-n 6` significa solo l'output dei 6 mirrors più veloci:

```
# rankmirrors -n 6 mirrorlist.backup > mirrorlist

```

Eseguire `rankmirrors -h` per una lista di tutte le opzioni disponibili.

**Forzare pacman ad aggiornare la lista dei pacchetti**
Dopo la creazione/modifica di `/etc/pacman.d/mirrorlist` (manualmente o usando `rankmirrors`), eseguire il seguente comando:

```
# pacman -Syy

```

**Tip:** L'esecuzione di una doppia flag `--refresh` o `-y` forza pacman ad aggiornare tutti i pacchetti nella lista anche se sono considerati perfettamente aggiornati. Eseguire `pacman -Syy`, *ogni volta che si cambia mirror*, è una buona abitudine, e si evitano eventuali e sempre possibili problemi.

### Elenco misto in base a velocità e stato

Non è una buona idea quella di utilizzare solo i mirror più veloci, dal momento che potrebbe anche non essere ben aggiornato. La soluzione migliore sarebbe usare [#Elenco per velocità](#Elenco_per_velocità), che elenca i 6 mirror più veloci tramite il loro [#Mirror status](#Mirror_status).

Basta visitare uno o più [#Mirror status](#Mirror_status) link e ordinarli in base al più alto livello di aggiornamento. Spostare i mirror più aggiornati in cima a `/etc/pacman.d/mirrorlist` e se non sono aggiornati, semplicemente non usarli; ripetere il processo tralasciando i mirror non aggiornati. Così si ottiene un totale di 6 mirror ordinati per velocità e stato, lasciando da parte quelli obsoleti.

Quando si rileva una qualche irregolarità con i mirror, il procedimento descritto dovrebbe essere ripetuto. Lo si può anche rifare una volta ogni tanto, anche se non si riscontrano problemi, per mantenere aggiornato `/etc/pacman.d/mirrorlist`.

### Script per automatizzare l'uso di Pacman Mirrorlist Generator

È possibile utilizzare il seguente script di shell per aggiornare i propri mirror in base ai punteggi di [Pacman Mirrorlist Generator](https://www.archlinux.org/mirrorlist/). Se non si vive negli Stati Uniti, è possibile modificare la variabile `country`.

 `updatemirrors.sh` 
```
#!/bin/sh

[ "$UID" != 0 ] && su=sudo

country='US'
url="https://www.archlinux.org/mirrorlist/?country=$country&protocol=ftp&protocol=http&ip_version=4&use_mirror_status=on"

tmpfile=$(mktemp --suffix=-mirrorlist)

# Get latest mirror list and save to tmpfile
wget -qO- "$url" | sed 's/^#Server/Server/g' > "$tmpfile"

# Backup and replace current mirrorlist file (if new file is non-zero)
if [ -s "$tmpfile" ]
then
  { echo " Backing up the original mirrorlist..."
    $su mv -i /etc/pacman.d/mirrorlist /etc/pacman.d/mirrorlist.orig; } &&
  { echo " Rotating the new list into place..."
    $su mv -i "$tmpfile" /etc/pacman.d/mirrorlist; }
else
  echo " Unable to update, could not download list."
fi

# allow global read access (required for non-root yaourt execution)
chmod +r /etc/pacman.d/mirrorlist
```

**Nota:** É necessario copiare e salvare il testo in un file e accordargli i permessi di esecuzione tramite il comando `chmod +x`. Se non si è effettuato l'accesso come root lo script invocherà il comando `sudo` per poter essere eseguito con i giusti privilegi ed effettuare la rotazione del mirrorlist.

### Uso di reflector

È possibile utilizzare [Reflector](/index.php/Reflector "Reflector") per recuperare gli ultimi mirrorlist dalla pagina [MirrorStatus](https://www.archlinux.de/?page=MirrorStatus), filtrare i mirror più aggiornati, ordinarli in base alla velocità e sovrascrivere il file `/etc/pacman.d/mirrorlist`.

## Mirror ufficiali

La lista dei mirror ufficiali di Arch Linux è disponibile con il pacchetto [pacman-mirrorlist](https://www.archlinux.org/packages/?name=pacman-mirrorlist). Per ottenere un elenco mirror ancora più aggiornato, usare la pagina [Pacman Mirrorlist Generator](https://www.archlinux.org/mirrorlist/) sul sito ufficiale.

Nell'improbabile caso in cui ci si trovi senza nessun mirror configurato e `pacman-mirrorlist` non sia installato:

 `# wget -O /etc/pacman.d/mirrorlist [https://www.archlinux.org/mirrorlist/all/](https://www.archlinux.org/mirrorlist/all/)` 

Assicurarsi di decommentare il mirror preferito come descritto sopra, quindi:

```
# pacman -Syy
# pacman -S --force pacman-mirrorlist

```

Se si volesse vedere il proprio mirror aggiunto alla lista ufficiale, presentare una richiesta ai responsabili del progetto. Nel frattempo, aggiungerlo alla lista [#Unofficial mirrors](#Unofficial_mirrors) alla fine di questa pagina.

Se si verifica un errore che indica che la variabile $arch è usata ma non definita, aggiungere al proprio `/etc/pacman.conf`:

 `Architecture = x86_64` 
**Nota:** È anche possibile utilizzare il valore `auto` e `i686` per l'architettura.

### IPv6-ready mirrors

Il [*pacman mirrorlist generator*](https://www.archlinux.org/mirrorlist/?country=all&protocol=http&ip_version=6) può essere usato per generare una lista di mirrors IPv6.

## Mirror non ufficiali

Questi mirror *non* sono elencati in `/etc/pacman.d/mirrorlist`.

### Globali

*   [http://sourceforge.net/projects/archlinux/files/](http://sourceforge.net/projects/archlinux/files/) - *Non dispone di ISO delle release post 2006\. Usarlo solo per ISO datate.*

### TOR Network

*   [http://cz2jqg7pj2hqanw7.onion/archlinux](http://cz2jqg7pj2hqanw7.onion/archlinux)
*   [ftp://mirror:mirror@cz2jqg7pj2hqanw7.onion/archlinux](ftp://mirror:mirror@cz2jqg7pj2hqanw7.onion/archlinux)

### Singapore

*   [http://mirror.nus.edu.sg/archlinux/](http://mirror.nus.edu.sg/archlinux/)

### Bulgaria

*   [http://mirror.telepoint.bg/archlinux/](http://mirror.telepoint.bg/archlinux/)
*   [ftp://mirror.telepoint.bg/archlinux/](ftp://mirror.telepoint.bg/archlinux/)

### Vietnam

**FPT TELECOM**

*   [http://mirror-fpt-telecom.fpt.net/archlinux/](http://mirror-fpt-telecom.fpt.net/archlinux/)

### Cina

**CHINA TELECOM**

*   [http://mirror.lupaworld.com/archlinux/](http://mirror.lupaworld.com/archlinux/)

**CHINA UNICOM**

*   [http://mirrors.sohu.com/archlinux/](http://mirrors.sohu.com/archlinux/)

**Cernet**

*   [http://ftp.sjtu.edu.cn/archlinux/](http://ftp.sjtu.edu.cn/archlinux/) - *Shanghai Jiaotong University*
*   [ftp://ftp.sjtu.edu.cn/archlinux/](ftp://ftp.sjtu.edu.cn/archlinux/)
*   [http://mirrors.ustc.edu.cn/archlinux/](http://mirrors.ustc.edu.cn/archlinux/) - *University of Science and Technology of China*
*   [ftp://mirrors.ustc.edu.cn/archlinux/](ftp://mirrors.ustc.edu.cn/archlinux/)
*   [http://mirrors.tuna.tsinghua.edu.cn/archlinux/](http://mirrors.tuna.tsinghua.edu.cn/archlinux/) - *Tsinghua University*
*   [http://mirrors.4.tuna.tsinghua.edu.cn/archlinux/](http://mirrors.4.tuna.tsinghua.edu.cn/archlinux/) *(IPv4 only)*
*   [http://mirrors.6.tuna.tsinghua.edu.cn/archlinux/](http://mirrors.6.tuna.tsinghua.edu.cn/archlinux/) *(IPv6 only)*
*   [http://mirror.lzu.edu.cn/archlinux/](http://mirror.lzu.edu.cn/archlinux/) - *Lanzhou University*

### Francia

*   [http://delta.archlinux.fr/](http://delta.archlinux.fr/) - *Supporto al Delta Package. È necessario il pacchetto xdelta3 da [extra]*
*   [http://mirror.soa1.org/archlinux](http://mirror.soa1.org/archlinux)
*   [ftp://mirror:mirror@mirror.soa1.org/archlinux](ftp://mirror:mirror@mirror.soa1.org/archlinux)

### Germania

*   [http://ftp.uni-erlangen.de/mirrors/archlinux/](http://ftp.uni-erlangen.de/mirrors/archlinux/)
*   [ftp://ftp.uni-erlangen.de/mirrors/archlinux/](ftp://ftp.uni-erlangen.de/mirrors/archlinux/)
*   [http://ftp.u-tx.net/archlinux/](http://ftp.u-tx.net/archlinux/)
*   [ftp://ftp.u-tx.net/archlinux/](ftp://ftp.u-tx.net/archlinux/)
*   [http://mirror.michael-eckert.net/archlinux/](http://mirror.michael-eckert.net/archlinux/)
*   [http://linux.rz.rub.de/archlinux/](http://linux.rz.rub.de/archlinux/)

### Indonesia

*   [http://mirror.kavalinux.com/archlinux/](http://mirror.kavalinux.com/archlinux/) - *solo per l'indonesia*
*   [http://kambing.ui.ac.id/archlinux/](http://kambing.ui.ac.id/archlinux/)
*   [http://repo.ukdw.ac.id/archlinux/](http://repo.ukdw.ac.id/archlinux/)

### Kazakistan

*   [http://archlinux.kz/](http://archlinux.kz/)
*   [http://mirror.neolabs.kz/archlinux/](http://mirror.neolabs.kz/archlinux/)
*   [http://mirror-kt.neolabs.kz/archlinux/](http://mirror-kt.neolabs.kz/archlinux/)

### Lituania

*   [http://edacval.homelinux.org/mirrors/archlinux/](http://edacval.homelinux.org/mirrors/archlinux/) - *Solo per Lituania, no ISO*

### Malesia

*   [http://mirror.oscc.org.my/archlinux/](http://mirror.oscc.org.my/archlinux/)
*   [http://mirrors.inetutils.net/archlinux/](http://mirrors.inetutils.net/archlinux/) - *ISO and Core*

### Nuova Zelanda

*   [http://mirror.ihug.co.nz/archlinux/](http://mirror.ihug.co.nz/archlinux/)
*   [http://mirror.ece.auckland.ac.nz/archlinux/](http://mirror.ece.auckland.ac.nz/archlinux/) *solo NZ*

### Polonia

*   [ftp://ftp.icm.edu.pl/pub/Linux/dist/archlinux/](ftp://ftp.icm.edu.pl/pub/Linux/dist/archlinux/) - ICM UW
*   [http://ftp.icm.edu.pl/pub/Linux/dist/archlinux/](http://ftp.icm.edu.pl/pub/Linux/dist/archlinux/) - ICM UW
*   rsync://ftp.icm.edu.pl/pub/Linux/dist/archlinux/ - ICM UW

### Russia

*   [http://hatred.homelinux.net/archlinux/](http://hatred.homelinux.net/archlinux/) - *Vladivostok, without iso, with <sub>[3SPY](http://hatred.homelinux.net/wiki/proekty:3spy:start)</sub> project repos and [**mingw32**](http://hatred.homelinux.net/archlinux/mingw32/os/i686) repo*
*   [http://mirrors.krasinfo.ru/archlinux/](http://mirrors.krasinfo.ru/archlinux/) - *Krasnoyarsk, Classica-Service Ltd*

### Sud Africa

*   [http://ftp.sun.ac.za/ftp/pub/mirrors/archlinux/](http://ftp.sun.ac.za/ftp/pub/mirrors/archlinux/) - *Università di Stellenbosch*
*   [ftp://ftp.sun.ac.za/pub/mirrors/archlinux/](ftp://ftp.sun.ac.za/pub/mirrors/archlinux/)
*   [http://ftp.leg.uct.ac.za/pub/linux/arch/](http://ftp.leg.uct.ac.za/pub/linux/arch/) - *Università di Cape Town*
*   [ftp://ftp.leg.uct.ac.za/pub/linux/arch/](ftp://ftp.leg.uct.ac.za/pub/linux/arch/)
*   [http://mirror.ufs.ac.za/archlinux/](http://mirror.ufs.ac.za/archlinux/) - *Università di Free State*
*   [ftp://mirror.ufs.ac.za/os/linux/distros/archlinux/](ftp://mirror.ufs.ac.za/os/linux/distros/archlinux/)
*   [http://ftp.wa.co.za/pub/archlinux/](http://ftp.wa.co.za/pub/archlinux/) - *Web Africa Networks*
*   [ftp://ftp.wa.co.za/pub/archlinux/](ftp://ftp.wa.co.za/pub/archlinux/)
*   [http://archlinux.mirror.ac.za](http://archlinux.mirror.ac.za) - *TENET - Tertiary Education and Research Network of South Africa*
*   [ftp://archlinux.mirror.ac.za](ftp://archlinux.mirror.ac.za)

### Stati Uniti

*   [http://archlinux.linuxfreedom.com](http://archlinux.linuxfreedom.com) - *contiente molte ISO ma NON l'ultima 2011.08.19*
*   [http://mirror.pointysoftware.net/archlinux/](http://mirror.pointysoftware.net/archlinux/)

## Risoluzioni dei problemi

### Mirror non sincronizzati: pacchetti corrotti/file non trovati

Le problematiche relative ai mirror *out-of-sync* sottolineate in [questo post](https://www.archlinux.org/news/482/) possono essere già state risolte per molti utenti, ma nel caso si ripresentino di nuovo gli stessi problemi, provare semplicemente a vedere se sono presenti i pacchetti nel repository [testing].

Dopo aver sincronizzato con `pacman -Sy`, usare questo comando:

```
# pacman -Ud $(pacman -Sup | tail -n +2 | sed -e 's,/\(core\|extra\)/,/testing/,' \
                                              -e 's,/\(community\)/,/\1-testing/,')

```

Ciò potrebbe aiutare in quelle occasioni in cui i pacchetti nel mirror non siano stati sincronizzati a [core] o [extra], e resiedano ancora in [testing]. È completamente sicuro installare da [testing] in questo caso, poiché i pacchetti sono accompagnati dai numeri di versione e di rilascio.

In ogni caso, è meglio dare una rinfrescata ai mirror e alla sincronizzazione con `pacman -Syy` che ricorrere a un repository alternativo. Tuttavia, tutti, o alcuni mirror, potrebbero a volte non essere sincronizzati, in qualche misura.

#### Usare tutti i mirror

Per emulare il comportamento di `pacman -Su`, e cioè di scorrere l'intera lista dei mirror, utilizzare questo script:

 `~/bin/pacup` 
```
#!/bin/bash

# Pacman will not exit on the first error. Comment the line below to
# try from [testing] directly.
pacman -Su "$@" && exit

while read -r pkg; do
  if pacman -Ud "$pkg"; then
    continue
  else
    while read -r mirror; do
      pacman -Ud $(sed "s,.*\(/\(community-\)*testing/os/\(i686\|x86_64\)/\),$mirror\1," <<<"$pkg") &&
      break
    done < <(sed -ne 's,^ *Server *= *\|/$repo/os/\(i686\|x86_64\).*,,gp' \
           </etc/pacman.d/mirrorlist | tail -n +2 )
  fi
done < <(pacman -Sup | tail -n +2 | sed -e 's,/\(core\|extra\)/,/testing/,' \
                                        -e 's,/\(community\)/,/\1-testing/,')

```

## Vedere anche

*   [GitHub archweb mirrorlist.py](https://github.com/archlinux/archweb/blob/master/mirrors/views/mirrorlist.py) - codice sorgente del mirrorlist generator di archweb