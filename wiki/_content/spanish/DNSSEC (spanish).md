**Estado de la traducción**
Este artículo es una traducción de [DNSSEC](/index.php/DNSSEC "DNSSEC"), revisada por última vez el **2018-09-14**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=DNSSEC&diff=0&oldid=537948) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Unbound#DNSSEC validation](/index.php/Unbound#DNSSEC_validation "Unbound")

Del [artículo de Wikipedia sobre DNSSEC](https://en.wikipedia.org/wiki/Domain_Name_System_Security_Extensions "wikipedia:Domain Name System Security Extensions"):

	Las [extensiones de seguridad para el sistema de nombres de dominio](https://en.wikipedia.org/wiki/es:Domain_Name_System_Security_Extensions "wikipedia:es:Domain Name System Security Extensions") (siglas en inglés «*DNSSEC*») son un conjunto de especificaciones del [Grupo de Trabajo de Ingeniería de Internet](https://en.wikipedia.org/wiki/es:Grupo_de_Trabajo_de_Ingenier%C3%ADa_de_Internet "wikipedia:es:Grupo de Trabajo de Ingeniería de Internet") (siglas en inglés, «*IETF*») para proteger cierto tipo de información proporcionada por el sistema de nombres de dominio (siglas en inglés «*DNS*») que se utiliza en el Protocolo de Internet (siglas en inglés «*IP*»). Se trata de un conjunto de extensiones para los DNS que proporcionan a los clientes DNS (o *resolvers*) la autenticación del origen de los datos del DNS, la denegación autenticada de las existencia e integridad de los datos, pero no su disponibilidad ni confidencialidad.

## Contents

*   [1 Validación básica de DNSSEC](#Validaci.C3.B3n_b.C3.A1sica_de_DNSSEC)
    *   [1.1 Instalación](#Instalaci.C3.B3n)
    *   [1.2 Consulta con validación de DNSSEC](#Consulta_con_validaci.C3.B3n_de_DNSSEC)
    *   [1.3 Comprobación](#Comprobaci.C3.B3n)
*   [2 Instalar un servidor recursivo de validación con reconocimiento DNSSEC](#Instalar_un_servidor_recursivo_de_validaci.C3.B3n_con_reconocimiento_DNSSEC)
*   [3 Activar DNSSEC en un software específico](#Activar_DNSSEC_en_un_software_espec.C3.ADfico)
*   [4 Hardware con DNSSEC](#Hardware_con_DNSSEC)
*   [5 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Validación básica de DNSSEC

**Nota:** Se requiere una configuración adicional para que las búsquedas de DNS se realicen a través de DNSSEC por defecto. Consulte [#Instalar un servidor recursivo de validación con reconocimiento DNSSEC](#Instalar_un_servidor_recursivo_de_validaci.C3.B3n_con_reconocimiento_DNSSEC) y [#Activar DNSSEC en un software específico](#Activar_DNSSEC_en_un_software_espec.C3.ADfico).

### Instalación

La herramienta *drill* se puede utilizar para la validación básica de DNSSEC. Para utilizar *drill*, [instale](/index.php/Install "Install") el paquete [ldns](https://www.archlinux.org/packages/?name=ldns).

### Consulta con validación de DNSSEC

Luego, para consultar la validación con DNSSEC, utilice el parámetro `-D`:

```
$ drill -D *ejemplo.com*

```

### Comprobación

Como prueba, utilice los siguientes dominios, añadiendo el parámetro `-T`, que rastreará desde los servidores base hasta el dominio que se está resolviendo:

```
$ drill -DT sigfail.verteiltesysteme.net

```

El resultado debe terminar con las siguientes líneas, lo que indica que la firma DNSSEC es falsa:

```
[B] sigfail.verteiltesysteme.net.       60      IN      A       134.91.78.139
;; Error: Bogus DNSSEC signature
;;[S] self sig OK; [B] bogus; [T] trusted

```

Ahora, para probar una firma confiable:

```
$ drill -DT sigok.verteiltesysteme.net

```

El resultado debe terminar con las siguientes líneas, lo que indica que la firma es de confianza:

```
[T] sigok.verteiltesysteme.net. 60      IN      A       134.91.78.139
;;[S] self sig OK; [B] bogus; [T] trusted

```

## Instalar un servidor recursivo de validación con reconocimiento DNSSEC

Para utilizar DNSSEC en todo el sistema, puede usar un sistema de resolución recursivo de validación que sea compatible con DNSSEC, de modo que todas las búsquedas de DNS pasen por dicho sistema de resolución recursivo. Consulte [Domain name resolution#Resolvers](/index.php/Domain_name_resolution#Resolvers "Domain name resolution") para conocer las opciones disponibles. Tenga en cuenta que cada una requiere opciones específicas para activar su función de validación DNSSEC.

Si intenta visitar un sitio con una dirección IP falsa (*spoofed*), el sistema de resolución de validación le impedirá recibir los datos del DNS no válidos y su navegador (u otra aplicación) recibirá el aviso de que no existe dicho servidor. Dado que todas las búsquedas de DNS pasarán por el sistema de resolución de validación, no necesitará un software que tenga compatibilidad con DNSSEC incorporada al usar esta opción.

## Activar DNSSEC en un software específico

Si elige no [#Instalar un servidor recursivo de validación con reconocimiento DNSSEC](#Instalar_un_servidor_recursivo_de_validaci.C3.B3n_con_reconocimiento_DNSSEC), necesitará utilizar un software que tenga incorporado soporte de DNSSEC para aprovechar sus funciones. A menudo, esto significa que deberá parchear el software usted mismo. Puede encontrar una lista de varias aplicaciones parcheadas [aquí](https://www.dnssec-tools.org/wiki/index.php?title=DNSSEC_Applications). Además, algunos navegadores web tienen extensiones o complementos que se pueden instalar para implementar DNSSEC sin parchear el programa.

## Hardware con DNSSEC

Puede verificar si el enrutador, módem, punto de acceso, etc. admite DNSSEC (muchos recursos diferentes) utilizando [dnssec-tester](http://www.dnssec-tester.cz/) (aplicación basada en Python y GTK +) para saber si es compatible con DNSSEC. Al tiempo que utiliza esta herramienta, también es posible cargar datos recopilados en un servidor, para que otros usuarios y fabricantes puedan estar informados sobre la compatibilidad de sus dispositivos y, eventualmente, arreglar el firmware (probablemente se les inste a hacerlo). Antes de ejecutar dnssec-tester, asegúrese de que no tenga ningún otro servidor de nombres en `/etc/resolv.conf`. También puede encontrar los resultados de las pruebas realizadas en el sitio web [dnssec-tester](http://www.dnssec-tester.cz/).

## Véase también

*   [DNSSEC Resolver Test](http://dnssec.vs.uni-due.de/) — prueba simple para ver si tiene DNSSEC implementado en su equipo.
*   [DNSSEC-Tools](https://www.dnssec-tools.org/)
*   [DNSSEC Visualizer](http://dnsviz.net) — herramienta para visualizar el estado de una zona DNS.
*   [RedHat: Securing DNS Traffic with DNSSEC](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Security_Guide/sec-Securing_DNS_Traffic_with_DNSSEC.html) — artículo completo sobre la implementación de DNSSEC con *unbound*. Tenga en cuenta que algunas herramientas son específicas de RedHat y no se encuentran en Arch Linux.
*   [Wikipedia:Domain Name System Security Extensions](https://en.wikipedia.org/wiki/Domain_Name_System_Security_Extensions "wikipedia:Domain Name System Security Extensions")