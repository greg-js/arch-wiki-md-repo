[Gitolite](https://github.com/sitaramc/gitolite/wiki/) allows you to host Git repositories for multiple users easily and securely.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Admin SSH access](#Admin_SSH_access)
    *   [2.2 Adding http(s) access via Apache (with basic authentication)](#Adding_http.28s.29_access_via_Apache_.28with_basic_authentication.29)
*   [3 Add users](#Add_users)
    *   [3.1 ssh users](#ssh_users)
    *   [3.2 http(s) users](#http.28s.29_users)
*   [4 Troubleshooting](#Troubleshooting)
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
# sudo -u gitolite gitolite setup -pk /var/lib/gitolite/*username*.pub

```

This puts your public key into the gitolite-admin keydir and gives your username RW+ access to the gitolite-admin repository

You can now remove the copy of your SSH public key

```
# rm /var/lib/gitolite/*username*.pub

```

Now as your user you can check that everything went correctly

 `$ ssh gitolite@*hostname* info` 
```
hello *username*, this is gitolite@*hostname* running gitolite3 v3.6.2 on git 2.3.3

 R W    gitolite-admin
 R W    testing

```

Do **not** add repositories or users directly as *gitolite* on the server! The server **must** be managed by cloning the special *gitolite-admin* repository

```
$ git clone gitolite@*hostname*:gitolite-admin

```

For reference see [Gitolite](https://github.com/sitaramc/gitolite/).

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

Ask each user who will get access to send you an [SSH public key](/index.php/SSH_keys "SSH keys"). Rename each public key to `*username*.pub`, where `*username*` is the user name which will be used in `gitolite.conf`. Then move all new public keys to the `keydir` directory in the cloned `gitolite-admin` repo. You can also organise them into various subdirectories of `keydir` if you wish, since the entire tree is searched.

Finally commit and push the changes:

```
$ git commit -a
$ git push

```

See the [add/remove users](http://gitolite.com/gitolite/basic-admin/#addremove-users) in the official documentation for details.

To grant access rights to the new users, edit the config file (`conf/gitolite.conf` in the `gitolite-admin` repo). See [the "conf" file](http://gitolite.com/gitolite/conf/) in the official documentation for details.

### http(s) users

User management for http(s) is more suitable for single-user setups. To add a new user or to change an existing user's password:

```
# htpasswd /srv/http/git/htpasswd *username*

```

## Troubleshooting

In case you cannot log in with the gitolite account, it may be caused by the account being locked, and depending of your ssh configuration.

If you have done some SSH hardening, it may be the cause of this behavior, as noted in [SSH and locked users Article](http://arlimus.github.io/articles/usepam/) and [Unix & Linux StackExchange - How to unlock account for public key ssh authorization, but not for password authorization](http://unix.stackexchange.com/questions/193066/how-to-unlock-account-for-public-key-ssh-authorization-but-not-for-password-aut).

To solve this you have to allow PAM in `sshd_config` or unlock the account by:

```
# usermod -p '*' gitolite

```
 `/etc/passwd` 
```
...
gitolite:*:16199:0:99999:7:::
...

```

**Warning:** Do not leave the account in the state left by `passwd -u` (with a blank password field). Doing that will allow logins without entering a password!

## See also

*   [Gitolite Site](http://sitaramc.github.com/gitolite/index.html)
*   [SSH and locked users Article](http://arlimus.github.io/articles/usepam/)
*   [Unix & Linux StackExchange - How to unlock account for public key ssh authorization, but not for password authorization](http://unix.stackexchange.com/questions/193066/how-to-unlock-account-for-public-key-ssh-authorization-but-not-for-password-aut)