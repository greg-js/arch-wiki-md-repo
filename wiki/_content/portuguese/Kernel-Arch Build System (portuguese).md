**Status de tradução:** Esse artigo é uma tradução de [Arch Linux](/index.php/Arch_Linux "Arch Linux"). Data da última tradução: 2019-12-20\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Arch_Linux&diff=0&oldid=582518) na versão em inglês.

Veja [Kernel_(Português)](/index.php/Kernel_(Portugu%C3%AAs) "Kernel (Português)") para ir ao artigo principal.

O [Arch Build System](/index.php/Arch_Build_System "Arch Build System") pode ser usado para compilar um kernel personalizado baseado no pacote oficial [linux](https://www.archlinux.org/packages/?name=linux). Este método de compilação pode automatizar todo o processo, além de ser baseado em um pacote bem testado. Você pode editar o PKGBUILD para usar uma configuração personalizada além de poder adicionar patches.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Obtendo os ingredientes](#Obtendo_os_ingredientes)
*   [2 Modifying the PKGBUILD](#Modifying_the_PKGBUILD)
    *   [2.1 Changing prepare()](#Changing_prepare())
    *   [2.2 Generate new checksums](#Generate_new_checksums)
*   [3 Compiling](#Compiling)
*   [4 Installing](#Installing)
*   [5 Boot loader](#Boot_loader)
*   [6 Updating](#Updating)
*   [7 See also](#See_also)

## Obtendo os ingredientes

Como você estará usando o [makepkg](/index.php/Makepkg "Makepkg"), Siga as práticas recomendadas primeiro. Por exemplo, você nao pode executar o makepkg como root ou usando sudo. Portanto, crie um diretório `build` na home de seu usuário.

```
 $ cd ~/
 $ mkdir build
 $ cd build/

```

[Install](/index.php/Install "Install") O pacote [asp](https://www.archlinux.org/packages/?name=asp) e o grupo de pacotes [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/).

You need a clean kernel to start your customization from. [ABS#Retrieve PKGBUILD source using Git](/index.php/ABS#Retrieve_PKGBUILD_source_using_Git "ABS") and few other files into your build directory by running:

```
$ asp update linux
$ asp export linux

```

At this point, the directory tree looks like:

```
~/build/linux/-+
               +--config
               \__PKGBUILD
```

Then, get any other file you need (e.g. custom configuration files, patches, etc.) from the respective sources.

## Modifying the PKGBUILD

Edit `PKGBUILD` and look for the `pkgbase` parameter. Change this to your custom package name, e.g.:

```
 pkgbase=linux-custom

```

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

Best practice is to [install](/index.php/Install "Install") both packages together as they might be both needed (e.g. DKMS.)

```
# pacman -U *kernel-headers_package* *kernel_package*

```

## Boot loader

If you have modified `pkgbase` in order to have your new kernel installed alongside the default kernel you will need to update your bootloader configuration file and add new entries ('default' and 'fallback') for your custom kernel and the associated initramfs images.

## Updating

Assuming one has an arch kernel source that he wants to update, one method to do that is with [https://git.archlinux.org/linux.git](https://git.archlinux.org/linux.git). Follows a concrete example. In what follows, the top kernel source directory is assumed at ~/build/linux/.

In general, arch sets an arch kernel source with two local git repositories. The one at archlinux-linux/ is a local bare [git](/index.php/Git "Git") repository pointing to [git://git.archlinux.org/linux.git](git://git.archlinux.org/linux.git). The other one is at src/archlinux-linux/, pulling from the first repository. Possible local patches, and building, is expected at src/archlinux-linux/.

For this example, the HEAD of the locally installed bare git repository source at archlinux-linux/ was initially pointing to `4010b622f1d2 Merge branch 'dax-fix-5.3-rc3' of [git://git.kernel.org/pub/scm/linux/kernel/git/nvdimm/nvdimm](git://git.kernel.org/pub/scm/linux/kernel/git/nvdimm/nvdimm)`, which is somewhere between v5.2.5-arch1 and v5.2.6-arch1.

```
$ cd ~/build/linux/archlinux-linux/
$ git fetch --verbose

```

One can see it fetched v5.2.7-arch1, which was the newest archlinux tag, because it prints what new tags were obtained. If no new tags were obtained then there is no newer archlinux source available.

Now the source can be updated where the actual build will take place.

```
$ cd ~/build/linux/src/archlinux-linux/
$ git checkout master
$ git pull
$ git fetch --tags --verbose
$ git branch --verbose 5.2.7-arch1 v5.2.7-arch1
$ git checkout 5.2.7-arch1

```

You can verify you are on track with something like

```
$ git log --oneline 5.2.7-arch1 --max-count=7
13193bfc03d4 Arch Linux kernel v5.2.7-arch1
9475c6772d05 netfilter: nf_tabf676926c7f60les: fix module autoload for redir
498d650048f6 iwlwifi: Add support for SAR South Korea limitation
bb7293abdbc7 iwlwifi: mvm: disable TX-AMSDU on older NICs
f676926c7f60 ZEN: Add CONFIG for unprivileged_userns_clone
5e4e503f4f28 add sysctl to disallow unprivileged CLONE_NEWUSER by default
5697a9d3d55f Linux 5.2.7
```

This shows few specific archlinux patches between Linux 5.2.7 and Arch Linux kernel v5.2.7-arch1\. The important lines here are Linux 5.2.7 and Arch Linux kernel v5.2.7-arch1\. Obviously, there might be other patches at other versions, and the commit identifiers, such as f676926c7f60, as well as the kernel version, will be different for other versions.

The up to date PKGBUILD, as well archlinux kernel configuration file, can be pulled in by the `asp` command:

```
$ cd ~/build/linux/
$ asp update linux
$ asp -f export linux

```

**Note:** Sometimes the `asp` command does not update linux files even though there is a newer archlinux source tag. A possible reason is that archlinux linux files lag behind archlinux linux source.

Now you should [Vim#Merging files](/index.php/Vim#Merging_files "Vim") located in `~/build/linux/linux/*` into `~/build/linux/`. Merging can also done manually, or with [list of applications#Comparison, diff, merge](/index.php/List_of_applications#Comparison,_diff,_merge "List of applications"). Then run manually most, if not all, the shell commands of PKGBUILD::prepare().

At this point, `makepkg --verifysource` should succeed. And `makepkg --noextract` should be able to build the packages as if the source was extracted by `makepkg --nobuild`.

## See also

*   [https://kernel.org/doc/Documentation/kbuild/kconfig.txt](https://kernel.org/doc/Documentation/kbuild/kconfig.txt) and the parent directory