Quest'anno per Natale ho deciso di regalarmi una tavoletta grafica. Non disponendo di fondi a sufficienza per acquistare una Wacom mi sono rivolto altrove e sono riuscito a comprarmi una Trust TB-3100 ad un prezzo veramente bassissimo.

Purtroppo la Trust non rilascia driver per linux per le sue tavolette, ma vista l'utilità di questo dispositivo mi sono dato da fare per trovare una soluzione.

## Contents

*   [1 Introduzione](#Introduzione)
*   [2 Installazione](#Installazione)
*   [3 Configurazione](#Configurazione)
*   [4 Riavvio e Test della tavoletta](#Riavvio_e_Test_della_tavoletta)
*   [5 Risoluzione dei problemi](#Risoluzione_dei_problemi)
*   [6 Tips & Tricks](#Tips_.26_Tricks)

## Introduzione

Appena connessa la tavoletta dò un lsusb da terminale e noto con (grande) stupore che il produttore non è Trust ma Aiptek, una ditta Taiwanese che produce accessori per PC, tra i quali le tavolette grafiche.

La TB-3100 non è altro che una Aiptek Hyperpen 8000.

Questo tutorial vi spiegherà come configurare la vostra Archlinux box per utilizzare la tavoletta (si, anche la pressione).

**TESTATO CON** ID 08ca:0021 Aiptek International, Inc. APT-2 Tablet

xorg-server-1.5.3

hal-0.5.11

## Installazione

XORG I driver di xorg sono distribuiti già pacchettizzati, l'installazione avviene quindi con il gestore di pacchetti predefinito del sistema:

```
sudo pacman -S xf86-input-aiptek

```

## Configurazione

Da root, apriamo il file /etc/X11/xorg.conf e nella sezione "Modules" aggiungiamo la riga

```
Load "aiptek"

```

quindi salviamo e chiudiamo il file.

Ora, sempre da root creiamo un nuovo file /etc/hal/fdi/policy/10-aiptek.fdi e copiamoci dentro queste righe:

```
<?xml version="1.0" encoding="UTF-8"?>
<deviceinfo version="0.2">
 <device>
  <match key="info.product" contains="Aiptek">
   <merge key="input.x11_driver" type="string">aiptek</merge>
   <merge key="input.x11_options.SendCoreEvents" type="string">true </merge>
   <merge key="input.x11_options.USB" type="string">On</merge>
   <merge key="input.x11_options.Type" type="string">stylus</merge>
   <merge key="input.x11_options.Mode" type="string">absolute</merge>
   <merge key="input.x11_options.zMin" type="string">0</merge>
   <merge key="input.x11_options.zMax" type="string">511</merge>
  </match>
 </device>
</deviceinfo>

```

Quindi salviamo e chiudiamo anche questo file.

## Riavvio e Test della tavoletta

Bene, la tavoletta è installata, non ci resta che provarla.

	**IMPORTANTE!!!** LA TAVOLETTA DEVE ESSERE SCOLLEGATA QUANDO SI AVVIA IL PC OPPURE XORG ANDRA' IN CRASH!!!

Riavviate Xorg e hal (in alternativa riavviate il PC).

Potete semplicemente fare logout e da terminale dare

```
sudo /etc/rc.d/hal/restart

```

Quando il nostro desktop sarà pronto colleghiamo la tavoletta al PC ed è fatta!

## Risoluzione dei problemi

**D: Xorg non si avvia**

**R:** Per ragioni a me sconosciute Xorg va in crash se si cerca di avviarlo con la tavoletta connessa al PC. Quindi tutte le volte che fate un log out o che spegnete il PC dovrete rimuovere la tavoletta.

## Tips & Tricks

Per chi come me utilizza monitor in 16:9 utilizzare una tavoletta 4:3 è alquanto innaturale. Fortunatamente i driver open per linux sono più evoluti di quelli ufficiali sotto questo aspetto e ci permettono di impostare l'area attiva della tavoletta da utilizzare. A questo proposito è sufficiente attivare l'opzione KeepShape nel file /etc/hal/fdi/policy/10-aiptek.fdi che diventerà all'incirca così:

```
<?xml version="1.0" encoding="UTF-8"?>
<deviceinfo version="0.2">
 <device>
  <match key="info.product" contains="Aiptek">
   <merge key="input.x11_driver" type="string">aiptek</merge>
   <merge key="input.x11_options.SendCoreEvents" type="string">true </merge>
   <merge key="input.x11_options.USB" type="string">On</merge>
   <merge key="input.x11_options.Type" type="string">stylus</merge>
   <merge key="input.x11_options.Mode" type="string">absolute</merge>
   <merge key="input.x11_options.zMin" type="string">0</merge>
   <merge key="input.x11_options.zMax" type="string">511</merge>
   <merge key="input.x11_options.KeepShape" type="string">on</merge>
  </match>
 </device>
</deviceinfo>

```

Per le altre opzioni supportate potete dare un occhiata alle pagine del man:

```
man aiptek

```