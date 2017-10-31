Mono is an open source, cross-platform, implementation of C# and the CLR that is binary compatible with Microsoft.NET.

## Contents

*   [1 Installation](#Installation)
*   [2 Running Mono applications](#Running_Mono_applications)
*   [3 Testing Mono](#Testing_Mono)
*   [4 Development](#Development)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 I get an error "cannot execute "path/to/your/binary" file name has not been set."](#I_get_an_error_.22cannot_execute_.22path.2Fto.2Fyour.2Fbinary.22_file_name_has_not_been_set..22)
    *   [5.2 I get an error when I try to run Mono binaries directly: "cannot execute binary file"](#I_get_an_error_when_I_try_to_run_Mono_binaries_directly:_.22cannot_execute_binary_file.22)
    *   [5.3 I get an TLS handshake (or similar certificate based) error](#I_get_an_TLS_handshake_.28or_similar_certificate_based.29_error)
*   [6 See also](#See_also)

## Installation

Mono can be [installed](/index.php/Pacman "Pacman") with the package [mono](https://www.archlinux.org/packages/?name=mono).

If you need VisualBasic.Net support you have to [install](/index.php/Install "Install") the VisualBasic.Net interpreter with the package [mono-basic](https://aur.archlinux.org/packages/mono-basic/).

MonoDevelop calls [xterm](/index.php/Xterm "Xterm") when you run your project. You might install it, when you're writing a console application.

## Running Mono applications

You can execute Mono binaries by calling `mono` manually:

```
$ mono programsname.exe

```

You can also execute Mono binaries directly, just like native binaries:

```
$ chmod 755 exefile.exe
$ ./exefile.exe

```

## Testing Mono

Make a new file:

 `test.cs` 
```
using System;

public class Test {
 public static void Main(string[] args) {
  Console.WriteLine("Hello World!");
 }
}

```

Then run:

```
$ mcs test.cs
$ mono test.exe
Hello world!

```

## Development

Starting to develop in Mono/C# is very easy. Just [install](/index.php/Install "Install") the [MonoDevelop IDE](http://monodevelop.com/) with packages [monodevelop](https://aur.archlinux.org/packages/monodevelop/). Alternatively, you can install the [rider](https://aur.archlinux.org/packages/rider/) IDE.

If you want the API documentation browser and some testing and development tools you have to install [mono-tools](https://www.archlinux.org/packages/?name=mono-tools).

## Troubleshooting

### I get an error "cannot execute "path/to/your/binary" file name has not been set."

You might install [xterm](/index.php/Xterm "Xterm"), since MonoDevelop starts [xterm](/index.php/Xterm "Xterm") when you press on run. This might be a possible dependency.

### I get an error when I try to run Mono binaries directly: "cannot execute binary file"

The [binfmt_misc](https://en.wikipedia.org/wiki/Binfmt_misc "wikipedia:Binfmt misc") handler for Mono has not yet been set up, as explained in detail on the [Mono Project website](http://www.mono-project.com/Guide:Running_Mono_Applications#Registering_.exe_as_non-native_binaries_.28Linux_only.29).

To fix this, [restart](/index.php/Daemon "Daemon") the `systemd-binfmt` service.

### I get an TLS handshake (or similar certificate based) error

Try `mozroots --import --ask-remove` which should update monos certificates. `mozroots` is part of the mono package.

## See also

*   [Official Mono website](http://www.mono-project.com)
*   [The Mono Handbook](http://mono-project.com/Monkeyguide)
*   [The API reference of Mono](http://go-mono.org/docs)
*   [ECMA-334: C# Language Specification](http://www.ecma-international.org/publications/standards/ECMA-334.HTM)
*   [ECMA-335: Common Language Infrastructure (CLI)](http://www.ecma-international.org/publications/standards/ECMA-335.HTM)
*   [Instructions for running Mono applications](http://www.mono-project.com/Guide:Running_Mono_Applications)