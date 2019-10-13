See [Kernels](/index.php/Kernels "Kernels") for the main article.

The [Arch Build System](/index.php/Arch_Build_System "Arch Build System") can be used to build a custom kernel based on the official [linux](https://www.archlinux.org/packages/?name=linux) package. This compilation method can automate the entire process, and is based on a very well tested package. You can edit the PKGBUILD to use a custom kernel configuration or add additional patches.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Getting the Ingredients](#Getting_the_Ingredients)
*   [2 Modifying the PKGBUILD](#Modifying_the_PKGBUILD)
    *   [2.1 Changing prepare()](#Changing_prepare())
    *   [2.2 Generate new checksums](#Generate_new_checksums)
*   [3 Compiling](#Compiling)
*   [4 Installing](#Installing)
*   [5 Boot Loader](#Boot_Loader)
*   [6 Updating](#Updating)
*   [7 See Also](#See_Also)

## Getting the Ingredients

Since you'll be using [makepkg](/index.php/Makepkg "Makepkg"), follow the best practices outlined there first. For example, you cannot run makepkg as root/sudo. Therefore, create a `build` directory in your user home first.

```
 $ cd ~/
 $ mkdir build
 $ cd build/

```

[Install](/index.php/Install "Install") the [asp](https://www.archlinux.org/packages/?name=asp) package and the [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) package group.

You need a clean kernel to start your customization from. Fetch the latest kernel package files from ABS into your build directory by running:

```
$ asp update linux
$ asp checkout linux

```

At this point, the directory tree looks like:

```
~/build/linux/-+
               +--60-linux.hook
               +--90-linux.hook
               +--config
               +--linux.install
               +--linux.preset
               \__PKGBUILD
```

Then, get any other file you need (e.g. custom configuration files, patches, etc.) from the respective sources.

## Modifying the PKGBUILD

Edit `PKGBUILD` and look for the `pkgbase` parameter. Change this to your custom package name, e.g.:

```
 pkgbase=linux-custom

```

Depending on the PKGBUILD you may have to also rename `linux.install` to match the modified `pkgbase`.

### Changing prepare()

In `prepare()` function, you can [apply needed kernel patches](/index.php/Patching_packages#Applying_patches "Patching packages") or change kernel build configuration.

If you need to change a few config options you can edit config file in the source.

Or you can use GUI tool to tweak the options. Comment `make olddefconfig` in the prepare() function of the PKGBUILD, and add your favorite tool:

 `PKGBUILD` 
```
...
  msg2 "Setting config..."
  cp ../config .config
  #make olddefconfig

  make nconfig # new CLI menu for configuration
  #make menuconfig # CLI menu for configuration
  #make xconfig # X-based configuration
  #make oldconfig # using old config from previous kernel version
  # ... or manually edit .config
...

```

**Warning:** systemd has a number of kernel configuration requirements for general use, for specific usecases (e.g., UEFI) and for specific systemd functionality (e.g., bootchart). Failure to meet these requirements can result in your system being degraded or unusable. The list of required and recommended kernel CONFIGs can be found in `/usr/share/doc/systemd/README`. Check them before you compile.These requirements also change over time. Because Arch assumes you are using the official kernel, there will be no announcement of these changes. Before you install a new version of systemd, check the version release notes to make sure your current custom kernel meets any new systemd requirements.

### Generate new checksums

[#Changing prepare()](#Changing_prepare()) suggests a possible modification to `$_srcname/.config`. Since this path is not where downloading the package files ended, its checksum was not checked by makepkg (which actually checked `$_srcname/../../config`).

If you replaced the downloaded `config` with another config file before running makepkg, [Install](/index.php/Install "Install") the [pacman-contrib](https://www.archlinux.org/packages/?name=pacman-contrib) package. Which will generate new checksums by running:

```
$ updpkgsums

```

## Compiling

You can now proceed to compile your kernel by the usual command `makepkg`

If you have chosen an interactive program for configuring the kernel parameters (like menuconfig), you need to be there during the compilation.

```
 $ makepkg -s

```

The `-s` parameter will download any additional dependencies used by recent kernels such as xml and docs.

**Note:**

*   Kernel sources are [PGP signed](https://www.kernel.org/signature.html#kernel-org-web-of-trust), and makepkg will attempt to verify them. See [Makepkg#Signature checking](/index.php/Makepkg#Signature_checking "Makepkg") for details.
*   [Running compilation jobs simultaneously](/index.php/Makepkg#Parallel_compilation "Makepkg") can reduce compilation time significantly on multi-core systems.

## Installing

After running *makepkg*, you can have a look at the `linux.install` file. You will see that some variables have changed.

Now, you only have to install the packages as usual. Best practice is to install both packages together as they might be both needed (e.g. DKMS.)

```
# pacman -U *kernel-headers_package* *kernel_package*

```

## Boot Loader

Now, the folders and files for your custom kernel have been created, e.g. `/boot/vmlinuz-linux-test`. To test your kernel, update your [bootloader](/index.php/Bootloader "Bootloader") configuration file and add new entries ('default' and 'fallback') for your custom kernel. If you renamed your kernel in the *PKGBUILD pkgbase* you may have to rename the initramfs.img in your *$build/pkg/kernel/etc* before installing with pacman. That way, you can have both the stock kernel and the custom one to choose from.

## Updating

Assuming one has an arch kernel source that he wants to update, one method to do that is with [https://git.archlinux.org/linux.git](https://git.archlinux.org/linux.git). Follows a concrete example. In what follows, the paths are relative to the top kernel source directory, which is assumed at ~/build/linux/. In general, arch sets an arch kernel source with two local git repositories. The one at archlinux-linux/ is a local bare [git](/index.php/Git "Git") repository pointing to [git://git.archlinux.org/linux.git](git://git.archlinux.org/linux.git). The other one is at src/archlinux-linux, pulling from the first repository. Possible local patches, and building, is expected at src/archlinux-linux/.

For this example, the HEAD of the locally installed bare git repository source at archlinux-linux/ was initially pointing to `4010b622f1d2 Merge branch 'dax-fix-5.3-rc3' of [git://git.kernel.org/pub/scm/linux/kernel/git/nvdimm/nvdimm](git://git.kernel.org/pub/scm/linux/kernel/git/nvdimm/nvdimm)`, which is somewhere between v5.2.5-arch1 and v5.2.6-arch1.

```
$ cd archlinux-linux/
$ git fetch --verbose

```

That was fetching v5.2.7-arch1, which was the newest archlinux tag.

```
$ cd ../src/archlinux-linux/
$ git checkout master
$ git pull
$ git fetch --tag --verbose
$ git branch --verbose 5.2.7-arch1 v5.2.7-arch1
$ git checkout 5.2.7-arch1

```

You can verify you are on track with something like

```
$ git log --oneline 5.2.7-arch1 | head --lines 7
13193bfc03d4 Arch Linux kernel v5.2.7-arch1
9475c6772d05 netfilter: nf_tabf676926c7f60les: fix module autoload for redir
498d650048f6 iwlwifi: Add support for SAR South Korea limitation
bb7293abdbc7 iwlwifi: mvm: disable TX-AMSDU on older NICs
f676926c7f60 ZEN: Add CONFIG for unprivileged_userns_clone
5e4e503f4f28 add sysctl to disallow unprivileged CLONE_NEWUSER by default
5697a9d3d55f Linux 5.2.7

```

This shows few specific archlinux patches between Linux 5.2.7 and Arch Linux kernel v5.2.7-arch1\. The important lines here are Linux 5.2.7 and Arch Linux kernel v5.2.7-arch1\. Obviously, there might be other patches at other versions, and the commit identifiers, such as f676926c7f60, as well as the kernel version, will be different for other versions.

Other than the directory archlinux-linux/, and the version file, all other 4 files at ../../src/ are symlinked to files by the same name on its parent directory.

```
$ ls ../../src
60-linux.hook  archlinux-linux	linux.preset
90-linux.hook  config		version

```

The up to date version of these 4 files, as well as the newer PKGBUILD, can be pulled in by the `asp` command:

```
$ cd ../../
$ asp update
$ asp export linux
$ mv --verbose linux linux-tmp

```

```
$ ls linux-tmp
60-linux.hook  config	      linux.preset
90-linux.hook  linux.install  PKGBUILD

```

Now one should manually merge, probably copy, the files at linux-tmp to the files by the same name at its parent directory. After which, the directory linux-tmp/, with all the files in it, can be deleted. Then run manually most, if not all, of PKGBUILD::prepare(). This should also take care for src/version.

At this point, `makepkg --verifysource` should succseed. And `makepkg --noextract` should be able to build the packages as if the source was extracted by `makepkg --nobuild`.

## See Also

*   [https://kernel.org/doc/Documentation/kbuild/kconfig.txt](https://kernel.org/doc/Documentation/kbuild/kconfig.txt) and the parent directory