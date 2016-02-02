# Odoo

[Odoo](https://www.odoo.com/) (formerly OpenERP) is Enterprise Resource Planning software. It provides a complete, integrated ERP solution for small and medium sized businesses and organizations. Odoo includes financial and analytic accounting, warehouse and inventory management, sales and purchase management, customer and supplier relations management, association management, tasks automation, human resource management, marketing campaign, document management, help desk, e-commerce integration, and point of sale functionality.

Odoo features an application server which uses PostgreSQL as database back-end, with a web-based client. It is written in the Python programming language, with a highly modular design which allows for the rapid development of new modules through Open Object RAD. Odoo developers have a strong commitment to free software.

A thriving support and development community has grown up around Odoo, providing free technical support, bug-fixing, new development, and support services. Odoo provides extensive documentation in various electronic formats, as well as hardcopy. The company responsible for development of Odoo earns profits through partnership services with Odoo consultants, and by providing support, training, hosting services, software development, and software quality testing and verification.

**Note:** Much of the documentation for Odoo, including the remainder of this article, still refers to the old name OpenERP.

## Contents

*   [1 Before Installing](#Before_Installing)
    *   [1.1 Installing PostgreSQL](#Installing_PostgreSQL)
    *   [1.2 Configuring PostgreSQL for remote use over a network](#Configuring_PostgreSQL_for_remote_use_over_a_network)
    *   [1.3 Setting up PostgreSQL to run with OpenERP](#Setting_up_PostgreSQL_to_run_with_OpenERP)
*   [2 Installation and configuration](#Installation_and_configuration)
    *   [2.1 Installation](#Installation)
    *   [2.2 Configuration](#Configuration)
    *   [2.3 Starting the server](#Starting_the_server)
    *   [2.4 Logging in](#Logging_in)
*   [3 Additional OpenERP Documentation](#Additional_OpenERP_Documentation)
*   [4 OpenERP Community](#OpenERP_Community)
*   [5 Open Object RAD](#Open_Object_RAD)

## Before Installing

### Installing PostgreSQL

OpenERP uses the PostgreSQL database, which should be installed and configured before installing OpenERP. Follow [PostgreSQL#Installing PostgreSQL](/index.php/PostgreSQL#Installing_PostgreSQL "PostgreSQL"). Complete these installation instructions, but do **not** perform any other configuration from that page. Return to this page for additional configuration steps.

### Configuring PostgreSQL for remote use over a network

The by default, PostgreSQL only accepts connections from the local machine. If you plan to run PostgreSQL and OpenERP on different machines, you will need to follow [PostgreSQL#Configure PostgreSQL to be accessible from remote hosts](/index.php/PostgreSQL#Configure_PostgreSQL_to_be_accessible_from_remote_hosts "PostgreSQL").

### Setting up PostgreSQL to run with OpenERP

Next, it is necessary to create a new PostgreSQL user for OpenERP.

First, log in as the default PostgreSQL superuser, 'postgres', by executing the following command from the CLI:

*   If you have [sudo](https://www.archlinux.org/packages/?name=sudo) set up:

```
$ sudo -i -u postgres

```

*   Otherwise:

```
$ su
# su - postgres

```

Once logged in as _postgres_, begin the process of creating the _openerp_ database user, with the following command:

```
[postgres]$ createuser _openerp_ --interactive -P

```

You will first be asked for a password. For highly secure yet easy to remember passwords, consider using a [Diceware Passphrase](http://world.std.com/~reinhold/diceware.html). Re-enter the password as requested. The next three questions should be answered in sequence with n, y, and n. Shall the new role be a superuser? n Shall the new role be allowed to create database? y Shall the new role be allowed to create more new roles? n

You may also use options as below to skip the interactive questions to set the attributes:

```
[postgres]$ createuser _openerp_ --createdb --login --no-superuser --no-createrole -P

```

Once you are finished answering these questions, type `exit` to log out from _postgres_ and return to your regular user.

This completes the installation and setup of PostgreSQL for use with OpenERP under Arch Linux. Additional detailed information about PostgreSQL configuration may be found in the [PostgreSQL](/index.php/PostgreSQL "PostgreSQL") article, and the [PostgreSQL Manuals webpage](http://www.postgresql.org/docs/manuals/). Also, there is a powerful GUI PostgreSQL Admin tool, [pgAdmin](http://www.pgadmin.org/), which is available in the Arch repositories.

## Installation and configuration

OpenERP requires the installation of the OpenERP Server, OpenERP comes with a webserver so you can use your web browser to use it. Currently, OpenERP is not available in the official repositories, but it is available through the Arch User Repository.

### Installation

Install [odoo_8.0](https://aur.archlinux.org/packages/odoo_8.0/) from the [AUR](/index.php/AUR "AUR"), which is the new stable version of OpenERP. However the postgres database of odoo is not compatible with Openerp's. you might lose your data during the upgrade. If you want to try old version, install [openerp](https://aur.archlinux.org/packages/openerp/).

### Configuration

The configuration file of OpenERP server is at `/etc/openerp/openerp-server.conf`. Edit `db_user` and `db_password`. If the PostgreSQL server is on a different machine, also edit `db_host`.

```
 [options]
 ; This is the password that allows database operations:
 ; admin_passwd = admin
 db_host = localhost
 db_port = 5432
 db_user = _openerp_
 db_password = _password_

```

If you need help with configuration, please run `python2 /bin/openerp-server --help`

### Starting the server

Use the command below to enable autostart openerp server at boot:

```
# systemctl enable openerp.service

```

Use the command below to start openerp:

```
# systemctl start openerp.service

```

### Logging in

Go to [http://localhost:8069](http://localhost:8069) in your web browser and you will be greeted by the OpenERP login page.

## Additional OpenERP Documentation

There are various sources of OpenERP documentation. The best place to start is the [OpenERP Documentation webpage](http://doc.openerp.com/). This page links to different online documents, including [detailed installation instructions](http://doc.openerp.com/install/index.html). Additionally, there is an online copy of the book, ["OpenERP for Retail and Industrial Management"](http://doc.openerp.com/book/index.html),and can be purchased from [Amazon.com](http://www.amazon.com/Open-ERP-Retail-Industrial-Management/dp/2960087607/). While OpenERP documentation, such as "OpenERP for Retail and Industrial Management" is freely downloadable, it does not come with a free documentation license.

## OpenERP Community

The OpenERP Community is centered upon the [Open Object website](http://openobject.com/). Free technical support for OpenERP may be found in the [webforums](http://openobject.com/forum/index.php), a [mailing list](http://tiny.be/mailman/listinfo/tinyerp-users) which is linked to the webforums, an [IRC channel](http://openobject.com/irc/) on freenode.net, an [OpenERP wiki](http://www.openobject.com/wiki/index.php/Main_Page), and the [Official ERP Documentation webpage.](http://doc.openerp.com/) The latest news may be found on [OpenERP Planet](http://openerp.com/planet/), while various OpenERP screencasts are provided on [OpenERP TV](http://www.openerp.tv/). Fee-based support services are provided by [OpenERP Partners](http://openerp.com/en/partners.html).

## Open Object RAD

Open Object is the Python-based [Rapid Application Development framework](http://openobject.com/index.php?option=com_content&view=article&id=46&Itemid=53) for developing OpenERP modules. It allows developers and businesses to customize OpenERP for specific needs. Open Object RAD development work is centered upon the [Open Object Launchpad page](https://launchpad.net/openobject). Developer news and blogs are published on [Open Object Planet](http://openobject.com/planet/). There are pages for [software downloads](http://www.openerp.com/index.php?option=com_content&view=article&id=18&Itemid=28), [OpenERP module downloads](http://doc.openerp.com/modindex.html), and [development source code downloads](http://openobject.com/index.php?option=com_content&view=article&id=53&Itemid=61).

Retrieved from "[https://wiki.archlinux.org/index.php?title=Odoo&oldid=392511](https://wiki.archlinux.org/index.php?title=Odoo&oldid=392511)"