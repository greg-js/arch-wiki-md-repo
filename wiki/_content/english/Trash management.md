To prevent accidental deletion of files, you can use a trash can. To ensure compatibility between multiple applications, you can use software (CLI, GUI or Library) that follow the [FreeDesktop.org's Trash specification](https://specifications.freedesktop.org/trash-spec/trashspec-latest.html).

**Note:** Some applications can use a trash can per filesystem (see the specification)

**Warning:** When deleting a file on another filesystem, usage of a trash can might lead to a copy between filesystems, leading to some latency

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Trash creation](#Trash_creation)
*   [2 Trash space usage management](#Trash_space_usage_management)
    *   [2.1 Software list](#Software_list)
    *   [2.2 Criterias](#Criterias)
    *   [2.3 Automation](#Automation)

## Trash creation

*   **trash-cli** — A command-line interface implementing [FreeDesktop.org's Trash specification](https://specifications.freedesktop.org/trash-spec/trashspec-latest.html).

	[https://github.com/andreafrancia/trash-cli](https://github.com/andreafrancia/trash-cli) || [trash-cli](https://www.archlinux.org/packages/?name=trash-cli)

## Trash space usage management

To prevent the trash can from using to much space, you can empty it yourself, or have a pruning policy

### Software list

autotrash (not in the AUR)

### Criterias

*   make sure to have at least x MB of free space
*   delete files older than x days
*   only empty if you have less than x MB of free space (useful in combination of previous criteria)
*   maximum trash can size
*   file size
*   file type
*   original path

### Automation

To automate emptying the trash can, you can use [cron](/index.php/Cron "Cron"), [systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers"), or [inotify](/index.php/Inotify "Inotify") (using inotify, only new deletion would trigger the trash can automation)