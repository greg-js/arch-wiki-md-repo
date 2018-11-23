Artículos relacionados

*   [Hadoop](/index.php/Hadoop "Hadoop")

**Estado de la traducción**
Este artículo es una traducción de [Apache Spark](/index.php/Apache_Spark "Apache Spark"), revisada por última vez el **2018-11-22**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Apache_Spark&diff=0&oldid=480069) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[Apache Spark](https://spark.apache.org) es un framework de computación en clúster de código abierto desarrollado originalmente en el AMPLab de la UC Berkeley. En contraste con el paradigma MapReduce basado en disco de dos etapas de Hadoop, las primitivas en memoria de Spark ofrecen un rendimiento hasta 100 veces mayor en ciertas aplicaciones. Al permitir que los programas del usuario carguen datos en la memoria de un clúster y lo consulten repetidamente, Spark está bien adaptado a los algoritmos de aprendizaje automático.

## Instalación

Instale el paquete [apache-spark](https://aur.archlinux.org/packages/apache-spark/).

## Configuración

Algunas variables de entorno se configuran en `/etc/profile.d/apache-spark.sh`.

| ENV | Valor | Descripción |
| PATH | `$PATH:/opt/apache-spark/bin` | Spark binaries |

Es posible que deba ajustar la [variable de entorno](/index.php/Environment_variables_(Espa%C3%B1ol) "Environment variables (Español)") `PATH` si su shell inhibe `/etc/profile.d`:

```
export PATH=$PATH:/opt/apache-spark/bin

```

## Habilitar el soporte de R

El paquete [R](/index.php/R "R") de [sparkR](https://spark.apache.org/docs/latest/sparkr.html) se distribuye con el paquete pero no se compila durante la instalación. Para conectarse a Spark desde R, primero debe compilar el paquete ejecutando

```
# $SPARK_HOME/R/install-dev.sh

```

como se describe en `$SPARK_HOME/R/README.md`. También puede desear compilar la documentación del paquete siguiendo las instrucciones en `$SPARK_HOME/R/DOCUMENTATION.md`. Una vez que se haya compilado el paquete sparkR R, puede conectarse utilizando `/usr/bin/sparkR`.