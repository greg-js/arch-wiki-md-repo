# Clojure

[Clojure](http://clojure.org/) is a dynamic programming language that targets the Java Virtual Machine (and the CLR, and JavaScript). It is designed to be a general-purpose language, combining the approachability and interactive development of a scripting language with an efficient and robust infrastructure for multithreaded programming. Clojure is a compiled language - it compiles directly to JVM bytecode, yet remains completely dynamic. Every feature supported by Clojure is supported at runtime. Clojure provides easy access to the Java frameworks, with optional type hints and type inference, to ensure that calls to Java can avoid reflection.

Clojure is a dialect of Lisp, and shares with Lisp the code-as-data philosophy and a powerful macro system. Clojure is predominantly a functional programming language, and features a rich set of immutable, persistent data structures. When mutable state is needed, Clojure offers a software transactional memory system and reactive Agent system that ensure clean, correct, multithreaded designs.

## Installation

From the [Official repositories](/index.php/Official_repositories "Official repositories"): [clojure](https://www.archlinux.org/packages/?name=clojure), or from the [AUR](/index.php/AUR "AUR"): [clojure-git](https://aur.archlinux.org/packages/clojure-git/)<sup><small>AUR</small></sup>.

## REPL

To run the REPL, install [leiningen](http://leiningen.org/) from [leiningen](https://aur.archlinux.org/packages/leiningen/)<sup><small>AUR</small></sup> [AUR](/index.php/AUR "AUR") package. Then in a terminal type

```
lein repl

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Clojure&oldid=388105](https://wiki.archlinux.org/index.php?title=Clojure&oldid=388105)"