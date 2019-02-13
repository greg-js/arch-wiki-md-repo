[Ledger](http://ledger-cli.org/) is a powerful, double-entry accounting system that is accessed from the UNIX command-line. Ledger, begun in 2003, is written by John Wiegley and released under the BSD license.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Assign commodity during ledger convert](#Assign_commodity_during_ledger_convert)

## Installation

There are several ports of ledger to various languages. [ledger](https://www.archlinux.org/packages/?name=ledger) is the original. [hledger](https://www.archlinux.org/packages/?name=hledger) is a port to haskell, which is also popular.

## Usage

[The online documentation](http://ledger-cli.org/3.0/doc/ledger3.html) contains [a tutorial](http://ledger-cli.org/3.0/doc/ledger3.html#Ledger-Tutorial) to help new users get started.

**Tip:** To avoid having to type `--file /path/to/finances.ledger` every time you invoke ledger, consider setting `LEDGER_FILE` as one of your [Environment variables](/index.php/Environment_variables "Environment variables") or add `--file /path/to/finances.ledger` to your `.ledgerrc`.

Emacs users may be interested in using ledger-mode. ledger-mode is available on MELPA and comes with info, accessible via `C-h i m Ledger mode RET`.

## Tips and tricks

### Assign commodity during ledger convert

By default, ledger does not assign a commodity when it converts from csv files to ledger format. To have it assign a currency when one is missing, you can make a currency the default commodity of a ledger file by adding something like this to the file:

```
commodity $
  note US Dollar
  default
  nomarket
  format $1,000.00
```