[Node.js](http://nodejs.org/) is a javascript runtime environment combined with useful libraries. It uses [Google's V8 engine](https://code.google.com/p/v8/) to execute code outside of the browser. Due to its event-driven, non-blocking I/O model, it is suitable for real-time web applications.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Alternate Installations](#Alternate_Installations)
*   [2 Node Packaged Modules](#Node_Packaged_Modules)
    *   [2.1 Managing packages with npm](#Managing_packages_with_npm)
        *   [2.1.1 Installing packages](#Installing_packages)
        *   [2.1.2 Updating packages](#Updating_packages)
            *   [2.1.2.1 Updating All Packages](#Updating_All_Packages)
        *   [2.1.3 Removing packages](#Removing_packages)
        *   [2.1.4 Listing packages](#Listing_packages)
    *   [2.2 Managing packages with pacman](#Managing_packages_with_pacman)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 node-gyp python errors](#node-gyp_python_errors)
*   [4 Additional Resources](#Additional_Resources)

## Installation

[nodejs](https://www.archlinux.org/packages/?name=nodejs) package is available in the [official repositories](/index.php/Official_repositories "Official repositories").

### Alternate Installations

It is not uncommon to need or desire to work in different versions of [nodejs](https://www.archlinux.org/packages/?name=nodejs). A preferred method among node users is to use [NVM](https://github.com/creationix/nvm) (Node Version Manger). NVM allows for cheap and easy alternative installs. Usage is well documented on the projects github but is as simple as:

```
  $ nvm install VERSION_NUM

```

**Warning:** This section refers to [Node Version Manager](https://github.com/creationix/nvm), installing from [npm](https://www.npmjs.com/) will load a **different** project with the same name.

## Node Packaged Modules

[npm](https://www.npmjs.org/) is the official package manager for node.js. Since [nodejs](https://www.archlinux.org/packages/?name=nodejs) 0.12.2-4, `npm` is no longer included in the package. It is available as [npm](https://www.archlinux.org/packages/?name=npm) in the [official repositories](/index.php/Official_repositories "Official repositories").

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

By default this command installs the package under `/usr/lib/node_modules/npm` and requires admin privileges to do so.

For a user-wide installation you can configure `npm` to use a local folder instead. This can be done in various ways:

*   Manually with the `--prefix` command line flag (e.g. `npm -g install packageName --prefix ~/.node_modules`).
*   Using the `npm_config_prefix` environment variable.
*   Using a user config file `~/.npmrc`.

First method is not recommended since you need to remember the location and give it as the parameter each time you do an operation.

For the second method simply add the following lines to your shell configuration file (e.g. `.bash_profile`).

```
PATH="$HOME/.node_modules/bin:$PATH"
export npm_config_prefix=~/.node_modules

```

Do not forget to log out and log back in or restart your shell accordingly.

For the third method you can use the command:

```
$ npm config edit

```

You can then find the `prefix` option and set a desired location:

```
prefix=~/.node_modules

```

Do not forget to delete the preceding `;` on the line or it will be read as a comment. You can now add the location of your executables to your shell configuration file (e.g. `.bash_profile`).

```
PATH="$HOME/.node_modules/bin:$PATH"

```

Again do not forget to log out and log back in or restart your shell accordingly.

#### Updating packages

Updating packages is as simple as

```
$ npm update packageName

```

For the case of globally installed packages (`-g`)

```
# npm update -g packageName

```

**Note:** Remember that globally installed packages require administrator privileges

##### Updating All Packages

However, sometimes you may just wish to update all packages. Be it locally or globally. Leaving off the packageName `npm` will attempt to update all the packages

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

To show a tree view of the installed packages use:

```
$ npm -g list

```

### Managing packages with pacman

Some node.js packages can be found in [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") with the name `nodejs-packageName`.

## Troubleshooting

### node-gyp python errors

Some node modules use the `node-gyp` utility which does not support Python 3, which in most cases will be the default system-wide Python executable. To resolve such errors, make sure you have [python2](https://www.archlinux.org/packages/?name=python2) installed, then set the default npm Python like so:

```
$ npm config set python /usr/bin/python2

```

In case of errors like **gyp WARN EACCES user "root" does not have permission to access the ... dir** *--unsafe-perm* option might help:

```
$ sudo npm install --unsafe-perm -g node-inspector

```

## Additional Resources

For further information on [nodejs](https://www.archlinux.org/packages/?name=nodejs) and use of its official package manager [npm](https://www.npmjs.org/) you may wish to consult the following external resources

*   [NodeJs Documentation](http://nodejs.org/documentation/) Documentation and Tutorials for Node
*   [NodeJS Community](http://nodejs.org/community/) Webpage
*   [API Documentation](https://www.npmjs.org/doc/) Official `npm` API documentation
*   IRC channel #node.js on irc.freenode.net