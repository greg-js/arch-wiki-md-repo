**OSH** (Oil Shell) is a Bash-compatible UNIX [command-line shell](/index.php/Command-line_shell "Command-line shell"). OSH can be run on most UNIX-like operating systems, including GNU/Linux. It is written in Python (v2.7), but ships with a native executable. The dialect of Bash recognized by OSH is called the OSH language.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Smoke Test](#Smoke_Test)
    *   [1.2 Making OSH your default shell](#Making_OSH_your_default_shell)
*   [2 Uninstallation](#Uninstallation)
*   [3 Project Goals](#Project_Goals)
    *   [3.1 Use Cases](#Use_Cases)
    *   [3.2 Oil Language Design Goals](#Oil_Language_Design_Goals)
    *   [3.3 Language Design Style](#Language_Design_Style)
    *   [3.4 Implementation Goals](#Implementation_Goals)
    *   [3.5 Longer Term Goals](#Longer_Term_Goals)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [osh](https://aur.archlinux.org/packages/osh/) package.

### Smoke Test

Make sure that OSH has been installed correctly by running the following in a terminal:

```
$> osh

```

This will start an OSH session and change the shell prompt to:

```
osh$

```

Identify an installed binary and attempt to invoke it in the OSH session to confirm that the output is correct.

For example:

```
osh$ ls
...

```

### Making OSH your default shell

See [Command-line shell#Changing your default shell](/index.php/Command-line_shell#Changing_your_default_shell "Command-line shell").

## Uninstallation

Change the default shell before removing the [osh](https://aur.archlinux.org/packages/osh/) package.

**Warning:** Failure to follow the below procedure may result in users no longer having access to a working shell.

Run following command:

```
$ chsh -s /bin/bash *user*

```

Use it for every user with *osh* set as their login shell (including root if needed). When completed, the [osh](https://aur.archlinux.org/packages/osh/) package can be removed.

Alternatively, change the default shell back to Bash by editing `/etc/passwd` as root.

**Warning:** It is strongly recommended to use `vipw` when editing `/etc/passwd` as it helps prevent invalid entries and/or syntax errors.

For example, change the following:

```
*username*:x:1000:1000:*Full Name*,,,:/home/*username*:/bin/osh

```

To this:

```
*username*:x:1000:1000:*Full Name*,,,:/home/*username*:/bin/bash

```

## Project Goals

**Immediate goal:** Implement a bash-compatible shell called OSH.

**Long term goal:** Design a modern Unix shell language called Oil that can do everything bash/zsh/etc. can do, and more.

Oil treats shell seriously as a programming language, in terms of both its implementation and defining its semantics.

For a more immediate view of the project, see the [Oil Blog](http://www.oilshell.org/blog/). In particular, this [blog entry](http://www.oilshell.org/blog/2017/01/19.html) was written at the same time as this page.

### Use Cases

*   System Administration
    *   Building Linux distributions (e.g. Arch Linux uses bash for PKGBUILD).
    *   Startup scripts
    *   Configure and build scripts. Reproducible and distributed builds.
*   Distributed Computing
    *   Building containers
    *   Specifying remote jobs
    *   Feedback and Monitoring: performance measurement, security testing.
*   Data Science / Scientific Computing
    *   Heterogeneous "big data" and small data pipelines. The language should scale down as well as scale up, i.e. low startup latency for small jobs.
    *   Incorporate features of "workflow languages" and systems in the MapReduce family.
    *   Concise data cleaning, transformation, and summarization.
    *   [Reproducible Research](https://en.wikipedia.org/wiki/Reproducibility#Reproducible_research).
    *   Non-goal: mathematical modeling. That should be left to specialized languages like R, Julia, and Matlab. Communicate with those languages through **coprocesses** (to avoid startup overhead and concurrency.)
*   Interactive Computing
    *   A general purpose REPL (terminal and probably a Jupyter kernel).
*   Document Publishing
    *   [http://oilshell.org/](http://oilshell.org/) and many programming books are built and orchestrated with shell scripts / Makefiles

### Oil Language Design Goals

*   Easy upgrade path from bash, the most popular shell in the world.
    *   To do this, I've written a very compatible bash parser bash-parser, which will allow automatic conversion of bash (osh) to oil. So the language has a different syntax and a superset of bash semantics.
*   Consistent syntax.
    *   POSIX sh and bash have evolved [many quirks](http://www.oilshell.org/blog/2016/10/28.html).
*   Fix sh and bash semantics to be more developer-friendly (in a backward compatible way).
    *   Proper [Arrays](http://www.oilshell.org/blog/2016/11/06.html)
    *   Strict mode for developer productivity (enhanced set -o errexit, nounset, pipefail)
*   Enhance the shell language; treat it as a real programming language.
    *   Fill in obvious gaps, like abspath, etc.
    *   Compound data structures
    *   Example: Completion functions in bash have a bad API involving globals and are difficult to write. It should feel more like writing completion functions in Python or JavaScript.
    *   Selected influences: Python, R, Ruby, Perl 6, Lua (API), ML, C and C++. Power Shell.
*   Reduce language cacophony in shell programming by reimplementing tools closely related to the shell.
    *   Example: combine [shell, awk, and make](http://oilshell.org/blog/2016/11/13.html).
    *   Also combine tools like find (which has its own expression parser and starts processes), and xargs/GNU parallel, which start processes in parallel. GNU parallel is actually mentioned in the bash manual.
*   Richer constructs for concurrency and parallelism.
    *   Folding in `make -j` and `xargs -P` goes a long way.
*   Allow secure programs to be written.
    *   In emitting strings: escaping
    *   In reading strings: error checking should be easy, better control over "read" delimiters, etc.
    *   Fix issues with globs and flags, i.e. untrusted file system and untrusted variables
*   C and C++ bindings
    *   provide access to advanced Linux kernel features - namespaces, cgroups, seccomp, tracing, /proc, etc. (but remain portable to other Unices)
    *   It should be possible to write a busybox in oil.
*   Should be the best language for writing quick command line tools.
    *   In particular, replace the getopt interface in bash with something much better.
*   Expand the range of things that can be done with the "polyglot" model.
    *   Coprocesses
    *   Built-in serialization formats like CSV, JSON, maybe HTML
    *   Maybe some binary formats as libraries
*   No extra "macro processing" on top of the parser. History substitution will be built in, but disabled in batch mode. procs can be used instead of aliases.

[bash-parser](http://www.oilshell.org/blog/2016/11/09.html)

### Language Design Style

*   Imperative on the scale of code, but declarative/functional/concurrent on scale of architecture, not unlike `sh` itself.

### Implementation Goals

*   Proper error messages like Clang/Swift. [Static Parsing](http://www.oilshell.org/blog/2016/10/22.html).
*   Provide end-to-end tracing and profiling tools (e.g. for pipelines that run for hours)
*   Library-based design like LLVM. Example: the same parser is used in batch mode as well as completion mode, which is not true of all shell implementations. The parser can be used for auto-formatting and linting, which is also not true of other implementations.
*   Few dependencies so it can be used in bootstrapping Unix systems and clusters. (e.g. distributed as a C++ file and optional oil source.)
*   Much of oil should be written in oil (which means the VM needs to be fast enough for this).

### Longer Term Goals

*   Expose our toolkit for little languages -- lexing, parsing, AST representation, etc. So that other languages can be built in the same way.
*   Metaprogramming with ASTs as first class data structures.
*   FastCGI Scripts on shared hosting (using strict input validation and hygienic text generation).

## See also

*   [Oil Github](https://github.com/oilshell/oil)
*   [Oil Project Home](http://www.oilshell.org/)
*   [Oil Twitter Feed](https://twitter.com/oilshellblog)
*   [Oil Subreddit](https://www.reddit.com/r/oilshell/)