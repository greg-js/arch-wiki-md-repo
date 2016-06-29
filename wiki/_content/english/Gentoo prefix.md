Gentoo Prefix is a way to use the gentoo packaging tools to manage software in your user space.

With the current toolchain (gcc 6) the prefix bootstrap does not work, but the [RAP variant](https://wiki.gentoo.org/wiki/Prefix/libc) of prefix does. Use that one.

At the time of this writing there was a mismatch between the prefix ebuild tree and the gentoo ebuild tree (which RAP uses). You will need to modify `${EPREFIX}/startprefix` .

Change the `RETAIN=` line to:

 `RETAIN="HOME=$HOME TERM=$TERM USER=$USER SHELL=$SHELL ENV=${EPREFIX}/etc/profile"` 

and the `env` line to:

 `env -i $RETAIN $SHELL --posix -l`