# mod_perl

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

**This article is a stub.**

**Notes:** please use the first argument of the template to provide more detailed indications. (Discuss in [Talk:Mod perl#](https://wiki.archlinux.org/index.php/Talk:Mod_perl))

## Contents

*   [1 Enabling Perl + Apache](#Enabling_Perl_.2B_Apache)
    *   [1.1 Allow perl to execute scripts for certain directories](#Allow_perl_to_execute_scripts_for_certain_directories)
        *   [1.1.1 Alternative 1: Using virtual hosts](#Alternative_1:_Using_virtual_hosts)
        *   [1.1.2 Alternative 2: Just enable for a certain subdirectory](#Alternative_2:_Just_enable_for_a_certain_subdirectory)
    *   [1.2 Turn on perl for directory listings](#Turn_on_perl_for_directory_listings)
    *   [1.3 Try it out](#Try_it_out)

## Enabling Perl + Apache

Install [mod_perl](https://aur.archlinux.org/packages/mod_perl/)<sup><small>AUR</small></sup>.

Add this to `httpd.conf`:

```
LoadModule perl_module modules/mod_perl.so

```

### Allow perl to execute scripts for certain directories

There are two possible methods: creating a virtual host, or enabling perl for a subdirectory.

#### Alternative 1: Using virtual hosts

Add a virtual host with various settings in extra/httpd-vhosts.conf:

```
<VirtualHost perlwebtest:80>
	Servername perlwebtest
	DocumentRoot /srv/http/perlwebtest
	ErrorLog /var/log/httpd/perlwebtest-error.log
	CustomLog /var/log/httpd/perlwebtest-access.log combined
	<Directory /srv/http/perlwebtest>
		AddHandler perl-script .pl
		PerlResponseHandler ModPerl::Registry
		Options +ExecCGI
		PerlOptions +ParseHeaders
		AllowOverride All
		Order allow,deny
		Allow from all
	</Directory>
</VirtualHost>

```

Ensure `/etc/httpd/conf/httpd.conf` includes the line

```
Include conf/extra/httpd-vhosts.conf

```

Make sure you do not have "Options Indexes FollowSymLinks"!

Add "perlwebtest" as localhost in `/etc/hosts`:

```
127.0.0.1	localhost YOURHOSTNAME perlwebtest

```

Use your hostname instead of `YOURHOSTNAME`.

#### Alternative 2: Just enable for a certain subdirectory

Add the following to `/etc/httpd/conf/httpd.conf`:

```
Alias /perlwebtest/ /srv/http/perlwebtest/
<Location /perlwebtest/>
      AddHandler perl-script .pl
      AddHandler perl-script .cgi
      PerlResponseHandler ModPerl::Registry
      PerlOptions +ParseHeaders
      Options +ExecCGI
      Order allow,deny
      Allow from all
</Location>

```

### Turn on perl for directory listings

Create `/etc/httpd/conf/extra/perl_module.conf` as well:

```
# Required modules: dir_module, perl_module

<IfModule dir_module>
        <IfModule perl_module>
                DirectoryIndex index.pl index.html
        </IfModule>
</IfModule>

```

Then include it in `/etc/httpd/conf/httpd.conf`:

```
# Perl
Include conf/extra/perl_module.conf

```

### Try it out

Create `index.pl` in `/srv/http/perlwebtest`:

```
#!/usr/bin/perl
print "Content-type: text/plain\n\n";
print "mod_perl now works\n";

```

Restart apache:

```
# systemctl restart httpd

```

Usually you can just reload:

```
# systemctl reload httpd

```

Then visit [http://perlwebtest](http://perlwebtest) (if you created a virtual host) or [http://localhost/perlwebtest](http://localhost/perlwebtest) (if you only enabled one directory).

Retrieved from "[https://wiki.archlinux.org/index.php?title=Mod_perl&oldid=399414](https://wiki.archlinux.org/index.php?title=Mod_perl&oldid=399414)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Web server](/index.php/Category:Web_server "Category:Web server")