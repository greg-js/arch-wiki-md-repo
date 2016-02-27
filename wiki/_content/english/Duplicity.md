Duplicity is a network backup program.

It can save snapshots of directories and files to a remote GnuPG encrypted tar file, which acts as a backup repository. Connecting with the remote backup repository can take place through any of the following protocols: rsync, ftp, HSI, WebDAV, Tahoe-LAFS, or Amazon S3.

Backups are granularly incremental, meaning that only changes in files (since the last snapshot) are stored.

## Contents

*   [1 Installation](#Installation)
*   [2 Basic Usage](#Basic_Usage)
    *   [2.1 Doing backups](#Doing_backups)
    *   [2.2 Restoring files from backup](#Restoring_files_from_backup)
    *   [2.3 Repository inspection and house-keeping](#Repository_inspection_and_house-keeping)
    *   [2.4 Example backup script](#Example_backup_script)
*   [3 Troubleshooting](#Troubleshooting)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") [duplicity](https://www.archlinux.org/packages/?name=duplicity) from the [Official repositories](/index.php/Official_repositories "Official repositories").

*   [duply](/index.php/Duply "Duply"), a shell front-end, is available in [AUR](/index.php/AUR "AUR").
*   [deja-dup](https://www.archlinux.org/packages/?name=deja-dup), an easy-to-use front-end, is available in the [Official repositories](/index.php/Official_repositories "Official repositories"). It provides the command-line tool `deja-dup` and the GTK frontend `deja-dup-preferences`.

## Basic Usage

### Doing backups

To backup the local folder */home/me* to the remote location */usr/backup* on host *other.host* through the *scp/ssh* protocol, use:

```
duplicity /home/me scp://uid@other.host//usr/backup

```

The first time this command is run, it will create a full backup. Running the exact same command again causes an incremental backup to the existing backup repository.

Additional command-line options options allow to:

*   include or exclude specific files and directories from the backup (using shell patterns or regular expressions)
*   fine-tune encryption and signing of the backups

### Restoring files from backup

To restore the local folder */home/me* to the state of the last snapshot saved in the remote repository */usr/backup* on host *other.host*, do:

```
duplicity scp://uid@other.host//usr/backup /home/me 

```

Note the reversed ordering of the arguments compared to the backup command above. The URL argument is always treated as the backup repository, and the local path argument as the directory to sync with the backup. (A local backup repository would need to be explicitly specified using the file:// protocol prefix!)

Additional command-line option exist to allow:

*   restore a specific file instead of the whole repository
*   restore file(s) to the state they had on a specific date, rather than to the most recent available snapshot

### Repository inspection and house-keeping

Some additional command-line options exist for comparing the repository state to the state of the local files, and to delete old snapshots so as to only keep a fixed amount of snapshots or only ones that are newer than a given date.

See the man page for details.

### Example backup script

```
#!/bin/sh
## Remote backup script. Requires duplicity and gpg-agent with the keys and passphrases loaded as root.
## Uses separate encryption and signing keys
## Usage:  'backup_remote.sh'

enc_key=44D79E41
sign_key=F5C978E3
src="/mnt/backup/"
dest="scp://destination.com//backups/homeserver"

# Keychain is used to source the ssh-agent keys when running from a cron job
type -P keychain &>/dev/null || { echo "I require keychain but it's not installed.  Aborting." >&2; exit 1; }
eval `keychain --eval web_rsa` || exit 1
## Note: can't use keychain for gpg-agent because it doesn't currently (2.7.1) read in all the keys correctly. 
## Gpg will ask for a passphrase twice for each key...once for encryption/decryption and once for signing. 
## This makes unattended backups impossible, especially when trying to resume an interrupted backup.
if [ -f "${HOME}/.gnupg/gpg-agent-info" ]; then
      . "${HOME}/.gnupg/gpg-agent-info"
      export GPG_AGENT_INFO
fi

duplicity --use-agent \
         --verbosity notice \
         --encrypt-key "$enc_key" \
         --sign-key "$sign_key" \
         --full-if-older-than 60D \
         --num-retries 3 \
         --asynchronous-upload \
         --volsize 100 \
         --archive-dir /root/.cache/duplicity \
         --log-file /var/log/duplicity.log \
         --exclude /mnt/backup/fsarchiver \
         --exclude '**rdiff-backup-data' \
         "$src" "$dest"

```

**Note:** There is an issue with the current version of pinentry (0.8.1-3) that will not allow passphrase entry for a root gpg-agent when logged in as root using su - or sudo. If you are accessing a remote server where direct root ssh login is not allowed (or desired!), then you have to either [patch pinentry](https://bugzilla.redhat.com/show_bug.cgi?id=677665) or `chown root `tty`` before running pinentry. This is not an issue when running gpg-agent as a non-root user.

**Note:** If you want to start gpg-agent on root login and then cache the passphrases for gpg-agent at your convenience, you can add these functions to your /root/.bashrc:

```
function gpg_start {
       gnupginf="${HOME}/.gnupg/gpg-agent-info"
       if pgrep -u "${USER}" gpg-agent >/dev/null 2>&1; then
           eval "$(cat $gnupginf)"
           eval "$(cut -d= -f1 < $gnupginf | xargs echo export)"
       else
           eval "$(gpg-agent -s --daemon --write-env-file $gnupginf)"
       fi
}
function keys {
       touch test-gpg.txt
       touch test-gpg.txt1
       gpg -r 'Duplicity Encryption Key' -e test-gpg.txt
       gpg -r 'Duplicity Signature Key' -e test-gpg.txt1
       gpg -u <signing key> --detach-sign test-gpg.txt
       gpg -u <encryption key> --detach-sign test-gpg.txt1
       gpg -d test-gpg.txt.gpg
       gpg -d test-gpg.txt1.gpg
       rm test-gpg.txt*
}
gpg_start

```

## Troubleshooting

If you get gpg errors revolving around “inappropriate ioctl for device” it most likely has to do with changes to the gpg agent behavior from gpg version 2.1 up. See [this thread](https://bbs.archlinux.org/viewtopic.php?id=190301) for more information. Generally speaking one needs to explicitly allow programs to provide the passphrase to gpg agent instead of prompting the user.

The steps to remediate this issue are outlined in [GnuPG#Unattended passphrase](/index.php/GnuPG#Unattended_passphrase "GnuPG").

## See also

*   [Synchronization and backup programs](/index.php/Synchronization_and_backup_programs "Synchronization and backup programs")
*   [Duplicity home page](http://duplicity.nongnu.org/)
*   [Wikipedia:Duplicity (software)](https://en.wikipedia.org/wiki/Duplicity_(software) "wikipedia:Duplicity (software)")
*   [Déjà Dup home page](https://launchpad.net/deja-dup)