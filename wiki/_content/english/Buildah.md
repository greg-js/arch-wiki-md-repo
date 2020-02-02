Related articles

*   [Cgroups](/index.php/Cgroups "Cgroups")
*   [Docker](/index.php/Docker "Docker")
*   [Linux Containers](/index.php/Linux_Containers "Linux Containers")

[Buildah](https://buildah.io/) is a tool that facilitates building [Open Container Initiative](https://www.opencontainers.org/) (OCI) container images. The Buildah package provides a command line tool that can be used to:

*   create a working container, either from scratch or using an image as a starting point
*   create an image, either from a working container or via the instructions in a Dockerfile
*   images can be built in either the OCI image format or the traditional upstream docker image format
*   mount a working container's root filesystem for manipulation
*   unmount a working container's root filesystem
*   use the updated contents of a container's root filesystem as a filesystem layer to create a new image
*   delete a working container or an image
*   rename a local container

The most widely known alternative for building containers is [docker](/index.php/Docker "Docker"). Do note that Buildah does not run containers, for that you may want to consider [podman](https://www.archlinux.org/packages/?name=podman).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Enable support to build unprivileged containers](#Enable_support_to_build_unprivileged_containers)
*   [3 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [buildah](https://www.archlinux.org/packages/?name=buildah) and [podman](https://www.archlinux.org/packages/?name=podman) packages or, for the development version, the [buildah-git](https://aur.archlinux.org/packages/buildah-git/) package.

If you want to run as [non-root user](#Enable_support_to_build_unprivileged_containers), also install [fuse-overlayfs](https://aur.archlinux.org/packages/fuse-overlayfs/) for better performance and storage space efficiency.

**Note:** [official podman tutorial](https://github.com/containers/libpod/blob/master/docs/tutorials/rootless_tutorial.md) mentions that V1 cgroups will not allow running rootless containers. In order to use cgroups V2 optional **crun** runtime should be used - check what cgroups you have by running **podman info --debug** and then look for **CgroupVersion**; Look at wiki [to disable V1 cgroups](/index.php/Cgroups#Disabling_v1_cgroups "Cgroups")

**Note:** [official buildah installation guide](https://github.com/containers/buildah/blob/master/docs/tutorials/01-intro.md#rootless-user-configuration) points at [podman section](https://github.com/containers/libpod/blob/master/docs/tutorials/rootless_tutorial.md#ensure-fuse-overlayfs-is-installed) where advise is given to install fuse-overlays before installing podman

## Configuration

#### Enable support to build unprivileged containers

Users wishing to use Buildah to build *unprivileged* containers need to complete additional setup steps *before running podman for the first time*.

**Note:** If you are building system dedicated for running unprivileged containers then follow below steps before adding any user - this way you won't have to edit **/etc/subuid** and **/etc/subgid** - **useradd** will do that for you, you only need to run **touch /etc/subgid** and **touch /etc/subuid** as root

Firstly, a kernel is required that has support for **User Namespaces** (a kernel with `CONFIG_USER_NS`). All Arch Linux kernels have support for `CONFIG_USER_NS`. However, due to more general security concerns, the default Arch kernel does ship with User Namespaces enabled only for the *root* user.

Enable the *sysctl* setting `kernel.unprivileged_userns_clone` to allow normal users to run unprivileged containers. This can be done for the current session with `sysctl kernel.unprivileged_userns_clone=1` and can be made permanent with [sysctl.d(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sysctl.d.5).

Finally, create both `/etc/subuid` and `/etc/subgid` to contain the mapping to the containerized uid/gid pairs for each user who shall be able to run the containers.[[1]](https://github.com/containers/libpod/blob/master/docs/tutorials/rootless_tutorial.md#etcsubuid-and-etcsubgid-configuration) The example below is for the root user (and systemd system unit) and an example user `buildah`:

 `/etc/subuid` 
```
buildah:100000:65536

```
 `/etc/subgid` 
```
buildah:100000:65536

```

If you did run podman before applying the changes above, you will get errors when trying to pull images as an unprivileged user. Run `podman system migrate` to fix it.

If everything went well then after logging out and logging back in `buildah images` should not result in error

**Note:** If you see errors accessing **/run/user/0** then you have probably used **su** to become user you are using for test - you should log in as such user since **su** will not set **XDG_RUNTIME_DIR** and other environmental variables to correct values

## See also

*   [Builah Blog Post Series](https://buildah.io/)
*   [Containers Organization GitHub projects](https://github.com/containers)
*   [Podman daemonless container engine](https://podman.io/)