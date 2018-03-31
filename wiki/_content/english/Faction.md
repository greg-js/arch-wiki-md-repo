**Faction** is a C library for test-driven software development.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Example](#Example)
*   [4 Modes](#Modes)
    *   [4.1 Extended Mode Features](#Extended_Mode_Features)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [libfaction](https://aur.archlinux.org/packages/libfaction/) package.

## Usage

The library provides several C macros to make writing tests quicker.

*   FI represents Faction Initialization
*   FT denotes a Faction Test
*   FC represent Faction Close

Using the FT macro, three fields are required.

*   AUTHORS() takes a comma-separated list of double-quotation surrounded author names
*   SPEC() takes a single double-quotation surrounded test specification description
*   A C boolean expression (just like when using C assert macros)

Convention dictates that Faction tests are to be written at the bottom of the source file containing the code that will be tested. Tests are to be surrounded by a FACTION macro guard (see below example) so that they can be enabled at compile time. C compilers such as the GNU C Compiler (GCC) offer a way to enable macros on the command-line (i.e. the `-D` flag)

## Example

```
/* This is the function to be tested */
increment(int input)
{
  return (input + 1);
}

#ifdef FACTION
#include <faction.h>
#include <limits.h>
FI

  FT(
    AUTHORS( "timetoplatypus" ),
    SPEC( "increment() returns 1 when given 0" ),
    increment(0) == 1
  );

  FT(
    AUTHORS( "timetoplatypus" ),
    SPEC( "increment() returns 0 when given the largest integer value" ),
    increment(INT_MAX) == 0;
  );

FC
#endif

```

This can be compiled using `gcc <filename.c> -D FACTION`

## Modes

There are two modes that Faction can compile in: *minimal* mode and *extended* mode.

The above example compiles Faction in minimal mode. A minimal compilation has exactly three library dependencies: stdlib, stdio, and getopt. An extended compilation has additional dependencies, including some functions that are only available through the GNU feature test macro.

So, to compile in extended mode, simply define the GNU feature test macro at the top of the file. For instance, the previous example modified to be compiled in extended mode would look like this:

```
#ifdef FACTION
#define _GNU_SOURCE
#endif
```

```
/* This is the function to be tested */
increment(int input)
{
  return (input + 1);
}

#ifdef FACTION
#include <faction.h>
#include <limits.h>
FI

  FT(
    AUTHORS( "timetoplatypus" ),
    SPEC( "increment() returns 1 when given 0" ),
    increment(0) == 1
  );

  FT(
    AUTHORS( "timetoplatypus" ),
    SPEC( "increment() returns 0 when given the largest integer value" ),
    increment(INT_MAX) == 0;
  );

FC
#endif
```

### Extended Mode Features

In extended mode,

*   the output can be optionally mirrored to a user-specified log file using the `-l` flag at runtime.
*   the results table will dynamically resize to the width of the terminal being used. Otherwise, it defaults to a 78 character width.

## See also

*   [Faction Releases](https://timetoplatypus.com/static/faction/)