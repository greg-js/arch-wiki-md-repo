# Duply

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

From [duply.net](http://www.duply.net/):

_Duply is a frontend for the mighty duplicity magic. [Duplicity](/index.php/Duplicity "Duplicity") is a python based shell application that makes encrypted incremental backups to remote storages._

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Configuration](#Configuration)
    *   [3.1 No GPG Passphrase](#No_GPG_Passphrase)
*   [4 Backup configuration](#Backup_configuration)

## Installation

Duply is available in the [duply](https://aur.archlinux.org/packages/duply/)<sup><small>AUR</small></sup> package.

## Usage

For an overview on how to use Duply run `duply usage`.

The first thing to do is create a profile. Run `duply my_profile create` to create a profile named _my_profile_. Then configure the profile using the file _~/.duply/my_profile/conf_.

Use `duply my_profile backup` to make backups and `duply my_profile restore restore_directory` to restore after configuration is complete.

## Configuration

Set _GPG_KEY_ to encrypt and sign the backup with a GPG key. Set the _GPG_PW_ with the GPG passphrase. See [#No GPG Passphrase](#No_GPG_Passphrase) for details on Duply prompting for the GPG passphrase. Set _TARGET_ for the destination of the backup. Set _SOURCE_ for the base location to backup. See the _conf_ file for information on other Duply backup settings.

Example:

 `~/.duply/my_profile/conf` 

```
GPG_KEY='72AD0468'
GPG_PW='password'
TARGET='file://my_profile_backup'
SOURCE='/tmp/important_files'
```

Now run `duply my_profile backup` to backup everything in _/tmp/important_files_. The first time `duply my_profile backup` the user will be prompted for the GPG passphrase so that the key can be exported for safe keeping. Afterwords, Duply should run without prompting for a passphrase.

To exclude files backed up, see the _~/.duply/my_profile/exclude_ file.

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

Because of [a bug](https://sourceforge.net/p/ftplicity/bugs/83/) in the Duply, duplicity will prompt for a GPG passphrase even though it is available from the gpg-agent. Simply pressing return during the prompt will work as the passphrase is not needed to use the key (if the key is cached), or the `DUPL_PARAMS="$DUPL_PARAMS --use-agent"` line can be added to the _conf_.

 `~/.duply/my_profile/conf` 

```
# Turn on --use-agent option no matter what
DUPL_PARAMS="$DUPL_PARAMS --use-agent"
```

## Backup configuration

It is important to backup the configuration for your profile so that the backup can be recovered. One way to do this automatically is to add a _post_ script which tars the profile after a _backup_. For example:

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

Copy the _*.tar.gz_ file to a secure storage location such as LastPass, KeePass, Peerio or an offline USB harddrive. The configuration file should accessable even if access is lost to the computer being backed up because the whole point of the backup is that it can be recovered even if the computer is lost or destroyed.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Duply&oldid=401447](https://wiki.archlinux.org/index.php?title=Duply&oldid=401447)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Data compression and archiving](/index.php/Category:Data_compression_and_archiving "Category:Data compression and archiving")
*   [System recovery](/index.php/Category:System_recovery "Category:System recovery")