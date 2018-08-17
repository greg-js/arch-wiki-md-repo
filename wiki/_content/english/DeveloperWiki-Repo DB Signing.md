## Contents

*   [1 [RFC] Repo DB signing (and ISO's/other artefacts)](#.5BRFC.5D_Repo_DB_signing_.28and_ISO.27s.2Fother_artefacts.29)
    *   [1.1 Proposed solutions](#Proposed_solutions)
        *   [1.1.1 Signing from a 'secure' enclave (solution 1)](#Signing_from_a_.27secure.27_enclave_.28solution_1.29)
        *   [1.1.2 Signing from a 'secure' enclave (solution 2)](#Signing_from_a_.27secure.27_enclave_.28solution_2.29)
    *   [1.2 Comparison benefits/pitfalls](#Comparison_benefits.2Fpitfalls)
    *   [1.3 Solutions in other distro's](#Solutions_in_other_distro.27s)
        *   [1.3.1 Debian](#Debian)
        *   [1.3.2 OpenSuSe build service](#OpenSuSe_build_service)
        *   [1.3.3 Fedora](#Fedora)
    *   [1.4 Open issues](#Open_issues)

## [RFC] Repo DB signing (and ISO's/other artefacts)

Our repository DB's are currently unsigned due to security concerns of having GPG private keys on the server which add's packages to the repository. However we want to sign our db's, iso's and other artefacts automatically so some compromises have to be made.

Several discussions have taken place about this topic:

*   [https://www.mail-archive.com/arch-dev-public@archlinux.org/msg25635.html](https://www.mail-archive.com/arch-dev-public@archlinux.org/msg25635.html)

Signing the repository database is as easy as:

```
repo-add -v -s foo.db pacman-3.0.0-1-x86_64.pkg.tar.gz
lrwxrwxrwx 1 jelle users  13 Aug 15 20:56 foo.db -> foo.db.tar.gz
lrwxrwxrwx 1 jelle users  17 Aug 15 20:56 foo.db.sig -> foo.db.tar.gz.sig
-rw-r--r-- 1 jelle users 504 Aug 15 20:56 foo.db.tar.gz
-rw-r--r-- 1 jelle users 503 Aug 15 20:56 foo.db.tar.gz.old
-rw-r--r-- 1 jelle users 310 Aug 15 20:56 foo.db.tar.gz.sig
lrwxrwxrwx 1 jelle users  16 Aug 15 20:56 foo.files -> foo.files.tar.gz
lrwxrwxrwx 1 jelle users  20 Aug 15 20:56 foo.files.sig -> 
foo.files.tar.gz.sig
-rw-r--r-- 1 jelle users 782 Aug 15 20:56 foo.files.tar.gz
-rw-r--r-- 1 jelle users 782 Aug 15 20:56 foo.files.tar.gz.old
-rw-r--r-- 1 jelle users 310 Aug 15 20:56 foo.files.tar.gz.sig

```

repo-add signs the repo as following:

```
gpg --detach-sign --use-agent --no-armor

```

Either intended or not, repo-add can just sign the db without adding packages.

```
repo-add foo.db.tar.gz -s

```

### Proposed solutions

#### Signing from a 'secure' enclave (solution 1)

Create a dedicated signing host which received files and then returns the signature.

A few restrictions should be added to this host:

*   rate limiting of signing (sign iso only once per month)
*   record signed artefacts securely
*   request coming from a specific IP (this should only be repos.archlinux.org)
*   Authentication (SSH?)
*   Separate host or Virtual Machine or Container?
*   Minimal access list

See proposal of [Bluewind](https://www.mail-archive.com/arch-dev-public@archlinux.org/msg25636.html).

#### Signing from a 'secure' enclave (solution 2)

Instead of sending arbitrary files into the 'secure' enclave, the enclave pulls the to be signed file and returns a new signed file.

Workflow:

1.  A DB changing action is fired, repos are locked.
2.  A new DB file is created and put into a temporary location.
3.  A notification is sent to (or more exactly retrieved by) the secure enclave telling there is a new DB file to sign.
4.  The secure enclaves retrieves the file to sign.
5.  It signs it, and (optionally, TBD) logs that it did.
6.  It uploads the signature back to the DB server.
7.  The DB server moves the DB and its sig in place, release the repos lock and resets the notification channel.

Global implementation details:

1.  Nothing special/new here.
2.  Here there is the need to put the new generated DB somewhere specific.
3.  Two possibilities (mainly) at this point for the DB changing action to notify the need for a new sig:
    1.  Do nothing: the enclave is looking for the DB at the temporary location, and knows there is something to be done when it sees the file (instead of e.g. a 404).
    2.  Write something to a given specific file: the file could contain a 0 when there is no new DB to sign, and an 1 else or even a checksum of the actual DB file to avoid corruption issues during the transfer.
4.  If you did the second case above, just retrieve the DB using the same kind of secured connection.
5.  Here there could be a lot to be thought about. Especially *secure* logging is hard. This will be expanded below.
6.  Lots of upload mechanisms possible here, see after.
7.  This requires the DB changing action to be watching for the signature to come back.

Specifics:

*   Regarding retrieving file(s) from the DB server on the enclave: the most secure I can come with is over a very hardened HTTPS connection. This means both server and client authentication with certs issued by a custom CA (that could resides on the enclave), only TLS 1.3, ECDHE with Ed448 and Poly1305-Chacha20 or AES-GCM. We would need to keep the connection open while watching the notification file in order to avoid re-etablishing new TLS session at the watching frequency.
*   Uploading the sig back: we can use HTTP(S) upload using the same setup as above, but not sure if that is very important (unless we signed a bad file, the signature is to be a public file anyway so…). Some careful thinking about attack scenarios is required here.
*   For both above points, we can enforce used IP address on both sides for more security. The actual entry point on the repos server could also be a TOR hidden service, but not sure we want that (I guess there might be downsides).
*   Now, let’s dig in logging and threats models. This is likely the hard part.

1.  If we don’t consider that the enclave can be compromised, then we just need the signing script to also log the signature to a remote upload point and a local file (in case of network failure for instance).
2.  If we consider the enclave can be compromised but without root rights, we can have the key only accessible by root or be in a HSM, but have the (only root-writable) signing+logging script be usable by a normal user. That way an attacker would not be able to sign a file without it being logged.
3.  If we consider the enclave to be root compromised, having an HSM is the only thing that would protect us a bit from total failure (it would requires the attacker to maintain their presence on the enclave, which would protects against long term attack), but this is still basically game over.

Note that most of those specifics also apply for solution 1.

Benefits vs solution 1:

*   At least one less port opened on the enclave (“submission” one), which means it can goes to zero if we only allow physical access to that machine and not SSH (we can also hide SSH inside TOR).
*   Depending on the implementation details, the protection against arbitrary file signing could be more robust.

Inconvenients vs solution 1:

*   Needs watchers on both side (waiting for a file to sig, waiting for the sig to be uploaded) vs practically none (well you still need to wait for the sig to be returned, but that’s part of your “handshake”).
*   More complexity for not a lot more security (well, after some point gaining a bit in security requires a lot of efforts).

[https://www.mail-archive.com/arch-dev-public@archlinux.org/msg25637.html](https://www.mail-archive.com/arch-dev-public@archlinux.org/msg25637.html)

### Comparison benefits/pitfalls

*   One issue with both solutions is that there is a time that the repository db is not signed. A solution would be a temporary db and then moving that db

### Solutions in other distro's

#### Debian

#### OpenSuSe build service

OBS (OpenSuSe Build Service) has a signing deamon which accepts data and returns a signature.

[code](https://github.com/openSUSE/obs-sign/blob/master/signd) [wiki](https://en.opensuse.org/openSUSE:Build_Service_Signer)

#### Fedora

### Open issues

*   Which key should sign the repository db?
*   [repo signing with remote signing via SSH?](https://wiki.archlinux.org/index.php/DeveloperWiki:TheBigIdeaPage#Signing_database_files)
*   Distribution the pubkey. In the keyring?
*   Use a hardware token?