**Bytewalk** is a firmware extraction tool & binwalk fork

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Smoke Test](#Smoke_Test)
*   [2 Troubleshooting](#Troubleshooting)
*   [3 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [bytewalk](https://aur.archlinux.org/packages/bytewalk/) package.

### Smoke Test

Make sure that Bytewalk has been installed correctly by running the following in a terminal:

```
$> bytewalk

```

This should print a help menu like this:

```
 Usage: bytewalk [OPTIONS] [FILE1] [FILE2] [FILE3] ...
 Signature Scan Options:
   -B, --signature              Scan target file(s) for common file signatures
   -R, --raw=<str>              Scan target file(s) for the specified sequence of bytes
   -A, --opcodes                Scan target file(s) for common executable opcode signatures
   -m, --magic=<file>           Specify a custom magic file to use
   -b, --dumb                   Disable smart signature keywords
   -I, --invalid                Show results marked as invalid
   -x, --exclude=<str>          Exclude results that match <str>
   -y, --include=<str>          Only show results that match <str>
 Extraction Options:
   -e, --extract                Automatically extract known file types
   -D, --dd=<type:ext:cmd>      Extract <type> signatures, give the files an extension of <ext>, and execute <cmd>
   -M, --matryoshka             Recursively scan extracted files
   -d, --depth=<int>            Limit matryoshka recursion depth (default: 8 levels deep)
   -C, --directory=<str>        Extract files/folders to a custom directory (default: current working directory)
   -j, --size=<int>             Limit the size of each extracted file
   -n, --count=<int>            Limit the number of extracted files
   -r, --rm                     Delete carved files after extraction
   -z, --carve                  Carve data from files, but don't execute extraction utilities
   -V, --subdirs                Extract into sub-directories named by the offset
 Entropy Options:
   -E, --entropy                Calculate file entropy
   -F, --fast                   Use faster, but less detailed, entropy analysis
   -J, --save                   Save plot as a PNG
   -Q, --nlegend                Omit the legend from the entropy plot graph
   -N, --nplot                  Do not generate an entropy plot graph
   -H, --high=<float>           Set the rising edge entropy trigger threshold (default: 0.95)
   -L, --low=<float>            Set the falling edge entropy trigger threshold (default: 0.85)
 Binary Diffing Options:
   -W, --hexdump                Perform a hexdump / diff of a file or files
   -G, --green                  Only show lines containing bytes that are the same among all files
   -i, --red                    Only show lines containing bytes that are different among all files
   -U, --blue                   Only show lines containing bytes that are different among some files
   -u, --similar                Only display lines that are the same between all files
   -w, --terse                  Diff all files, but only display a hex dump of the first file
 Raw Compression Options:
   -X, --deflate                Scan for raw deflate compression streams
   -Z, --lzma                   Scan for raw LZMA compression streams
   -P, --partial                Perform a superficial, but faster, scan
   -S, --stop                   Stop after the first result
 General Options:
   -l, --length=<int>           Number of bytes to scan
   -o, --offset=<int>           Start scan at this file offset
   -O, --base=<int>             Add a base address to all printed offsets
   -K, --block=<int>            Set file block size
   -g, --swap=<int>             Reverse every n bytes before scanning
   -f, --log=<file>             Log results to file
   -c, --csv                    Log results to file in CSV format
   -t, --term                   Format output to fit the terminal window
   -q, --quiet                  Suppress output to stdout
   -v, --verbose                Enable verbose output
   -h, --help                   Show help output
   -a, --finclude=<str>         Only scan files whose names match this regex
   -p, --fexclude=<str>         Do not scan files whose names match this regex
   -s, --status=<int>           Enable the status server on the specified port

```

## Troubleshooting

Reproducible bugs/errors may be reported on [Gitlab](https://gitlab.com/bytesweep/bytewalk/issues).

## See also

*   [Bytewalk Gitlab](https://gitlab.com/bytesweep/bytewalk)