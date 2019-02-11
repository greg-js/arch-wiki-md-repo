MySQL è un database SQL ampiamente diffuso e multi-threaded. Per maggiori informazioni sulle sue caratteristiche consultare la [pagina ufficiale](http://www.mysql.it/).

**Note:** MariaDB è l'implementazione ufficialmente adottata da Archlinux. Si raccomandano gli utenti di [passare](#Passare_da_Oracle_MySQL_a_MariaDB) a MariaDB. Oracle MySQL è in [AUR](/index.php/AUR "AUR"). Annuncio ufficiale: [[1]](https://www.archlinux.org/news/mariadb-replaces-mysql-in-repositories/).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installazione](#Installazione)
    *   [1.1 Passare da Oracle MySQL a MariaDB](#Passare_da_Oracle_MySQL_a_MariaDB)
    *   [1.2 Aggiornare](#Aggiornare)
*   [2 Configurazione](#Configurazione)
    *   [2.1 Disabilitare l'accesso remoto](#Disabilitare_l'accesso_remoto)
    *   [2.2 Abilitare il completamento automatico](#Abilitare_il_completamento_automatico)
*   [3 Backup](#Backup)
*   [4 Risoluzione di problemi](#Risoluzione_di_problemi)
    *   [4.1 Il demone MySQL non parte](#Il_demone_MySQL_non_parte)
    *   [4.2 Impossibile eseguire mysql_upgrade perchè MySQL non parte](#Impossibile_eseguire_mysql_upgrade_perchè_MySQL_non_parte)
    *   [4.3 Resettare la password di amministratore](#Resettare_la_password_di_amministratore)
*   [5 Altre risorse](#Altre_risorse)

## Installazione

[Installare](/index.php/Pacman "Pacman") [mariadb](https://www.archlinux.org/packages/?name=mariadb), [libmariadbclient](https://www.archlinux.org/packages/?name=libmariadbclient) e [mariadb-clients](https://www.archlinux.org/packages/?name=mariadb-clients) dai [repository ufficiali](/index.php/Official_repositories "Official repositories"). Alcune implementazioni alternative sono [percona-server](https://www.archlinux.org/packages/?name=percona-server) and Oracle [mysql](https://aur.archlinux.org/packages/mysql/).

Avviare il demone `mysqld`, eseguire lo script di installazione e riavviare:

```
# systemctl start mysqld
# mysql_secure_installation
# systemctl restart mysqld

```

Sono disponibili le interfacce [mysql-gui-tools](https://aur.archlinux.org/packages/mysql-gui-tools/) e [mysql-workbench](https://www.archlinux.org/packages/?name=mysql-workbench).

### Passare da Oracle MySQL a MariaDB

Gli utenti che desiderano usare l'implementazione supportata devono installare **mariadb**, **libmariadbclient** o **mariadb-clients** ed eseguire `mysql_upgrade` per migrare i propri sistemi.

```
# systemctl stop mysqld
# pacman -S mariadb libmariadbclient mariadb-clients
# systemctl start mysqld
# mysql_upgrade -p

```

### Aggiornare

È opportuno l'uso di questo comando dopo l'aggiornamento e l'avvio di MySQL:

```
# mysql_upgrade -u root -p

```

## Configurazione

Una volta avviato il server MySQL, vorrete probabilmente aggiungere un account root con il quale gestire i database e gli utenti MySQL. Ciò è possibile o in maniera automatica, o manualmente, così come anticipato dall'output dello script precedente. O lanciate i comandi per settare la password per l'account root, oppure lanciate lo script di installazione sicura.

Ora potrete configurare il tutto dalla vostra interfaccia preferita. Per esempio usando la riga di comando di MySQL loggandovi come root sul vostro server MySQL:

```
$ mysql -p -u root

```

### Disabilitare l'accesso remoto

Il server MySQL è fin da subito accessibile dalla rete. Se MySQL severe solo al computer locale, si può migliorare la sicurezza evitando i controlli della porta TCP 3306\. Per rifiutare connesioni remote, togliete il commento alla seguente linea di `/etc/mysql/my.cnf`:

```
skip-networking

```

Questo non impedisce di connettersi al server sul computer locale.

### Abilitare il completamento automatico

**Note:** Questa procedura allunga i tempi di inizializzazione del client MySQL.

Il completamento automatico nel client MySQL è disabilitato di default. Per abilitarlo per tutti gli utenti bisogna modificare `/etc/mysql/my.cnf` e rimpiazzare `no-auto-rehash` con `auto-rehash`. Il completamento funzionerà dopo il riavvio del client MySQL.

## Backup

Il database può essere scaricato su un file per facilitare il backup. Il seguente script serve agevola l'operazione, creando il backup `db_backup.gz` nella stessa directory dello script:

```
#!/bin/bash

THISDIR=$(dirname $(readlink -f "$0"))

mysqldump --single-transaction --flush-logs --master-data=2 --all-databases \
  | gzip > $THISDIR/db_backup.gz
echo 'purge master logs before date_sub(now(), interval 7 day);' | mysql
```

Vedere ache la [pagina](http://dev.mysql.com/doc/refman/5.6/en/mysqldump.html) su `mysqldump`nel manuale di MySQL.

## Risoluzione di problemi

### Il demone MySQL non parte

Se MySQL non parte e non ci sono errori nei file di log, provate a verificare i permessi delle directory `/var/lib/mysql` e `/var/lib/mysql/mysql`. Se non appartengono a `mysql:mysql`, impostatelo voi:

```
 # chown mysql:mysql /var/lib/mysql -R

```

Se avete problemi di permessi anche dopo aver eseguito il comando, assicuratevi che esista una copia di `my.cnf` in `/etc/`:

```
 # cp /etc/mysql/my.cnf /etc/my.cnf

```

Riavviate.

Se leggete questi messaggi in `/var/lib/mysql/hostname.err`:

```
 [ERROR] Can't start server : Bind on unix socket: Permission denied
 [ERROR] Do you already have another mysqld server running on socket: /var/run/mysqld/mysqld.sock ?
 [ERROR] Aborting

```

`/var/run/mysqld` potrebbe avere i permessi sbagliati:

```
 # chown mysql:mysql /var/run/mysqld -R

```

Se **mysqld** mostra i seguenti errori:

```
Fatal error: Can’t open and lock privilege tables: Table ‘mysql.host’ doesn’t exist

```

Eseguite il comando per installare le tavole predefinite da `/usr`:

```
# cd /usr
# mysql_install_db --user=mysql --ldata=/var/lib/mysql/

```

### Impossibile eseguire mysql_upgrade perchè MySQL non parte

Provare in modalità di ripristino:

```
# mysqld_safe --datadir=/var/lib/mysql/

```

Eseguire:

```
# mysql_upgrade -u root -p

```

### Resettare la password di amministratore

Interrompere il servizio *mysqld*. Eseguire questo comando:

```
# mysqld_safe --skip-grant-tables &

```

Connettersi al server MySQL. Eseguire:

```
# mysql -u root mysql

```

Cambiare la password di amministratore:

```
 mysql> UPDATE mysql.user SET Password=PASSWORD('MyNewPass') WHERE User='root';
 mysql> FLUSH PRIVILEGES;
 mysql> exit

```

Riavviare il servizio *mysqld*.

## Altre risorse

*   [LAMP](/index.php/LAMP_(Italiano) "LAMP (Italiano)") - Articolo del wiki di Archlinux che si mostra come installare un server LAMP (Linux Apache MySQL PHP)
*   [http://mariadb.org/](http://mariadb.org/) - Implementazione comunitaria
*   [http://www.mysql.com/](http://www.mysql.com/) - Implementazione di Oracle
*   [http://www.percona.com/software](http://www.percona.com/software) - Implementazione di Percona