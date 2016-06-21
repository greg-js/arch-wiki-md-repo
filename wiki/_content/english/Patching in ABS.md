This document covers the steps to creating and/or applying patches to packages when using [ABS](/index.php/ABS "ABS").

## Contents

*   [1 Creating patches](#Creating_patches)
*   [2 Applying patches](#Applying_patches)
*   [3 Using quilt](#Using_quilt)
    *   [3.1 Creating a new patch](#Creating_a_new_patch)
    *   [3.2 Applying and reverting patches](#Applying_and_reverting_patches)
    *   [3.3 Importing patches](#Importing_patches)
*   [4 See also](#See_also)

## Creating patches

If you are attempting to use a patch that you got from elsewhere (ie: you downloaded a patch to the Linux kernel), you can skip to the next section. However, if you need to edit source code, make files, configuration files, etc, you will need to be able to create a patch.

**Note:** If you need only to change one or two lines in a file (e.g. a Makefile), you may be better off investigating the properties of `sed` instead.

Creating a patch for a package involves creating two copies of the package, editing the new copy, and creating a unified diff between the two files. When creating an Arch Linux package, this can be done as follows:

1.  Add the download source of the file to the source array of the `PKGBUILD` you are creating. Of course, if you are altering an existing PKGBUILD, this step is taken care of.
2.  Create a dummy (empty, or containing a single `echo` command is good) build() function. If you are altering an existing `PKGBUILD`, you should comment out most of the lines of the build function, as you are likely going to be running `makepkg` several times, and you will not want to spend a lot of time waiting for a broken package to build.
3.  Run `makepkg -o` This will download the source files you need to edit into the `src` directory.
4.  Change to the `src` directory. In standard cases, there will be a directory containing a bunch of files that were unzipped or untarred from a downloaded archive there (Sometimes it's a single file, but diffs work on multiple files too!) You should make two copies of these directories. One is a pristine copy that makepkg will not be allowed to manipulate, and one will be the new copy that you will create a patch from. You can name the two copies `package.pristine` and `package.new` or something similar.
5.  Change into the `package.new` directory. Edit whichever files need to be edited. The changes needed depend on what the patch has to do; it might correct a Makefile paths, it may have to correct source errors (for example, to agree with `gcc 3.4`), and so on. You can also edit files in subfolders of the `package.new` directory, of course. **Do not** issue any commands that will inadvertently create a bunch of files in the `package.new` directory; ie: do not try to compile the program to make sure your changes work. The problem is that all the new files will show up in the patch, and you do not want that. Instead, apply the patch to another copy of the directory (**not** the pristine directory), either manually with the `patch` command, or in the `PKGBUILD` (described below) and test the changes from there.
6.  Change back to the `src` directory.
7.  Run `diff -aur package.pristine package.new` This will output all the changes you made in unified diff format. You can scan these to make sure the patch is good.
8.  Run `diff -aur package.pristine package.new > package.patch` to capture all the changes in a file named `package.patch`. This is the file that will be used by patch. You may now apply the changes to a copy of the original directory and make sure they are working properly. You should also check to ensure that the patch does not contain any extraneous details. For example, you do not want the patch to convert all tabs in the files you edited to spaces because your text editor did that behind your back. You can edit the patch either using a text editor, or to be safer (and not accidentally introduce errors into the diff file), edit the original files and create the patch afresh.

**Note:** A simpler way to create patches is using [quilt](https://www.archlinux.org/packages/?name=quilt) which has better job to manage many patches, such as applying patches, refreshing patches, and reverting patched files to original state. [quilt](https://www.archlinux.org/packages/?name=quilt) is used on [Debian](https://wiki.debian.org/UsingQuilt) to manage their patches. [#Using quilt](#Using_quilt) section of this wiki has basic information about basic quilt usage to generate, apply patches, and reverting patched files. [git](/index.php/Git "Git") is also capable to generate patch via `git diff -p -u commit_hash > patchfile.diff` inside a working tree.

## Applying patches

This section outlines how to apply patches you created or downloaded from the Internet from within a `PKGBUILD`'s `prepare()` function. Follow these steps:

1.  Add an entry to the `source` array of the `PKGBUILD` for the patch file, separated from the original source url by a space. If the file is available online, you can provide the full URL and it will automatically be downloaded and placed in the `src` directory. If it is a patch you created yourself, or is otherwise not available, you should place the patch file in the same directory as the `PKGBUILD` file, and just add the name of the file to the source array so that it is copied into the `src` directory. If you redistribute the `PKGBUILD`, you should, of course, include the patch with the `PKGBUILD`.
2.  Then use `updpkgsums` to update the `md5sums` array. Or manually add an entry to the `md5sums` array; you can generate sum of your patch using `md5sum` tool.
3.  Create the `prepare()` function in the `PKGBUILD` if one is not already present.
4.  The first step is to change into the directory that needs to be patched (in the `prepare()` function, not on your terminal! You want to automate the process of applying the patch). You can do this with something like `cd $srcdir/$pkgname-$pkgver` or something similar. `$pkgname-$pkgver` is often the name of a directory created by untarring a downloaded source file, but not in all cases.
5.  Now you simply need to apply the patch from within this directory. This is very simply done by adding

```
patch -p1 <pkgname.patch 

```

to your `prepare()` function, changing `pkgname.patch` to the name of the file containing the diff (the file that was automatically copied into your `src` directory because it was in the `source` array of the `PKGBUILD` file).

An example prepare-function:

```
prepare() {
 cd $pkgname-$pkgver
 patch -Np1 <../eject.patch
}

```

Run `makepkg` (from the terminal now). If all goes well, the patch will be automatically applied, and your new package will contain whatever changes were included in the patch. If not, you may have to experiment with the `-p` option of patch. read `man patch` for more information. Basically it works as follows. If the diff file was created to apply patches to files in `myversion/`, the diff files will be applied to `myversion/file`. You are running it from within the `yourversion/` directory (because you cd would into that directory in the `PKGBUILD`), so when patch applies the file, you want it to apply it to the file `file`, taking off the `myversion/` part. `-p1` does this, by removing one directory from the path. However, if the developer patched in `myfiles/myversion`, you need to remove two directories, so you use `-p2`.

If you do not apply a -p option, it will take off all directory structure. This is ok if all the files are in the base directory, but if the patch was created on `myversion/` and one of the edited files was `myversion/src/file`, and you run the patch without a `-p` option from within `yourversion`, it will try to patch a file named `yourversion/file`.

Most developers create patches from the parent directory of the directory that is being patched, so `-p1` will usually be right.

## Using quilt

Here, I'll explain basic `quilt` usage. For more detailed information about `quilt`, read the quilt manual page.

### Creating a new patch

1.  Navigate to source directory.
2.  Set environment variable `QUILT_PATCHES='.'` and `QUILT_REFRESH_ARGS='-p ab'`. #*This can be done automatically by setting a `~/.quiltrc` file as below.

    	`QUILT_PATCHES='.'`

    	`QUILT_REFRESH_ARGS='-p ab'`

3.  Create a new patch file via quilt. `$ quilt new 001-fix.diff`
4.  Add a file to be included in the patch. `$ quilt add Makefile`
5.  Edit the desired file. `$ nano Makefile`.
6.  After saving the file, review the patch that will be generated. `$ quilt diff -p ab`.
7.  If the generated patch is ok, refresh the patch file. `$ quilt refresh`.
8.  Optionally, add a header to describe what the patch is doing. `$ EDITOR=nano quilt header -e`
9.  The patch `001-fix.diff` is ready and can be attached to bug tracking system or emailed as text to development mailing list.

### Applying and reverting patches

1.  Set `QUILT_PATCHES` environment variable. In this case, `QUILT_PATCHES='.'` (the current working directory). This step can be skipped if you have a `~/.quiltrc` file containing `QUILT_PATCHES='.'` line.
2.  In the current working directory, create a `series` file containing patch filenames. The patches will be applied according to their order in the `series` file. For example, I have three patch files: `001-fix.diff`, `002-hello.diff`, and `003-Makefile.diff`. The content of `series` file will be as follow.

    	`001-fix.diff`

    	`002-hello.diff`

    	`003-Makefile.diff`

    *   The `series` file can be generated simply using this command.

    	`$ ls *.diff | tee ./series`

    	You may need to sort the `series` file for correct patching order.

3.  To apply the patches, simply use this command.

    	`$ quilt push -a`

4.  If you want to revert patched files to the original state (reverse patching), simply issue this command.

    	`$ quilt pop -a`

### Importing patches

Instead of manually creating `series` file, patches can be imported and quilt will automatically generate series file. Just issue these command (according to my example before).

```
$ quilt import 001-fix.diff
$ quilt import 002-hello.diff
$ quilt import 003-Makefile.diff

```

Or to simplify, just issue this one line command. `$ quilt import *.diff`

## See also

*   [http://www.kegel.com/academy/opensource.html](http://www.kegel.com/academy/opensource.html) — Useful information on patching files
*   [https://packages.gentoo.org/](https://packages.gentoo.org/)
*   [http://pkgs.fedoraproject.org/cgit/](http://pkgs.fedoraproject.org/cgit/)
*   [https://wiki.debian.org/UsingQuilt](https://wiki.debian.org/UsingQuilt)