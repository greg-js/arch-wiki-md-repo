The Battle.net client is a tool to download, update and launch games by Blizzard Entertainment. It is not officially available for Linux, but usable through [Wine](/index.php/Wine "Wine").

## Contents

*   [1 Installation](#Installation)
*   [2 Known issues](#Known_issues)
    *   [2.1 Crash after login/no 'Login' buttons](#Crash_after_login.2Fno_.27Login.27_buttons)
    *   [2.2 Login region select](#Login_region_select)
    *   [2.3 White flashing](#White_flashing)
    *   [2.4 Login screen stuck at loading spinner (input fields disabled/greyed out)](#Login_screen_stuck_at_loading_spinner_.28input_fields_disabled.2Fgreyed_out.29)
*   [3 See also](#See_also)

## Installation

You need to install [wine](/index.php/Wine "Wine"), [winetricks](https://www.archlinux.org/packages/?name=winetricks), [lib32-gnutls](https://www.archlinux.org/packages/?name=lib32-gnutls), and [lib32-libldap](https://www.archlinux.org/packages/?name=lib32-libldap)

From winetricks, install:

```
$ winetricks corefonts

```

## Known issues

### Crash after login/no 'Login' buttons

If the launcher crashes after logging in, and/or you are missing the 'Log in to Blizzard' and 'Log in with Facebook' buttons, try running `winecfg` and changing your Windows Version to Windows XP.

### Login region select

When logging in, you must move the mouse over where the dropdown would be for 'Region Select' - otherwise it does not show up.

### White flashing

The client often flashes when the window is moved, or other windows are moved over it. This should not affect the running of the app.

### Login screen stuck at loading spinner (input fields disabled/greyed out)

There are two possible causes for this:

1.  Missing [lib32-gnutls](https://www.archlinux.org/packages/?name=lib32-gnutls) (cannot connect due to no HTTPS)
2.  Battle.net's "Browser Acceleration" has been enabled

To fix #1, install lib32-gnutls package. If wine still complains about it not being found, you may need to remove `.wine` folder and restart the whole installtion process (if you do this, remember to rerun `winetricks corefonts` to install the runtime files.

To fix #2, disconnect from the internet and relaunch Battle.net Launcher. The email/password field should now be enabled and you can click the little gear icon beside the fields to configure options. Go to 'Advanced' and disable browser acceleration.

## See also

[Battle.net App (WineHQ AppDB)](https://appdb.winehq.org/objectManager.php?iId=28855&sClass=version)