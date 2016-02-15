[Odoo](https://www.odoo.com) (formerly known as OpenERP and before that, TinyERP) is a suite of open-source enterprise management applications. Targeting companies of all sizes, the application suite includes billing, accounting, manufacturing, purchasing, warehouse management, and project management.

Odoo features an application server which uses PostgreSQL as database back-end, with a web-based client. Odoo is written in Python, with a highly modular design which allows rapid development of new modules through Open Object RAD. Odoo developers have a strong commitment to free software.

A thriving support and development community has grown up around Odoo, providing free technical support, bug-fixing, new development, and support services. Odoo provides extensive documentation in various electronic formats, as well as hardcopy. The company responsible for development of Odoo earns profits through partnership services with Odoo consultants, and by providing support, training, hosting services, software development, and software quality testing and verification.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Installing Odoo](#Installing_Odoo)
    *   [1.2 Configuring PostgreSQL to run with Odoo](#Configuring_PostgreSQL_to_run_with_Odoo)
    *   [1.3 Configuring Odoo to run with PostgreSQL](#Configuring_Odoo_to_run_with_PostgreSQL)
    *   [1.4 Starting the server](#Starting_the_server)
    *   [1.5 Logging in](#Logging_in)
*   [2 Additional documentation](#Additional_documentation)

## Installation

### Installing Odoo

Install the [odoo](https://aur.archlinux.org/packages/odoo/) package. Please note that the Odoo package comes with a bunch of python2 packages available in the [AUR](/index.php/AUR "AUR"). These dependencies and the size of Odoo require much disk space to be used (1.8Gio only for the source and the final Odoo pkg without its dependencies). If you are building manually in the current directory (i.e. without [AUR helpers](/index.php/AUR_helpers "AUR helpers")), please make sure your current directory is on a device with enough free space. If you are using an AUR helper, please [increase the size of your tmpfs](/index.php/Tmpfs#Examples "Tmpfs") or use an option specific to your AUR helper. [Yaourt](/index.php/Yaourt "Yaourt") for example allows you to specify your own destination for building packages; for this, see the `TMPDIR` statement from `/etc/yaourtrc`.

### Configuring PostgreSQL to run with Odoo

Odoo uses PostgreSQL as the database backend. The latter should have been installed with the odoo package as [postgresql](https://www.archlinux.org/packages/?name=postgresql) comes as a dependency.

It is necessary to create a new PostgreSQL user for Odoo. For that log in as the default PostgreSQL superuser, 'postgres', by executing the following command:

*   If you have [sudo](https://www.archlinux.org/packages/?name=sudo) and your username is in `sudoers`:

	 `$ sudo -i -u postgres` 

*   Otherwise:

```
$ su
# su - postgres

```

If the PostgreSQL instance has not been initialized yet, please follow first the [PostgreSQL install process](/index.php/PostgreSQL#Installing_PostgreSQL "PostgreSQL").

Once logged as the 'postgres' user, create the database user (called _role_ in the PostgreSQL ) _odoo_ with the command that follows.

*   where _--interactive_ is used to prompt for missing role name and attributes rather than using defaults
*   and _--pwprompt'_ is used to assign a password to the new role

You will first be asked for a password. For highly secure yet easy to remember passwords, consider using a [Diceware Passphrase](http://world.std.com/~reinhold/diceware.html). Re-enter the password as requested. The next three questions should be answered in sequence with n, y, and n.

```
$ createuser odoo --interactive --pwprompt
Enter password for new role: 
Enter it again: 
Shall the new role be a superuser? (y/n) n
Shall the new role be allowed to create databases? (y/n) y
Shall the new role be allowed to create more new roles? (y/n) n

```

You can also use the following command line to specify the options to skip the interactive questions:

```
[postgres]$ createuser _odoo_ --createdb --login --no-superuser --no-createrole --pwprompt

```

Once you are finished answering these questions, type `exit` to return to your regular user.

This completes the required installation and setup of PostgreSQL for use with Odoo under Arch Linux. Additional detailed information about PostgreSQL configuration can be found in the [PostgreSQL](/index.php/PostgreSQL "PostgreSQL") article. By default, PostgreSQL only accepts connections from the local machine. If you plan to run PostgreSQL and Odoo on two different machines, you will need to follow [PostgreSQL#Configure PostgreSQL to be accessible from remote hosts](/index.php/PostgreSQL#Configure_PostgreSQL_to_be_accessible_from_remote_hosts "PostgreSQL").

### Configuring Odoo to run with PostgreSQL

The configuration file of Odoo is located at `/etc/odo/odoo.conf`. Specify the `db_user` and `db_password` according to the username and password you specified at previous step. If the PostgreSQL server is on a different machine, also edit `db_host`.

```
[options]
; This is the password that allows database operations:
; admin_passwd = admin
db_host = False
db_port = False
db_user = odoo
db_password = False
addons_path = /usr/lib/python2.7/site-packages/openerp/addons

```

### Starting the server

Ensure PostgreSQL is running and enabled first before running the following commands.

Use the command below to start odoo automatically at boot:

```
# systemctl enable odoo.service

```

Use the command below to start odoo:

```
# systemctl start odoo.service

```

### Logging in

Go to [http://localhost:8069](http://localhost:8069) in your web browser to access the Odoo login page.

## Additional documentation

As Odoo is a complete enterprise solution, it might be rather complex to use for newcomers. Therefore, reading the [Odoo User Documentation](https://www.odoo.com/documentation/user/9.0/) and [Odoo technical documentation](https://www.odoo.com/documentation/9.0/) is highly advised.