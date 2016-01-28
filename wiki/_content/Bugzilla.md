# Bugzilla

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [LAMP](/index.php/LAMP "LAMP")
*   [MariaDB](/index.php/MariaDB "MariaDB")
*   [Sqlite](/index.php/Sqlite "Sqlite")

[Bugzilla](http://www.bugzilla.org/) is server software designed to help you manage software development.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Module Dependencies](#Module_Dependencies)
    *   [2.2 Missing Modules](#Missing_Modules)
    *   [2.3 Final Module Check](#Final_Module_Check)
    *   [2.4 Apache](#Apache)
*   [3 See also](#See_also)

## Installation

You can [install](/index.php/Install "Install") [bugzilla](https://www.archlinux.org/packages/?name=bugzilla) from the [official repositories](/index.php/Official_repositories "Official repositories").

It requires a bunch of [perl](https://www.archlinux.org/packages/?name=perl) modules to be installed too, but some required modules still need to be installed manually

## Configuration

### Module Dependencies

Make a module check first:

```
# cd /srv/http/bugzilla
# ./checksetup.pl --check-modules

```

Check the screen output, you will learn which module is required and which is optional, for missing modules, it will also show you the shell command to install them.

Install all required and optional modules using:

```
# perl install-module.pl -all

```

### Missing Modules

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** No bug report, if there is none file one (Discuss in [Talk:Bugzilla#](https://wiki.archlinux.org/index.php/Talk:Bugzilla))

**Warning:** BugZilla _may_ have missing dependencies that can effect normal usage and prevent the final configuration from completing successfully.

Because of a missing dependency, the following perl module needs to be installed for user creation and bug filing to work properly:

```
# perl install-module.pl DateTime:TimeZone

```

Absence of **Email-Abstract** will generate an error on the final module check and configuration for BugZilla 5.0rc2 (in the next step). To fix this, issue the command:

 `BugZilla v5.0rc2` 

```
 # perl install-module.pl Email::Abstract

```

There is an [open bug](https://bugzilla.mozilla.org/show_bug.cgi?id=1129046) for the above issue

### Final Module Check

Next, some more configuration to let bugzilla know how to connect mysql and create initial tables in it.

Run checksetup.pl again, this time without the –check-modules switch:

```
# ./checksetup.pl

```

A file called "localconfig" is generated if everything is ok. Then edit it, modify some parameters there:

```
$webservergroup = 'http';
$db_driver = 'DATABASE_TO_USE_HERE';
$db_name = 'DATABASE_NAME_HERE';
$db_user = 'DATABASE_USER_HERE';
$db_pass = 'YOUR_PASSWORD_HERE';

```

### Apache

Finally, configure apache to run bugzilla using mod_cgi (also can be configured using mod_perl, refer this for details)

First uncomment the following line in /etc/httpd/conf/httpd.conf:

```
LoadModule cgi_module modules/mod_cgi.so

```

Then add the following lines to /etc/httpd/conf/httpd.conf:

```
<Directory /srv/http/bugzilla>
  AddHandler cgi-script .cgi
  Options +ExecCGI
  DirectoryIndex index.cgi
  AllowOverride All
</Directory>

```

Now restart apache and required modules.

Access [http://server-domain-or-ip/bugzilla/](http://server-domain-or-ip/bugzilla/) using your web browser.

## See also

*   [bugzilla documentation](http://www.bugzilla.org/docs/)
*   [http://blog.samsonis.me/2009/04/bugzilla-on-archlinux/](http://blog.samsonis.me/2009/04/bugzilla-on-archlinux/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Bugzilla&oldid=412047](https://wiki.archlinux.org/index.php?title=Bugzilla&oldid=412047)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Web server](/index.php/Category:Web_server "Category:Web server")
*   [Development](/index.php/Category:Development "Category:Development")

Hidden category:

*   [Pages or sections flagged with Template:Style](/index.php/Category:Pages_or_sections_flagged_with_Template:Style "Category:Pages or sections flagged with Template:Style")