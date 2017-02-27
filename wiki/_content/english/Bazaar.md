[Bazaar](https://bazaar.canonical.com/) is a version control system that helps you track project history over time and to collaborate easily with others.

## Installation

Install the [bzr](https://www.archlinux.org/packages/?name=bzr) package. For the development version, install the [bzr-bzr](https://aur.archlinux.org/packages/bzr-bzr/) package. The Bazaar Explorer is provided by the [bzr-explorer](https://aur.archlinux.org/packages/bzr-explorer/) package.

## Setting up Bazaar server with xinetd

Add a `*bzr-usr*` [user](/index.php/User "User") if needed.

Create a repository:

```
$ bzr init /home/bzr/repo.bzr
$ chown -R *bzr_usr* /home/bzr/repo.bzr

```

Add configuration for *xinetd*:

```
service bzr
{
	flags			= REUSE
	socket_type		= stream
	wait			= no
	user			= *bzr_usr*
	server			= /usr/bin/bzr
	server_args		= serve --inet --directory=/home/bzr/repo.bzr
	env			= HOME=/home/bzr
	log_on_failure		+= USERID
	disable			= no
	cps			= 50 10
	instances		= 60
}
```