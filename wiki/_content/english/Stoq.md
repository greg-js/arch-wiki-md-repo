[Stoq](http://www.stoq.com.br) is a suite of open-source enterprise management.

Stoq application uses PostgreSQL as database back-end, with a graphical interface client.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Installing Stoq](#Installing_Stoq)
    *   [1.2 Installing stoq-server](#Installing_stoq-server)
    *   [1.3 Accessing serial](#Accessing_serial)
*   [2 Additional documentation](#Additional_documentation)

## Installation

### Installing Stoq

Install the [stoq](https://aur.archlinux.org/packages/stoq/) package. Please note that the Stoq package comes with a bunch of python2 packages available in the [AUR](/index.php/AUR "AUR"). The dependency of [webkitgtk2](https://aur.archlinux.org/packages/webkitgtk2/) take long time for installation process.

The main Stoq configuration file is located at ~/.stoq/stoq.conf.

### Installing stoq-server

Install the [stoq-server](https://aur.archlinux.org/packages/stoq-server/) package. Then [set a password](/index.php/Users_and_groups#Example_adding_a_user "Users and groups") for the newly created *stoqserver* user.

As root, [start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") the `postgresql.service`. If the PostgreSQL instance has not been initialized yet, please follow first the [PostgreSQL install process](/index.php/PostgreSQL#Installing_PostgreSQL "PostgreSQL").

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

The main stoqserver configuration file is located at /usr/share/stoqserver/.stoq/stoq.conf.

As root, [start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") the `supervisord.service`.

Restart the supervisor process:

```
# supervisorctl update

```

```
# supervisorctl restart stoqserver

```

It's necessary [start](/index.php/Start "Start") or [enable](/index.php/Enable "Enable") the `postgresql.service` and `supervisord.service` before start Stoq with stoqserver.

### Accessing serial

The stoqserver communicates with the computer via a serial connection or a serial over USB connection. So the user needs read/write access to the serial device file. [Udev](/index.php/Udev "Udev") creates files in `/dev/tts/` owned by group `uucp` so adding the user to the `uucp` group gives the required read/write access.

```
# gpasswd -a stoqserver uucp

```

**Note:** You will have to logout and login again for this to take effect.

## Additional documentation

Therefore, reading the [Stoq Manual](https://doc.stoq.com.br/manual/latest/).