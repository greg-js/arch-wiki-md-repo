[Hamachi](https://en.wikipedia.org/wiki/Hamachi_(software) è un software VPN proprietario (closed source) commerciale. Con Hamachi si possono associare due o più computer con una connessione ad Internet in una propria rete virtuale per una comunicazione diretta sicura.

## Contents

*   [1 Installazione](#Installazione)
*   [2 Configurazione](#Configurazione)
    *   [2.1 Usare hamachi da linea di comando come normale utente](#Usare_hamachi_da_linea_di_comando_come_normale_utente)
    *   [2.2 Impostazione automatica del nickname](#Impostazione_automatica_del_nickname)
*   [3 Eseguire Hamachi](#Eseguire_Hamachi)
    *   [3.1 Systemd](#Systemd)
*   [4 GUI](#GUI)
*   [5 Altre risorse](#Altre_risorse)

## Installazione

Installare il pacchetto [logmein-hamachi](https://aur.archlinux.org/packages/logmein-hamachi/) da [AUR](/index.php/Arch_User_Repository "Arch User Repository").

## Configurazione

Hamachi è configurato in `/var/lib/logmein-hamachi/h2-engine-override.cfg` (creare il file nel caso non esistesse). Sfortunatamente, non è facile trovare una lista completa di opzioni di configurazione possibili, quindi sono qui elencate alcune.

### Usare hamachi da linea di comando come normale utente

Per usare il comando `hamachi` da terminale come normale utente, aggiungere la seguente riga al file di configurazione:

```
Ipc.User TuoNomeUtente

```

### Impostazione automatica del nickname

Normalmente, Hamachi usa l'hostname del sistema come nickname che sarà visto dagli altri utenti di Hamachi. Se si desidera impostare automaticamente un nickname personalizzato ad ogni avvio di Hamachi, aggiungere la seguente riga al file di configurazione:

```
Setup.AutoNick TuoNickname

```

Si può anche impostare manualmente il nickname usando `hamachi` da terminale:

```
# hamachi set-nick TuoNickname

```

Tuttavia, questo deve essere fatto ogni volta che Hamachi (ri-)parte, quindi, se si vuole usare sempre lo stesso nickname, impostare automaticamente il nickname (come spiegato sopra) è la soluzione più semplice.

## Eseguire Hamachi

```
# systemctl start logmein-hamachi

```

Ora si hanno vari comandi a disposizione. Questi elencati non sono in alcun ordine particolare e sono autoesplicativi.

```
$hamachi set-nick pippo
$hamachi login
$hamachi create mia-rete passwordsegreta
$hamachi go-online mia-rete
$hamachi list
$hamachi go-offline mia-rete

```

Per la lista di tutti i comandi, eseguire:

```
$hamachi ?

```

**Nota:** Assicurarsi di impostare "online" lo stato del canale (o dei canali) se si vuole effettuare qualsiasi operazione tra i computer di quella rete.

### Systemd

Il pacchetto AUR [logmein-hamachi](https://aur.archlinux.org/packages/logmein-hamachi/) include anche un piccolo demone [Systemd](/index.php/Systemd "Systemd").

Se si vuole, si può impostare l'avvio automatico di Hamachi nella fase di boot con Systemd:

```
# systemctl enable logmein-hamachi

```

Per avviare immediatamente il demone Hamachi, utilizzare questo comando:

```
# systemctl start logmein-hamachi

```

## GUI

Sono disponibili su AUR le seguenti GUI per Hamachi:

*   [haguichi](https://aur.archlinux.org/packages/haguichi/) (Gtk3, Vala)
*   [quamachi](https://aur.archlinux.org/packages/quamachi/) (Qt4, Python)

## Altre risorse

*   [Project home page](https://www.vpn.net/)