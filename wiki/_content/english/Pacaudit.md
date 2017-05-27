*pacaudit* audits installed packages on Arch Linux against known vulnerabilities listed on [https://security.archlinux.org](https://security.archlinux.org).

## Installation

[Install](/index.php/Install "Install") the [pacaudit](https://aur.archlinux.org/packages/pacaudit/) package.

## Usage

```
$ pacaudit

```

Prints all vulnerable packages by name and the sum of all vulnerable packages.

```
$ pacaudit -v

```

Prints all vulnerable packages by name, with CVE, severity and the sum of all vulnerable packages.

```
$ pacaudit -n

```

Returns "OK" if no vulnerable packages are installed, "WARNING" if no vulnerable package with severity HIGH or higher is installed and CRITICAL else.

## Development

Please report bugs, feature requests and stars on Github: [https://github.com/steffenfritz/pacaudit](https://github.com/steffenfritz/pacaudit).