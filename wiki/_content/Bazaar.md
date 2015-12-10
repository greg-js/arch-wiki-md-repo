# Bazaar

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

**This article is a stub.**

**Notes:** please use the first argument of the template to provide more detailed indications. (Discuss in [Talk:Bazaar#](https://wiki.archlinux.org/index.php/Talk:Bazaar))

## Setting up bzr server with xinetd

*   Install bzr package

```
 pacman -S bzr

```

*   Add <bzr-user> if needed
*   Create repo:

```
 bzr init /home/bzr/repo.bzr
 chown -R <bzr-user> /home/bzr/repo.bzr

```

*   Add config for xinetd:

```
service bzr
{
	flags			= REUSE
	socket_type		= stream
	wait			= no
	user			= <bzr-user>
	server			= /usr/bin/bzr
	server_args		= serve --inet --directory=/home/bzr/repo.bzr
	env			= HOME=/home/bzr
	log_on_failure		+= USERID
	disable			= no
	cps			= 50 10
	instances		= 60
}

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Bazaar&oldid=207130](https://wiki.archlinux.org/index.php?title=Bazaar&oldid=207130)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Version Control System](/index.php/Category:Version_Control_System "Category:Version Control System")