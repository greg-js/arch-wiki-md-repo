**Osiris** è un sistema gratuito per la creazione di portali che non necessitano di un server centrale, sicuri, indistruttibili e anonimi. Nei portali creati in Osiris tutti gli utenti hanno gli stessi diritti e poteri, ovvero non esistono gerarchie amministrative a cui i classici sistemi centralizzati ci hanno abituato (tale tipologia viene comunque supportata).

## Contents

*   [1 Installazione](#Installazione)
    *   [1.1 Installazione Tramite Binari](#Installazione_Tramite_Binari)
    *   [1.2 Installazione Tramite AUR](#Installazione_Tramite_AUR)
*   [2 Configurazione](#Configurazione)
*   [3 Visibilità sul web (Isis)](#Visibilit.C3.A0_sul_web_.28Isis.29)
    *   [3.1 Isis](#Isis)
*   [4 Links Esterni](#Links_Esterni)

## Installazione

È installabile tramite AUR oppure direttamente dal sito del produttore che fornisce binari compatibili con archlinux.

### Installazione Tramite Binari

È disponibile sia a 32 che a 64 bit. Per installarlo è sufficiente scaricarlo dalla sezione sezione [download](http://www.osiris-sps.org/download/) ed estrarre l'archivio.

Per Lanciare il programma spostatevi nella cartella in cui l'avete estratto e lanciate il comando

```
# ./osiris 

```

### Installazione Tramite AUR

Dal momento che il pachhetto risulta essere *orfano* questo metodo non è consigliato, utilizzatelo solo se avete avuto dei problemi con l'istallazione tramite binari.

Scaricate il [PKGBUILD](https://aur.archlinux.org/packages.php?ID=25621) , compilatelo ed installatelo.

Per Lanciare il programma lanciate da qualsiasi terminale il comando

```
# osiris-sps

```

## Configurazione

**Osiris** non necessita di particolari configurazioni, offre un opzionale supporto per l'utilizzo di proxy facilmente impostabili fin dalla procedura automatica del primo avvio. A seconda del modo in cui vi connettete ad internet potreste aver bisogno di aprire le porte per l'applicazione, avrete bisogno di due porte una per le connessioni web e nel caso lo abbiate abilitato una per il p2p.

Una volta Installato e configurato il programma è raggiungibile all'indirizzo :[http://127.0.0.1:34471](http://127.0.0.1:34471)

## Visibilità sul web (Isis)

Normalmente i siti creati con **Osiris** non sono raggiungibili da motori di ricerca o simili. Per ovviare a ciò possiamo usare il programma Isis che offre i seguenti servizi.

Servizi generali (dal sito ufficiale)

Link - Link user-friendly e/o link permanenti (permalink). Osiris HTTP url - Mostra un link di invito Osiris, nel formato osiris. Utile per pubblicare dei link di invito ove i link osiris:// non sono permessi, ad esempio sulla maggior parte dei motori di forum tradizionali (vBulletin, Invision, SMF etc.) Redirection - Alternativa a servizi di anonimizzazione del referrer, come ad esempio anonym.to Check - Controllo per verificare se Osiris (o un generico servizio TCP) è raggiungibile dall'esterno.

Servizi di appoggio ad Osiris

Osiris si appoggia ad un Isis per avere una serie di servizi di appoggio. Nella configurazione di Osiris, è possibile cambiare l'Isis di riferimento, che di default punta all'Isis del progetto ([http://isis.kodeware.net](http://isis.kodeware.net)). Tali servizi non pregiudicano il funzionamento di Osiris, che pertanto rimane un software server-less. Questi servizi sono disabilitati di default nelle nuove installazioni di Isis. E' possibile attivarli e anche specificare un'altro Isis a cui redirigere le richieste sui singoli servizi (che di default puntano anch'essi dall'Isis del progetto ([http://isis.kodeware.net](http://isis.kodeware.net)). Nota importante: i servizi devono essere accessibili da SSL, cioè da un url https://

Clock - Osiris di default conosce l'ora esatta attraverso il protocollo NTP. Può succedere che tale protocollo non sia accessibile, o che il server di riferimento sia down. In tal caso, contatta Isis per sapere l'ora esatta. Update System - Osiris richiama questo url per sapere se sono disponibili nuove versioni del software Osiris, per un aggiornamento automatico. Bootstrap - Gestione degli indirizzi IP di bootstrap.

### Isis

Per l'installazione, la configurazione e l'uso di Isis vi rimando alla sua pagina sul wiki: [Isis](/index.php?title=Isis&action=edit&redlink=1 "Isis (page does not exist)")

## Links Esterni

[Sito Ufficiale di Osiris e Isis](http://www.osiris-sps.org/)