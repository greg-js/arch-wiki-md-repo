[XAMPP](http://www.apachefriends.org/en/xampp.html) è una distribuzione Apache facile da installare contenente MySQL, PHP e Perl. Il pacchetto contiene: Apache, MySQL, PHP & PEAR, Perl, ProFTPD, phpMyAdmin, OpenSSL, GD, Freetype2, libjpeg, libpng, gdbm, zlib, expat, Sablotron, libxml, Ming, Webalizer, pdf class, ncurses, mod_perl, FreeTDS, gettext, mcrypt, mhash, eAccelerator, SQLite e IMAP C-Client.

## Contents

*   [1 Installazione](#Installazione)
    *   [1.1 AUR](#AUR)
    *   [1.2 Manuale](#Manuale)
*   [2 Configurazione](#Configurazione)
*   [3 Avvio del server](#Avvio_del_server)
*   [4 Rimozione](#Rimozione)
*   [5 Cambiare la cartella predefinita "htdocs"](#Cambiare_la_cartella_predefinita_.22htdocs.22)

## Installazione

### AUR

*   Scaricate [xampp](https://aur.archlinux.org/packages/xampp/) da [AUR](/index.php/AUR "AUR")

### Manuale

1.  Scaricate l'ultima versione da [qui](http://www.apachefriends.org/en/xampp-linux.html#374).
2.  Da terminale entrate nella cartella in cui avete scaricato l'archivio e digitate quanto segue: `sudo tar xvfz xampp-linux-*.tar.gz -C /opt` 

**Note:** Se usate Archlinux a 64-bit, dovete installare `lib32-glibc` e `gcc-libs-multilib`. `sudo pacman -S lib32-glibc gcc-libs-multilib` per fare questo dovete aver attivato la multilib repositorie in /etc/pacman.conf

## Configurazione

Per configurare le singole parti di XAMPP basta modificare i seguenti files:

**/opt/lampp/etc/httpd.conf** - File di configurazione di Apache.

**/opt/lampp/etc/php.ini** - File di configurazione di PHP.

**/opt/lampp/phpmyadmin/config.inc.php** - File di configurazione di phpMyAdmin.

**/opt/lampp/etc/proftpd.conf** - File di configurazione di proFTP.

**/opt/lampp/etc/my.cnf** - File di configurazione di MySQL.

Se volete impostare la protezione del server, digitate semplicemente questo comando:

 `sudo /opt/lampp/lampp security` 

Vi verrà chiesto passo dopo passo di scegliere le password per l'accesso alle pagine web, l'utente "PMA" di phpMyAdmin, l'utente "root" per MySQL e l'utente "nobody" per ProFTP.

## Avvio del server

Usate i seguenti comandi per controllare XAMPP: `sudo /opt/lampp/lampp start,stop,restart` 

## Rimozione

Tutti i file necessari per XAMPP si trovano nella cartella /opt/lampp. Quindi, per disinstallare XAMPP, digitate questo comando:

 `# rm -rf /opt/lampp` 

**NOTA:** Se avete creato dei link simbolici dovete cancellare anche quelli!

## Cambiare la cartella predefinita "htdocs"

La web root si trova in **/opt/lampp/htdocs/**. Tutti i file inseriti in questa directory saranno processati dal web server.

Per aggiungere una cartella diversa da quella predefinita potete aggiungere un "alias".

*   Modificate il file httpd.conf con il vostro editor preferito.

```
# nano /opt/lampp/etc/httpd.conf

```

oppure

```
# vim /opt/lampp/etc/httpd.conf

```

*   trovato "DocumentRoot", vedrete qualcosa di simile:

```
DocumentRoot "/opt/lampp/htdocs"
<Directory "/opt/lampp/htdocs">
    ...    
    ...

</Directory>
```

*   Nella riga dopo "</Directory>" incollate questo, dove /home/web/ rappresenta, come esempio una cartella che avrete già creato:

```
<Directory "/home/web/">
    Options Indexes FollowSymLinks ExecCGI Includes
    AllowOverride All
    Require all granted
</Directory>
```

1.  Nella sezione alias, aggiungete un alias:

```
<IfModule alias_module>
    Alias /test /home/web/
        <directory /home/web/>
            AllowOverride FileInfo Limit Options Indexes
            Order allow,deny
            Allow from all
        </directory>

    ...    
    ...

</IfModule>

```

È necessario modificare i permessi. È possibile utilizzare il proprio nome utente, e lasciare l'impostazione di gruppo invariate. In tal caso, qualsiasi cartella in cui si ha accesso funzionerà. Un altro modo è quello di settare utente e gruppo in 'http', che dovrebbe già esistere. In questo caso, tutte le cartelle che si desidera consentire l'accesso devono appartenere al gruppo 'http'.

```
<IfModule !mpm_netware_module>
User http
Group http
</IfModule>
```
Ora non dimenticatevi di riavviare Apache: `/opt/lampp/lampp restart` 

Questa procedura vi permetterà di "hostare" i vostri files all'interno della home o di una qualsiasi cartella.

Nel precedente esempio potete accedere ai files digitando nel browser: **localhost/test**.