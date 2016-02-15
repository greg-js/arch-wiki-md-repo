## Contents

*   [1 Introduzione](#Introduzione)
*   [2 Installazione](#Installazione)
*   [3 Configurazione](#Configurazione)
*   [4 Cambiare il tema](#Cambiare_il_tema)
*   [5 Risoluzione dei problemi](#Risoluzione_dei_problemi)
*   [6 Crediti](#Crediti)

## Introduzione

[Plymouth](http://fedoraproject.org/wiki/Releases/FeatureBetterStartup) è un progetto Fedora che serve a fornire un processo di boot grafico senza sfarfallio. Essa si basa sul [KMS](/index.php/KMS "KMS") (Kernel Mode-Setting) per impostare la risoluzione nativa del display il prima possibile, fornisce quindi una schermata iniziale fino al login manager.

**Note:** l'impostazione del [KMS](/index.php/KMS "KMS") è attualmente disponibile solo per processori Intel e schede grafiche ATI (come del Kernel 2.6.31). Plymouth può funzionare senza, ma può ricadere in text-mode.

**Attenzione:** Plymouth è attualmente in pesante fase di sviluppo e può contenere bug

## Installazione

Prima di utilizzare Plymouth, è necessario attivare l'impostazione del modulo del kernel. Si prega di fare riferimento alle istruzioni per le [schede ATI](/index.php/ATI#AMD.2FAti_cards_and_KernelModeSetting_.28KMS.29 "ATI") e per [le schede Intel](/index.php/Intel#KMS_.28Kernel_Mode_Setting.29 "Intel"). Entrambi sono richiesti per ricostruire l'immagine del kernel. Potete farlo anche in seguito, così da saltare questo passo per ora.

Se non si dispone di KMS è necessario utilizzare framebuffer.

**Note:** Questo può anche non funzionare. Plymouth è progettato per funzionare con KMS, anche se a volte può funzionare con il framebuffer.

Utilizza Plymouth da AUR. È meglio utilizzare la [versione git](https://aur.archlinux.org/packages.php?ID=26117), in quanto è la più aggiornata ed è in grado di lavorare meglio.

Istruzioni su come installare i pacchetti da AUR sono [disponibili qui](/index.php/AUR_User_Guidelines_(Italiano)#Installare_pacchetti_da_AUR "AUR User Guidelines (Italiano)")

## Configurazione

Prima di tutto bisogna impostare un tema per Plymouth. Plymouth viene fornito con vari temi:

1.  Fade-in: "tema semplice che sfuma dentro e fuori con le stelle scintillanti"
2.  Glow: "tema grafico con i progressi a torta seguito da un logo luminoso che emerge"
3.  Solar: "Spazio con stelle blu" e
4.  Spinfinity: "tema semplice che mostra un segno di rotazione all'infinito nel centro dello schermo"

Per impostare il tema desiderato con l'utility plymouth-set-default-theme, con:

```
$ su 
# plymouth-set-default-theme spinfinity 

```

Aggiungi Plymouth a hooks array in mkinitcpio.conf. Si deve aggiungere, dopo l'autodetect di udev per farlo funzionare.

```
# nano /etc/mkinitcpio.conf 

```

Aggiungi Plymouth a hooks array:

```
HOOKS="base udev **plymouth** autodetect ..."

```

Ricostruire l'immagine del kernel:

```
# mkinitcpio -p linux

```

Grub ora ha bisogno di lavorare con la configurazione di Plymouth:

```
# nano /boot/grub/menu.lst

```

Se avete attivato KMS, alla fine della riga kernel rimuovere qualsiasi istruzione VGA =. Se non si dispone di KMS è necessario utilizzare framebuffer e quindi sarà necessario aggiungere l'istruzione VGA = . In entrambi i casi, aggiungere "quiet splash" alla fine:

```
kernel /vmlinuz26 root=/dev/disk/by-uuid/xxxx ro quiet splash 

```

Infine, il demone Plymouth deve essere "killato" verso la fine del processo di boot. Questo può essere fatto con un comando in rc.local:

```
# nano /etc/rc.local 

```

ed aggiungere questa linea

/bin/plymouth quit --retain-splash

Riavviate, e godetevi il vostro nuovo start-up!

## Cambiare il tema

Come accennato in precedenza, Plymouth viene fornito con diversi temi. Se si desidera provarne un'altro, è facilissimo

```
# plymouth-set-default-theme NOME_TEMA 

```

Ricostruire l'immagine del kernel:

```
# mkinitcpio -p linux

```

E riavviare.

## Risoluzione dei problemi

Per qualche ragione in entrambi i miei computer (un portatile con una scheda grafica ATI e KMS, e il mio desktop con una scheda nVidia e framebuffer) il comando per uscire da Plymouth crea a sinistra piccoli quadrati neri intorno al bordo del mio schermo, che si sono fissati in modo permanente a qualsiasi finestra che passava sotto di loro. Il problema è stato causato dal mantenere l'opzione --retain-splash che è necessaria per mantenere il processo di boot. Se si riscontra questo problema, la soluzione è di "killare" Plymouth dopo il login, quando non è più necessario.

**Note:** Questo richiede l'uso di sudo. Le istruzioni per l'installazione e la configurazione di sudo le potete [trovare qui](/index.php/Sudo "Sudo")

Editare /etc/rc.local e rimuovere la linea "/bin/plymouth quit --retain-splash".

Modificare xinitrc e aggiungere una linea per "killare" Plymouth.

**Attenzione:** Questo deve essere al di sopra della linea che inizia la sessione (ad esempio, exec startxfce4) o la sessione del desktop **non si avvierà**

```
$ nano ~/.xinitrc 

```

Ed aggiungere

```
sudo /bin/plymouth quit & 

```

Si noti la mancanza di --retain-splash, i comandi addizionali e simboli per la terminazione. Questa operazione è necessaria in modo che lo script xinitrc andrà avanti per iniziare la sessione del desktop.

È ora necessario darsi il permesso di uccidere il demone Plymouth senza una password, modificando il file sudoers:

```
$ su 
# EDITOR=nano visudo

```

Ed aggiungere

```
TUO_USER       ALL=(ALL) NOPASSWD: /bin/plymouth 

```

Riavviate, e tutto sarà a posto.

## Crediti

Grazie a drf per il [suo post sul forum](https://bbs.archlinux.org/viewtopic.php?id=81406) su cui si basa questo articolo del wiki.