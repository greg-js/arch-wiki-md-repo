**Estado de la traducción:** este artículo es una versión traducida de [RethinkDB](/index.php/RethinkDB "RethinkDB"). Fecha de la última traducción/revisión: **2018-08-11**. Puedes ayudar a actualizar la traducción, si adviertes que la versión inglesa ha cambiado: [ver cambios](https://wiki.archlinux.org/index.php?title=RethinkDB&diff=0&oldid=533285).

RethinkDB es una base de datos orientada a documentos similar a [MongoDB](/index.php/MongoDB "MongoDB"), pero tiene como objetivo superar la escalabilidad y la limitación práctica de esta última. [[1]](http://www.rethinkdb.com/docs/comparisons/mongodb/) [[2]](http://www.rethinkdb.com/blog/mongodb-biased-comparison/) RethinkDB está diseñado para almacenar documentos JSON y escalar a múltiples máquinas con muy poco esfuerzo. Tiene un lenguaje de consulta agradable que admite consultas como la unión de tablas *(joins)* y agrupar por *(group by)*. Es fácil de configurar y aprender. Para más información, consulte la [página oficial](https://www.rethinkdb.com/).

## Instalación

Instale [rethinkdb](https://www.archlinux.org/packages/?name=rethinkdb) desde el repositorio oficial.

Cree y establezca permisos de usuario para la carpeta RethinkDB:

```
# mkdir /var/lib/rethinkdb/default
# chown -R rethinkdb:rethinkdb /var/lib/rethinkdb/

```

Ahora puede iniciar `rethinkdb` desde la línea de comandos:

```
# rethinkdb

```

O en su lugar, puede ejecutarlo como un servicio `systemd`. Habilite la instancia `rethinkdb` predeterminada como

```
# systemctl enable rethinkdb@default

```

e iníciela:

```
# systemctl start rethinkdb@default

```

RethinkDB's admin UI is now available on port [8080](http://localhost:8080).

## Configuración

RethinkDB tiene soporte para varias instancias, lo que significa que puede ejecutar varias instancias de bases de datos independientes en la misma máquina. El servicio `systemd` también admite la configuración de varias instancias.

Para crear una nueva instancia de RethinkDB, cree su archivo de configuración:

```
# cd /etc/rethinkdb
# cp default.conf.sample instances.d/<NOMBRE>.conf

```

Donde <NOMBRE> representa la configuración que usará más adelante. Cambie las opciones de configuración en el nuevo archivo de configuración. Entonces inicie el servicio:

```
# systemctl enable rethinkdb@<NOMBRE>
# systemctl start rethinkdb@<NOMBRE>

```

La instancia 'default' *(predeterminada)* se crea en el momento de la instalación para su comodidad. Sus datos se almacenan en `/var/lib/rethinkdb/default`.