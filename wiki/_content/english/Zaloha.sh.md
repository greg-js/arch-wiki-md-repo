[Zaloha.sh](https://github.com/Fitus/Zaloha.sh/) is a shell script to synchronize two local directories: a source directory and a backup directory.

Internally, it uses only standard Unix commands: **find**, **sort**, **awk**, **mkdir**, **rmdir**, **cp** and **rm**.

It's key feature is simplicity. To operate it, you need just one single file: the bash script **Zaloha.sh**.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Documentation](#Documentation)
*   [4 See also](#See_also)

## Installation

Download the shell script **Zaloha.sh** from the [Official repository](https://github.com/Fitus/Zaloha.sh/) and make it executable.

## Usage

```
$ Zaloha.sh --sourceDir="test_source" --backupDir="test_backup" [other options, see docu]

```

Upon invocation, it analyzes the two directories and prepares the actions (commands) necessary to synchronize the two directories.

The prepared actions are presented to the user for confirmation. If the user confirms, the actions are executed.

Using a command line option, the program can also be made non-interactive.

## Documentation

The program carries its documentation with itself:

```
$ Zaloha.sh --help

```

An online documentation (same contents, but nicer format) is available here: [Online documentation](https://github.com/Fitus/Zaloha.sh/blob/master/DOCUMENTATION.md/)

## See also

*   [Official repository](https://github.com/Fitus/Zaloha.sh/)
*   [Article in OSTechNix: How To Synchronize Files And Directories Using Zaloha.sh](https://www.ostechnix.com/how-to-synchronize-files-and-directories-using-zaloha-sh/)