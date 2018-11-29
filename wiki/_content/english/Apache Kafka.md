[Apache Kafka](https://kafka.apache.org) is a distributed streaming platform that:

1.  Lets you publish and subscribe to streams of records. In this respect it is similar to a message queue or enterprise messaging system.
2.  Lets you store streams of records in a fault-tolerant way.
3.  Lets you process streams of records as they occur.

## Installation

Install the [kafka](https://aur.archlinux.org/packages/kafka/) package. Start `kafka.service` with systemctl which should also automatically enable/start `zookeeper@kafka.service` as well.

## Usage

For usage see [official documentation](https://kafka.apache.org/quickstart#quickstart_createtopic)

## Clients

*   C - [librdkafka-git](https://aur.archlinux.org/packages/librdkafka-git/)
*   Python - [https://github.com/dpkp/kafka-python](https://github.com/dpkp/kafka-python)
*   Php - [php-rdkafka](https://aur.archlinux.org/packages/php-rdkafka/)
*   Perl - [perl6-pkafka](https://aur.archlinux.org/packages/perl6-pkafka/)