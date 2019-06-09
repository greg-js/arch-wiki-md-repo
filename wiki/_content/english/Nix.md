[Nix](https://nixos.org/nix/) is a purely functional package manager.

See the [Nix Package Manager Guide](https://nixos.org/nix/manual/) for information.

## Installation

Nix is available in the AUR as [nix](https://aur.archlinux.org/packages/nix/).

## Configuration

In order to use Nix for the first time, you need to add a channel. But before, you need to address some permission issues.

Nix is by default installed in the `/nix` folder. If you want to use Nix with an [unprivileged account](https://nixos.org/nix/manual/#sec-single-user), run

```
   sudo chown -R you:you /nix

```

Then, in order to add and update channels, run [the following commnads](https://nixos.org/nix/manual/#sec-channels):

```
   nix-channel --add [https://nixos.org/channels/nixpkgs-unstable](https://nixos.org/channels/nixpkgs-unstable)
   nix-channel --update
   nix-env -u

```