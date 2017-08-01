Kernel Live Patching (KLP) allows quick fixes to the kernel space without rebooting the whole system. Since version 4.0, related patches have been accepted [[1]](https://lwn.net/Articles/619390/)[[2]](https://lwn.net/Articles/622936/)[[3]](https://lwn.net/Articles/634649/), so one can configure his/her kernel to enable this feature. Generally, KLP is achieved by the following steps:

1.  Obtain the source tree of the running kernel
2.  Prepare the patch against the kernel
3.  Apply some tools (as follows) to help transform and load the patch

Some projects provide the live patching utilities before KLP was officially supported, such as Oracle's [#ksplice](#ksplice), SuSE's [#kGraft](#kGraft), and RedHat's [#kpatch](#kpatch). They implemented the KLP functionality in different ways. The minimalistic functional set of patches entered mainstream kernel were derived from kpatch and kGraft.

## Contents

*   [1 kpatch](#kpatch)
    *   [1.1 Installation](#Installation)
    *   [1.2 Usage](#Usage)
*   [2 kGraft](#kGraft)
*   [3 ksplice](#ksplice)
    *   [3.1 Installation](#Installation_2)
    *   [3.2 Usage](#Usage_2)
*   [4 See also](#See_also)

## kpatch

### Installation

Install [linux-kpatch](https://aur.archlinux.org/packages/linux-kpatch/) for an appropriate kernel and [kpatch-git](https://aur.archlinux.org/packages/kpatch-git/) for userspace tools.

You can also manually build a kernel that supports kpatch usage, by enabling `CONFIG_LIVEPATCH`, `CONFIG_DEBUG_INFO`, and `CONFIG_KALLSYMS`.

**Note:** Remember to update the bootloader after you install the special kernel.

### Usage

Once both packages are successfully built and after reboot, you may

```
$ export ROOTDIR=some/dir/aur/linux-kpatch/src/linux-x-y
$ cd $ROOTDIR

```

Assume that you have done some modifications and have a patch *some.patch* (against the source tree after a `makepkg -o`, not the vanilla kernel of version *x.y*) in the working directory. Launch the kpatch utility,

```
$ kpatch-build -s $(pwd) -t $(pwd)/vmlinux *some.patch*

```

This command involves two kernel builds, the original one and the patched one, so it may take a period of time to complete. After the build is over, there should be a *kpatch-some.ko* module in the same directory. And then,

```
# insmod *kpatch-some.ko*

```

should do the trick.

For further information, please check the manpages or [the github repository](https://github.com/dynup/kpatch).

## kGraft

KGraft hasn't been tested in Arch environment, so is not supported as of this writing.

## ksplice

### Installation

Install the [ksplice-git](https://aur.archlinux.org/packages/ksplice-git/) package from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository").

### Usage

First, you need the kernel source tree for the kernel you are currently running, and some files from the previous kernel build: `System.map` and `.config`.

If you don't have `System.map` from the previous build, you can copy `/proc/kallsyms` as an equivalent. If the `kernel.kptr_restrict` kernel parameter is enabled, remember to copy it as root.

This example makes use of the `--diffext` option which creates a patch based on the differences between the old and the new source files.

Make a `ksplice` directory in the kernel source tree, copy `System.map` over from the previous build, and copy `.config` into the tree if it is not already in the source tree:

```
# mkdir -p src/ksplice
# cp System.map src/ksplice
# cp .config src/

```

Create a ksplice patch and wait for the kernel to rebuild. All files that end with `new` will be compiled into the ksplice patch. C source files, for example, should end in `.cnew` as the diffext is appended directly.

```
# ksplice-create --diffext=new src/

```

Apply the newly generated patch to the running kernel:

```
# ksplice-apply ksplice-*.tar.gz

```

See man pages for `ksplice-apply`, `ksplice-create`, `ksplice-view`, and `ksplice-undo`.

## See also

*   [The kernel document of livepatch](https://www.kernel.org/doc/Documentation/livepatch/livepatch.txt)
*   [wikipedia:Kpatch](https://en.wikipedia.org/wiki/Kpatch "wikipedia:Kpatch")
*   [wikipedia:KGraft](https://en.wikipedia.org/wiki/KGraft "wikipedia:KGraft")
*   [wikipedia:Ksplice](https://en.wikipedia.org/wiki/Ksplice "wikipedia:Ksplice")