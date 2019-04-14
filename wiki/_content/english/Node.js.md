[Node.js](http://nodejs.org/) is a JavaScript runtime environment combined with useful libraries. It uses [Google's V8 engine](https://v8.dev) to execute code outside of the browser. Due to its event-driven, non-blocking I/O model, it is suitable for real-time web applications.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Alternate installations](#Alternate_installations)
*   [2 Node Packaged Modules](#Node_Packaged_Modules)
    *   [2.1 Managing packages with npm](#Managing_packages_with_npm)
        *   [2.1.1 Installing packages](#Installing_packages)
            *   [2.1.1.1 Allow user-wide installations](#Allow_user-wide_installations)
        *   [2.1.2 Updating packages](#Updating_packages)
            *   [2.1.2.1 Updating all packages](#Updating_all_packages)
        *   [2.1.3 Removing packages](#Removing_packages)
        *   [2.1.4 Listing packages](#Listing_packages)
    *   [2.2 Managing packages with pacman](#Managing_packages_with_pacman)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 node-gyp python errors](#node-gyp_python_errors)
    *   [3.2 Cannot find module ... errors](#Cannot_find_module_..._errors)
*   [4 Additional resources](#Additional_resources)

## Installation

[Install](/index.php/Install "Install") the [nodejs](https://www.archlinux.org/packages/?name=nodejs) package.

### Alternate installations

It is not uncommon to need or desire to work in different versions of [nodejs](https://www.archlinux.org/packages/?name=nodejs). A preferred method among node users is to use [NVM](https://github.com/creationix/nvm) (Node Version Manager). [nvm](https://aur.archlinux.org/packages/nvm/) allows for cheap and easy alternative installs.

You can set it up by adding this to your shell's startup file:

```
# Set up Node Version Manager
source /usr/share/nvm/init-nvm.sh

```

Or this if you want to use a custom nvm directory:

```
# Set up Node Version Manager
export NVM_DIR="$HOME/.nvm"                            # You can change this if you want.
export NVM_SOURCE="/usr/share/nvm"                     # The AUR package installs it to here.
[ -s "$NVM_SOURCE/nvm.sh" ] && . "$NVM_SOURCE/nvm.sh"  # Load NVM

```

Usage is well documented on the project's GitHub but is as simple as:

```
$ nvm install 8.0
Downloading and installing node v8.0.0...
[..]

$ nvm use 8.0
Now using node v8.0.0 (npm v5.0.0)

```

If you decide to use [nvm](https://aur.archlinux.org/packages/nvm/), previously it was suggested to use `nodejs-fake` package from AUR. Which is now [deleted](https://lists.archlinux.org/pipermail/aur-requests/2018-January/021828.html). Suggested way is to use `--assume-installed nodejs=<version>`, as per [pacman](https://www.archlinux.org/pacman/pacman.8.html#_transaction_options_apply_to_em_s_em_em_r_em_and_em_u_em) manual.

## Node Packaged Modules

[npm](https://www.npmjs.org/) is the official package manager for node.js. It can be [installed](/index.php/Install "Install") with the [npm](https://www.archlinux.org/packages/?name=npm) package.

### Managing packages with npm

#### Installing packages

Any package can be installed using:

```
$ npm install packageName

```

This command installs the package in the current directory under `node_modules` and executables under `node_modules/.bin`.

For a system-wide installation global switch `-g` can be used:

```
# npm -g install packageName

```

By default this command installs the package under `/usr/lib/node_modules/npm` and requires root privileges to do so.

##### Allow user-wide installations

To allow *global* package installations for the current [user](/index.php/User "User"), set the `npm_config_prefix` [environment variable](/index.php/Environment_variables#Per_user "Environment variables"). This is used by both npm and [yarn](https://yarnpkg.com/en/).

 `~/.profile` 
```
PATH="$HOME/.node_modules/bin:$PATH"
export npm_config_prefix=~/.node_modules
```

Re-login or *source* to update changes.

You can also specify the `--prefix` parameter for `npm install`. However, this is **not** recommended, since you'll need to add it every time you install a global package.

```
$ npm -g install packageName --prefix ~/.node_modules

```

#### Updating packages

Updating packages is as simple as

```
$ npm update packageName

```

For the case of globally installed packages (`-g`)

```
# npm update -g packageName

```

**Note:** Remember that globally installed packages require administrator privileges unless `prefix` is set to a user-writable directory

##### Updating all packages

However, sometimes you may just wish to update all packages, either locally or globally. Leaving off the packageName `npm` will attempt to update all packages

```
$ npm update

```

or add the `-g` flag to update globally installed packages

```
# npm update -g

```

#### Removing packages

To remove a package installed with the `-g` switch simply use:

```
# npm -g uninstall packageName

```

**Note:** Remember that globally installed packages require administrator privileges

to remove a local package drop the switch and run:

```
$ npm uninstall packageName

```

#### Listing packages

To show a tree view of the installed globally packages use:

```
$ npm -g list

```

This tree is often quite deep. To only display the top level packages use:

```
$ npm list --depth=0

```

To display obsolete packages that may need to be updated:

```
$ npm outdated

```

### Managing packages with pacman

Some node.js packages can be found in [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") with the name `nodejs-packageName`.

## Troubleshooting

### node-gyp python errors

Some node modules use the `node-gyp` utility which does not support Python 3, which in most cases will be the default system-wide Python executable. To resolve such errors, make sure you have [python2](https://www.archlinux.org/packages/?name=python2) installed, then set the default npm Python like so:

```
$ npm config set python /usr/bin/python2

```

In case of errors like `gyp WARN EACCES user "root" does not have permission to access the ... dir`, `--unsafe-perm` option might help:

```
# npm install --unsafe-perm -g node-inspector

```

### Cannot find module ... errors

Since npm 5.x.x. package-lock.json file is generated along with the package.json file. Conflictions may arise when the two files refer to different package versions. A temporary method to solving this problem has been:

```
$ rm package-lock.json
$ npm install

```

However, fixes were made after npm 5.1.0 or above. For further information, see: [missing dependencies](https://github.com/npm/npm/pull/17508)

## Additional resources

For further information on Node.js and the use of its official package manager NPM you may wish to consult the following external resources

*   [Node.js documentation](https://nodejs.org/en/docs/)
*   [NPM documentation](https://docs.npmjs.com/)
*   IRC channel #node.js on irc.freenode.net