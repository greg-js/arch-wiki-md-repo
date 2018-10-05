[Elixir](https://en.wikipedia.org/wiki/Elixir_(programming_language) is a dynamic, functional language designed for building scalable and maintainable applications. It leverages the [Erlang](https://www.erlang.org/) VM, known for running low-latency, distributed and fault-tolerant systems, while also being successfully used in web development and the embedded software domain.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Single Version](#Single_Version)
    *   [1.2 Multiple Versions](#Multiple_Versions)
*   [2 Configuration](#Configuration)
*   [3 See Also](#See_Also)

## Installation

### Single Version

For the latest version of Elixir, [install](/index.php/Install "Install") the [elixir](https://www.archlinux.org/packages/?name=elixir) package from the [official repositories](/index.php/Official_repositories "Official repositories"). It includes Erlang, which is needed to run Elixir.

### Multiple Versions

If you want to run multiple versions of Elixir and/or Erlang, these tools help with installing and managing multiple Elixir/Erlang versions:

*   [asdf](https://github.com/asdf-vm/asdf) - Elixir and Erlang
*   [exenv](https://github.com/mururu/exenv) - Elixir only
*   [kiex](https://github.com/taylor/kiex) - Elixir only
*   [kerl](https://github.com/kerl/kerl) - Erlang only

## Configuration

Be sure to have Elixir's bin path in your PATH environment variable to ease development.

*   Single version

	`/usr/bin`

*   Multiple versions

	Please refer to the tool you used to install Elixir

In both cases, you need to find your [shell profile file](http://unix.stackexchange.com/questions/117467/how-to-permanently-set-environmental-variables/117470#117470), and then add to the end of this file the following line reflecting the path to your Elixir installation:

```
 export PATH="$PATH:/path/to/elixir/bin"

```

## See Also

*   [Elixir](http://elixir-lang.org/)
*   [Erlang](https://www.erlang.org/)