[Apache Spark](https://spark.apache.org) is an open-source cluster computing framework originally developed in the AMPLab at UC Berkeley. In contrast to Hadoop's two-stage disk-based MapReduce paradigm, Spark's in-memory primitives provide performance up to 100 times faster for certain applications. By allowing user programs to load data into a cluster's memory and query it repeatedly, Spark is well-suited to machine learning algorithms.

## Installation

Install the [apache-spark](https://aur.archlinux.org/packages/apache-spark/) package.

## Configuration

Some environment variables are set in `/etc/profile.d/apache-spark.sh`.

| ENV | Value | Description |
| PATH | `$PATH:/opt/apache-spark/bin` | Spark binaries |

You may need to adjust your `PATH` [environment variable](/index.php/Environment_variable "Environment variable") if your shell inhibits `/etc/profile.d`:

```
export PATH=$PATH:/opt/apache-spark/bin

```

## Enable R support

The [R](/index.php/R "R") package [sparkR](https://spark.apache.org/docs/latest/sparkr.html) is distributed with the package but not built during installation. To connect to Spark from R you must first build the package by running

```
# $SPARK_HOME/R/install-dev.sh

```

as described in `$SPARK_HOME/R/README.md`. You may also wish to build the package documentation following the instructions in `$SPARK_HOME/R/DOCUMENTATION.md`.

Once the sparkR R package has been built you can connect using `/usr/bin/sparkR`.