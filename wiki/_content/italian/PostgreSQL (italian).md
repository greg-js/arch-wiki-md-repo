Questo documento descrive come installare PostgreSQL. Descrive anche come rendere PostgreSQL accessibile da un client remoto.

## Contents

*   [1 Installare PostgreSQL](#Installare_PostgreSQL)
*   [2 Creare il primo Database/User](#Creare_il_primo_Database.2FUser)
*   [3 Familiarizzare con PostgreSQL](#Familiarizzare_con_PostgreSQL)
    *   [3.1 Accedere alla shell del database](#Accedere_alla_shell_del_database)

## Installare PostgreSQL

*   Installare postgresql

```
# pacman -S postgresql

```

*   Avviare il server PostgreSQL

```
# systemctl start postgresql

```

*   In caso di errore, inizializzare il database

```
#su postgres
#initdb -D /path_a_scelta/

```

*   (Facoltativo) Aggiungi PostgreSQL alla lista dei demoni da avviare con il sistema:

```
# systemctl enable postgresql

```

## Creare il primo Database/User

*   Aggiungi un nuovo utente database usando il comando [createuser](http://www.postgresql.org/docs/9.0/static/app-createuser.html).

Se crei un utente come il tuo utente di login ($USER) ti permetterà di accedere al datatabase di postgresql senza avere un utente specifico per loggarti.

esempio per creare un superuser

```
 $ createuser -s -U postgres
 $ Enter name of role to add: myUsualArchLoginName

```

*   Crea un nuovo database dove l'utente appena creato abbia permessi di lettura/scrittura usando il comando [createdb](http://www.postgresql.org/docs/9.0/static/app-createdb.html).

```
 $ createdb [nome db]

```

se nome db viene omesso, il database verrà nominato come l'utente.

## Familiarizzare con PostgreSQL

### Accedere alla shell del database

*   Avvia la shell del database con [psql](http://www.postgresql.org/docs/8.3/static/app-psql.html), qui puoi gestire il database.

Usa "-d" per accedere al database creato, se non specificato verrà aperto il database nominato come il tuo nome utente.

```
  $ psql -d myDatabaseName

```

Alcuni comandi utili:

*   Connettersi ad un particolare database

```
=> \c <database>

```

*   Avere una lista degli utenti e dei loro permessi

```
=> \du

```

*   Visualizza un sommario sulle tabelle nel database corrente

```
=> \dt

```

*   Uscire dalla shell

```
=> \q or CTRL+d

```

Ci sono ovviamente molti più comandi, ma questi ti aiuteranno ad iniziare.