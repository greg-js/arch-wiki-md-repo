## Utilizzare systemd-logind

Se si sta usando [systemd](/index.php/Systemd_(Italiano) "Systemd (Italiano)") gli utenti con una sessione non remota potrebbero avere problemi con i comandi relativi a spegnimento/ibernazione ecc..anche con [polkit](https://www.archlinux.org/packages/?name=polkit) installato.

Per spegnere:

```
# systemctl poweroff

```

Sospensione, spegnimento, ibernazione e chiusura del coperchio (per i laptop) sono eventi gestiti anche da logind (vedere [logind.conf(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/logind.conf.5) per altre informazioni).

## Utilizzare sudo

Prima di tutto va installato `sudo`:

```
# pacman -S sudo

```

Ora, da root, vanno aggiunte delle righe alla fine di `/etc/sudoers` usando `visudo`. Va sostituito `**user**` con il proprio username e `**hostname**` con l'hostname della macchina.

```
**user** **hostname** =NOPASSWD: /sbin/shutdown -h now,/sbin/reboot

```

Ora l'utente potrà spegnere il computer con `sudo shutdown -h now`, e riavviare con `sudo reboot`. Per spegnere il sistema si può anche usare `poweroff` oppure `halt`.

Per comodità, è possibile aggiungere questi alias al proprio utente `~/.bashrc` (o a `/etc/bash.bashrc` per una configurazione globale del sistema):

```
alias reboot="sudo reboot"
alias poweroff="sudo poweroff"
alias halt="sudo halt"

```

## Utilizzare acpid

[acpid](/index.php/Acpid_(Italiano) "Acpid (Italiano)") può essere utilizzato per consentire a chiunque abbia accesso fisico al computer di spegnere in maniera pulita il sistema utilizzando il pulsante di accensione.