Questo documento descrive come impostare Drupal (5.0-rc1) con Apache, MySQL o PostgreSQL, PHP, e Postfix! Questo documento presuppone che si abbiano server già impostati quali LAMP(Apache, MySQL, PHP) o LAPP(Apache, PostgreSQL, PHP).

## Contents

*   [1 Installazione GD](#Installazione_GD)
*   [2 Installare Postfix](#Installare_Postfix)
*   [3 Installare e Impostare Drupal](#Installare_e_Impostare_Drupal)
*   [4 Extra](#Extra)

## Installazione GD

Drupal preferisce avere installata la libreria "GD image" assicurarsi perciò di averla prima di continuare.

1.  Installare il pacchetto
     ` pacman -S gd` 
2.  Aprire il file **`/etc/php.ini`** col proprio editor prescelto `es. nano /etc/php.ini` 
3.  Cercare la riga che inizia con, ";extension=gd.so" e cambiarla in, "extension=gd.so". (Rimuovere solo il primo ";"). Se la riga non fosse presente, aggiungerla. Questa riga può trovarsi nella sezione "Dynamic Extensions", oppure proprio verso la fine di quel file.
4.  Riavviare il server web Apache `/etc/rc.d/httpd restart` 

## Installare Postfix

Postfix è necessario per inviare e-mail da drupal. Queste sono utili per la verifica degli account, il recupero della password, etc.

1.  Installare Postfix ` pacman -S postfix ` 
2.  Configurare Postfix come necessario ` nano /etc/postfix/main.cf ` Tutto ciò che si deve fare è modificare gli hostname sotto "Internet Host and Domain Names" ` hostname = hostname1 `  ` hostname = hostname2` 
3.  Inviare una e-mail di test a se stessi ` mail myusername@localhost ` (Immettere un soggetto, qualche parola nel corpo, poi premere ctrl+d per uscire e inviare la lettera) Aspettare 10 seconds, e dopo digitare `mail` per controllare la propria mail. Se l'avete ricevuta, eccellente.
4.  Se si ha un router assicurarsi che la Porta 25 sia inoltrata così che le mail possano essere inviate attraverso internet
5.  Aprire il file **`/etc/php.ini`** con il proprio editor prescelto, ad esempio `nano /etc/php.ini` 
6.  Cercare la riga che inizia con, **`;sendmail_path=""` **e modificarla in, **`sendmail_path="/usr/sbin/sendmail -t -i"`**
7.  Riavviate il server web Apache `/etc/rc.d/httpd restart` 

## Installare e Impostare Drupal

Così come l'ultima release 5.0, Drupal ha un nuovo sistema di installazione.

1.  Scaricare l'ultimo pacchetto da [http://drupal.org](http://drupal.org) ed estrarlo.
2.  Spostare le directory nella propria **`/home/httpd/html/` **.
3.  Aprire un browser web, e accedere a "localhost"
4.  Seguire le istruzioni delle pagine, e drupal dovrebbe auto-impostarsi e portarsi al login!

## Extra

Drupal richiede di eseguire dei job a tempo, ogni ora. Dal momento che non si sono esaminati per vedere cosa essi fanno, è possibile eseguire i job manualmente attraverso il pannello dell'amministratore. Se si crede, copiare l'esatto script dalla directory "scripts" in "/etc/cron.hourly" e renderlo eseguibile.