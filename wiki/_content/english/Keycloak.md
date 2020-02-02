[Keycloak](https://en.wikipedia.org/wiki/Keycloak "wikipedia:Keycloak") is an identity management solution implemented in Java that can be used as an authentication backend for many different applications.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Running](#Running)
*   [3 Creating an admin user](#Creating_an_admin_user)
*   [4 Configuration](#Configuration)
    *   [4.1 H2 configuration](#H2_configuration)
    *   [4.2 PostgreSQL configuration](#PostgreSQL_configuration)
*   [5 External links](#External_links)

## Installation

Install the [keycloak](https://www.archlinux.org/packages/?name=keycloak) package.

## Running

[Start/enable](/index.php/Start/enable "Start/enable") `keycloak.service`. In the default configuration, it will start in standalone mode which is not recommended for production environments but will be used in this article for the sake of simplicity.

## Creating an admin user

The recommended way to create a Keycloak admin user is via the included `add-user-keycloak.sh` utility as Keycloak does not have to be running for that operation.

```
/opt/keycloak/bin/add-user-keycloak.sh -u my-keycloak-user -p my-keycloak-password

```

This command creates a file at `/opt/keycloak/standalone/configuration/keycloak-add-user.json` that contains your user information.

## Configuration

The default standalone configuration can be found at `/etc/keycloak/standalone/configuration/standalone.xml`.

The ports used by the service can found in that file, albeit in a slightly unusual format:

 `/etc/keycloak/standalone/configuration/standalone.xml` 
```
    <socket-binding-group name="standard-sockets" default-interface="public" port-offset="${jboss.socket.binding.port-offset:0}">
        <socket-binding name="ajp" port="${jboss.ajp.port:8009}"/>
        <socket-binding name="http" port="${jboss.http.port:8080}"/>
        <socket-binding name="https" port="${jboss.https.port:8443}"/>   
        <socket-binding name="management-http" interface="management" port="${jboss.management.http.port:9990}"/>
        <socket-binding name="management-https" interface="management" port="${jboss.management.https.port:9993}"/>
        <socket-binding name="txn-recovery-environment" port="4712"/>
        <socket-binding name="txn-status-manager" port="4713"/>
        <outbound-socket-binding name="mail-smtp">
            <remote-destination host="localhost" port="25"/>
        </outbound-socket-binding>
    </socket-binding-group>

```

### H2 configuration

Keycloak's `standalone.xml` file is preconfigured with two [h2](https://www.h2database.com/html/main.html) datasources. One is "ExampleDS", and can be safely removed. The other is "KeycloakDS" and is used to store Keycloak's configuration. (`jboss.home.dir` refers to `/opt/keycloak` in the Keycloak package)

Example configuration parts for the H2 file-based database:

 `/etc/keycloak/standalone/configuration/standalone.xml` 
```
        <subsystem xmlns="urn:jboss:domain:datasources:5.0">
            <datasources>
                <datasource jndi-name="java:jboss/datasources/ExampleDS" pool-name="ExampleDS" enabled="true" use-java-context="true" statistics-enabled="${wildfly.datasources.statistics-enabled:${wildfly.statistics-enabled:false}}">
                    <connection-url>jdbc:h2:mem:test;DB_CLOSE_DELAY=-1;DB_CLOSE_ON_EXIT=FALSE</connection-url>
                    <driver>h2</driver>
                    <security>
                        <user-name>sa</user-name>
                        <password>sa</password>
                    </security>
                </datasource>
                <datasource jndi-name="java:jboss/datasources/KeycloakDS" pool-name="KeycloakDS" enabled="true" use-java-context="true" statistics-enabled="${wildfly.datasources.statistics-enabled:${wildfly.statistics-enabled:false}}">
                    <connection-url>jdbc:h2:${jboss.server.data.dir}/keycloak;AUTO_SERVER=TRUE</connection-url>
                    <driver>h2</driver>
                    <security>
                        <user-name>sa</user-name>
                        <password>sa</password>
                    </security>
                </datasource>
                <drivers>
                    <driver name="h2" module="com.h2database.h2">
                        <xa-datasource-class>org.h2.jdbcx.JdbcDataSource</xa-datasource-class>
                    </driver>
                </drivers>
            </datasources>
        </subsystem>
   ...
            <default-bindings context-service="java:jboss/ee/concurrency/context/default" datasource="java:jboss/datasources/KeycloakDS" managed-executor-service="java:jboss/ee/concurrency/executor/default" managed-scheduled-executor-service="java:jboss/ee/concurrency/scheduler/default" managed-thread-factory="java:jboss/ee/concurrency/factory/default"/>

```

### PostgreSQL configuration

The official Arch Linux Keycloak package already comes with inbuilt PostgreSQL support.

Example configuration parts for PostgreSQL:

 `/etc/keycloak/standalone/configuration/standalone.xml` 
```
        <subsystem xmlns="urn:jboss:domain:datasources:5.0">
            <datasources>
                <datasource jndi-name="java:jboss/datasources/KeycloakDS" pool-name="KeycloakDS" enabled="true" use-java-context="true" statistics-enabled="${wildfly.datasources.statistics-enabled:${wildfly.statistics-enabled:false}}">
                    <connection-url>jdbc:postgresql://localhost:5432/keycloak</connection-url>
                    <driver>postgresql</driver>
                    <security>
                        <user-name>keycloak</user-name>
                        <password>keycloak</password>
                    </security>
                </datasource>
                <drivers>
                    <driver name="postgresql" module="org.postgresql">
                        <xa-datasource-class>org.postgresql.xa.PGXADataSource</xa-datasource-class>
                    </driver>
                </drivers>
            </datasources>
        </subsystem>
   ...
            <default-bindings context-service="java:jboss/ee/concurrency/context/default" datasource="java:jboss/datasources/KeycloakDS" managed-executor-service="java:jboss/ee/concurrency/executor/default" managed-scheduled-executor-service="java:jboss/ee/concurrency/scheduler/default" managed-thread-factory="java:jboss/ee/concurrency/factory/default"/>

```

## External links

*   [Configuring Keycloak with Postgres](https://devopstales.github.io/sso/keycloak2/)
*   [Official Keycloak documentation](https://www.keycloak.org/docs/)