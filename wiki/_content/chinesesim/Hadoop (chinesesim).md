Related articles

*   [Apache spark](/index.php/Apache_spark "Apache spark")

[Apache Hadoop](http://hadoop.apache.org) 是一个支持在商业硬件大型集群上运行应用程序框架。Hadoop框架透明地提供应用程序可靠性和数据传输。Hadoop实现了一个名为Map/Reduce计算模式，应用程序被划分成许多小片段，这些小片段可能在集群中的任何节点上被执行或反复执行。此外，它提供了一个分布式文件系统（HDFS）来存储在计算节点上的数据，它使集群有非常高的带宽。MapReduce和Hadoop分布式文件系统使框架能自行处理失效节点。

## Contents

*   [1 安装](#安装)
*   [2 配置](#配置)
*   [3 单节点设置](#单节点设置)
    *   [3.1 独立操作](#独立操作)
    *   [3.2 伪分布式操作](#伪分布式操作)
        *   [3.2.1 设置无需密码的ssh](#设置无需密码的ssh)
        *   [3.2.2 执行](#执行)

## 安装

安装 [hadoop](https://aur.archlinux.org/packages/hadoop/)包。

## 配置

默认情况下, hadoop已经被配置成伪分布模式。在一些不同环境下要修改文件 `/etc/profile.d/hadoop.sh`中的和传统Hadoop不同的变量。

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

你必须在 `/etc/hadoop/hadoop-env.sh`告诉hadoop你的JAVA_HOME因为它并不自己找它自己安装的的地方:

 `/etc/hadoop/hadoop-env.sh`  `export JAVA_HOME=/usr/lib/jvm/java-8-openjdk/` 

用下面命令检查安装:

```
hadoop version

```

如果你得到警告信息"WARNING: HADOOP_SLAVES has been replaced by HADOOP_WORKERS. Using value of HADOOP_SLAVES." 那么用下面的语句替换掉替换掉`/etc/profile.d/hadoop.sh`的 `export HADOOP_SLAVES=/etc/hadoop/slaves`:

```
export HADOOP_WORKERS=/etc/hadoop/workers

```

## 单节点设置

**Note:** 这个部分内容基于 [Hadoop官方文档](http://hadoop.apache.org/docs/stable/)

### 独立操作

默认地, Hadoop被配置为非分布式模式,作为一个单独的Java进程. 这对调试很有帮助.

下面的例子复制了解压缩的conf目录来用作输入然后寻找并展示每个匹配正则表达式的结果。输出被写入给定的输出目录。

```
$ HADOOP_CONF_DIR=/usr/lib/hadoop/orig_etc/hadoop/
$ mkdir input
$ cp /etc/hadoop/*.xml input
$ hadoop jar /usr/lib/hadoop/share/hadoop/mapreduce/hadoop-mapreduce-examples-3.0.0.jar grep input output 'dfs[a-z.]+'
$ cat output/*

```

### 伪分布式操作

Hadoop 能在伪分布式模式下运行在单一节点，这样每个hadoop守护进程运行在不同的Java进程.

默认地，hadoop将会以root用户运行。你可以改变默认用户，在 `/etc/conf.d/hadoop`里的:

```
HADOOP_USERNAME="<your user name>"

```

#### 设置无需密码的ssh

确定你的 [sshd](/index.php/Sshd "Sshd")服务启用了, 或者用`systemctl enable sshd`手动开启. 现在确定你能不用密码连接到localhost:

```
$ ssh localhost

```

如果你不能用ssh无密码连接到localhost, 执行下面的命令:

```
$ ssh-keygen -t rsa -P "" -f ~/.ssh/id_rsa
$ cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
$ chmod 0600 ~/.ssh/authorized_keys

```

确定`/etc/ssh/sshd_config`文件里的下面这行被注释了

 `/etc/ssh/sshd_config`  `#AuthorizedKeysFile .ssh/authorized_keys` 

#### 执行

格式化一个新的分布式文件系统:

```
$ hadoop namenode -format

```

开启hadoop守护进程:

```
# systemctl start hadoop-datanode
# systemctl start hadoop-jobtracker
# systemctl start hadoop-namenode
# systemctl start hadoop-secondarynamenode
# systemctl start hadoop-tasktracker

```

hadoop守护进程的日志输出写在 `${HADOOP_LOG_DIR}`目录(默认在 `/var/log/hadoop`).

为NameNode和JobTracker流量网络接口; 默认它们在:

*   NameNode - [http://localhost:50070/](http://localhost:50070/)
*   JobTracker - [http://localhost:50030/](http://localhost:50030/)

复制输入文件到分布式文件系统:

```
$ hadoop fs -put /etc/hadoop input

```

运行一些提供的例子:

```
$ hadoop jar /usr/lib/hadoop/hadoop-examples-*.jar grep input output 'dfs[a-z.]+'

```

检查输出文件:

复制分布式文件系统的输出文件到本地文件系统并检查它们:

```
$ hadoop fs -get output output
$ cat output/*

```

或者

在分布式文件系统浏览输出文件:

```
$ hadoop fs -cat output/*

```

当你结束后停止以下守护进程:

```
# systemctl stop hadoop-datanode
# systemctl stop hadoop-jobtracker
# systemctl stop hadoop-namenode
# systemctl stop hadoop-secondarynamenode
# systemctl stop hadoop-tasktracker

```