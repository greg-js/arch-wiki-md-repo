Related articles

*   [ABS](/index.php/ABS "ABS")

This article covers how to create and how to apply patches to packages in the [Arch Build System](/index.php/Arch_Build_System "Arch Build System") (ABS).

## Contents

*   [1 Creating patches](#Creating_patches)
*   [2 Applying patches](#Applying_patches)
*   [3 Using quilt](#Using_quilt)
*   [4 See also](#See_also)

## Creating patches

A patch describes a set of line changes for one or multiple files. Patches are typically used to automate the changing of source code.

**Note:** If you only need to change one or two lines, you might want to use `sed` instead.

The `diff` tool compares files line by line if you save its output you have got a patch, e.g. `diff -ura foo bar > patch`. If you pass directories `diff` will compare the files they contain.

1.  Delete the `src` directory if you have already built the package.
2.  Run `makepkg -o` which will download and extract the source files, specified in `PKGBUILD`, but not build them.
3.  Create two copies of the extracted directory in the `src` directory, one as a pristine copy and one for your altered version. We will call them `package.orig` and `package.new`.
4.  Make your changes in the `package.new` directory.
5.  Run `diff -ura package.orig package.new --color` and check if the patch looks good.
6.  Run `diff -ura package.orig package.new > package.patch` to create the patch.
7.  Change into the `package.orig` directory and apply the patch using `patch -p1 < ../package.patch`. Verify that the patch is working by building and installing the modified package with `makepkg -ei`.

**Note:** You can also create patches with [Git](/index.php/Git "Git") using `git diff` or `git format-patch` [[1]](https://stackoverflow.com/questions/6658313/generate-a-git-patch-for-a-specific-commit).

## Applying patches

This section outlines how to apply patches you created or downloaded from the Internet from within a `PKGBUILD`'s `prepare()` function. Follow these steps:

1.  Add an entry to the `source` array of the `PKGBUILD` for the patch file, separated from the original source url by a space. If the file is available online, you can provide the full URL and it will automatically be downloaded and placed in the `src` directory. If it is a patch you created yourself, or is otherwise not available, you should place the patch file in the same directory as the `PKGBUILD` file, and just add the name of the file to the source array so that it is copied into the `src` directory. If you redistribute the `PKGBUILD`, you should, of course, include the patch with the `PKGBUILD`.
2.  Then use `updpkgsums` to update the `md5sums` array. Or manually add an entry to the `md5sums` array; you can generate sum of your patch using `md5sum` tool.
3.  Create the `prepare()` function in the `PKGBUILD` if one is not already present.
4.  The first step is to change into the directory that needs to be patched (in the `prepare()` function, not on your terminal! You want to automate the process of applying the patch). You can do this with something like `cd $srcdir/$pkgname-$pkgver` or something similar. `$pkgname-$pkgver` is often the name of a directory created by untarring a downloaded source file, but not in all cases.
5.  Now you simply need to apply the patch from within this directory. This is very simply done by adding

```
patch -p1 -i *pkgname*.patch 

```

to your `prepare()` function, changing `*pkgname*.patch` to the name of the file containing the diff (the file that was automatically copied into your `src` directory because it was in the `source` array of the `PKGBUILD` file).

An example prepare-function:

```
prepare() {
 cd $pkgname-$pkgver
 patch -Np1 -i "${srcdir}/eject.patch"
}

```

Run `makepkg` (from the terminal now). If all goes well, the patch will be automatically applied, and your new package will contain whatever changes were included in the patch. If not, you may have to experiment with the `-p` option of patch. read [patch(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/patch.1) for more information. Basically it works as follows. If the diff file was created to apply patches to files in `myversion/`, the diff files will be applied to `myversion/file`. You are running it from within the `yourversion/` directory (because you cd would into that directory in the `PKGBUILD`), so when patch applies the file, you want it to apply it to the file `file`, taking off the `myversion/` part. `-p1` does this, by removing one directory from the path. However, if the developer patched in `myfiles/myversion`, you need to remove two directories, so you use `-p2`.

If you do not apply a -p option, it will take off all directory structure. This is ok if all the files are in the base directory, but if the patch was created on `myversion/` and one of the edited files was `myversion/src/file`, and you run the patch without a `-p` option from within `yourversion`, it will try to patch a file named `yourversion/file`.

Most developers create patches from the parent directory of the directory that is being patched, so `-p1` will usually be right.

## Using quilt

A simpler way to create patches is using [quilt](https://www.archlinux.org/packages/?name=quilt) which has better job to manage many patches, such as applying patches, refreshing patches, and reverting patched files to original state. [quilt](https://www.archlinux.org/packages/?name=quilt) is used on [Debian](https://wiki.debian.org/UsingQuilt "debian:UsingQuilt") to manage their patches. See [Using Quilt](http://www.shakthimaan.com/downloads/glv/quilt-tutorial/quilt-doc.pdf) for basic information about basic quilt usage to generate, apply patches, and reverting patched files.

## See also

*   [http://www.kegel.com/academy/opensource.html](http://www.kegel.com/academy/opensource.html) — Useful information on patching files