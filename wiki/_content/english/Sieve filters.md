[Sieve](https://en.wikipedia.org/wiki/Sieve_(mail_filtering_language) is a programming language that can be used to create filters for email on mail server.

## Servers

[pigeonhole](https://www.archlinux.org/packages/?name=pigeonhole) can be used with [Dovecot](/index.php/Dovecot "Dovecot"). It implements the ManageSieve protocol.

## Client tools

To manage sieve filters remotely, clients exist for servers implementing the ManageSieve protocol ([RFC 5804](https://tools.ietf.org/html/rfc5804)

*   **sieve-connect** — Client for the MANAGESIEVE protocol

	[https://people.spodhuis.org/phil.pennock/software/](https://people.spodhuis.org/phil.pennock/software/) || [sieve-connect](https://aur.archlinux.org/packages/sieve-connect/)

*   **Thunderbird sieve** — This Extension implements the ManageSieve protocol for securely managing Sieve Script on a remote IMAP server

	[https://github.com/thsmi/sieve](https://github.com/thsmi/sieve) || [thunderbird-sieve](https://aur.archlinux.org/packages/thunderbird-sieve/)

### sieve-connect

To connect:

```
$ sieve-connect -s mail.example.com -u user@example.com

```

Then the help is short and explicit:

```
> help

```