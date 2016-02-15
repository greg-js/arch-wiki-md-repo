## Contents

*   [1 Suddivisone dei pacchetti](#Suddivisone_dei_pacchetti)
    *   [1.1 Linee di guida](#Linee_di_guida)
    *   [1.2 Funzionamento](#Funzionamento)
*   [2 Posizione dei file](#Posizione_dei_file)

## Suddivisone dei pacchetti

I pacchetti che contengono i moduli del kernel dovrebbero essere trattati in modo particolare, per supportare quegli utenti che posseggono più di un kernel installato su un sistema.

Quando si prepara un pacchetto contenente un modulo del kernel e altri file di supporto, è bene tenerli separati.

### Linee di guida

Quando si prepara un pacchetto di questo tipo (prendendo come esempio driver NVidia) la convenzione è:

*   creare un pacchetto nvidia contenente solo i moduli compilati per il kernel vanilla;
*   creare un pacchetto nvidia-utils contenente i file di supporto;
*   assicurarsi che il pacchetto nvidia dipenda da nvidia-utils (a meno che ci sia una buona ragione per non farlo);
*   per gli altri kernel, come kernel26-mm, creare il pacchetto nvidia-mm contenente i moduli compilati per quel kernel;
*   assicurarsi che il pacchetto nvidia dipenda dall'attuale versione del kernel, ad esempio:

```
depends=('kernel26>=2.6.24-2' 'kernel26<2.6.25-0' 'nvidia-utils')

```

Nell'esempio è stato scritto 2.6.24-2, e non -1, perché c'è stato un importante cambiamento nella configurazione in un sottosistema del kernel che ha richiesto la ricompilazione di tutti i moduli. In casi come questo, bisogna sempre controllare le dipendenze, altrimenti alcune persone con versioni non aggiornate di kernel e di driver segnaleranno che quel modulo è difettoso.

### Funzionamento

Mentre i moduli compilati per diverse versioni del kernel si trovano sempre in directory diverse e quindi possono tranquillamente coesistere, i file di supporto, di norma, si trovano sempre in uno stesso posto. Se un pacchetto contiene moduli e file di supporto, sarà impossibile installare un modulo per più di un kernel a causa degli stessi file di supporto presenti nei pacchetti, e questo provoca conflitti.

La separazione dei moduli e dei file di supporto permettono di installare i pacchetti per più versioni di kernel nello stesso sistema, condividendo gli stessi file di supporto che si trovano in una sola posizione.

## Posizione dei file

Se un pacchetto include un modulo del kernel che è destinato a sostituire un modulo esistente con lo stesso nome, il modulo dovrebbe essere messo nella directory `/lib/modules/2.6.xx-ARCH/updates`. Quando verrà eseguito `depmod`, i moduli presenti in questa directory avranno la precedenza.