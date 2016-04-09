Da quando Intel fornisce e sviluppa driver open source, le schede video Intel sono essenzialmente plug-and-play.

Per un elenco completo dei modelli GPU-Intel e dei corrispondenti chipset e CPU, si veda [questo confronto su wikipedia](https://en.wikipedia.org/wiki/Comparison_of_Intel_graphics_processing_units "wikipedia:Comparison of Intel graphics processing units").

**Nota:** Le schede basate su chip PowerVR (serie [GMA 500](/index.php/Poulsbo "Poulsbo") e [GMA 3600](/index.php/Intel_GMA3600 "Intel GMA3600")) non sono supportate dai driver opensource

## Contents

*   [1 Installazione](#Installazione)
*   [2 Configurazione](#Configurazione)
*   [3 KMS (Kernel Mode Setting)](#KMS_.28Kernel_Mode_Setting.29)
*   [4 Opzioni di risparmio energetico del modulo base](#Opzioni_di_risparmio_energetico_del_modulo_base)
*   [5 Consigli e trucchi](#Consigli_e_trucchi)
    *   [5.1 Scegliere il metodo di accelerazione](#Scegliere_il_metodo_di_accelerazione)
    *   [5.2 Disattivare la sincronizzazione verticale (VSYNC)](#Disattivare_la_sincronizzazione_verticale_.28VSYNC.29)
    *   [5.3 Configurare lo scaling mode](#Configurare_lo_scaling_mode)
    *   [5.4 Problema KMS: la console è limitata ad una piccola porzione di schermo](#Problema_KMS:_la_console_.C3.A8_limitata_ad_una_piccola_porzione_di_schermo)
    *   [5.5 Decodifica H.264 su chip GMA 4500](#Decodifica_H.264_su_chip_GMA_4500)
    *   [5.6 Impostare il valore di gamma e luminosità](#Impostare_il_valore_di_gamma_e_luminosit.C3.A0)
*   [6 Risoluzione dei Problemi](#Risoluzione_dei_Problemi)
    *   [6.1 Schermo vuoto durante l’avvio, alla fase "Loading modules"](#Schermo_vuoto_durante_l.E2.80.99avvio.2C_alla_fase_.22Loading_modules.22)
    *   [6.2 Video tearing](#Video_tearing)
    *   [6.3 Freeze/crash del server X con i driver intel](#Freeze.2Fcrash_del_server_X_con_i_driver_intel)
    *   [6.4 Aggiungere risoluzioni non rilevate](#Aggiungere_risoluzioni_non_rilevate)
    *   [6.5 Colori alterati](#Colori_alterati)
    *   [6.6 Retroilluminazione non completamente funzionante, o non regolabile dopo un riavvio](#Retroilluminazione_non_completamente_funzionante.2C_o_non_regolabile_dopo_un_riavvio)
    *   [6.7 Disabilitare la compressione frame buffer](#Disabilitare_la_compressione_frame_buffer)
    *   [6.8 Problemi grafici/insensibilità in Chromium e Firefox](#Problemi_grafici.2Finsensibilit.C3.A0_in_Chromium_e_Firefox)
*   [7 Altre Risorse](#Altre_Risorse)

## Installazione

Prerequisiti: [Xorg](/index.php/Xorg_(Italiano) "Xorg (Italiano)")

[installare](/index.php/Pacman_(Italiano) "Pacman (Italiano)") il pacchetto [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) che è reperibile nei [repository ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)"). Esso fornisce il driver DDX per l'accelerazione 2D e il driver per [XvMC](/index.php/XvMC "XvMC") la decodifica video sulle vecchie GPU. Inoltre ha come dipendenza il pacchetto [mesa](https://www.archlinux.org/packages/?name=mesa), che fornisce il driver DRI per l'accelerazione 3D.

Per il supporto 3D a 32-bit sui sistemi x86_64, installare il pacchetto [lib32-mesa](https://www.archlinux.org/packages/?name=lib32-mesa) dal deposito [multilib](/index.php/Multilib "Multilib").

L'accelerazione hardware video di decodifica/codifica sulle vecchie GPU è fornita dal driver [XvMC](/index.php/XvMC "XvMC") incluso del driver DDX. Per le più recenti GPU, è fornito dal driver [VA-API](/index.php/VA-API "VA-API") fornito dal pacchetto [libva-intel-driver](https://www.archlinux.org/packages/?name=libva-intel-driver).

## Configurazione

Non è necessario alcun tipo di configurazione per far funzionare Xorg (il file `xorg.conf` non è necessario ma ha bisogno di essere configurato correttamente se presente).

Per una lista delle opzioni eseguire `man intel`.

## KMS (Kernel Mode Setting)

**Suggerimento:** Se avete problemi con la risoluzione , controllare [questa pagina](/index.php/Kernel_mode_setting#Forcing_modes_and_EDID "Kernel mode setting").

[KMS](/index.php/KMS "KMS") è necessario per eseguire X e gli ambienti desktop come [GNOME](/index.php/GNOME_(Italiano) "GNOME (Italiano)"), [KDE](/index.php/KDE_(Italiano) "KDE (Italiano)"), [XFCE](/index.php/Xfce_(Italiano) "Xfce (Italiano)"), [LXDE](/index.php/LXDE_(Italiano) "LXDE (Italiano)"), etc. KMS è supportato dai chipset Intel i915 che utilizzano il driver DRM ed è ora abilitato di default dal kernel v2.6.32\. Le versioni 2.10 e le più recenti di [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) non supportano più UMS (ad eccezione delle vecchie famiglie di chipset 810), rendendo necessario l’utilizzo di KMS indispensabile. KMS è tipicamente inizializzato dopo che si è avviato il kernel. E' possibile comunque abilitare KMS durante la fase di avvio del kernel, permettendo all'intero processo di boot di funzionare alla risoluzione nativa.

**Nota:** É **necessario** rimuovere ogni riferimento deprecato a `vga` o `nomodeset` dalla propria configurazione di boot.

Per procedere, aggiungere il modulo `i915` all'array `MODULES` in `/etc/mkinitcpio.conf`:

```
MODULES="**i915**"

```

Se si utilizza un file EDID personalizzato, lo si dovrebbe anche incorporare in initramfs:

 `/etc/mkinitcpio.conf`  `FILES="/lib/firmware/edid/your_edid.bin"` 

Quindi, ricreare l'initramfs:

```
# mkinitcpio -p linux

```

E Riavviare il sistema. Ora tutto dovrebbe funzionare.

## Opzioni di risparmio energetico del modulo base

Il modulo del kernel `i915` consente la configurazione attraverso [opzioni del modulo](/index.php/Kernel_modules#Setting_module_options "Kernel modules"). Alcune di queste opzioni hanno impatto sul risparmio energetico.

Per verificare che le opzioni siano attualmente abilitate, eseguire :

```
# for i in /sys/module/i915/parameters/*; do echo $i=$(cat $i); done

```

Un elenco di tutte le opzioni insieme a brevi descrizioni e valori di default può essere generato con il seguente comando :

```
$ modinfo i915 | grep parm

```

La seguente serie di opzioni dovrebbe essere generalmente sicura da consentire :

 `/etc/modprobe.d/i915.conf` 
```
 options i915 i915_enable_rc6=7 i915_enable_fbc=1 lvds_downclock=1

```

La compressione framebuffer può essere inaffidabile sulle vecchie generazioni di GPU intel ( quali esattamente non è precisato ). Ciò può essere verificato tramite il Journal del sistema, se vi sono presenti messaggi come :

```
kernel: drm: not enough stolen space for compressed buffer, disabling.

```

## Consigli e trucchi

### Scegliere il metodo di accelerazione

*   UXA - (Unified Acceleration Architecture) è il backend maturo che è stato introdotto per supportare il modello di driver GEM .
*   SNA - (Sandybridge's New Acceleration) è il successore più veloce per l'hardware che lo supportano.

Il metodo predefinito è SNA(dal 2013-08-05 [[2]](https://projects.archlinux.org/svntogit/packages.git/commit/trunk?h=packages/xf86-video-intel&id=d03f5fb77df413017821f492aa81e5d68def7e48)), il quale è meno stabile ma più veloce di UXA. Potete controllare i benchmarks fatti da Phoronix [[3]](http://www.phoronix.com/scan.php?page=news_item&px=MTEzOTE), che sono reperibili [qui](http://www.phoronix.com/scan.php?page=article&item=intel_glamor_first&num=1) per Sandy Bridge e [qui](http://www.phoronix.com/scan.php?page=article&item=intel_ivy_glamor&num=1) per Ivy Bridge. UXA è ancora una scelta consigliata, se avete dei problemi con SNA. Se riscontrate problemi con UXA si potrebbe avere più fortuna con SNA. SNA può ad esempio causare una schermata nera quando si esegue a schermo intero un video Flash .

Per utilizzare il vecchio metodo UXA, creare il file `/etc/X11/xorg.conf.d/20-intel.conf` con il seguente contenuto:

 `/etc/X11/xorg.conf.d/20-intel.conf` 
```
 Section "Device"
    Identifier  "Intel Graphics"
    Driver      "intel"
    Option      "AccelMethod"  "uxa"
 EndSection
```

Si può anche voler testare la nuova modalità di Glamor che accelera la grafica 2D con OpenGL . Per usarlo , creare `/etc/X11/xorg.conf.d/20-intel.conf` con il seguente contenuto :

 `/etc/X11/xorg.conf.d/20-intel.conf` 
```
Section "Device"
   Identifier  "Intel Graphics"
   Driver      "intel"
   Option      "AccelMethod"  "glamor"
EndSection
```

### Disattivare la sincronizzazione verticale (VSYNC)

Il driver Intel utilizza il [Triple Buffering](http://www.intel.com/support/graphics/sb/CS-004527.htm) per la sincronizzazione verticale, e questo permette prestazioni migliori ed evita il tearing. Per disattivare la sincronizzazione verticale (ad esempio per l'analisi comparativa) usare questo file .drirc nella vostra directory home:

 `~/.drirc` 
```
<device screen="0" driver="dri2">
	<application name="Default">
		<option name="vblank_mode" value="0"/>
	</application>
</device>
```

Non usare [driconf](https://www.archlinux.org/packages/?name=driconf) per creare questo file, poichè è pieno di bug e selezionerà il driver sbagliato.

### Configurare lo scaling mode

Questa procedura può essere utile per alcune applicazioni a schermo intero:

```
$ xrandr --output LVDS1 --set PANEL_FITTING param

```

dove `param` può assumere i valori

*   `center`: la risoluzione sarà mantenuta esattamente come è stata definita, non verrà applicato alcun ridimensionamento
*   `full`: ridimensiona la risoluzione in modo da occupare l'intero schermo
*   `full_aspect`: ridimensiona la risoluzione al massimo consentito, mantenendo le proporzioni dell'immagine.

Se ciò non dovesse funzionare, si provi con :

```
$ xrandr --output LVDS1 --set "scaling mode" param

```

dove `param` può assumere il valore di `"Full"`, `"Center"` o `"Full aspect"`.

### Problema KMS: la console è limitata ad una piccola porzione di schermo

Una porta video a bassa risoluzione potrebbe essere abilitata all’avvio, causando l’utilizzo solo di una piccola area dello schermo. Per risolvere, disabilitare esplicitamente la porta incriminata tramite un'impostazione del modulo i915 con `video=SVIDEO-1:d` come parametro della riga di comando del kernel nel vostro bootloader. Si veda [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters") per ulteriori informazioni.

Se ciò non dovesse funzionare, provare a sostituire TV1 o VGA1 a SVIDEO-1.

### Decodifica H.264 su chip GMA 4500

Il pacchetto [libva-intel-driver](https://www.archlinux.org/packages/?name=libva-intel-driver) fornisce la decodifica MPEG-2 solo per la serie GPU GMA 4500\. Il supporto alla decodifica H.264 è tenuto in un separato ramo G45-h264, che può essere utilizzato con l'installazione del pacchetto [libva-intel-driver-G45-H264](https://aur.archlinux.org/packages/libva-intel-driver-G45-H264/), disponibile in [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)"). Si noti tuttavia che questo supporto è sperimentale e non è attualmente in fase di sviluppo. Utilizzando il VA-API con questo driver sulle schede della serie GMA 4500, scarica la CPU ma non può portare a una riproduzione più agevole come la riproduzione senza accelerazione. Le prove utilizzando mplayer, hanno dimostrato che l'utilizzo di vaapi per riprodurre un video H.264 con codifica a 1080p ha dimezzato il carico della CPU (rispetto alla sovrapposizione XV), ma ha determinato una riproduzione molto mossa, mentre a codifica 720p ha funzionato abbastanza bene [[4]](https://bbs.archlinux.org/viewtopic.php?id=150550). Gli fanno da eco altre esperienze [[5]](http://www.emmolution.org/?p=192&cpage=1#comment-12292).

### Impostare il valore di gamma e luminosità

Intel non offre un metodo per impostare questi parametri a livello driver. Fortunatamente questi possono essere impostati tramite `xgamma` e `xrandr`.

Il valore di Gamma può essere impostato con:

```
$ xgamma -gamma 1.0

```

oppure

```
$ xrandr --output VGA1 --gamma 1.0:1.0:1.0

```

La luminosità può essere impostata con:

```
$ xrandr --output VGA1 --brightness 1.0

```

## Risoluzione dei Problemi

### Schermo vuoto durante l’avvio, alla fase "Loading modules"

Se si sta utilizzando "late start" KMS e lo schermo diventa vuoto alla fase "Loading modules", potrebbe essere d’aiuto aggiungere `i915` e `intel_agp` all’initramfs. Vedere la sezione KMS [precedente](#KMS_.28Kernel_Mode_Setting.29).

In alternativa, si potrebbe risolvere aggiungendo ai [parametri del kernel](/index.php/Kernel_parameters "Kernel parameters") quanto segue:

```
video=SVIDEO-1:d

```

Se invece bisogna trasmettere tramite un collegamento VGA, provare questo :

```
video=VGA-1:1280x800

```

### Video tearing

**Suggerimento:** Se state utilizzando l'ambiente desktop [GNOME](/index.php/GNOME_(Italiano) "GNOME (Italiano)") una correzione prestazioni più semplice e di poco impatto può essere trovata in questo articolo [GNOME#Tear-free_video_with_Intel_HD_Graphics](/index.php/GNOME#Tear-free_video_with_Intel_HD_Graphics "GNOME").

Il metodo di accelerazione SNA causa il problema del tearing a molti utenti. Per risolvere questo problema abilitare l'opzione `"Tearfree"` del drive:

 `/etc/X11/xorg.conf.d/20-intel.conf` 
```
Section "Device"
   Identifier  "Intel Graphics"
   Driver      "intel"
   Option      "TearFree"    "true"
EndSection
```

Si veda l'[originale bug report](https://bugs.freedesktop.org/show_bug.cgi?id=37686) per maggiori informazioni.

**Nota:**

*   Questa opzione non funziona quando il l'opzione `SwapbuffersWait` è impostato su `false`.

*   Questa opzione risulta dare problemi alle applicazioni che sono molto esigenti in fatto di tempistica vsync, come [Super Meat Boy](https://en.wikipedia.org/wiki/Super_Meat_Boy "wikipedia:Super Meat Boy").*   Questa opzione non funziona con l'accelerazione UXA, ma solo con il metodo SNA.

}}

### Freeze/crash del server X con i driver intel

Problemi con il server X che termina inaspettatamente, o che sembra bloccarsi, o la GPU non risponde correttamente, possono essere risolti disabilitando l'uso GPU con l'opzione `NoAccel`:

 `/etc/X11/xorg.conf.d/20-intel.conf` 
```
 Section "Device"
   Identifier "Intel Graphics"
   Driver "intel"
   Option "NoAccel" "True"
 EndSection
```

In alternativa, si provare a disabilitare l'accelerazione 3D solo con tramite l'opzione `DRI`:

 `/etc/X11/xorg.conf.d/20-intel.conf` 
```
Section "Device"
   Identifier "Intel Graphics"
   Driver "intel"
   Option "DRI" "False"
EndSection
```

Se si verificano crash e avete

```
Option "TearFree" "true"
Option "AccelMethod" "sna"

```

nel file di configurazione , nella maggior parte dei casi questi possono essere fissati con l'aggiunta di

```
i915.semaphores=1

```

ai parametri di avvio del kernel.

### Aggiungere risoluzioni non rilevate

Questo problema è trattato nell'articolo di [Xrandr](/index.php/Xrandr#Adding_undetected_resolutions "Xrandr").

### Colori alterati

**Nota:** Questo problema è legato ai cambiamenti nel kernel 3.9\. Questo problema permane anche nella versione 3.10

Il Kernel 3.9 contiene le modifiche dei driver di Intel che consente una facile impostazione RGB limitata alla gamma, che può causare l'alterazione dei colori in alcuni casi. Esso è legato alla nuova modalità "Automatic" per la proprietà "Broadcast RGB". Si può forzare la modalità, ad esempio con `xrandr --output <HDMI> --set "Broadcast RGB" "Full"`, usare il dispositivo output appropriato se diverso da HDMI (verificare con `$ xrandr`), è possibile aggiungerlo al proprio file `.xprofile` e renderlo eseguibile per eseguire il comando prima che si avvii la modalità grafica .

**Nota:** Alcuni televisori possono visualizzare solo i colori da 16-255, così il modo di impostazione per Full causerà un clipping del colore nella gamma da 0 a 15, quindi è meglio lasciarlo su Automatic, poiché rileva automaticamente se è necessario comprimere lo spazio colore per la vostra TV.

Inoltre ci sono altri problemi correlati, che possono essere risolti modificando i registri della GPU. Maggiori informazioni possono essere trovate [qui](http://lists.freedesktop.org/archives/intel-gfx/2012-April/016217.html) ed in questa [pagina](http://github.com/OpenELEC/OpenELEC.tv/commit/09109e9259eb051f34f771929b6a02635806404c)

### Retroilluminazione non completamente funzionante, o non regolabile dopo un riavvio

Se si utilizza una scheda grafica Intel e non avete alcun controllo tramite i tasti di scelta rapida per modificare la luminosità dello schermo, provare ad avviare il sistema con questo parametro del kernel:

```
acpi_backlight=vendor

```

Se questo non risolve il problema, molte persone hanno risolto aggiungendo anche:

```
acpi_osi=Linux

```

oppure

```
acpi_osi="!Windows 2012"

```

in aggiunta al parametro citato in precedenza, o da solo.

A partire dalla versione del kernel 3.13 , vi è anche un altro parametro che si può aggiungere alla riga del kernel, che è stato rivelato utile per alcuni utenti :

```
video.use_native_backlight=1

```

Se nessuna di quelle risolvere il tuo problema, è necessario modificare o creare il file `/etc/X11/xorg.conf.d/20-intel.conf`, aggiungendo quanto segue:

 `/etc/X11/xorg.conf.d/20-intel.conf` 
```
Section "Device"
        Identifier  "card0"
        Driver      "intel"
        Option     "Backlight"          "intel_backlight"
        BusID       "PCI:0:2:0"
EndSection
```

se si utilizza l'accelerazione SNA, come detto sopra, create il file come segue :

 `/etc/X11/xorg.conf.d/20-intel.conf` 
```
Section "Device"
        Identifier  "card0"
        Driver      "intel"
        Option      "AccelMethod"  "sna"
        Option      "Backlight"          "intel_backlight"
        BusID       "PCI:0:2:0"
EndSection
```

### Disabilitare la compressione frame buffer

Su alcune schede come le Intel Corporation Mobile 4 Series Chipsets, la compressione frame buffer risulta abilitata e costretto a messaggi di errore senza fine :

```
$ dmesg |tail 
[ 2360.475430] [drm] not enough stolen space for compressed buffer (need 4325376 bytes), disabling
[ 2360.475437] [drm] hint: you may be able to increase stolen memory size in the BIOS to avoid this

```

La soluzione è quella di disabilitare la compressione frame buffer che aumenterà leggermente il consumo di energia. Per disabilitarlo aggiungere `i915.i915_enable_fbc=0` ai parametri del kernel. Ulteriori informazioni sui risultati con la compressione disabilitata possono essere trovati [qui](http://zinc.canonical.com/~cking/power-benchmarking/background-colour-and-framebuffer-compression/results.txt).

### Problemi grafici/insensibilità in Chromium e Firefox

Se si verificano problemi di corruzione della grafica o di insensibilità in Chromium e/o Firefox, impostare il valore di accelerazione in [uxa](#Scegliere_il_metodo_di_accelerazione).

## Altre Risorse

*   [https://01.org/linuxgraphics/](https://01.org/linuxgraphics/) Documentazione (include una lista dell'hardware supportato)
*   [KMS](/index.php/KMS "KMS") - Arch wiki sul kernel mode setting
*   [Xrandr](/index.php/Xrandr "Xrandr") - Problemi con l'impostazione della risoluzione
*   Arch Linux forums: [Intel 945GM, Xorg, Kernel - performance](https://bbs.archlinux.org/viewtopic.php?pid=522665#p522665)