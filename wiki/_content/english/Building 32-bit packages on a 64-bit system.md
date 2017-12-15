**Note:** [devtools](https://www.archlinux.org/packages/?name=devtools) is needed. Because of circular dependencies, you may need to install [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts) at the same time.

This example uses mkarchroot to create the chroot environment. First, create /opt/arch32 or another directory of your choice. The next steps is to copy your existing pacman.conf and makepkg.conf file to /opt/arch32 or your chosen directory. In the following tutorial, substitute /opt/arch32 with your chosen directory if you decide to use a different directory.

**Note:** If you have customized either makepkg.conf or pacman.conf, then you will need to use the standard pacman.conf and makepkg.conf files. Also make sure your /etc/pacman.d/mirrorlist contains the $arch variable instead of x86_64 or i686

**Edit your /opt/arch32/pacman.conf**

Change `Architecture = auto` to `Architecture = i686`.

You will also need to comment out any multi-lib repos.

**Edit /opt/arch32/makepkg.conf**

```
Change CARCH="x86_64" **to** *CARCH="i686"*
CHOST="x86_64-unknown-linux-gnu" **to** CHOST="i686-unknown-linux-gnu".
CFLAGS="-march=x86-64 -mtune=generic -O2 -pipe" **to** CFLAGS="-march=i686 -mtune=generic -O2 -pipe" .
CXXFLAGS="-march=x86-64 -mtune=generic -O2 -pipe" **to** CXXFLAGS="-march=i686 -mtune=generic -O2 -pipe" .

```

After the changes have been made, you will need to create another directory, I created /aur as mine.

**Next run:**

```
sudo mkarchroot -C /opt/arch32/pacman.conf -M /opt/arch32/makepkg.conf <chrootdir>/root base base-devel 

```

If you create the /aur directory like mine you would run

```
*sudo mkarchroot -C /opt/arch32/pacman.conf -M /opt/arch32/makepkg.conf /aur/root base base-devel*

```

You will need to edit /aur/copy/etc/pacman.d/mirrorlist and select which mirrors to use.

Now you can use makechrootpkg to build i686 packages like this:

```
# makechrootpkg -r /aur/

```