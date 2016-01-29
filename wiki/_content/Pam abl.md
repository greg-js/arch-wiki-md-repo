# Pam abl

Related articles

*   [One Time PassWord](/index.php/One_Time_PassWord "One Time PassWord")
*   [S/KEY Authentication](/index.php/S/KEY_Authentication "S/KEY Authentication")
*   [Secure Shell](/index.php/Secure_Shell "Secure Shell")
*   [Using SSH Keys](/index.php/Using_SSH_Keys "Using SSH Keys")
*   [A Cure for the Common SSH Login Attack](/index.php/A_Cure_for_the_Common_SSH_Login_Attack "A Cure for the Common SSH Login Attack")

**Pam_abl** provides another layer of security against brute-force SSH password guessing. It allows you to set a maximum number of unsuccessful login attempts within a given time period, after which a host and/or user is blacklisted. Once a host/user is blacklisted, all authentication attempts will fail even if the correct password is given. Hosts/users which stop attempting to login for a specified period of time will be removed from the blacklist.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Add pam_abl to the PAM auth stack](#Add_pam_abl_to_the_PAM_auth_stack)
    *   [2.2 Create pam_abl.conf](#Create_pam_abl.conf)
    *   [2.3 Create the blacklist databases](#Create_the_blacklist_databases)
*   [3 Managing the blacklist databases](#Managing_the_blacklist_databases)
    *   [3.1 Check blacklisted hosts/users](#Check_blacklisted_hosts.2Fusers)
    *   [3.2 Manually removed a host or user from the blacklist](#Manually_removed_a_host_or_user_from_the_blacklist)
    *   [3.3 Manually add a host or user to the blacklist](#Manually_add_a_host_or_user_to_the_blacklist)
    *   [3.4 Other pam_abl commands](#Other_pam_abl_commands)
*   [4 Known Issues](#Known_Issues)

## Installation

Install the [pam_abl](https://aur.archlinux.org/packages/pam_abl/)<sup><small>AUR</small></sup> PKGBUILD from the [AUR](/index.php/AUR "AUR") using [makepkg](/index.php/Makepkg "Makepkg").

## Configuration

### Add pam_abl to the PAM auth stack

Open `/etc/pam.d/sshd` as root in your editor of choice. Add the following line above all other lines:

```
auth            required        pam_abl.so config=/etc/security/pam_abl.conf

```

Assuming you haven't made any other modifications, your `/etc/pam.d/sshd` should now look like this:

```
#%PAM-1.0
auth            required        pam_abl.so config=/etc/security/pam_abl.conf
auth            include         system-login
account         include         system-login
password        include         system-login
session         include         system-login

```

Note that this only enables pam_abl for ssh. Other services will not be affected.

### Create pam_abl.conf

Create `/etc/security/pam_abl.conf` by copying over the sample configuration file:

```
# cp /etc/security/pam_abl.conf.example /etc/security/pam_abl.conf

```

As of version 0.6.0, the sample configuration looks like this:

```
db_home=/var/lib/abl
host_db=/var/lib/abl/hosts.db
host_purge=1d
host_rule=*:30/1h
user_db=/var/lib/abl/users.db
user_purge=1d
user_rule=*:3/1h
host_clear_cmd=[logger] [clear] [host] [%h]
host_block_cmd=[logger] [block] [host] [%h]
user_clear_cmd=[logger] [clear] [user] [%u]
user_block_cmd=[logger] [block] [user] [%u]
limits=1000-1200
host_whitelist=1.1.1.1/24;2.1.1.1
user_whitelist=danta;chris

```

See `man pam_abl.conf` for details on how to customize the rules and other settings.

### Create the blacklist databases

As root, create the directory for the database (assuming you specified the recommended path above):

```
# mkdir /var/lib/abl

```

As root, run the pam_abl utility to initialize the databases:

```
# pam_abl

```

That's it! Pam_abl should now be working. Since PAM is not a daemon, nothing needs to be restarted for these changes to take effect. It's strongly recommended to verify that pam_abl is working by purposely getting a remote host blacklisted. Don't worry though! For directions on how to manually remove a host or user from the blacklist, see below.

## Managing the blacklist databases

### Check blacklisted hosts/users

As root, simply run:

```
# pam_abl

```

**Note:** As pam_abl does not run as a daemon, it performs "lazy purging" of the blacklist. In other words, it does not remove users/hosts from the blacklist until an authentication attempt occurs. This does not affect functionality, although it will frequently cause extra failures to show up when running the above command. To force a purge, run:

```
# pam_abl -p

```

### Manually removed a host or user from the blacklist

As root, simply run:

```
# pam_abl -w -U <user>

```

or

```
# pam_abl -w -H <host>

```

Using * as a wildcard to match multiple hosts/users is allowed in both of the above commands.

### Manually add a host or user to the blacklist

As root, simply run:

```
# pam_abl -f -U <user>

```

or

```
# pam_abl -f -H <host>

```

### Other pam_abl commands

Like virtually all linux utilities, a manpage is available to see all options:

```
$ man pam_abl

```

## Known Issues

The current version (0.6.0) of pam_abl has a problem that can affect its ability to blacklist under specific conditions.

Due to the way sshd operates and the way pam modules are passed information, failure of a given attempt is not logged until either a second attempt is made or the connection is closed. This means that long as the attacker only makes one attempt per connection, and never closes any connections, no failures are ever logged.

In practice, the sshd_config settings "MaxStartups" (default 10) and to a lesser degree "LoginGraceTime" (default 120s) limit the viability of this approach, but it still could be used to squeeze out more attempts then you specify.

In the meantime, the workaround is to set "MaxAuthTries" to 1 (or expect that an additional "MaxStartups" number of attempts could be made above and beyond what you specify in your pam_abl config).

Retrieved from "[https://wiki.archlinux.org/index.php?title=Pam_abl&oldid=409101](https://wiki.archlinux.org/index.php?title=Pam_abl&oldid=409101)"