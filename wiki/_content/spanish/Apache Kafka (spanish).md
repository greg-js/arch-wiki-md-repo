**Estado de la traducción**
Este artículo es una traducción de [Apache Kafka](/index.php/Apache_Kafka "Apache Kafka"), revisada por última vez el **2019-02-09**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Apache_Kafka&diff=0&oldid=557546) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[Apache Kafka](https://kafka.apache.org) es una plataforma de transmisión distribuida que:

1.  Le permite publicar y suscribirse a transmisiones de registros. En este sentido, es similar a una cola de mensajes o un sistema de mensajería empresarial.
2.  Le permite almacenar transmisiones de registros de forma tolerante a fallos.
3.  Le permite procesar transmisiones de registros a medida que ocurren.

## Instalación

Instale el paquete [kafka](https://aur.archlinux.org/packages/kafka/). Inicie `kafka.service` con systemctl, el cual también debería activar/iniciar `zookeeper@kafka.service` de manera automática.

## Utilización

Para su utilización, véase la [documentación oficial](https://kafka.apache.org/quickstart#quickstart_createtopic)

## Clientes

*   C - [librdkafka-git](https://aur.archlinux.org/packages/librdkafka-git/)
*   Python - [https://github.com/dpkp/kafka-python](https://github.com/dpkp/kafka-python)
*   Php - [php-rdkafka](https://aur.archlinux.org/packages/php-rdkafka/)
*   Perl - [perl6-pkafka](https://aur.archlinux.org/packages/perl6-pkafka/)