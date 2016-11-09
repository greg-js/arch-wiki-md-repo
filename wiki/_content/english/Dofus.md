[Dofus](http://www.dofus.com) is an MMORPG by [Ankama](http://www.ankama.com).

## Installation

[Install](/index.php/Install "Install") the [dofus](https://aur.archlinux.org/packages/dofus/) package.

Currently the game files are installed under the "games" group with group writability. You can add your user to the group (`usermod -a -G games *username*`) to take advantage of this. Otherwise, you may need to enter your password in order to update the game files.

## Troubleshooting

When debugging problems, it is helpful to set the environment variable `AK_LOG_CONSOLE=1` when running Dofus. It will then print detailed logs in the console.

A known problem is that some systems require `unset SESSION_MANAGER` in the environment, to avoid crashes on start up.

Occasionally the updater cannot function because of a leftover process from previous runs. Killing `transition` processes can solve this problem.