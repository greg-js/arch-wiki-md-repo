## Contents

*   [1 FAQ](#FAQ)
    *   [1.1 Perché non ricevo messaggi di log sulla console?](#Perch.C3.A9_non_ricevo_messaggi_di_log_sulla_console.3F)
    *   [1.2 Come posso cambiare il numero di console funzionanti di default?](#Come_posso_cambiare_il_numero_di_console_funzionanti_di_default.3F)
    *   [1.3 Come posso ottenere un output più dettagliato durante l'avvio?](#Come_posso_ottenere_un_output_pi.C3.B9_dettagliato_durante_l.27avvio.3F)
    *   [1.4 Come evitare che la console sia pulita dopo l'avvio?](#Come_evitare_che_la_console_sia_pulita_dopo_l.27avvio.3F)
    *   [1.5 Quali opzioni del kernel occorrono attive nel mio kernel nel caso non usassi il kernel Arch ufficiale?](#Quali_opzioni_del_kernel_occorrono_attive_nel_mio_kernel_nel_caso_non_usassi_il_kernel_Arch_ufficiale.3F)
    *   [1.6 Quali altre unità dipendono da una unità?](#Quali_altre_unit.C3.A0_dipendono_da_una_unit.C3.A0.3F)
    *   [1.7 Il mio computer si spegne, ma l'alimentatore resta acceso.](#Il_mio_computer_si_spegne.2C_ma_l.27alimentatore_resta_acceso.)
    *   [1.8 Dopo la migrazione a systemd, perché non riesco a montare fakeRAID?](#Dopo_la_migrazione_a_systemd.2C_perch.C3.A9_non_riesco_a_montare_fakeRAID.3F)
    *   [1.9 Come posso fare in modo che uno script sia eseguito al boot?](#Come_posso_fare_in_modo_che_uno_script_sia_eseguito_al_boot.3F)
    *   [1.10 Lo stato del .service dice "active (exited)" in verde. (per iptables)](#Lo_stato_del_.service_dice_.22active_.28exited.29.22_in_verde._.28per_iptables.29)
    *   [1.11 Failed to issue method call: File exists error](#Failed_to_issue_method_call:_File_exists_error)

## FAQ

Per una lista aggiornata dei problemi conosciuti, vedere il [TODO](http://cgit.freedesktop.org/systemd/systemd/tree/TODO).

### Perché non ricevo messaggi di log sulla console?

Si deve configurare il proprio livello di log. Un tempo, `/etc/rc.sysinit` lo faceva e configurava il livello di log di dmesg a `3`, che era un ragionevole livello. Ora aggiungere `loglevel=3` o `quiet` ai [parametri del kernel](/index.php/Kernel_parameters "Kernel parameters").

### Come posso cambiare il numero di console funzionanti di default?

Per aggiungere un'altra console, semplicemente creare un altro collegamento per ottenere un'altra console nella cartella `/etc/systemd/system/getty.target.wants/` :

```
# ln -sf /lib/systemd/system/getty@.service /etc/systemd/system/getty.target.wants/getty@tty9.service
# systemctl start getty@tty9.service

```

Per rimuovere una console, semplicemente rimuovere il collegamento alla console nella cartella `/etc/systemd/system/getty.target.wants/` :

```
# rm /etc/systemd/system/getty.target.wants/getty@{tty5,tty6}.service
# systemctl stop getty@tty5.service getty@tty6.service

```

Gli utenti possono cambiare il numero delle console anche editando `/etc/systemd/logind.conf` e cambiando il valore di `NAutoVTs`. Seguendo questo metodo, l'attivazione al bisogno sarà preservata, mentre con il metodo iniziale semplicemente si avranno le console funzionanti al boot.

systemd non usa il file /etc/inittab.

**Nota:** Dalla versione 30 di systemd, solo una console sarà lanciata di default. Se si accede ad un'altra console una nuova istanza sarà lanciata (è lo stile socket-activation). Si può forzare l'avvio di console addizionali usando il metodo sopra.

### Come posso ottenere un output più dettagliato durante l'avvio?

Se non si ottiene nessun output dalla console dopo i messaggi di caricamento dell'initram, significa che il parametro `quiet` è presente nella linea di comando del kernel. E' meglio rimuoverlo, almeno per i primi avvii con systemd, per vedere se tutto è ok. Poi, si potrà vedere una lista di `[ OK ]` in verde o `[ FAILED ]` in rosso.

Tutti i messaggi sono registrati nel log di sistema e se si vuole scoprire lo stato del proprio sistema usare `$ systemctl` (non sono necessari privilegi di root) oppure guardare il log di avvio con `journalctl`.

### Come evitare che la console sia pulita dopo l'avvio?

Creare un file g`getty@tty1.service` personalizzato copiando `/usr/lib/systemd/system/getty@.service` in `/etc/systemd/system/getty@tty1.service` e cambiando `TTYVTDisallocate` in `no`. e si permette l'esportazione di `LANG` in `/etc/locale.conf`

### Quali opzioni del kernel occorrono attive nel mio kernel nel caso non usassi il kernel Arch ufficiale?

I Kernels precedenti al 2.6.39 non sono supportati.

Questa è una lista parziale delle opzioni richieste/raccomandate, ce ne possono essere ulteriori:

```
**General setup**
 CONFIG_FHANDLE=y
 CONFIG_AUDIT=y (raccomandata)
 CONFIG_AUDIT_LOGINUID_IMMUTABLE=y (non raccomandata, può danneggiare la compatibilità con sysvinit)
 CONFIG_CGROUPS=y
 **-> Namespaces support**
    CONFIG_NET_NS=y (per reti private)
**Networking support -> Networking options**
 CONFIG_IPV6=[y|m] (altamente raccomandata)
**Device Drivers**
 **-> Generic Driver Options**
    CONFIG_UEVENT_HELPER_PATH=""
    CONFIG_DEVTMPFS=y
    CONFIG_DEVTMPFS_MOUNT=y (richiesta se non si usa un initramfs)
 **-> Real Time Clock**
    CONFIG_RTC_DRV_CMOS=y (altamente raccomandata)
**File systems**
 CONFIG_FANOTIFY=y (richiesta per readahead)
 CONFIG_AUTOFS4_FS=[y|m]
 **-> Pseudo filesystems**
    CONFIG_TMPFS_POSIX_ACL=y (raccomandata se si vuole usare  pam_systemd.so)
```

### Quali altre unità dipendono da una unità?

Per esempio, se si vuole evidenziare quali servizi e target attiva `multi-user.target`, si usi qualcosa del genere:

 `$ systemctl show -p "Wants" multi-user.target`  `Wants=rc-local.service avahi-daemon.service rpcbind.service NetworkManager.service acpid.service dbus.service atd.service crond.service auditd.service ntpd.service udisks.service bluetooth.service org.cups.cupsd.service wpa_supplicant.service getty.target modem-manager.service portreserve.service abrtd.service yum-updatesd.service upowerd.service test-first.service pcscd.service rsyslog.service haldaemon.service remote-fs.target plymouth-quit.service systemd-update-utmp-runlevel.service sendmail.service lvm2-monitor.service cpuspeed.service udev-post.service mdmonitor.service iscsid.service livesys.service livesys-late.service irqbalance.service iscsi.service` 

Invece di `Wants` si può provare `WantedBy`, `Requires`, `RequiredBy`, `Conflicts`, `ConflictedBy`, `Before`, `After` per i rispettivi tipi di dipendenza e il loro contrario.

### Il mio computer si spegne, ma l'alimentatore resta acceso.

Usare

```
$ systemctl poweroff

```

invece di `systemctl halt`.

### Dopo la migrazione a systemd, perché non riesco a montare fakeRAID?

Assicurarsi di usare

```
# systemctl enable dmraid.service

```

### Come posso fare in modo che uno script sia eseguito al boot?

Creare un nuovo file in `/etc/systemd/system` (e.g. "myscript".service) e aggiungere il seguente contenuto:

[Unit] Description=My script

[Service] ExecStart=/usr/bin/my-script

[Install] WantedBy=multi-user.target

Poi

```
# systemctl enable "myscript".service

```

Questo esempio presuppone che si voglia avviare lo script quando il target multi-user sarà lanciato. **Nota:** Nel caso si voglia avviare uno script di schell, assicurarsi di avere

```
#!/bin/sh

```

nella prima riga dello script. Non scrivere qualcosa come

```
ExecStart=/bin/sh /path/to/script.sh # NON FUNZIONA

```

perché non funziona.

### Lo stato del .service dice "active (exited)" in verde. (per iptables)

Ciò è perfettamente normale. Nel caso specifico di iptables è perché non c'è nessun demone da avviare, è controllato dal kernel. Tuttavia esiste dopo che le regole sono state caricate. Per verificare se le regole di iptables sono state caricate correttamente:

 `# iptables --list` 

### `Failed to issue method call: File exists` error

Questo accade quando si usa `systemctl enable` e si tenta di creare il link simbolico in `/etc/systemd/system/` ed esiste già. Di solito accade quando si passa da un display manager ad un altro (per esempio da GDM a KDM, che possono essere abilitati con `gdm.service` e `kdm.service`, rispettivamente) e il link simbolico corrispondente `/etc/systemd/system/display-manager.service` esiste già. Per risolvere il problema usare `systemctl -f enable` per sovrascrivere link simbolici già esistenti.