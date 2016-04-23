*This page contains information related to a [third-party initiative](/index.php/Getting_involved#Community_projects "Getting involved"). You may instead want to read about [professional audio](/index.php/Professional_audio "Professional audio") tips.*

If you have come here from another page, or were referred, you are probably interested in the [ArchAudio](http://archaudio.org/) [repositories](http://archaudio.org/packages/).

Read on if you are looking to contribute to the project, or are just plain bored.

## Contents

*   [1 Repositories](#Repositories)
*   [2 Packaging](#Packaging)
    *   [2.1 Getting Started](#Getting_Started)
        *   [2.1.1 Password Hashing](#Password_Hashing)
        *   [2.1.2 Buildscript Contributor](#Buildscript_Contributor)
        *   [2.1.3 Binary Contributor](#Binary_Contributor)
            *   [2.1.3.1 Committing Packages](#Committing_Packages)
            *   [2.1.3.2 Building Packages](#Building_Packages)
    *   [2.2 Subversion Maintenance](#Subversion_Maintenance)
    *   [2.3 Guidelines](#Guidelines)

## Repositories

*   **production** - tried and tested packages promoted from *preview* by a developer

*   **preview** - contributed packages from trusted ArchAudio members; may also house testing updates for packages in *production*

*   **nightly** - nightly/daily builds of packages not necessarily tested but whose PKGBUILDs have been verified by a developer; promoted from *experimental*

*   **experimental** - nightly/daily builds of packages whose PKGBUILDs have been contributed by trusted ArchAudio members

## Packaging

Prerequisite(s):

*   [Creating packages](/index.php/Creating_packages "Creating packages")
*   [Arch packaging standards](/index.php/Arch_packaging_standards "Arch packaging standards")

### Getting Started

Take a look [here](http://archaudio.org/participate/).

Anyone and everyone keen on contributing to the buildscripts ([PKGBUILDs](/index.php/PKGBUILD "PKGBUILD") and related files) can start immediately. You only have to take the time to get in touch with either **schivmeister** or **jonkristian** with a *password hash*. The fastest way is to log on to IRC (#archaudio@Freenode) and look for them, but a more straightforward approach is to simply e-mail them directly:

```
printf 'schiv#%s.fun
' archaudio | sed -e 's/#/@/' -e 's/fun/org/'
printf 'jon$%s.fun
' archaudio | sed -e 's/\$/@/' -e 's/fun/org/'

```

#### Password Hashing

As we mentioned above, this is needed for anyone wanting to have write access to the Subversion repository:

```
[http://aspirine.org/htpasswd_en.html](http://aspirine.org/htpasswd_en.html)

```

Simply enter a username and password, select either SHA-1 or MD5 (up to you), then click on "encrypt password". The output is what we want.

Or if you prefer an offline method:

```
htpasswd -cs hashForArchAudio.txt $preferred_username # you need to install 'apache' for this tool

```

In this example, the file 'hashForArchAudio.txt' will be created with your new [password hash](http://phpsec.org/articles/2005/password-hashing.html). Either send the file itself or copy the hash (the whole line). Do not worry, you are only sharing the *cryptographic hash* of your password - and not the password itself - so that you can be authenticated.

#### Buildscript Contributor

Simply checkout the repository via HTTPS with your username:

```
svn co [https://svn.archaudio.org/trunk](https://svn.archaudio.org/trunk) archaudio --username $your_username

```

You will only have write-access to the **preview** and **experimental** repositories, as far as PKGBUILDs and packages are concerned, as well as **devel** and **projects** for other things. If you are only concerned about editing PKGBUILDs and nothing else, then you may want to just checkout those specific directories:

```
svn co [https://svn.archaudio.org/trunk/buildscripts](https://svn.archaudio.org/trunk/buildscripts) archaudio --depth empty --username $your_username
cd archaudio
svn up preview experimental

```

Or if you want to be even more specific and work with one repository only:

```
svn co [https://svn.archaudio.org/trunk/buildscripts/$repo_name](https://svn.archaudio.org/trunk/buildscripts/$repo_name) archaudio --username $your_username

```

You can also checkout a package directly:

```
svn co [https://svn.archaudio.org/trunk/buildscripts/$repo_name/$pkg_dir](https://svn.archaudio.org/trunk/buildscripts/$repo_name/$pkg_dir) --username $your_username

```

We hope to incorporate these (commands) into a helper script soon.

#### Binary Contributor

*It is mandatory that you be well-acquainted with Arch Linux packaging before applying to become a (binary) packager. If you maintain packages in [AUR](/index.php/AUR "AUR") you are on the right path.*

The only difference here is that you have to do a second, *non-recursive* checkout for the private **packages** area, where the binaries are contained and pushed. Although Subversion will not track this directory, we are going to keep it under the main checkout for the sake of consistency. We have already made the necessary amendments so that SVN does not display the '?' symbol as the directory's status.

##### Committing Packages

If you are a 'developer', you have write access to almost everything:

```
(
echo -n 'Username: '
read your_username
svn co [https://svn.archaudio.org/trunk](https://svn.archaudio.org/trunk) archaudio --username $your_username
cd archaudio
svn co [https://svn.archaudio.org/trunk/packages](https://svn.archaudio.org/trunk/packages) --depth empty --username $your_username
cd packages
svn up production preview --set-depth immediates # nightly/experimental will contain only automated builds
) # if you copy-pasted you have to press ENTER now

```

If you are a 'packager', your binary-write-access is limited to the **preview** repository. So, for example, if you are only concerned about editing PKGBUILDs and uploading packages for this repository and nothing else, then it may be less clutter to just do two separate checkouts:

```
svn co [https://svn.archaudio.org/trunk/buildscripts/preview](https://svn.archaudio.org/trunk/buildscripts/preview) archaudiosrc --username $your_username
svn co [https://svn.archaudio.org/trunk/packages/preview](https://svn.archaudio.org/trunk/packages/preview) archaudiobin --depth immediates --username $your_username

```

So, after having done all that, you would copy the (binary) package that you built to the proper architecture directory, add it to SVN, and finally commit the addition. Optionally, you may clear out the directory again to maintain the 'sparseness':

```
cp $somewhere/foo-1.1-1-i686.pkg.tar.xz $svn_dir/packages/preview/i686/
svn add $svn_dir/packages/preview/i686/foo-1.1-1-i686.pkg.tar.xz
svn ci $svn_dir/packages/preview/i686 -m "Added binary package $package"
svn up $vcscopy/packages/preview/i686 --set-depth empty

```

Old packages will be automatically deleted on the server, so you need not worry about removing them yourself. Be careful to add real binary packages and not symlinks or any other file that may deceive you.

##### Building Packages

It is recommended to [build packages in a chroot environment](/index.php/DeveloperWiki:Building_in_a_Clean_Chroot "DeveloperWiki:Building in a Clean Chroot"). To ease up the process you may use the tools like *extra-i686-build* from the **devtools** package in Arch Linux's **extra** repository.

It is best to edit the chroot's **pacman.conf** so that any ArchAudio-related dependencies can be pulled in. Just run the following anywhere *but* within a PKGBUILD directory:

```
extra-i686-build # or x86_64

```

It will go on to create the chroot, which will by default be located at **/var/tmp/archbuild**, and then fail upon not finding a PKGBUILD. You can now make your changes to the pristine copy of the chroot (the other copy will be named after your username and will be recreated upon every build from this pristine copy):

```
vi /var/tmp/archbuild/extra-i686/root/etc/pacman.conf

```

If you are on 64-bit, you can build for both architectures:

```
extra-x86_64-build && extra-i686-build

```

If you have a powerful machine (anything more than a dual-core), you may want to run each of those builds in two separate windows.

If needed, you may build against the **multilib** repository, i.e *multilib-build*.

Unless you know what you are doing, *never* build against Arch Linux's **testing** repository, i.e *testing-i686-build*.

There is a work-in-progress suite of helper scripts called **archaudio-devtools**, and it is hoped that it will automate most of the labour involved here in a future release.

### Subversion Maintenance

It is always a good idea to make the following sanity checks a routine:

```
svn stat

```

```
svn merge --dry-run -r BASE:HEAD . # basically a more intuitive **svn stat -u**

```

And if you really cannot find out how to use SVN (man, wiki, google):

```
svn add $somedir $somefile # to add (recursive)

```

```
svn del $somedir $somefile # to delete

```

*Warning: If you remove something without the **svn** command, Subversion will complain that it is missing since it is not aware of the removal.*

```
svn mv $oldname $newname # same warning applies; you **cannot forget** the **svn** before the *mv*!

```

```
svn revert $somedir $somefile # revert some changes (selective)

```

```
svn revert -R . # revert ALL changes (recursive)

```

```
svn ci -m "$yourmessage" # to finally commit all changes

```

### Guidelines

*   Use tools such as *namcap* and those from [pacman](https://www.archlinux.org/packages/?name=pacman) to help yourself
*   Always ensure a package installs and runs as expected before distributing your changes
*   Try to keep in touch with upstream developers of packages you regularly update
*   Always check the upstream changelog if an update does not go smoothly