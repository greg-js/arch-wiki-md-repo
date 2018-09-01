Related articles

*   [find](/index.php/Find "Find")
*   [Core utilities](/index.php/Core_utilities "Core utilities")
*   [List of applications/Utilities#File searching](/index.php/List_of_applications/Utilities#File_searching "List of applications/Utilities")

[mlocate](https://pagure.io/mlocate) (Merging Locate) is a more secure version of the [locate](https://en.wikipedia.org/wiki/locate_(Unix) utility, that only shows files accessible to the user.

`locate` is a common Unix tool for quickly finding files by name. It offers speed improvements over the [find](/index.php/Find "Find") tool by searching a pre-constructed database file, rather than the [filesystem](/index.php/Filesystem "Filesystem") directly. The downside of this approach is that changes made since the construction of the database file cannot be detected by `locate`. This problem can be minimised by scheduled database updates.

## Installation

[Install](/index.php/Install "Install") the [mlocate](https://www.archlinux.org/packages/?name=mlocate) package.

While the [GNU findutils](https://www.gnu.org/software/findutils/) also include a *locate* implementation, Arch's [findutils](https://www.archlinux.org/packages/?name=findutils) package does not.

## Usage

Before [locate(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/locate.1) can be used, the database will need to be created, this is done with the [updatedb(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/updatedb.1) command, which (as the name suggests) updates the database.

The package contains an `updatedb.timer` unit, which invokes a database update each day. The timer is enabled right after installation, [start](/index.php/Start "Start") it manually if you want to use it before reboot. You can also manually run *updatedb* as root at any time.

To save time, *updatedb* can be (and by default is) configured to ignore certain filesystems and paths by editing `/etc/updatedb.conf`. [updatedb.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/updatedb.conf.5) describes the semantics of this file. It is worth noting that among the paths ignored in the default configuration (`PRUNEPATHS`) are `/media` and `/mnt`, so *locate* may not discover files on external devices.

## See also

*   [How locate works and rewrite it in one minute](http://jvns.ca/blog/2015/03/05/how-the-locate-command-works-and-lets-rewrite-it-in-one-minute/)