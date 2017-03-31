[goldendict](http://goldendict.org) is a feature-rich dictionary lookup program.

## Installation

[Install](/index.php/Install "Install") [goldendict](https://www.archlinux.org/packages/?name=goldendict) from the [official repositories](/index.php/Official_repositories "Official repositories").

## Configuration

### Offline Dictionary Lookup with dictd

First `dictd` must be configured for hosting offline dictionaries. See [Hosting Offline Dictionaries](/index.php/Dictd#Hosting_Offline_Dictionaries "Dictd").

Once the dictionaries have been installed, and `dictd` has been configured, `goldendict` can be configured to access the `dictd` dictionary databases by following these steps:

*   Press F3 to bring up the "Dictionaries" window.
*   Click on the "DICT servers" tab
*   Click "Add..."
*   Click to put a checkmark under "Enabled"
*   Double click under "Address" and type: `dict://localhost`. Make sure to change `localhost` if `dictd` is running on another server.
*   And finally click "OK".