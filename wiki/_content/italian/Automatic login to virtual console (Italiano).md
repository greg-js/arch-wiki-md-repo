Questo articolo descrive come accedere automaticamente a una “console virtuale” o tty alla fine del [processo di boot](/index.php/Arch_Boot_Process_(Italiano) "Arch Boot Process (Italiano)"). Questo articolo tratta solamente dell'accesso alla console; i metodi per avviare [il server X](/index.php/Xorg_(Italiano) "Xorg (Italiano)") sono descritti in [Start X at Login](/index.php/Start_X_at_Login_(Italiano) "Start X at Login (Italiano)").

## Service

Creare un nuovo servizio tipo `getty@.service` e copiarlo in `/etc/systemd/system/`

```
# cp /usr/lib/systemd/system/getty@.service /etc/systemd/system/autologin@.service

```

**Nota:** `/etc/systemd/system/` ha la precedenza su `/usr/lib/systemd/system/`

Cambiare la linea`ExecStart` per includere il parametro `-a "USERNAME"`:

 `/etc/systemd/system/autologin@.service` 

```
[Service]
_[...]_
ExecStart=-/sbin/agetty --noclear -a _USERNAME_ %I 38400
_[...]_
[Install]
WantedBy=getty.target
```

**Tip:** È possibile cambiare `Type=idle` in `Type=simple` per permettere un leggero ritardo per l'esecuzione di agetty fino a che tutti i processi non siano completati. Questa opzione è molto utile quando si [avvia X al boot in modo automatico](/index.php/Far_partire_X_al_boot "Far partire X al boot"). Vedere `man systemd.service` per ulterioti informazioni.
**Nota:** `Type=simple` può provocare messaggi di debug da parte di systemd che vanno a "sovrascrivere" le tty.

**Nota:** Se si usa mingetty, cambiare /sbin/agetty con /sbin/mingetty

.

Infine, disabilitare il vecchio `getty@tty_X_.service` per la TTY specifica e abilitare il relativo `autologin@tty_X_.service` per la stessa TTY:

```
# systemctl daemon-reload
# systemctl disable getty@_tty1_
# systemctl enable autologin@_tty1_
# systemctl start autologin@_tty1_

```

**Attenzione:** Se si è in una sessione di X sulla stessa tty configurata nel file .service, avviare `autologin@tty_X_.service` farà crashare il server X.

Per evitare errori relativi a display-manager.service in dsmeg, è possibile settare come default il target "multi-user":

```
# systemctl enable multi-user.target

```

### Killare X

Per killare X e prevenirne l'immediato ricaricamento, stoppare il servizio `autologin@tty1.service`:

```
# # systemctl stop autologin@tty1.service

```

### Vedere anche

*   [Cambiare il runlevel/target predefinito all'avvio](/index.php/Systemd_(Italiano)#Cambiare_il_runlevel.2Ftarget_predefinito_all.27avvio "Systemd (Italiano)").)