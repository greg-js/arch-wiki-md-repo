The **Blizzard App** (previously known as the **Battle.net client**) is a tool to download, update and launch games by Blizzard Entertainment. It is not officially available for Linux, but usable through [Wine](/index.php/Wine "Wine").

## Contents

*   [1 Installation](#Installation)
*   [2 Known issues](#Known_issues)
    *   [2.1 Crash after login/no 'Login' buttons/region select missing](#Crash_after_login.2Fno_.27Login.27_buttons.2Fregion_select_missing)
    *   [2.2 Login screen stuck at loading spinner (input fields disabled/greyed out)](#Login_screen_stuck_at_loading_spinner_.28input_fields_disabled.2Fgreyed_out.29)
    *   [2.3 Installer crashes after language selection](#Installer_crashes_after_language_selection)
*   [3 See also](#See_also)

## Installation

You need to install [wine](/index.php/Wine "Wine"), [winetricks](https://www.archlinux.org/packages/?name=winetricks), [lib32-gnutls](https://www.archlinux.org/packages/?name=lib32-gnutls), and [lib32-libldap](https://www.archlinux.org/packages/?name=lib32-libldap)

From winetricks, install:

```
$ winetricks corefonts

```

## Known issues

### Crash after login/no 'Login' buttons/region select missing

	Related Wine bugs: [38845](https://bugs.winehq.org/show_bug.cgi?id=38845), [42000](https://bugs.winehq.org/show_bug.cgi?id=42000)

This bug is fixed in Wine staging [2.18](https://www.wine-staging.com/news/2017-10-04-release-2.18.html). Install [wine-staging](https://www.archlinux.org/packages/?name=wine-staging) instead of [wine](https://www.archlinux.org/packages/?name=wine).

### Login screen stuck at loading spinner (input fields disabled/greyed out)

There are two possible causes for this:

1.  Missing [lib32-gnutls](https://www.archlinux.org/packages/?name=lib32-gnutls) (cannot connect due to no HTTPS)
2.  Battle.net's "Browser Acceleration" has been enabled

To fix #1, install lib32-gnutls package. If wine still complains about it not being found, you may need to remove `.wine` folder and restart the whole installtion process (if you do this, remember to rerun `winetricks corefonts` to install the runtime files.

To fix #2, disconnect from the internet and relaunch Battle.net Launcher. The email/password field should now be enabled and you can click the little gear icon beside the fields to configure options. Go to 'Advanced' and disable browser acceleration.

### Installer crashes after language selection

If you are using nvidia graphics driver, installing [lib32-nvidia-utils](https://www.archlinux.org/packages/?name=lib32-nvidia-utils) might solve the problem.

## See also

[Blizzard App (WineHQ AppDB)](https://appdb.winehq.org/objectManager.php?iId=28855&sClass=version)