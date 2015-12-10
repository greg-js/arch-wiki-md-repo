# Apache Spark

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Hadoop](/index.php/Hadoop "Hadoop")

[Apache Spark](https://spark.apache.org) is an open-source cluster computing framework originally developed in the AMPLab at UC Berkeley. In contrast to Hadoop's two-stage disk-based MapReduce paradigm, Spark's in-memory primitives provide performance up to 100 times faster for certain applications. By allowing user programs to load data into a cluster's memory and query it repeatedly, Spark is well-suited to machine learning algorithms.

## Installation

Install the [apache_spark](https://aur.archlinux.org/packages/apache_spark/)<sup><small>AUR</small></sup> package.

## Configuration

Some environment variables are set in `/etc/profile.d/apache_spark.sh`.

<table class="wikitable">

<tbody>

<tr>

<th>ENV</th>

<th>Value</th>

<th>Description</th>

</tr>

<tr>

<td>PATH</td>

<td>`$PATH:/usr/lib/apache_spark/bin`</td>

<td>Spark binaries</td>

</tr>

</tbody>

</table>

You may need to adjust your `PATH` [environment variable](/index.php/Environment_variable "Environment variable") if your shell inhibits `/etc/profile.d`:

```
export PATH=$PATH:/usr/lib/apache_spark/bin

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Apache_Spark&oldid=408222](https://wiki.archlinux.org/index.php?title=Apache_Spark&oldid=408222)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Distributed computing](/index.php/Category:Distributed_computing "Category:Distributed computing")