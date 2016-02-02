# Tomb

Related articles

*   [Disk encryption](/index.php/Disk_encryption "Disk encryption")
*   [dm-crypt](/index.php/Dm-crypt "Dm-crypt")
*   [TrueCrypt](/index.php/TrueCrypt "TrueCrypt")
*   [Tcplay](/index.php/Tcplay "Tcplay")

From [the official website](http://tomb.dyne.org/):

	Tomb is 100% free and open source software to make strong encryption easy to use.

	A tomb is like a locked folder that can be safely transported and hidden in a filesystem.

	Keys can be kept separate: for instance the tomb on your computer and the key on a USB stick.

Tomb aims to be a really simple to use software to manage "encrypted directories", called tombs. A tomb can only be opened if you both have a keyfile and you know the password. It also has advanced features, like steganography.

You can install [tomb](https://aur.archlinux.org/packages/tomb/)<sup><small>AUR</small></sup> from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository").

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 GUI Usage](#GUI_Usage)
*   [4 Advanced features](#Advanced_features)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") [tomb](https://aur.archlinux.org/packages/tomb/)<sup><small>AUR</small></sup> or [tomb-git](https://aur.archlinux.org/packages/tomb-git/)<sup><small>AUR</small></sup>.

## Usage

Tomb is meant to be used from the console as a single, non-interactive script. it also provides **tomb-open**, which is a simple interactive script to help you create a tomb, open it, retrieve keys from USB.

Tombs are operated from a terminal commandline and require root access to the machine (or just [sudo](/index.php/Sudo "Sudo") access to the script).

To create a 100MB tomb called "secret" do:

```
# tomb dig -s 100 secret.tomb
# tomb forge secret.tomb.key
# tomb lock secret.tomb -k secret.tomb.key

```

To open it, do:

```
# tomb open secret.tomb -k secret.tomb.key

```

And after you are done:

```
# tomb close

```

For more information see `tomb -h` and `man tomb`.

## GUI Usage

To make usage of tomb even easier, you can use a GUI wrapper called gtomb. Find it here: [gtomb-git](https://aur.archlinux.org/packages/gtomb-git/)<sup><small>AUR</small></sup>

It includes almost all features tomb offers, but is still in active development so use it with caution.

## Advanced features

*   steganography (to hide the key inside a jpeg/wav file)
*   bind hooks: can mount some of its subdirectories as "bind" to some other. Suppose, for example, you would like to encrypt your .Mail, .firefox and Documents directories. Then you can create a tomb which contains these subdirectories (and others too, if you want) and create a simple configuration file inside the tomb itself; when you run `tomb open` it will automatically bind that directories into the right places. This way you will easily get an encrypted firefox profile, or maildir.
*   post hooks: commands that are run when the tomb is open, or closed. You can imagine lot of things for this: open files inside the tomb, put your computer in a "paranoid" status (for example, disabling swap), whatever.

## See also

*   [manpage](http://tomb.dyne.org/manual.html)
*   [home page](http://tomb.dyne.org/)
*   [quickstart](https://github.com/dyne/Tomb/wiki/Quickstart)
*   [advanced features](https://github.com/dyne/Tomb/wiki/Advancedfeatures)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Tomb&oldid=414881](https://wiki.archlinux.org/index.php?title=Tomb&oldid=414881)"