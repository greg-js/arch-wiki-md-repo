From [Wikipedia](https://en.wikipedia.org/wiki/Scala_(programming_language)):

	*Scala is an object-functional programming and scripting language for general software applications. Scala has full support for functional programming (including currying, pattern matching, algebraic data types, lazy evaluation, tail recursion, immutability, etc.) and a very strong static type system. This allows programs written in Scala to be very concise and thus smaller in size than most general purpose programming languages. Many of Scala's design decisions were inspired by criticism over the shortcomings of Java.*

## Installation

[Install](/index.php/Install "Install") the [scala](https://www.archlinux.org/packages/?name=scala) package available in the [official repositories](/index.php/Official_repositories "Official repositories"). Additionally you can install the packages [scala-docs](https://www.archlinux.org/packages/?name=scala-docs) and/or [scala-sources](https://www.archlinux.org/packages/?name=scala-sources) for further reference.

Since Scala runs on the [JVM](https://en.wikipedia.org/wiki/JVM) (Java Virtual Machine), you'll need a fully functional [Java Runtime Environment](/index.php/Java#Installation "Java") (JRE) in order to execute or compile your programs.

## Usage and IDEs

Just as in other programming languages like [Python](/index.php/Python "Python"), you can interact with an interpreter

```
$ scala

Welcome to Scala version 2.*.* (OpenJDK Server VM, Java 1.*.*).
Type in expressions to have them evaluated.
Type :help for more information.

scala>

```

as well as simply compile and run your programs from the command line.

```
$ scalac HelloWorld.scala
$ scala HelloWorld

```

Many different [IDEs](/index.php/IDE#Integrated_development_environments "IDE") such as [Eclipse](/index.php/Eclipse "Eclipse") or [Netbeans](/index.php/Netbeans "Netbeans") offer support for Scala. The [eclipse-scala-ide](https://aur.archlinux.org/packages/eclipse-scala-ide/) package for example is available in the [AUR](/index.php/AUR "AUR"). But you can also download an IDE that is optimized for Scala and also based on Eclipse directly from [the official Scala Website](https://scala-lang.org).

## See also

*   [Scala Lang](http://scala-lang.org) - official website
*   [Scala Tutorial](http://tutorials.jenkov.com/scala/index.html) - a series of small Scala tutorials
*   [Learn X=Scala in Y minutes](http://learnxinyminutes.com/docs/scala/)