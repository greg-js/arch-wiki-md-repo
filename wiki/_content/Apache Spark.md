# Apache Spark

Related articles

*   [Hadoop](/index.php/Hadoop "Hadoop")

[Apache Spark](https://spark.apache.org) is an open-source cluster computing framework originally developed in the AMPLab at UC Berkeley. In contrast to Hadoop's two-stage disk-based MapReduce paradigm, Spark's in-memory primitives provide performance up to 100 times faster for certain applications. By allowing user programs to load data into a cluster's memory and query it repeatedly, Spark is well-suited to machine learning algorithms.

## Installation

Install the [apache_spark](https://aur.archlinux.org/packages/apache_spark/)<sup><small>AUR</small></sup> package.

## Configuration

Some environment variables are set in `/etc/profile.d/apache_spark.sh`.

| ENV | Value | Description |
| PATH | `$PATH:/usr/lib/apache_spark/bin` | Spark binaries |

You may need to adjust your `PATH` [environment variable](/index.php/Environment_variable "Environment variable") if your shell inhibits `/etc/profile.d`:

```
export PATH=$PATH:/usr/lib/apache_spark/bin

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Apache_Spark&oldid=408222](https://wiki.archlinux.org/index.php?title=Apache_Spark&oldid=408222)"