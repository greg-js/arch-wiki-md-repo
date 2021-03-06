From [duply.net](http://www.duply.net/):

	Duply is a frontend for the mighty duplicity magic. [Duplicity](/index.php/Duplicity "Duplicity") is a python based shell application that makes encrypted incremental backups to remote storages.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Configuration](#Configuration)
    *   [3.1 No GPG Passphrase](#No_GPG_Passphrase)
    *   [3.2 Signing fails using GPG version 2.1.0 or later](#Signing_fails_using_GPG_version_2.1.0_or_later)
*   [4 Backup configuration](#Backup_configuration)

## Installation

Duply is available in the [duply](https://aur.archlinux.org/packages/duply/) package.

## Usage

For an overview on how to use Duply run `duply usage`.

The first thing to do is create a profile. Run `duply my_profile create` to create a profile named *my_profile*. Then configure the profile using the file *~/.duply/my_profile/conf*.

Use `duply my_profile backup` to make backups and `duply my_profile restore restore_directory` to restore after configuration is complete.

## Configuration

Set *GPG_KEY* to encrypt and sign the backup with a GPG key. Set the *GPG_PW* with the GPG passphrase. See [#No GPG Passphrase](#No_GPG_Passphrase) for details on Duply prompting for the GPG passphrase. Set *TARGET* for the destination of the backup. Set *SOURCE* for the base location to backup. See the *conf* file for information on other Duply backup settings.

Example:

 `~/.duply/my_profile/conf` 
```
GPG_KEY='72AD0468'
GPG_PW='password'
TARGET='file://my_profile_backup'
SOURCE='/tmp/important_files'
```

Now run `duply my_profile backup` to backup everything in */tmp/important_files*. The first time `duply my_profile backup` the user will be prompted for the GPG passphrase so that the key can be exported for safe keeping. Afterwords, Duply should run without prompting for a passphrase.

To exclude files backed up, see the *~/.duply/my_profile/exclude* file.

 `~/.duply/my_profile/exclude` 
```
# Backup everything except this directory
- **/less_important_files

```

OR

 `~/.duply/my_profile/exclude` 
```
# Individual files
+ /tmp/important_files/file1
+ /tmp/important_files/file2

# Exclude cache inside directory
- /tmp/important_files/directory/cache
+ /tmp/important_files/directory

# Exclude everything else
- **

```

Dupicity exclude requires `**` as to match the base directory.

### No GPG Passphrase

Because of [a bug](https://sourceforge.net/p/ftplicity/bugs/83/) in the Duply, duplicity will prompt for a GPG passphrase even though it is available from the gpg-agent. Simply pressing return during the prompt will work as the passphrase is not needed to use the key (if the key is cached), or the `DUPL_PARAMS="$DUPL_PARAMS --use-agent"` line can be added to the *conf*.

 `~/.duply/my_profile/conf` 
```
# Turn on --use-agent option no matter what
DUPL_PARAMS="$DUPL_PARAMS --use-agent"
```

### Signing fails using GPG version 2.1.0 or later

Due to changes in recent versions of GPG, this message may occur during backup process:

```
duply gpg: signing failed: Inappropriate ioctl for device

```

This can be fixed by uncommenting *GPG_OPTS* section of Duply's *conf* file and adding *--pinentry-mode loopback* argument into it:

 `~/.duply/my_profile/conf OR /etc/duply/my_profile/conf (if running as root)`  `GPG_OPTS='--pinentry-mode loopback'` 

## Backup configuration

It is important to backup the configuration for your profile so that the backup can be recovered. One way to do this automatically is to add a *post* script which tars the profile after a *backup*. For example:

 `~/.duply/my_profile/post` 
```
#!/bin/bash

profile_name=$(basename $CONFDIR)

time=$(date +%s)
backup_file="$HOME/.duply/duply-$profile_name-"$time".tar.gz"

# Archive the profile in the ~/.duply directory.
tar -zcvf $backup_file -C $HOME/.duply $profile_name
chmod 600 $backup_file
```

Copy the **.tar.gz* file to a secure storage location such as LastPass, KeePass, Bitwarden or an offline USB harddrive. Another option is to archive the profile on a piece of paper as QR code ([duply_qr-git](https://aur.archlinux.org/packages/duply_qr-git/)). The configuration file should accessible even if access is lost to the computer being backed up because the whole point of the backup is that it can be recovered even if the computer is lost or destroyed.