Related articles

*   [Disk encryption](/index.php/Disk_encryption "Disk encryption")
*   [Encfs](/index.php/Encfs "Encfs")

From [gocryptfs](https://nuetzlich.net/gocryptfs/):

	gocryptfs uses file-based encryption that is implemented as a mountable FUSE filesystem. Each file in gocryptfs is stored one corresponding encrypted file on the hard disk.

	The highlights are: Scrypt password hashing, GCM encryption for all file contents, EME wide-block encryption for file names with a per-directory IV.

See the [gocryptfs](https://nuetzlich.net/gocryptfs/) project home for further introduction of its features, benchmarks, etc. See [Disk encryption#Comparison table](/index.php/Disk_encryption#Comparison_table "Disk encryption") for an overview of alternative methods and [EncFS](/index.php/EncFS "EncFS") for the direct alternative.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Example using reverse mode](#Example_using_reverse_mode)
*   [3 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") [gocryptfs](https://aur.archlinux.org/packages/gocryptfs/) or [gocryptfs-git](https://aur.archlinux.org/packages/gocryptfs-git/).

As a FUSE filesystem, gocryptfs is fully configurable by the user and stores its configuration files in the user's directory paths.

## Usage

See [gocryptfs(1)](https://manned.org/gocryptfs.1) and its examples first.

**Warning:**

*   To achieve its design goal of [authenticated encryption](https://en.wikipedia.org/wiki/Authenticated_encryption "w:Authenticated encryption"), gocryptfs implements a AES-EME encryption mode (for filenames, not the content). While this mode is not widely used/audited yet, it offers integrity protection for the data, a feature not available for direct alternative encryption methods.
*   See the project's tracking [bug report](https://github.com/rfjakob/gocryptfs/issues/90) regarding findings of the first security audit for more information.

**Tip:** Execute `gocryptfs -speed` to test throughput for available encryption methods. Note the slowest `AES-SIV-512-Go` mode is required (and automatically selected) for reverse mode.

### Example using reverse mode

A major application for file-based encryption methods are encrypted backups. FUSE-based filesystems are flexible for this, since they allow a wide array of backup destinations using standard tools. For example, a gocryptfs-encrypted FUSE mount point can be easily created directly on a [Samba](/index.php/Samba "Samba")/[NFS](/index.php/NFS "NFS") share or [Dropbox](/index.php/Dropbox "Dropbox") location, synchronized to a remote host with [rsync](/index.php/Rsync "Rsync"), or just be manually copied to a remote backup storage.

The [reverse mode](https://nuetzlich.net/gocryptfs/reverse_mode/) of gocryptfs is particularly useful for creating encrypted backups, since it requires virtually no extra storage capacity on the machine to back up.

The following shows an example of user *archie* creating a backup of `/home/archie`:

First, *archie* creates an empty directory for the encrypted view:

```
$ mkdir /tmp/*crypt*

```

Second, user *archie* creates an encrypted view of the home directory:

 `/home/archie` 
```
$ gocryptfs -reverse /home/*archie* /tmp/*crypt*
Password:
Decrypting master key

Your master key is:
...
Filesystem mounted and ready.
$
```

Third, *archie* creates a backup of the encrypted directory, a simple local copy for this example:

```
$ cp -a /tmp/*crypt* /tmp/*backup*

```

and done.

The encrypted directory can stay mounted for the user session, or be unmounted manually:

```
$ fusermount -u /tmp/*crypt*
$ rmdir /tmp/*crypt*

```

To restore from the encrypted backup, a plain-text view is mounted using gocryptfs's normal mode:

```
$ mkdir /tmp/*restore*
$ gocryptfs /tmp/*backup*/ /tmp/*restore*
Password: 
Decrypting master key
...
Filesystem mounted and ready.
$
```

Now the required files can be restored.

## See also

*   [A first security audit](https://defuse.ca/audits/gocryptfs.htm) of gocryptfs
*   [RFC5297](https://tools.ietf.org/html/rfc5297) Synthetic Initialization Vector (SIV) Authenticated Encryption Using the Advanced Encryption Standard (AES)