[Nix](https://nixos.org/nix/) is a purely functional package manager.

See the [Nix Package Manager Guide](https://nixos.org/nix/manual/) for information.

## Installation

Nix is available in the AUR as [nix](https://aur.archlinux.org/packages/nix/).

## Configuration

In order to use Nix for the first time, you need to add a channel. But before, you need to address some permission issues.

Nix is by default installed in the `/nix` folder. If using Nix with an [unprivileged account](https://nixos.org/nix/manual/#sec-single-user) is desired, run

```
sudo chown -R $USER. /nix/var/nix/{gcroots,profiles}

```

Then, in order to add and update channels, run [the following commands](https://nixos.org/nix/manual/#sec-channels):

```
nix-channel --add [https://nixos.org/channels/nixpkgs-unstable](https://nixos.org/channels/nixpkgs-unstable)
nix-channel --update
nix-env -u

```

If only using unprivileged Nix access, run to silence "warning: Nix search path entry '...' does not exist, ignoring":

```
sudo nix-channel --update

```

### Using archlinux-nix

[archlinux-nix](https://aur.archlinux.org/packages/archlinux-nix/) can be used to 'bootstrap' an archlinux compatible nix system setting up required groups and permissions.

After installing [nix](https://aur.archlinux.org/packages/nix/), which should install [archlinux-nix](https://aur.archlinux.org/packages/archlinux-nix/), to see available commands run:

```
 archlinux-nix

```

To bootstrap a system, run:

```
 archlinux-nix bootstrap

```

To setup build groups run:

```
 archlinux-nix setup-build-group

```