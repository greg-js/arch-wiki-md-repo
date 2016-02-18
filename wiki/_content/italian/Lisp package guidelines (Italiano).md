## Contents

*   [1 Introduzione](#Introduzione)
*   [2 Struttura delle cartelle e nomi](#Struttura_delle_cartelle_e_nomi)
*   [3 ASDF](#ASDF)
*   [4 Packaging per versioni specifiche di Lisp](#Packaging_per_versioni_specifiche_di_Lisp)
*   [5 Cose che l'utente può fare](#Cose_che_l.27utente_pu.C3.B2_fare)

## Introduzione

Attualmente ci sono relativamente pochi pacchetti lisp disponibili nei repository di Arch. Questo significa che prima o poi, probabilmente, se ne aggiungeranno altri. E' dunque utile pensare, adesso che ce ne sono pochi, a come dovrebbero essere pacchettizzati. Questa pagina vuole essere un punto di riferimento sulle linee guida per i pacchetti lisp. E' bene comunque tenere a mente che questa non è una versione definitiva; se non siete d'accordo con alcune idee suggerite qui, sentitevi liberi di modificare la pagina e proporre qualcosa di migliore.

## Struttura delle cartelle e nomi

C'è almeno un pacchetto nel repository base (libgpg-errpor) che include dei file lisp, che sono posizionati in **/usr/share/common-lisp/source/gpg-error**. Per conformità, gli altri pacchetti lisp dovrebbero installare i propri files in **/usr/share/common-lisp/source/**. Ogni pacchetto dovrebbe avere la propria cartella, in modo da non creare disordine in questa cartella di base.

La cartella del pacchetto dovrebbe avere lo stesso nome del pacchetto lisp, e non dovrebbe essere nominata come nel repository Arch (o AUR). Questo si applica anche ai pacchetti costituiti soltanto da un file.

Ad esempio, un pacchetto Lisp chiamato **cl-ppcre** dovrebbe essere nominato **cl-ppcre** in AUR e risiedere in **/usr/share/common-lisp/source/cl-ppcre**. Un pacchetto chiamato **alexandria** dovrebbe essere nominato **cl-alexandria** in AUR e risiedere in in **/usr/share/common-lisp/source/alexandria**.

## ASDF

Cercare di evitare l'utilizzo di ASDF-Install per l'installazione di questi pacchetti di sistema.

ASDF può essere necessario o utile per la compilazione e/o il caricamento di pacchetti. In questo caso, è consigliabile che la cartella usata per il registro centrale (la posizione di tutti i link simbolici a *.asd) sia **/usr/share/common-lisp/systems/**.

Sono stati riscontrati problemi effettuando la compilazione con asdf come parte del processo di compilazione di un pacchetto. Si può risolvere attraverso l'uso di un file package.install di questo tipo:

```
# cl-ppcre.install
# arg 1:  the new package version
post_install() {
    echo "---> Compiling lisp files <---"

    clisp --silent -norc -x \
        "(load #p\"/usr/share/common-lisp/source/asdf/asdf\") \
        (pushnew #p\"/usr/share/common-lisp/systems/\" asdf:*central-registry* :test #'equal) \
        (asdf:operate 'asdf:compile-op 'cl-ppcre)"

    echo "---> Done compiling lisp files <---"

    cat << EOM

    To load this library, load asdf and then place the following lines
    in your ~/.clisprc.lisp file:

    (push #p"/usr/share/common-lisp/systems/" asdf:*central-registry*)
    (asdf:operate 'asdf:load-op 'cl-ppcre)
EOM
}

post_upgrade() {
    post_install $1
}

pre_remove() {
    rm /usr/share/common-lisp/source/cl-ppcre/{*.fas,*.lib}
}

op=$1
shift

$op $*

```

Naturalmente, per far funzionare questo esempio, è necessario avere un link simbolico a package.asd nella cartella di sistema di asdf. Durante la compilazione del pacchetto, questo dovrebbe risolvere...

```
pushd ${_lispdir}/systems
ln -s ../source/cl-ppcre/cl-ppcre.asd .
ln -s ../source/cl-ppcre/cl-ppcre-test.asd .
popd

```

...dove *$_lispdir* è **${startdir}/pkg/usr/share/common-lisp**. Creando un link con un path relativo piuttosto che assoluto, è possibile garantire che il link rimanga valido anche dopo l'installazione.

## Packaging per versioni specifiche di Lisp

Quando possibile, non creare pacchetti relativi ad una singola implementazione di lisp, cercare di essere indipendenti dall piattaforma per quanto il pacchetto lo permetta. Se, nonostante tutto, il pacchetto è specificatamente pensato per una singola implementazione di lisp (ad esempio, gli sviluppatori non hanno ancora aggiunto il supporto per altre implementazioni, o il pacchetto è stato sviluppato per fornire una funzionalità già presente in altre implementazioni), è corretto fare il proprio pacchetto Arch specifico per una particolare implementazione di lisp.

Per evitare di creare pacchetti specifici per una particolare implementazione, idealmente i pacchetti relativi a tutte le implementazioni (SBCL, cmucl, clisp) dovrebbero essere creati con il campo del PKGBUILD **common-lisp**. Comunque, non è il caso (e questo potrebbe creare problemi alla persone che preferiscono avere implementazioni multiple di lisp a portata di mano). Allo stesso tempo, si potrebbe (a) non rendere il proprio pacchetto dipendente da nessun lisp e includere nel package.install un messaggio che richieda l'installazione di lisp (non ottimale) opppure (b) seguire l'esempio del PKGBUILD di *sbcl* e includere un controllo condizionale per capire quale lisp è necessario (che è una soluzione complessa e, ancora, non ottimale). Altre idee sono le benvenute.

C'è anche da notare che se ASDF è necessario per installare/compilare/caricare il pacchetto le cose possono potenzialmente diventare più complicate a causa delle dipendenze, dal momento che SBCL viene fornito con asdf, clisp no ma c'è un pacchetto in AUR, e CMUCL potrebbe o meno fornirlo. (Purtroppo l'autore di questa pagina non conosce praticamente niente di CMUCL; mi dispiace).

Le persone che stanno attualmente mantenendo dei pacchetti lisp relativi ad una particolare implementazione di lisp ma che non necessitano di una particolare implementazione per funzionare potrebbero considerare di fare almeno una delle seguenti cose:

*   Modificare i propri PKGBUILD(s) per essere indipendenti dalla piattaforma, assicurandosi che qualcun'altro che non stia già mantenendo lo stesso pacchetto per un'implementazione diversa.

*   Offrirsi di farsi carico o aiutare con il mantenimento di versioni dello stesso pacchetto anche per altre implementazioni di lisp e combinarle in un unico pacchetto

*   Offire il proprio pacchetto al maintainer di una versione dello stesso pacchetto per un'altra implementazione, in modo da permettergli di combinarle in un unico pacchetto.

(Notare che joyfulgirl, l'autrice di questo documento, che attualmente mantiene le versioni per clisp di cl-ppcre e stumpwm; è disponibile sia a donare questi pacchetti ai maintainer delle versioni SBCL oppure mantenere la nuova versione indipendente dalla piattaforma da sola se i maintainer delle versione SBCL non se ne vogliono fare carico)

## Cose che l'utente può fare

*   Mantenere pacchetti lisp seguendo queste linee-guida.
*   Aggiornare e correggere queste linee-guida
*   Seguire i cambiamenti di questa pagina
*   Fornire (educatamente) consigli, pareri e suggerimenti sia su questo documento che sul lavoro delle persone
*   Tradurre questa pagina e futuri aggiornamenti a questa pagina.