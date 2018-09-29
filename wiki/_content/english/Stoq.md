[Stoq](http://www.stoq.com.br) is a suite of open-source enterprise management.

Stoq application uses [PostgreSQL](/index.php/PostgreSQL "PostgreSQL") as database back-end, with a graphical interface client.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Installing Stoq](#Installing_Stoq)
    *   [1.2 Configure Stoq](#Configure_Stoq)
        *   [1.2.1 Connect to the database locally](#Connect_to_the_database_locally)
        *   [1.2.2 Manually configure the database connection](#Manually_configure_the_database_connection)
        *   [1.2.3 Stoq configuration file](#Stoq_configuration_file)
    *   [1.3 Installing stoq-server](#Installing_stoq-server)
    *   [1.4 Configure stoq-server](#Configure_stoq-server)
        *   [1.4.1 Stoq-server configuration file](#Stoq-server_configuration_file)
    *   [1.5 Accessing serial](#Accessing_serial)
*   [2 Additional documentation](#Additional_documentation)

## Installation

### Installing Stoq

[Install](/index.php/Install "Install") the [stoq](https://aur.archlinux.org/packages/stoq/) package. The dependency of [webkitgtk](https://aur.archlinux.org/packages/webkitgtk/) take long time for installation process.

### Configure Stoq

After running Stoq for the first time, you will need to configure the database location. In this step there are two options for the client connect to the database:

*   Connect to the database locally;
*   Manually configure the database connection.

#### Connect to the database locally

To connect to the database locall, you must [install](/index.php/Install "Install") the [postgresql](https://www.archlinux.org/packages/?name=postgresql).

If the PostgreSQL database cluster has not been initialized yet, please follow the [PostgreSQL#Initial_configuration](/index.php/PostgreSQL#Initial_configuration "PostgreSQL") first.

As root, [start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") the `postgresql.service`.

On the screen "Database location" use the option "I want to use Stoq just on this computer".

#### Manually configure the database connection

On the screen "Database location" use the option "I want to manually configure the database connection" and fill the details about the database.

#### Stoq configuration file

The main Stoq configuration file is located at `~/.stoq/stoq.conf`.

### Installing stoq-server

[Install](/index.php/Install "Install") the [stoq-server](https://aur.archlinux.org/packages/stoq-server/) package. Then [set a password](/index.php/Users_and_groups#Example_adding_a_user "Users and groups") for the newly created *stoqserver* user.

### Configure stoq-server

If the PostgreSQL database cluster has not been initialized yet, please follow the [PostgreSQL#Initial_configuration](/index.php/PostgreSQL#Initial_configuration "PostgreSQL") first.

As root, [start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") the `postgresql.service`.

It is necessary to create a new PostgreSQL configuration for stoqserver. For that log in as the default PostgreSQL superuser, 'postgres', by executing the following command:

*   If you have [sudo](https://www.archlinux.org/packages/?name=sudo) and your username is in `sudoers`:

	 `$ sudo -u postgres -i` 

*   Otherwise:

```
$ su
# su -l postgres

```

Use stoqsconf script to generate the necessary configuration files:

```
[postgres]$ stoqsconf -p 5432 -D "/usr/share/stoqserver"

```

Where:

*   the `-p` is the port that PostgreSQL uses to remote conecctions;
*   and `-D` is the location where the configuration files of stoq-server must be stored.

Return to the regular user using `exit`.

In order for the stoq-server to be accessible remotely it is necessary to follow the article [Configure PostgreSQL to be accessible from remote hosts](/index.php/PostgreSQL#Configure_PostgreSQL_to_be_accessible_from_remote_hosts "PostgreSQL").

As root, [start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") the `supervisord.service`.

Restart the supervisor process:

```
# supervisorctl update

```

```
# supervisorctl restart stoqserver

```

#### Stoq-server configuration file

The main stoqserver configuration file is located at `/usr/share/stoqserver/.stoq/stoq.conf`.

### Accessing serial

The stoqserver communicates with the computer via a serial connection or a serial over USB connection. So the user needs read/write access to the serial device file. [Udev](/index.php/Udev "Udev") creates files in `/dev/tts/` owned by group `uucp` so adding the user to the `uucp` group gives the required read/write access.

```
# gpasswd -a stoqserver uucp

```

**Note:** You will have to logout and login again for this to take effect.

## Additional documentation

Therefore, reading the [wiki](https://wiki.stoq.com.br/index.php/Getting_started) and the [manual](https://doc.stoq.com.br/manual/latest/) of Stoq (manual only in Portuguese).