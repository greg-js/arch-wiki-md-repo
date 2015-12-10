# Cobalt strike

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** See [Help:Style](/index.php/Help:Style "Help:Style"). (Discuss in [Talk:Cobalt strike#](https://wiki.archlinux.org/index.php/Talk:Cobalt_strike))

Cobalt Strike is penetration testing software that executes targeted attacks and replicates advanced threats.

## Contents

*   [1 Requirements](#Requirements)
*   [2 Dependencies](#Dependencies)
*   [3 setting up postgres](#setting_up_postgres)
*   [4 Enable required services](#Enable_required_services)
*   [5 Troubleshooting](#Troubleshooting)

## Requirements

*   metasploit
*   postgresql
*   database.yml # can set via MSF_DATABASE_CONFIG env

## Dependencies

sudo pacman -S postgresql metasploit

## setting up postgres

passwd postgress # set password  
su - postgres -c "initdb -D '/var/lib/postgres/data'" # create db, some people recommended the appending the "--locale en_US.UTF-8 " flag

## Enable required services

```
sudo systemctl start postgresql
./msfconsole # should be enough to start metasploit service listening on 127.0.0.1:55553

```

```
# copy sample yml database file for MSF_DATABASE_CONFIG env
cp /usr/share/metasploit/config/database.yml.example  /usr/share/metasploit/config/database.yml 

```

```
#
# you should change the default creds in the database.yml
# ~/.msf4/ ... database.yml is not there.
#

```

```
msfrpcd -a 127.0.0.1 -U [user] -P [pass] -S -f # instead of msfcli?

```

```
# run cobaltstrike
sudo MSF_DATABASE_CONFIG=/usr/share/metasploit/config/database.yml ./cobaltstrike

```

```
#
# use same user/pass combo to connect to cobalt strike server as you did for msfrpcd 
#

```

## Troubleshooting

*   if stuck at "progress" popup that says "login failed, your creds may not be correct (make sure they're the same as the msfrpcd creds)  

*   is /usr/share/metasploit/config/database.yml derived from metasploit? or is it unique?

Retrieved from "[https://wiki.archlinux.org/index.php?title=Cobalt_strike&oldid=370928](https://wiki.archlinux.org/index.php?title=Cobalt_strike&oldid=370928)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Security](/index.php/Category:Security "Category:Security")