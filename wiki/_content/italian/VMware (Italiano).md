Questo articolo tratta l'installazione di VMware in Arch, si potrebbe essere invece interessati a [Installare Arch Linux in VMware](/index.php/Installing_Arch_Linux_in_VMware "Installing Arch Linux in VMware").

**Note:** Questo articolo supporta **solo** l'ultima versione di VMware, ovvero VMware Workstation 8 e VMware Player 4.

## Contents

*   [1 Installazione](#Installazione)
*   [2 Configurazione](#Configurazione)
    *   [2.1 Patch per i moduli di VMware](#Patch_per_i_moduli_di_VMware)
        *   [2.1.1 kernel 3.19](#kernel_3.19)
        *   [2.1.2 kernel 3.1](#kernel_3.1)
    *   [2.2 Installazione dei moduli di VMware](#Installazione_dei_moduli_di_VMware)
*   [3 Treucchi e Consigli](#Treucchi_e_Consigli)
    *   [3.1 Estrazione del BIOS di VMware](#Estrazione_del_BIOS_di_VMware)
    *   [3.2 Utilizzare un BIOS modificato](#Utilizzare_un_BIOS_modificato)
*   [4 Risoluzione dei problemi](#Risoluzione_dei_problemi)
    *   [4.1 Could not open /dev/vmmon: No such file or directory](#Could_not_open_.2Fdev.2Fvmmon:_No_such_file_or_directory)
    *   [4.2 Kernel headers for version 3.x-xxxx were not found. If you installed them[...]](#Kernel_headers_for_version_3.x-xxxx_were_not_found._If_you_installed_them.5B....5D)
    *   [4.3 L'installer non parte](#L.27installer_non_parte)
    *   [4.4 I dispositivi USB non vengono riconosciuti da VMware workstation 8](#I_dispositivi_USB_non_vengono_riconosciuti_da_VMware_workstation_8)
*   [5 Disinstallazione](#Disinstallazione)

## Installazione

**Nota:** VMware Workstation/Player non potrà essere gestito con pacman se i file non saranno installati con esso.

**1.** Scaricare l'ultima versione di [VMware Workstation](http://downloads.vmware.com/d/info/desktop_end_user_computing/vmware_workstation/8_0) or[VMware Player](http://downloads.vmware.com/d/info/desktop_end_user_computing/vmware_player/4_0) (si può provare anche [una versione di test (Beta/RC)](http://communities.vmware.com/community/vmtn/beta)).

**2.** Avviare l'installazione (il flag `--console` usa il terminale invece dell'interfaccia grafica):

```
# chmod +x VMware-<edition>-<version>.<release>.<architecture>.bundle
# ./VMware-<edition>-<version>.<release>.<architecture>.bundle --console

```

**3.** Leggere & accettare la EULA per continuare.

**4.** Impostare gli script dei `servizi di sistema` in:

```
/etc/rc.d

```

**5.** (Opzionale) Se Eclipse è installato, immettere il percorso della cartella per il Debugger Virtuale Integrato.

**6.** Riceverete un errore che `"rc*.d style init script"` non è stato impostato. Questo può essere tranquillamente ignorato.

**7.** Creare collegamenti per i seguenti demoni:

```
# ln -s /etc/init.d/vmware /etc/rc.d/vmware
# ln -s /etc/init.d/vmware-workstation-server /etc/rc.d/vmware-workstation-server

```

## Configurazione

### Patch per i moduli di VMware

VMware Workstation 8 e VMware Player 4 sono supportati solo dai kernel 3.0 e superiori. I kernel più recenti richiedono l'applicazione dei moduli di VMware

**Suggerimento:** C'è un pacchetto chiamato [vmware-patch](https://aur.archlinux.org/packages/vmware-patch/) in [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)") che ha lo scopo di tentare l'automatizzazione del processo di patch (supporta anche le vecchie versioni di VMware).

#### kernel 3.19

Nella versione 3.19 kernel sarà impossibile compilare il modulo `vmnet`.

È disponibile una patch a questo [indirizzo](http://pastie.org/9934018):

```
$ curl [http://pastie.org/pastes/9934018/download](http://pastie.org/pastes/9934018/download) -o /tmp/vmnet-3.19.patch

```

Estraete i sorgenti del modulo `vmnet`:

```
$ cd /usr/lib/vmware/modules/source
# tar -xf vmnet.tar

```

Applicate la patch:

```
# patch -p0 -i /tmp/vmnet-3.19.patch

```

Ricostruite l'archivio:

```
# tar -cf vmnet.tar vmnet-only

```

Rimuovete i file temporanei:

```
# rm -r vmnet-only

```

Ricompilate i moduli:

```
# vmware-modconfig --console --install-all

```

#### kernel 3.1

La patch per i kernel 3.1 è reperibile a questo [indirizzo](http://weltall.heliohost.org/wordpress/2011/09/29/vmware-workstationplayer-fix-for-linux-3-1/):

```
 $ cd /tmp
 $ curl -O [http://weltall.heliohost.org/wordpress/wp-content/uploads/2011/09/vmware8linux31fix.tar.gz](http://weltall.heliohost.org/wordpress/wp-content/uploads/2011/09/vmware8linux31fix.tar.gz)
 $ tar -xvzf vmware8linux31fix.tar.gz
 # ./patch-modules_3.1.0.sh

```

### Installazione dei moduli di VMware

**8.** A questo punto potresti voler installare i moduli. Prima di tutto bisogna di cambiare sia la `lsmod binary path` in `/etc/rc.d/vmware` da `/sbin/lsmod` fino a `/bin/lsmod`:

```
# sed -i "s|/sbin/lsmod|/bin/lsmod|g" /etc/rc.d/vmware

```

o creare un link simbolico con:

```
# ln -s /bin/lsmod /sbin/lsmod

```

**9.** Ora si possono installare i moduli. È possibile fare questo o lanciando VMware (da root) e lasciandoglieli installare con l'interfaccia grafica o eseguendo:

```
# vmware-modconfig --console --install-all

```

**10.** (Opzionale) Aggiungere `vmware` alla serie di [DAEMONS](/index.php/Daemons "Daemons") in `/etc/[rc.conf](/index.php/Rc.conf "Rc.conf")` in modo che il server parta automaticamente all'avvio.

**11.** Ora aprire VMware Workstation (`vmware` nel terminale) o VMware Player (`vmplayer` nel terminale) per configurarli e usarli!

**Attenzione:** Quando viene aggiornato il kernel **bisogna** ricompilare i moduli di vmware con i seguenti comandi:

```
# vmware-modconfig --console --install-all

```

Il fallimento di questa operazione potrebbe risolversi in un crash di sistema quando si aprono le macchine virtuali.

## Treucchi e Consigli

### Estrazione del BIOS di VMware

Per estrarre il BIOS di VMware BIOS, che può essere manipolato e usato in seguito con le proprie macchine virtuali:

```
$ objcopy /usr/lib/vmware/bin/vmware-vmx -O binary -j bios440 --set-section-flags bios440=a bios440.rom.Z
$ perl -e 'use Compress::Zlib; my $v; read STDIN, $v, '$(stat -c%s "./bios440.rom.Z")'; $v = uncompress($v); print $v;' < bios440.rom.Z > bios440.rom

```

### Utilizzare un BIOS modificato

Se e quando si decide di modificare il BIOS estratto potete fare la vostra macchina virtuale da usare spostandolo in `~/vmware/<Nome della macchina virtuale>`

```
$ mv bios440.rom ~/vmware/<Virtual machine name>/

```

e aggiungere il nome al file `<Nome della macchina virtuale>.vmx`

 `~/vmware/<Virtual machine name>/<Virtual machine name>.vmx`  `bios440.filename = "bios440.rom"` 

## Risoluzione dei problemi

### Could not open /dev/vmmon: No such file or directory

L'errore completo è:

```
Could not open /dev/vmmon: No such file or directory.
Please make sure that the kernel module `vmmon' is loaded.

```

Questo significa che almeno il servizio di VMware `vmmon` non è partito. Tutti i servizi di VMware possono essere avviati con:

```
# rc.d start vmware

```

### Kernel headers for version 3.x-xxxx were not found. If you installed them[...]

Installarli con:

```
# pacman -S linux-headers

```

### L'installer non parte

Se si torna subito al prompt quando si apre il file `.bundle`, allore probabilmente è installata una versione vecchia del `vmware installer` e sarebbe opportuno rimuoverla (si può prendere spunto anche dalla sezione [Disinstallazione](https://wiki.archlinux.org/index.php/VMware_(Italiano)#Disinstallazione) di questo articolo):

```
# rm -r /etc/vmware-installer

```

### I dispositivi USB non vengono riconosciuti da VMware workstation 8

Per qualche ragione, in alcune installazioni manca lo script `vmware-USBArbitrator`. Per riaggiungerlo manualmente si veda [questa risposta](https://bbs.archlinux.org/viewtopic.php?id=127145) sul forum.

## Disinstallazione

La disinstallazione di VMware necessità del nome del prodotto (ovvero `vmware-workstation` o `vmware-player`). Per una lista completa dei prodotti:

```
# vmware-installer -l

```

e disinstallare con:

```
# vmware-installer -u <vmware-product>

```

Le parti inserite manualmente in `/etc/rc.d` devono essere cancellate manualmente:

```
# unlink /etc/rc.d/vmware
# unlink /etc/rc.d/vmware-workstation-server

```

Non dimenticarsi di rimuovere vmware dalla serie di `DEMONI` in `/etc/rc.conf`.