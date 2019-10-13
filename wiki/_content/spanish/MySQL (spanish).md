**Estado de la traducción**
Este artículo es una traducción de [MySQL](/index.php/MySQL "MySQL"), revisada por última vez el **2019-10-10**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=MySQL&diff=0&oldid=583449) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[MySQL](https://en.wikipedia.org/wiki/es:MySQL "wikipedia:es:MySQL") es una base de datos SQL multiusuario y multihilo muy extendida, desarrollada por Oracle.

Arch Linux favorece [MariaDB](/index.php/MariaDB "MariaDB"), una bifurcación de MySQL desarrollada por la comunidad, que apunta a la compatibilidad directa. MySQL de Oracle fue [desplazada](https://www.archlinux.org/news/mariadb-replaces-mysql-in-repositories/) hacia [AUR](/index.php/AUR_(Espa%C3%B1ol) "AUR (Español)"): [mysql](https://aur.archlinux.org/packages/mysql/). Otra bifurcación que apunta a ser totalmente compatible es [Percona Server](https://en.wikipedia.org/wiki/Percona_Server_for_MySQL "wikipedia:Percona Server for MySQL"), disponible como [percona-server](https://www.archlinux.org/packages/?name=percona-server).

El motor de almacenamiento [InnoDB](https://en.wikipedia.org/wiki/es:InnoDB "wikipedia:es:InnoDB") de Oracle fue también bifurcado por Percona como [XtraDB](https://en.wikipedia.org/wiki/XtraDB "wikipedia:XtraDB"). La bifurcación es utilizada por ambas, [MariaDB](/index.php/MariaDB "MariaDB") y Percona Server.

## Herramientas gráficas

*   **[phpMyAdmin](/index.php/PhpMyAdmin "PhpMyAdmin")** — Interfaz web para MySQL, escrito en PHP.

	[https://www.phpmyadmin.net](https://www.phpmyadmin.net) || [phpmyadmin](https://www.archlinux.org/packages/?name=phpmyadmin)

*   **[MySQL Workbench](https://en.wikipedia.org/wiki/MySQL_Workbench "wikipedia:MySQL Workbench")** — Herramienta visual unificada para arquitectos, desarrolladores y administradores de bases de datos. Está desarrollado por Oracle y no se garantiza que funcione con [MariaDB](/index.php/MariaDB "MariaDB").

	[https://www.mysql.com/products/workbench/](https://www.mysql.com/products/workbench/) || [mysql-workbench](https://www.archlinux.org/packages/?name=mysql-workbench)

Para herramientas que soporten múltiples DBMS, véase [List of applications/Documents#Database tools](/index.php/List_of_applications/Documents#Database_tools "List of applications/Documents").

## Herramientas de consola

*   **MyCLI** — Un cliente de terminal para MySQL con autocompletado y resaltado de sintaxis.

	[https://www.mycli.net](https://www.mycli.net) || [mycli](https://aur.archlinux.org/packages/mycli/)

## Acceso programado

*   [JDBC y MySQL](/index.php/JDBC_and_MySQL "JDBC and MySQL")
*   [PHP#MySQL/MariaDB](/index.php/PHP#MySQL/MariaDB "PHP")
*   [Python](/index.php/Python_(Espa%C3%B1ol) "Python (Español)")
    *   [mysql-python](https://www.archlinux.org/packages/?name=mysql-python)
    *   [python-mysqlclient](https://www.archlinux.org/packages/?name=python-mysqlclient)
    *   [python-mysql-connector](https://www.archlinux.org/packages/?name=python-mysql-connector), [python2-mysql-connector](https://www.archlinux.org/packages/?name=python2-mysql-connector)
*   [C++](/index.php/C%2B%2B_(Espa%C3%B1ol) "C++ (Español)")
    *   [mysql++](https://www.archlinux.org/packages/?name=mysql%2B%2B)
*   [Perl](/index.php/Perl "Perl")
    *   [perl-dbd-mysql](https://www.archlinux.org/packages/?name=perl-dbd-mysql)