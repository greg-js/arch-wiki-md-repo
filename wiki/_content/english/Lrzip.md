[Long Range ZIP](https://github.com/ckolivas/lrzip) (or Lzma RZIP) is a compression program optimised for large files, consisting mainly of an extended [rzip](https://en.wikipedia.org/wiki/rzip "wikipedia:rzip") step for long-distance redundancy reduction and a normal compressor (LZMA, LZO, gzip, bzip2, or ZPAQ) step. The larger the file and the more memory you have, the better the compression advantage this will provide, especially once the files are larger than 100MB. The advantage can be chosen to be either size (much smaller than bzip2) or speed (much faster than bzip2).

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Compression](#Compression)
    *   [2.2 Decompression](#Decompression)
*   [3 Details](#Details)
*   [4 Benchmarks](#Benchmarks)
*   [5 FAQ](#FAQ)
*   [6 Repository and issue tracker](#Repository_and_issue_tracker)

## Installation

[Install](/index.php/Install "Install") [lrzip](https://www.archlinux.org/packages/?name=lrzip), available in the [official repositories](/index.php/Official_repositories "Official repositories").

## Usage

### Compression

Compression of directories (recursive) requires *lrztar*, which first tars the directory, then compresses the single file just like *tar* does when users compress with *gzip* or *xz* (`tar zcf ...` and `tar Jcz ...`, respectively). Note that the compression algorithms are used after the rzip-like precompressing of the archive, instead of e.g. plain LZMA compression in normal "LZMA compressed archives".

This will produce an [LZMA](https://en.wikipedia.org/wiki/LZMA "wikipedia:LZMA") compressed archive `foo.tar.lrz` from a directory named `foo`:

```
$ lrztar foo

```

This will produce an LZMA compressed archive `bar.lrz` from a file named `bar`:

```
$ lrzip bar

```

For extreme compression, add the `-z` switch which enables [ZPAQ](https://en.wikipedia.org/wiki/ZPAQ "wikipedia:ZPAQ") but takes notably longer than LZMA:

```
$ lrztar -z foo

```

For extremely fast compression and decompression, use the `-l` switch for [LZO](https://en.wikipedia.org/wiki/LZO "wikipedia:LZO"):

```
$ lrzip -l bar

```

### Decompression

To completely extract an archived directory:

```
$ lrzuntar foo.tar.lrz

```

To decompress `bar.lrz` to `bar`:

```
$ lrunzip bar.lrz

```

## Details

Lrzip uses an extended version of [rzip](https://en.wikipedia.org/wiki/rzip "wikipedia:rzip"), which does a first pass long distance redundancy reduction. The lrzip modifications make it scale according to memory size. The data is then either:

1.  Compressed by LZMA (default), which gives excellent compression at approximately twice the speed of bzip2 compression
2.  Compressed by a number of other compressors chosen for different reasons, in order of likelihood of usefulness:
    1.  ZPAQ: Extreme compression up to 20% smaller than LZMA, but ultra slow at compression AND decompression.
    2.  LZO: Extremely fast compression and decompression, which on most machines compresses faster than disk writing making it as fast (or even faster) than simply copying a large file.
    3.  GZIP: Almost as fast as LZO, but with better compression.
    4.  BZIP2: A defacto linux standard of sorts, but is the middle ground between LZMA and gzip and neither here nor there.
3.  Leaving it uncompressed and rzip prepared. This form improves substantially any compression performed on the resulting file in both size and speed (due to the nature of rzip preparation merging similar compressible blocks of data and creating a smaller file). By "improving" it will either speed up the very slow compressors with minor detriment to compression, or greatly increase the compression of simple compression algorithms.

The major disadvantages are:

1.  The main *lrzip* application only works on single files, so it requires the *lrztar* wrapper to fake a complete archiver.
2.  It requires a lot of memory to get the best performance out of (as much memory as the size of the data to compress; but see the sliding mmap below), and is not really usable (for compression) with less than 256MB. Decompression requires less ram and works on smaller ram machines. Sometimes swap may need to be enabled on these lower ram machines for the operating system to be happy.
3.  STDIN/STDOUT works fine on both compression and decompression, but larger files compressed in this manner will end up being less efficiently compressed.

The unique feature of lrzip is that it tries to make the most of the available ram in your system at all times for maximum benefit. It does this by default, choosing the largest sized window possible without running out of memory. It also has a unique "sliding mmap" feature which makes it possible to even use a compression window larger than your ramsize, if the file is that large. It does this (with the `-U` option) by implementing one large mmap buffer as per normal, and a smaller moving buffer to track which part of the file is currently being examined, emulating a much larger single mmapped buffer. Unfortunately, this mode can be many times slower.

## Benchmarks

See the [README.benchmarks](http://ck.kolivas.org/apps/lrzip/README.benchmarks) included in the source/docs.

## FAQ

See the [README](http://ck.kolivas.org/apps/lrzip/README) included with the source package.

## Repository and issue tracker

On [https://github.com/ckolivas/lrzip](https://github.com/ckolivas/lrzip)