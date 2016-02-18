From the language's [home page](http://dartlang.org):

	*Dart is a cohesive, scalable platform for building apps that run on the web (where you can use Polymer) or on servers (such as with Google Cloud Platform). Use the Dart language, libraries, and tools to write anything from simple scripts to full-featured apps.*

## Contents

*   [1 Installation](#Installation)
*   [2 Example](#Example)
*   [3 Dart Editor](#Dart_Editor)
*   [4 Dart Vim Syntax](#Dart_Vim_Syntax)

## Installation

The latest version of Dart is available in the [official repositories](/index.php/Official_repositories "Official repositories") as [dart](https://www.archlinux.org/packages/?name=dart). The bleeding edge version of Dart is available in the [AUR](/index.php/AUR "AUR") as [dart-trunk](https://aur.archlinux.org/packages/dart-trunk/).

## Example

Place the following code in a temporary file named hello.dart:

```
void main() {
  print("Hello Arch User!");
}

```

Now, run the following in the same directory as hello.dart:

```
$ dart hello.dart

```

You should get the following output:

```
Hello Arch User!

```

## Dart Editor

Dart has its own editor, based on Eclipse, and it is available in the AUR as [dart-editor](https://aur.archlinux.org/packages/dart-editor/) or [dart-editor-dev](https://aur.archlinux.org/packages/dart-editor-dev/) for the development version.

## Dart Vim Syntax

[vim-dart-plugin](https://aur.archlinux.org/packages/vim-dart-plugin/) provides a Vim plugin that supports the Dart language's syntax and provides highlighting for the language.