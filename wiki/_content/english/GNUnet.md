[GNUnet](https://gnunet.org/) is a framework for secure peer-to-peer networking that does not use any centralized or otherwise trusted services. Currently, the service implemented on the framework serves to perform censorship-resistant file-sharing.

See also [Wikipedia:GNUnet](https://en.wikipedia.org/wiki/GNUnet "wikipedia:GNUnet").

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Usage](#Usage)
    *   [3.1 Downloading](#Downloading)
    *   [3.2 Uploading](#Uploading)
        *   [3.2.1 To index a file/directory](#To_index_a_file.2Fdirectory)
        *   [3.2.2 To unindex a file/directory](#To_unindex_a_file.2Fdirectory)
        *   [3.2.3 Modifying and removing indexed files](#Modifying_and_removing_indexed_files)

## Installation

GNUnet can be [installed](/index.php/Installed "Installed") with the [gnunet](https://www.archlinux.org/packages/?name=gnunet) package. If you also want to use the graphical interface, install [gnunet-gtk](https://www.archlinux.org/packages/?name=gnunet-gtk).

## Configuration

[Start](/index.php/Start "Start") and possibly [enable](/index.php/Enable "Enable") the `gnunet` service.

To start the peer immediately in a terminal:

```
# gnunet-arm -s

```

See also [How to start and stop a GNUnet peer](https://gnunet.org/how-start-and-stop-gnunet-peer).

## Usage

### Downloading

To use *gnunet-gtk* to download a file, just search for the file in the *Filesystem* tab. When you see the file you want, just download it as you would with any other P2P file-sharing program. Start it with:

```
# gnunet-fs-gtk

```

### Uploading

Uploading files to the gnunet network is more complicated. GNUnet differentiates between *indexing* a file and *inserting* a file. The details can be read at the [framework's website](https://gnunet.org). The following steps explain how to share data with the network, and are a shortened form of the instructions found on [this page](https://gnunet.org/file-sharing).

The following steps may have to be done manually. A module, called *gnunet-fuse*, is being developed to make this process easier for a user. However, as of December 2008, there is little documentation for it and it is not even in [AUR](/index.php/AUR "AUR") yet.

#### To index a file/directory

```
gnunet-insert [-n] [-k keword1] [-k keyword 2] [-m TYPE:VALUE] *filename*

```

It is not required to add keywords, but it is recommended. This is because GNUnet does not allow searching by filename, but by keywords. Libextractor, which is a dependency of gnunet, will extract keywords from the file, but you may wish to enter keywords of your own. The `-m` option is for meta-data. This is data (about the file) that other users of gnunet will see when your files show up during their searches. For further details, see the gnunet.org online documentation. The `-n` option is used to insert a file/directory into the gnunet MySQL/sqlite database, instead of just indexing it.

#### To unindex a file/directory

```
gnunet-unindex

```

Suppose you have forgotten which files you indexed, you can look up the pointers in the directory `/var/lib/gnunet/data/shared`, where `GNUNET_HOME=/var/lib/gnunet` (set by `gnunet-setup -d`).

**Warning:** Do not edit this directory yourself, use gnunet-insert and gnunet-unindex to make changes. This is because gnunet uses a database to store file information, and deleting (or modifying) the contents of the directory will not remove the entries in the gnunet database.

#### Modifying and removing indexed files

*   When you modify a file, the URI of the file changes. Therefore, GNUnet considers this to be a completely different file. Therefore, make sure that the original file is unindexed (using the gnunet-unindex command), modify the file, and then index the new file to make it accessible through the network.
*   If you want to move/remove a file from your system, then you should unindex it first.