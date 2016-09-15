**Unison** is a bidirectional file synchronization tool that runs on Unix-like operating systems (including Linux, macOS, and Solaris) and Windows. It allows two replicas of a collection of files and directories to be stored on different hosts (or different disks on the same host), modified separately, and then brought up to date by propagating the changes in each replica to the other. It also unrestricted in terms of which system can be the host.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 GUI](#GUI)
    *   [2.2 Manual](#Manual)
*   [3 Usage](#Usage)
*   [4 Version incompatibility](#Version_incompatibility)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Save human time and keystrokes](#Save_human_time_and_keystrokes)
    *   [5.2 More helpful diff output](#More_helpful_diff_output)
    *   [5.3 Merging in Emacs](#Merging_in_Emacs)
    *   [5.4 Common config sync](#Common_config_sync)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [unison](https://www.archlinux.org/packages/?name=unison) package, which provides CLI, GTK+ and GTK+ 2.0 interfaces.

## Configuration

In order to use Unison, you need to create a profile.

### GUI

To configure Unison with the GUI run:

```
$ unison-gtk2

```

### Manual

Alternatively, manually create a profile in `~/.unison` and add the following lines to the default configuration file, `~/.unison/*profilename*.prf`.

Define the root directory to be synchronized.

```
root=/home/user/

```

Define the remote directory where the files should be sychronized to.

```
root=[ssh://example.com//path/to/server/storags](ssh://example.com//path/to/server/storags)

```

Optionally, provide arguments to [SSH](/index.php/SSH "SSH").

```
sshargs=-p 4000

```

Define which directories and files should be synchronized:

```
# dirs
path=Documents
path=Photos
path=Study
# files
path=.bashrc
path=.vimrc

```

You can also define which files to ignore:

```
ignore=Name temp.*
ignore=Name .*~
ignore=Name *.tmp

```

**Note:** For more information see the [Sample profiles](http://www.cis.upenn.edu/~bcpierce/unison/download/releases/stable/unison-manual.html#profileegs) in the [User Manual and Reference Guide](http://www.cis.upenn.edu/~bcpierce/unison/download/releases/stable/unison-manual.html).

## Usage

Once your profile is set up, you can start syncing:

```
$ unison *profilename*

```

or using the GUI tool:

```
$ unison-gtk2

```

and select the profile. Unison has a nice interface where you can view the progress and changes.

## Version incompatibility

For Unison to function properly, the same version *must* be installed on all clients. If, for example, one computer has version 2.40 and the other has 2.32, they will not be able to sync with each other. This applies to *all* computers that share a directory to be synchronized across your machines.

The Unison binary/ies also *must* be compiled against the same version of OCaml, see [https://groups.yahoo.com/neo/groups/unison-users/conversations/topics/11439](https://groups.yahoo.com/neo/groups/unison-users/conversations/topics/11439) . This makes Unison virtualy unusable on heterogeneous networks.

Due to the staggered releases with varying Linux distros, you might be stuck with older versions of Unison, while Arch Linux has the latest upstream version in the Extra repository. There are unofficial [PKGBUILDs](/index.php/PKGBUILD "PKGBUILD") for versions 2.32 ([unison-232](https://aur.archlinux.org/packages/unison-232/)), 2.27 ([unison-227](https://aur.archlinux.org/packages/unison-227/)) and 2.40 ([unison-240-compat](https://aur.archlinux.org/packages/unison-240-compat/)) on the [AUR](/index.php/AUR "AUR") that allow users of multiple distros to continue using Unison with their existing systems.

## Tips and tricks

### Save human time and keystrokes

If one runs unison within a terminal emulator capable of maintaining a suitable scrollback buffer, there is no purpose in having to confirm every non-conflicting change; set the `auto` option to true to avoid these prompts.

### More helpful diff output

The unison default diff command is `diff -u CURRENT2 CURRENT1`. When looking at the output of this command, it can be difficult to remember which changes will be kept when propagating from left to right ('>'), versus right to left ('<'). The following configuration makes it easy to remember: '>' keeps lines which start with '>':

```
diff = diff -u CURRENT2 CURRENT1 | perl -pe 's/^\+/>/; s/^\-/</'

```

### Merging in Emacs

Unison has the capability to assist users in merging two conflicting files using an external merge program, but it does not configure such a program by default. The manual suggests

```
merge = Name *.txt -> emacs -q --eval '(ediff-merge-files-with-ancestor "CURRENT1" "CURRENT2" "CURRENTARCH" nil "NEW")'

```

This assumes that you are running Unison in X, because the merge command cannot be run in the terminal (Emacs: "standard input is not a tty"). Note also that Unison replaces the CURRENT1, etc., variables with single-quoted filenames. Thus, the above works, but using double quotes throughout, as in "(ediff-merge-files... \"CURRENT1\" ...)", would not work.

Using the variable CURRENTARCH tells Unison that you expect to do 3-way merges with a common ancestor, which is only possible if the "backupcurrent" preference has been set previously to the last sync. To perform an ordinary 2-way merge in a terminal, one could use the following configuration instead. This also uses emerge.el, which some find preferable to ediff.el:

```
merge = Name {*,.*} -> urxvt -e emacs -nw -q --eval '(emerge-files nil "CURRENT1" "CURRENT2" "NEW")'

```

If the variable CURRENTARCHOPT is used instead of CURRENTARCH, then Unison will provide a common ancestor when it is available, and otherwise fall back to requesting a 2-way merge (by setting the variable to the empty string). This can be detected in a shell script. For example:

```
merge = Name {*,.*} -> unison-merge-files CURRENT1 CURRENT2 NEW CURRENTARCHOPT

```

with `unison-merge-files` defined as follows:

```
#!/bin/sh
CURRENT1=$1
CURRENT2=$2
NEW=$3
CURRENTARCHOPT=$4
EMACS="urxvt -e emacs -nw"
if [ x$CURRENTARCHOPT = x ]; then
    $EMACS --eval "(emerge-files nil \"$CURRENT1\" \"$CURRENT2\" \"$NEW\")";
else
    $EMACS --eval "(emerge-files-with-ancestor nil \"$CURRENT1\" \"$CURRENT2\" \"$CURRENTARCHOPT\" \"$NEW\")";
fi

```

### Common config sync

When syncing configuration files which would vary (e.g., due to endemic applications, security-sensitive configuration) among systems (servers, workstations, laptops, smartphones, etc.) but nevertheless contain common constructs (e.g., key bindings, basic shell aliases), it would be apt to separate such content into separate config files (e.g., `.bashrc_common`), and sync only these.

**Warning:** Bidirectional syncing of config files can lend itself to become an avenue for an attack, by enabling the peer syncing system to receive malicious changes to config files (and perhaps even other peers the system syncs with). This is an attractive option for adversaries, especially when the conceptual security levels of the two systems differ (e.g., public shell server vs. personal workstation), since it would likely be simpler to compromise a system of lower security. Always use the `noupdate` option when bidirectional syncing between two particular systems is deemed unnecessary; when necessary, verify each change when syncing. Automatic bidirectional syncs should be done with extreme caution.

## See also

*   [Wikipedia:Unison (file synchronizer)](https://en.wikipedia.org/wiki/Unison_(file_synchronizer) "wikipedia:Unison (file synchronizer)")
*   [Official website](http://www.cis.upenn.edu/~bcpierce/unison/)
*   [Yahoo! user group](http://tech.groups.yahoo.com/group/unison-users)
*   *[Liberation through data replication](http://www.pgbovine.net/unison_guide.htm)* by Philip Guo
*   *[Setting up Unison for your mom](http://www.pgbovine.net/unison-for-your-mom.htm)* by Philip Guo
*   *[Replication using Unison](http://twiki.org/cgi-bin/view/Codev/ReplicationUsingUnison)* on TWiki