Related articles

*   [Cgroups](/index.php/Cgroups "Cgroups")
*   [Docker](/index.php/Docker "Docker")

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

*   [1 Setup](#Setup)
    *   [1.1 Required software](#Required_software)
        *   [1.1.1 Enable support to build unprivileged containers (optional)](#Enable_support_to_build_unprivileged_containers_(optional))
*   [2 See also](#See_also)

## Setup

### Required software

Installing [buildah](https://www.archlinux.org/packages/?name=buildah) will allow the host system to build privileged containers.

#### Enable support to build unprivileged containers (optional)

Users wishing to use Buildah to build *unprivileged* containers need to complete several additional setup steps.

Firstly, a kernel is required that has support for **User Namespaces** (a kernel with `CONFIG_USER_NS`). All Arch Linux kernels have support for `CONFIG_USER_NS`. However, due to more general security concerns, the default Arch kernel does ship with User Namespaces enabled only for the *root* user.

Enable the *sysctl* setting `kernel.unprivileged_userns_clone` to allow normal users to run unprivileged containers. This can be done for the current session with `sysctl kernel.unprivileged_userns_clone=1` and can be made permanent with [sysctl.d(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sysctl.d.5).

Finally, create both `/etc/subuid` and `/etc/subgid` to contain the mapping to the containerized uid/gid pairs for each user who shall be able to run the containers. The example below is for the root user (and systemd system unit) and an example user `buildah`:

 `/etc/subuid` 
```
root:100000:65536
buildah:100000:65536

```
 `/etc/subgid` 
```
root:100000:65536
buildah:100000:65536

```

## See also

*   [Builah Blog Post Series](https://buildah.io/)
*   [Containers Organization GitHub projects](https://github.com/containers)
*   [Podman daemonless container engine](https://podman.io/)