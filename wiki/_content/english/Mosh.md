From the [official website](http://mosh.mit.edu/):

	Remote terminal application that allows roaming, supports intermittent connectivity, and provides intelligent local echo and line editing of user keystrokes. Mosh is a replacement for [SSH](/index.php/SSH "SSH"). It is more robust and responsive, especially over slow connections such as Wi-Fi, cellular, and long-distance.

## Installation

[Install](/index.php/Install "Install") the [mosh](https://www.archlinux.org/packages/?name=mosh) package, or [mosh-git](https://aur.archlinux.org/packages/mosh-git/) for the latest revision.

## Usage

Mosh has an undocumented command line option `--predict=experimental` which produces more aggressive echoing of local keystrokes. Users interested in low-latency visual confirmation of keyboard input may prefer this prediction mode.

**Note:** Mosh by design does not let you access session history, consider installing a terminal multiplexer such as [tmux](/index.php/Tmux "Tmux") or [GNU Screen](/index.php/GNU_Screen "GNU Screen").