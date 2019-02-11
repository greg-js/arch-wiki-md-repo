I Locale sono utilizzati in linux per definire la lingua che l'utente utilizza. Così come i Locale definiscono il set di caratteri in uso, impostare il locale corretto è particolarmente importante se il linguaggio contiene caratteri non ASCII.

Il nome dei Locale sono definiti utilizzando il seguente formato:

```
<lingua>_<territorio>.<codeset>[@<modifificatori>]

```

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Abilitare il Locale necessario](#Abilitare_il_Locale_necessario)
    *   [1.1 Esempio IT Italiano](#Esempio_IT_Italiano)
*   [2 Impostare il locale a livello di sistema](#Impostare_il_locale_a_livello_di_sistema)
*   [3 Impostare un locale di ripiego](#Impostare_un_locale_di_ripiego)
*   [4 Impostazione dei locali utente](#Impostazione_dei_locali_utente)
*   [5 Impostare il collation](#Impostare_il_collation)
*   [6 Impostare il primo giorno della settimana](#Impostare_il_primo_giorno_della_settimana)
*   [7 Risoluzione dei problemi](#Risoluzione_dei_problemi)
    *   [7.1 Il mio terminale non supporta UTF-8](#Il_mio_terminale_non_supporta_UTF-8)
        *   [7.1.1 Xterm non supporta UTF-8](#Xterm_non_supporta_UTF-8)
        *   [7.1.2 Gnome-terminal o rxvt-unicode non supportano UTF-8](#Gnome-terminal_o_rxvt-unicode_non_supportano_UTF-8)
*   [8 Altre Fonti](#Altre_Fonti)

## Abilitare il Locale necessario

Prima che un locale possa essere utilizzato nel sistema, deve essere attivato. Per elencare tutte le versioni locali disponibili, utilizzare il comando:

```
$ locale -a

```

Per abilitare un locale, decommentare il nome del locale nel file `/etc/locale.gen`. Questo file contiene tutte le variabili locali che possono essere utilizzati sul sistema. Ripristinare il processo per disabilitare un locale. Dopo che i locali necessari sono abilitati, il sistema deve essere aggiornato con le nuove impostazioni locali:

```
# locale-gen

```

Per mostrare i locale che sono attualmente in uso, digitare:

```
$ locale

```

**Suggerimento:** Anche se è molto probabile che una sola lingua è utilizzata sul vostro computer, può essere utile o addirittura necessario consentire anche altri locali. Se si sta eseguendo un sistema multi-utente, con gli utenti che non parlano inglese, il loro locale individuale dovrebbe almeno essere supportata dal sistema.

### Esempio IT Italiano

Per prima cosa decommentare il seguente locale in `/etc/locale.gen`:

```
it_IT.UTF-8 UTF-8

```

Successivamente aggiornare il sistema come root:

```
# locale-gen

```

## Impostare il locale a livello di sistema

Per definire il locale a livello di sistema utilizzato sul sistema, impostare la variabile `LANG` in `/etc/locale.conf`:

`locale.conf` contiene un elenco per l'assegnazione delle variabile di ambiente in una nuova linea separata: oltre `LANG`, supporta tutte le variabili `LC_*`, con l'eccezione di `LC_ALL`.

**Nota:** `/etc/locale.conf` non esiste per impostazione predefinita e va creato manualmente.

**Suggerimento:** Se l'output del locale è di vostro gradimento durante l'installazione, è possibile salvare un po 'di tempo eseguendo : `# locale > /etc/locale.conf` mentre si è ancora in ambiente chroot.
 `/etc/locale.conf`  `LANG="it_IT.UTF-8"` 

Ecco un esempio di configurazione avanzata:

 `/etc/locale.conf` 
```
# Abilitare UTF-8 con impostazioni Italiane.
LANG="it_IT.UTF-8"

# Mantenere l'ordine predefinito (ad esempio i file che iniziano con un '.' 
# dovrebbe apparire all'inizio di un elenco di directory).
LC_COLLATE="C"

# Impostare la data (test con "date +%c")
LC_TIME="it_IT.UTF-8"
```

È possibile impostare la lingua di default in `locale.conf` anche usando `localectl`, per esempio:

```
# localectl set-locale LANG="it_IT.UTF8"

```

Si veda [localectl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/localectl.1) e [locale.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/locale.conf.5) per maggiori dettagli.

Queste modifiche avranno effetto dopo il riavvio del sistema e sarà impostato per le singole sessioni di login .

## Impostare un locale di ripiego

Nei programmi che utilizzano gettext per il rispetto delle traduzioni, l'opzione `LANGUAGE` è aggiunta alle consuete variabili. Questo permette agli utenti di specificare una [lista](http://www.gnu.org/software/gettext/manual/gettext.html#The-LANGUAGE-variable) di localizzazioni che verranno utilizzati in questo ordine. Se una traduzione per il locale preferito non è disponibile, un altro da un locale simile verrà usato al posto di quello di default. Ad esempio, un utente italiano potrebbe voler ricadere sull'ortografia britannica, piuttosto che su quella degli Stati Uniti:

 `~/.bashrc`  `export LANGUAGE="it_IT:en_GB:en"` 

oppure a livello di sistema

 `/etc/locale.conf` 
```
LANG="it_IT"
export LANGUAGE="it_IT:en_GB:en"
```

## Impostazione dei locali utente

Come abbiamo accennato in precedenza, alcuni utenti potrebbero voler definire un locale diverso da quello a livello di sistema locale.

Lo script `etc/profile.d/locale.sh` sostituisce il locale 'a livello di sistema"' con quello riscontrato in `~/.config/locale.conf`. Questo file non esiste per impostazione predefinita.

 `~/.config/locale.conf` 
```
LANG="it_IT.UTF-8"
LANGUAGE="it_IT.UTF-8"

```

## Impostare il collation

L'ordinamento (collation), è un po 'diverso. L'ordinamento è una stupida bestia poiché i vari locale si comportano in modo diverso. Per ovviare a potenziali problemi, Arch utilizza impostare `LC_COLLATE="C"` in `/etc/profile`. Tuttavia, questo metodo è obsoleto. Per abilitare questo comportamento, è sufficiente aggiungere la seguente variabile in `/etc/locale.conf`:

```
LC_COLLATE="C"

```

Ora il comando `ls` ordinerà i dotfile per primi, seguito da nomi di file che iniziano con maiuscole e minuscole. Si noti che senza una opzione `LC_COLLATE`, le applicazioni ripiegano sul valore di locale specificato da `LC_ALL` o `LANG`, ma l'impostazione di `LC_COLLATE` verranno sovrascritti se `LC_ALL` è impostato. Se ciò crea dei problemi, assicurarsi che LC_ALL non sia impostato aggiungendo quanto segue in `/etc/profile` :

```
 export LC_ALL=

```

Si noti che LC_ALL è l'unica variabile LC che **non** deve essere impostata in `/etc/locale.conf`.

## Impostare il primo giorno della settimana

In molti paesi il primo giorno della settimana è Lunedì. Per regolare questo comportamento, modificare o aggiungere le seguenti righe nella sezione `LC_TIME` in `/usr/share/i18n/locales/<tuo_locale>`:

```
week            7;19971130;5
first_weekday   2
first_workday   2

```

E aggiornare il sistema:

```
# locale-gen

```

## Risoluzione dei problemi

### Il mio terminale non supporta UTF-8

Sfortunatamente alcuni terminali non supportano UTF-8\. In questo caso dovreste utilizzare un terminale differente. Questa è una lista di alcuni terminali che hanno il supporto per UTF-8:

*   vte-based terminals
*   gnustep-terminal
*   konsole
*   [mlterm](/index.php/Mlterm "Mlterm")
*   [rxvt-unicode](/index.php/Rxvt-unicode "Rxvt-unicode")
*   [xterm](/index.php/Xterm "Xterm")

#### Xterm non supporta UTF-8

xterm supporta UTF-8 solo se eseguito come `uxterm` o `xterm -u8`.

#### Gnome-terminal o rxvt-unicode non supportano UTF-8

È necessario avviare queste applicazioni da un locale UTF-8 o cadrà il supporto ad UTF-8\. Abilitare il `en_US.UTF-8` locale (o il vostro locale UTF-8 alternativo) come spiegato precedentemente e impostarlo come la lingua predefinita, quindi riavviare.

## Altre Fonti

*   [Guida di Gentoo Linux sulla localizzazione](http://www.gentoo.org/doc/en/guide-localization.xml)
*   [http://wikigentoo.ksiezyc.pl/Locales.htm](http://wikigentoo.ksiezyc.pl/Locales.htm)
*   [Test interattivo ICU sull'ordinamento](http://demo.icu-project.org/icu-bin/locexp?_=en_US&x=col)
*   [Free Standards Group Open Internationalisation Initiative](http://www.openi18n.org/)
*   [*The Single UNIX Specification* definizione di locale](http://pubs.opengroup.org/onlinepubs/007908799/xbd/locale.html) dell'Open Group
*   [Variabili d'ambiente Locale](https://help.ubuntu.com/community/EnvironmentVariables#Locale_setting_variables)