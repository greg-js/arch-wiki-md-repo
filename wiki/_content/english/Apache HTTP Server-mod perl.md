From the [project](http://perl.apache.org/):

	mod_perl brings together the full power of the Perl programming language and the [Apache HTTP Server](/index.php/Apache_HTTP_Server "Apache HTTP Server"). You can use Perl to manage Apache, respond to requests for web pages and much more.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Allow perl to execute scripts for certain directories](#Allow_perl_to_execute_scripts_for_certain_directories)
        *   [2.1.1 Using virtual hosts](#Using_virtual_hosts)
        *   [2.1.2 For a subdirectory](#For_a_subdirectory)
    *   [2.2 Turn on perl for directory listings](#Turn_on_perl_for_directory_listings)
    *   [2.3 Try it out](#Try_it_out)

## Installation

Install the [mod_perl](https://aur.archlinux.org/packages/mod_perl/) package.

## Configuration

Load the module via the main Apache configuration file `httpd.conf`:

```
LoadModule perl_module modules/mod_perl.so

```

### Allow perl to execute scripts for certain directories

There are two possible methods to enable the `mod_perl` module:

*   [#Using virtual hosts](#Using_virtual_hosts), or
*   [#For a subdirectory](#For_a_subdirectory).

#### Using virtual hosts

Add a virtual host with settings. For example:

 `/etc/httpd/conf/extra/httpd-vhosts.conf` 
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

Ensure `/etc/httpd/conf/httpd.conf` includes the created virtual host:

```
Include conf/extra/httpd-vhosts.conf

```

Make sure it does not have `Options Indexes FollowSymLinks`!

Add "perlwebtest" as localhost in `/etc/hosts`, using the machine's hostname for *yourhostname*:

```
127.0.0.1	localhost *yourhostname* perlwebtest

```

#### For a subdirectory

Add the following to the main configuration file:

 `<code>/etc/httpd/conf/httpd.conf</code>` 
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
print "Content-type: text/plain

";
print "mod_perl now works
";

```

[Restart](/index.php/Restart "Restart") apache's `httpd.service` and let it [reload](/index.php/Reload "Reload") the configuration.

Finally, depending on chosen alternative configuration, visit

*   [http://perlwebtest](http://perlwebtest) for [#Using virtual hosts](#Using_virtual_hosts), or
*   [http://localhost/perlwebtest](http://localhost/perlwebtest) for [#For a subdirectory](#For_a_subdirectory)