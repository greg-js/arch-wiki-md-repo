[Gitolite](https://github.com/sitaramc/gitolite/wiki/) allows you to host Git repositories for multiple users easily and securely.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Admin SSH access](#Admin_SSH_access)
    *   [2.2 Adding http(s) access via Apache (with basic authentication)](#Adding_http.28s.29_access_via_Apache_.28with_basic_authentication.29)
*   [3 Add users](#Add_users)
    *   [3.1 ssh users](#ssh_users)
    *   [3.2 http(s) users](#http.28s.29_users)
*   [4 Gitosis-like ssh usernames](#Gitosis-like_ssh_usernames)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [gitolite](https://www.archlinux.org/packages/?name=gitolite) package.

## Configuration

Installing gitolite automatically adds the *gitolite* user to the system, with home directory `/var/lib/gitolite`.

### Admin SSH access

To give you admin access, copy your SSH public key to `/var/lib/gitolite/*username*.pub`, where `username` is your username.

```
# install -o gitolite -g gitolite ~/.ssh/id_rsa.pub /var/lib/gitolite/*username*.pub

```

Then run the Gitolite setup script as the *gitolite* user.

```
# su - gitolite
$ gitolite setup -pk *username*.pub

```

This puts your public key into the gitolite-admin keydir and gives your username RW+ access to the gitolite-admin repository

You can now remove the SSH public key you copied and exit the *gitolite* user shell

```
$ rm *username*.pub
$ exit

```

Now as your user you can check that everything went correctly

 `$ ssh gitolite@*hostname* info` 
```
hello *username*, this is gitolite@*hostname* running gitolite3 v3.6.2 on git 2.3.3

 R W    gitolite-admin
 R W    testing

```

Do NOT add repositories or users directly as *gitolite* on the server! You MUST manage the server by cloning the special *gitolite-admin* repository

```
$ git clone gitolite@*hostname*:gitolite-admin

```

For reference see [Gitolite](https://github.com/sitaramc/gitolite/)

### Adding http(s) access via Apache (with basic authentication)

We need to create an suEXEC wrapper script. To satisfy suEXEC's security requirements, the script and the directory containing it must be owned by `gitolite:gitolite` and below `/srv/http` in the directory hierarchy. For this example, we create the directory as `/srv/http/git/cgi-bin`.

```
# install -o gitolite -g gitolite -d /srv/http/git/cgi-bin

```

Create an suEXEC wrapper for the gitolite shell with the contents below. For this example, we create it as `/srv/http/git/cgi-bin/gitolite-suexec-wrapper`.

 `/srv/http/git/cgi-bin/gitolite-suexec-wrapper` 
```
#!/usr/bin/bash
#
# suEXEC wrapper for gitolite-shell
#

export GIT_PROJECT_ROOT=/var/lib/gitolite/repositories
export GITOLITE_HTTP_HOME=/var/lib/gitolite

exec /usr/lib/gitolite/gitolite-shell
```

Make the wrapper executable and owned by `gitolite:gitolite`.

```
# chown gitolite:gitolite /srv/http/git/cgi-bin/gitolite-suexec-wrapper
# chmod 0755 /srv/http/git/cgi-bin/gitolite-suexec-wrapper

```

Create an empty password database file, owned by `gitolite:http`

```
# install -o gitolite -g http -m 0640 /dev/null /srv/http/git/htpasswd

```

Apache's basic authentication mechanism is separate from ssh, and therefore requires a separate set of credentials. Create your web users using `htpasswd`.

```
# htpasswd /srv/http/git/htpasswd *username*

```

Add the following to your Apache vhost configuration:

```
SuexecUserGroup gitolite gitolite
ScriptAlias /git/ /srv/http/git/cgi-bin/gitolite-suexec-wrapper/

<Directory /srv/http/git/cgi-bin>
    Require all granted
</Directory>

<Location /git>
    AuthType Basic
    AuthName "Git Access"
    AuthBasicProvider file
    AuthUserFile /srv/http/git/htpasswd
    Require valid-user
</Location>

```

Restart `httpd.service`.

Finally, in the gitolite-admin repository you cloned in the previous section, edit `conf/gitolite.conf`, add an `R = daemon` access rule to all repositories you want to make available via http, and push the changes.

## Add users

### ssh users

Ask each user who will get access to send you a public key. On their workstation generate the pair of ssh keys:

```
$ ssh-keygen

```

Rename each public key according to the user's name, with a .pub extension, like sitaram.pub or john-smith.pub. You can also use periods and underscores. Have the users send you the keys.

Copy all these *.pub files to keydir in your gitolite-admin repo clone. You can also organise them into various subdirectories of keydir if you wish, since the entire tree is searched.

Edit the config file (conf/gitolite.conf in your admin repo clone). See the gitolite.conf documentation ([http://sitaramc.github.com/gitolite/admin.html#conf](http://sitaramc.github.com/gitolite/admin.html#conf)) for details on what goes in that file, syntax, etc. Just add new repos as needed, and add new users and give them permissions as required. The users names should be exactly the same as their keyfile names, but without the .pub extension

```
$ nano conf/gitolite.conf

```

Commit and push the changes them:

```
$ git commit -a
$ git push

```

### http(s) users

User management for http(s) is more suitable for single-user setups. To add a new user or to change an existing user's password:

```
# htpasswd /srv/http/git/htpasswd *username*

```

## Gitosis-like ssh usernames

If you want to distinguish users with the same login (like `username@server1`, `username@server2`) you may want to do the following (tested with [gitolite](https://www.archlinux.org/packages/?name=gitolite) 3.04-1):

*   edit `/usr/lib/gitolite/triggers/post-compile/ssh-authkeys` and replace

```
$user =~ s/(\@[^.]+)?\.pub$//;    # baz.pub, baz@home.pub -> baz

```

by

```
$user =~ s/\.pub$//;              # baz@home.pub -> baz@home

```

*   update authorized_keys file (for example, by pushing into the *gitolite-admin* repository)

## See also

[http://sitaramc.github.com/gitolite/index.html](http://sitaramc.github.com/gitolite/index.html)