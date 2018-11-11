Articoli correlati

*   [Display manager (Italiano)](/index.php/Display_manager_(Italiano) "Display manager (Italiano)")
*   [Silent boot](/index.php/Silent_boot "Silent boot")
*   [Start X at Login (Italiano)](/index.php/Start_X_at_Login_(Italiano) "Start X at Login (Italiano)")

Questo articolo descrive come accedere automaticamente a una “console virtuale” o tty alla fine del [processo di boot](/index.php/Arch_boot_process_(Italiano) "Arch boot process (Italiano)"). Questo articolo tratta solamente dell'accesso alla console; i metodi per avviare [il server X](/index.php/Xorg_(Italiano) "Xorg (Italiano)") sono descritti in [Start X at Login](/index.php/Start_X_at_Login_(Italiano) "Start X at Login (Italiano)").

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
*[...]*
ExecStart=-/sbin/agetty --noclear -a *USERNAME* %I 38400
*[...]*
[Install]
WantedBy=getty.target
```

**Tip:** È possibile cambiare `Type=idle` in `Type=simple` per permettere un leggero ritardo per l'esecuzione di agetty fino a che tutti i processi non siano completati. Questa opzione è molto utile quando si [avvia X al boot in modo automatico](/index.php/Far_partire_X_al_boot "Far partire X al boot"). Vedere [systemd.service(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.service.5) per ulterioti informazioni.
**Nota:** `Type=simple` può provocare messaggi di debug da parte di systemd che vanno a "sovrascrivere" le tty.

**Nota:** Se si usa mingetty, cambiare /sbin/agetty con /sbin/mingetty
.

Infine, disabilitare il vecchio `getty@tty*X*.service` per la TTY specifica e abilitare il relativo `autologin@tty*X*.service` per la stessa TTY:

```
# systemctl daemon-reload
# systemctl disable getty@*tty1*
# systemctl enable autologin@*tty1*
# systemctl start autologin@*tty1*

```

**Attenzione:** Se si è in una sessione di X sulla stessa tty configurata nel file .service, avviare `autologin@tty*X*.service` farà crashare il server X.

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

*   [Cambiare il runlevel/target predefinito all'avvio](/index.php/Systemd_(Italiano)#Cambiare_il_target_predefinito_all.27avvio "Systemd (Italiano)").)