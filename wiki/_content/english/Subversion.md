[Apache Subversion](http://subversion.apache.org/features.html) is "a full-featured version control system originally designed to be a better [CVS](/index.php/CVS "CVS"). Subversion has since expanded beyond its original goal of replacing CVS, but its basic model, design, and interface remain heavily influenced by that goal."

This article deals with setting up an svn-server on your machine. There are two popular svn-servers, the built in *svnserve* and the more advanced option, [Apache HTTP Server](/index.php/Apache_HTTP_Server "Apache HTTP Server") with svn plugins.

## Contents

*   [1 Apache Subversion setup](#Apache_Subversion_setup)
    *   [1.1 Goals](#Goals)
    *   [1.2 Installation](#Installation)
    *   [1.3 Subversion configuration](#Subversion_configuration)
        *   [1.3.1 Edit /etc/httpd/conf/httpd.conf](#Edit_/etc/httpd/conf/httpd.conf)
        *   [1.3.2 To SSL or not to SSL?](#To_SSL_or_not_to_SSL?)
        *   [1.3.3 Create /home/svn/.svn-policy-file](#Create_/home/svn/.svn-policy-file)
        *   [1.3.4 Create /home/svn/.svn-auth-file](#Create_/home/svn/.svn-auth-file)
        *   [1.3.5 Create a repository](#Create_a_repository)
        *   [1.3.6 Set permissions](#Set_permissions)
    *   [1.4 Create a project](#Create_a_project)
        *   [1.4.1 Directory structure for project](#Directory_structure_for_project)
        *   [1.4.2 Populate directory](#Populate_directory)
        *   [1.4.3 Import the project](#Import_the_project)
        *   [1.4.4 Test SVN checkout](#Test_SVN_checkout)
*   [2 Svnserve setup](#Svnserve_setup)
    *   [2.1 Install the package](#Install_the_package)
    *   [2.2 Create a repository](#Create_a_repository_2)
    *   [2.3 Set access policies](#Set_access_policies)
    *   [2.4 Start the server daemon](#Start_the_server_daemon)
    *   [2.5 svn+ssh](#svn+ssh)
*   [3 Subversion backup and restore](#Subversion_backup_and_restore)
*   [4 Subversion clients](#Subversion_clients)
*   [5 See also](#See_also)

## Apache Subversion setup

### Goals

The goal of this how to is to setup Subversion, with Apache. Why use Apache for Subversion? Well, quite simply, it provides features that the standalone `svnserve` does not have...

*   HTTPS support. This is more secure than the MD5 authentication used by svnserve.
*   fine-grained access controls. You can use Apache auth to limit permissions by directory. This means you can grant read access to everything, but commit access only to trunk for instance, while have another group with commit access to tags or branches.
*   a free repository viewer
*   The Subversion team is working on seamless WebDAV integration. At some point you should be able to use any WebDAV interface to update files in the repository.

### Installation

Install [Apache HTTP Server](/index.php/Apache_HTTP_Server "Apache HTTP Server") as described in its article.

Besides Apache, you will only need to [install](/index.php/Install "Install") the [subversion](https://www.archlinux.org/packages/?name=subversion) package.

### Subversion configuration

Create a directory for your repositories:

```
# mkdir -p /home/svn/repositories

```

#### Edit /etc/httpd/conf/httpd.conf

Ensure the following are listed...if not, add them (you will typically have to add just the last two), they must be in this order:

```
LoadModule dav_module           modules/mod_dav.so
LoadModule dav_fs_module        modules/mod_dav_fs.so
LoadModule dav_svn_module       modules/mod_dav_svn.so
LoadModule authz_svn_module     modules/mod_authz_svn.so

```

#### To SSL or not to SSL?

SSL for SVN access has a few benefits, for instance it allows you to use Apache's AuthType Basic, with little fear of someone sniffing passwords.

Generate the certificate by:

```
# cd /etc/httpd/conf/
# openssl req -new -x509 -keyout server.key -out server.crt -days 365 -nodes

```

Add the following to `/etc/httpd/conf/extra/httpd-ssl.conf` (or to `/etc/httpd/conf/extra/httpd-vhosts.conf` if you are not using ssl). Include the following inside of a virtual host directive:

```
<Location /svn>
   DAV svn
   SVNParentPath /home/svn/repositories
   AuthzSVNAccessFile /home/svn/.svn-policy-file
   AuthName "SVN Repositories"
   AuthType Basic
   AuthUserFile /home/svn/.svn-auth-file
   Require valid-user
</Location>

```

To make sure the SSL settings get loaded, uncomment the SSL configuration line in `/etc/httpd/conf/httpd.conf` so it looks like this:

```
LoadModule ssl_module modules/mod_ssl.so
LoadModule socache_shmcb_module modules/mod_socache_shmcb.so
Include /etc/httpd/conf/extra/httpd-ssl.conf

```

#### Create /home/svn/.svn-policy-file

```
[/]
* = r

[REPO_NAME:/]
USER_NAME = rw

```

The * in the / section is matched to anonymous users. Any access above and beyond read only will be prompted for a user/pass by apache AuthType Basic. The REPO_NAME:/ section inherits permissions from those above, so anon users have read only permission to it. The last bit grants read/write permission of the REPO_NAME repository to the user USER_NAME.

#### Create /home/svn/.svn-auth-file

This is either an htpasswd, or htdigest file. I used htpasswd. Again, because of SSL, I do not worry as much about password sniffing. htdigest would provide even more security vs. sniffing, but at this point, I do not have a need for it. Run the following command

```
# htpasswd -cs /home/svn/.svn-auth-file USER_NAME

```

The above creates the file (`-c`) and uses SHA-1 for storing the password (`-s`). The user `USER_NAME` is created.

To add additional users, leave off the (`-c`) flag.

```
# htpasswd -s /home/svn/.svn-auth-file OTHER_USER_NAME

```

#### Create a repository

```
# svnadmin create /home/svn/repositories/REPO_NAME

```

#### Set permissions

The Apache user needs permissions over the new repository.

```
# chown -R http:http /home/svn/repositories/REPO_NAME

```

### Create a project

#### Directory structure for project

Create a temporary directory with the `branches` `tags` `trunk` directory structure on your development machine.

```
$ mkdir -p ~/svn-import/{branches,tags,trunk}

```

#### Populate directory

Copy or move your project source files into the created trunk directory.

```
$ cp -R /my/existing/project/* ~/svn-import/trunk

```

#### Import the project

```
$ svn import -m "Initial import" ~/svn-import [https://yourdomain.net/svn/REPO_NAME/](https://yourdomain.net/svn/REPO_NAME/)

```

#### Test SVN checkout

```
$ svn checkout [https://yourdomain.net/svn/REPO_NAME/](https://yourdomain.net/svn/REPO_NAME/) /my/svn/working/copy

```

If everything worked out, you should now have a working, checked out copy of your freshly created SVN repo.

## Svnserve setup

### Install the package

Install the [subversion](https://www.archlinux.org/packages/?name=subversion) package.

### Create a repository

Create your repository

```
mkdir /path/to/repos/
svnadmin create /path/to/repos/repo1

```

Your initial repository is empty, if you want to import files into it, use the following command.

```
svn import ~/code/project1 file:///path/to/repos/repo1 --message 'Initial repository layout'

```

### Set access policies

Edit the file /path/to/repos/repo1/conf/svnserve.conf and uncomment or add the line under [general]

```
password-db = passwd

```

You might also want to change the default option for anonymous users.

```
anon-access = read

```

Replace "read" with "write" for a repository that anyone can commit to, or set it to "none" to disable all anonymous access.

Now edit the file /path/to/repos/repo1/conf/passwd

```
[users]
harry = foopassword
sally = barpassword

```

The above defines users harry and sally, with passwords foopassword and barpassword, change it as you like

### Start the server daemon

Before you start the server, edit the configuration file:

 `/etc/conf.d/svnserve`  `SVNSERVE_ARGS="--root=/path/to/repos"` 

The `--root=/path/to/repos` option set the root of repository tree. If you have multiple repositories use `--root=/path-to/reposparent`. Then access independent repositories by passing in repository name in the URL: `[svn://host/repo1](svn://host/repo1)`. make sure that the user has read/write access to the repository files)

Optionally add a `--listen-port` if you want a different port, or other options.

By default, the service runs as root. If you want to change that, add a drop-in:

 `/etc/systemd/system/svnserve.service.d/50-custom.conf` 
```
[Service]
User=svn
```

Now start the *svnserve.service* [daemon](/index.php/Daemon "Daemon").

### svn+ssh

To use svn+ssh://, we have to have a wrapper written for svnserve.

check where the svnserve binary is located:

```
 # which svnserve
/usr/local/bin/svnserve

```

Our wrapper is going to have to fall in PATH prior to this location...

create wrapper:

```
# touch /usr/bin/svnserve
# chmod 755 /usr/bin/svnserve 

```

now edit it to look like so:

```
/usr/bin/svnserve 
#!/bin/sh
# wrapper script for svnserve
umask 007
/usr/local/bin/svnserve -r /path/to "$@"

```

`-r /path/to` is what makes use of the svn co svn+[ssh://server.domain.com:/reponame](ssh://server.domain.com:/reponame) instead of `:/path/to/reponame`.

Start svnserve with new wrapper script like so:

```
# /usr/bin/svnserve -d  ( start daemon mode )

```

we can also check the perms for remote users like this:

```
$ svn ls svn+ssh://server.domain.com:/reponame
++server.domain.com++
dev/
qa/
release/

```

## Subversion backup and restore

To back up your subversion repositories,do this for each repository you have.

```
$ svnadmin dump /path/to/reponame > /tmp/reponame.dump
$ scp -rp /tmp/reponame.dump user@server.domain.com:/tmp/

```

To restore the backup, create the corresponding repositories first:

```
svnadmin create /path/to/reponame

```

Then load svn dump into new repo:

```
svnadmin load /path/to/reponame < /tmp/repo1.dump

```

Setting Permissions:

```
chown -R svn:svnusers /path/to/reponame ; 
chmod -R g+w /path/to/reponame/db/

```

These repositories should now be all setup.

## Subversion clients

See also [Wikipedia:Comparison of Subversion clients](https://en.wikipedia.org/wiki/Comparison_of_Subversion_clients "wikipedia:Comparison of Subversion clients").

*   **kdesvn** — Subversion client for KDE.

	[https://cgit.kde.org/kdesvn.git/](https://cgit.kde.org/kdesvn.git/) || [kdesvn](https://www.archlinux.org/packages/?name=kdesvn)

*   **[RabbitVCS](https://en.wikipedia.org/wiki/RabbitVCS "wikipedia:RabbitVCS")** — Set of graphical tools written to provide simple and straightforward access to the version control systems you use.

	[http://rabbitvcs.org/](http://rabbitvcs.org/) || [rabbitvcs](https://aur.archlinux.org/packages/rabbitvcs/)

*   **[RapidSVN](https://en.wikipedia.org/wiki/RapidSVN "wikipedia:RapidSVN")** — GUI front-end for the Subversion revision system written in C++ using the wxWidgets framework.

	[http://rapidsvn.tigris.org/](http://rapidsvn.tigris.org/) || [rapidsvn](https://aur.archlinux.org/packages/rapidsvn/)

## See also

*   [http://svnbook.red-bean.com/en/1.1/svn-book.html#svn-ch-9-sect-2.2-re-load](http://svnbook.red-bean.com/en/1.1/svn-book.html#svn-ch-9-sect-2.2-re-load)
*   [https://subversion.apache.org/](https://subversion.apache.org/)