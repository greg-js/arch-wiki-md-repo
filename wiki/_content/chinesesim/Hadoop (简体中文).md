**翻译状态：** 本文是英文页面 [Hadoop](/index.php/Hadoop "Hadoop") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-03-10，点击[这里](https://wiki.archlinux.org/index.php?title=Hadoop&diff=0&oldid=364609)可以查看翻译后英文页面的改动。

[Apache Hadoop](http://hadoop.apache.org) 是一个支持在商业硬件大型集群上运行应用程序框架。Hadoop框架透明地提供应用程序可靠性和数据传输。Hadoop实现了一个名为Map/Reduce计算模式，应用程序被划分成许多小片段，这些小片段可能在集群中的任何节点上被执行或反复执行。此外，它提供了一个分布式文件系统（HDFS）来存储在计算节点上的数据，它使集群有非常高的带宽。MapReduce和Hadoop分布式文件系统使框架能自行处理失效节点。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
*   [3 Single Node Setup](#Single_Node_Setup)
    *   [3.1 Standalone Operation](#Standalone_Operation)
    *   [3.2 Pseudo-Distributed Operation](#Pseudo-Distributed_Operation)
        *   [3.2.1 Set up passphraseless ssh](#Set_up_passphraseless_ssh)
        *   [3.2.2 Execution](#Execution)

## 安装

安装用户源[Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository")中的 [hadoop](https://aur.archlinux.org/packages/hadoop/)包。

## 配置

默认情况下, hadoop已经被配置成伪分布模式。在一些不同环境下要修改文件 `/etc/profile.d/hadoop.sh`中的变量。

| 环境变量 | 至 | 描述 | 权限 |
| HADOOP_CONF_DIR | `/etc/hadoop` | `存放配置文件` | Read |
| HADOOP_LOG_DIR | `/tmp/hadoop/log` | `存放日志文件` | Read and Write |
| HADOOP_SLAVES | `/etc/hadoop/slaves` | `命名远程从属主机` | Read |
| HADOOP_PID_DIR | `/tmp/hadoop/run` | `存放pid文件` | Read and Write |

你需要正确设置下列文件。

```
/etc/hosts
/etc/hostname 
/etc/locale.conf

```

`JAVA_HOME` 由[jdk7-openjdk](https://www.archlinux.org/packages/?name=jdk7-openjdk)自动设置 `/etc/profile.d/jre.sh`，查看 `JAVA_HOME`:

```
$ echo $JAVA_HOME

```

如果没有输出，请尝试重新登录。

## Single Node Setup

**Note:** This section is based on the [Hadoop Official Documentation](http://hadoop.apache.org/docs/stable/)

### Standalone Operation

By default, Hadoop is configured to run in a non-distributed mode, as a single Java process. This is useful for debugging.

The following example copies the unpacked conf directory to use as input and then finds and displays every match of the given regular expression. Output is written to the given output directory.

```
$ export HADOOP_CONF_DIR=/usr/lib/hadoop/orig_conf
$ mkdir input
$ cp /etc/hadoop/*.xml input
$ hadoop jar /usr/lib/hadoop/hadoop-examples-*.jar grep input output 'dfs[a-z.]+'
$ cat output/*

```

For the current 2.5.x release of hadoop included in the AUR:

```
$ HADOOP_CONF_DIR=/usr/lib/hadoop/orig_etc/hadoop/
$ mkdir input
$ cp /etc/hadoop/hadoop/*.xml input
$ hadoop jar /usr/lib/hadoop/share/hadoop/mapreduce/hadoop-mapreduce-examples-2.5.0.jar grep input output 'dfs[a-z.]+'
$ cat output/*

```

### Pseudo-Distributed Operation

Hadoop can also be run on a single-node in a pseudo-distributed mode where each Hadoop daemon runs in a separate Java process.

By default, Hadoop will run as the user root. You can change the user in `/etc/conf.d/hadoop`:

```
HADOOP_USERNAME="<your user name>"

```

#### Set up passphraseless ssh

Make sure you have [sshd](/index.php/Sshd "Sshd") enabled, or start it with `systemctl enable sshd`. Now check that you can connect to localhost without a passphrase:

```
$ ssh localhost

```

If you cannot ssh to localhost without a passphrase, execute the following commands:

```
$ ssh-keygen -t rsa -P "" -f ~/.ssh/id_rsa
$ cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys2

```

Also make sure this line is commented in `/etc/ssh/sshd_config`

 `/etc/ssh/sshd_config`  `#AuthorizedKeysFile .ssh/authorized_keys` 

#### Execution

Format a new distributed-filesystem:

```
$ hadoop namenode -format

```

Start the hadoop daemons:

```
# systemctl start hadoop-datanode
# systemctl start hadoop-jobtracker
# systemctl start hadoop-namenode
# systemctl start hadoop-secondarynamenode
# systemctl start hadoop-tasktracker

```

The hadoop daemon log output is written to the `${HADOOP_LOG_DIR}` directory (defaults to `/var/log/hadoop`).

Browse the web interface for the NameNode and the JobTracker; by default they are available at:

*   NameNode - [http://localhost:50070/](http://localhost:50070/)
*   JobTracker - [http://localhost:50030/](http://localhost:50030/)

Copy the input files into the distributed filesystem:

```
$ hadoop fs -put /etc/hadoop input

```

Run some of the examples provided:

```
$ hadoop jar /usr/lib/hadoop/hadoop-examples-*.jar grep input output 'dfs[a-z.]+'

```

Examine the output files:

Copy the output files from the distributed filesystem to the local filesytem and examine them:

```
$ hadoop fs -get output output
$ cat output/*

```

or

View the output files on the distributed filesystem:

```
$ hadoop fs -cat output/*

```

When you're done, stop the daemons with:

```
# systemctl stop hadoop-datanode
# systemctl stop hadoop-jobtracker
# systemctl stop hadoop-namenode
# systemctl stop hadoop-secondarynamenode
# systemctl stop hadoop-tasktracker

```