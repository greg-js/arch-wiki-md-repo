**Estado de la traducción**
Este artículo es una traducción de [Aurweb RPC interface](/index.php/Aurweb_RPC_interface "Aurweb RPC interface"), revisada por última vez el **2019-11-22**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Aurweb_RPC_interface&diff=0&oldid=589724) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Official repositories web interface](/index.php/Official_repositories_web_interface "Official repositories web interface")

La [interfaz RPC de Aurweb](https://aur.archlinux.org/rpc.php) es una interfaz liviana de [RPC](https://en.wikipedia.org/wiki/es:Llamada_a_procedimiento_remoto "wikipedia:es:Llamada a procedimiento remoto") para [AUR](/index.php/AUR_(Espa%C3%B1ol) "AUR (Español)"). Las consultas se envían como solicitudes [GET](https://en.wikipedia.org/wiki/es:Protocolo_de_transferencia_de_hipertexto#GET "wikipedia:es:Protocolo de transferencia de hipertexto") de [HTTP](https://en.wikipedia.org/wiki/es:Protocolo_de_transferencia_de_hipertexto "wikipedia:es:Protocolo de transferencia de hipertexto") y el servidor responde en formato [JSON](http://www.json.org/).

**Nota:** este artículo describe la versión 5 de la [API](https://en.wikipedia.org/wiki/es:Interfaz_de_programaci%C3%B3n_de_aplicaciones "wikipedia:es:Interfaz de programación de aplicaciones") de la interfaz RPC, actualizada con la versión 4.7.0 de AUR el 7 de julio de 2018.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Utilización de la API](#Utilización_de_la_API)
    *   [1.1 Tipos de consulta](#Tipos_de_consulta)
        *   [1.1.1 search](#search)
        *   [1.1.2 info](#info)
    *   [1.2 Tipos de retorno](#Tipos_de_retorno)
        *   [1.2.1 return data](#return_data)
        *   [1.2.2 error](#error)
        *   [1.2.3 search](#search_2)
        *   [1.2.4 info](#info_2)
    *   [1.3 jsonp](#jsonp)
*   [2 Limitaciones](#Limitaciones)
*   [3 Clientes de referencia](#Clientes_de_referencia)

## Utilización de la API

### Tipos de consulta

Hay dos tipos de consulta:

*   search
*   info

#### search

Las búsquedas de paquetes se pueden realizar emitiendo solicitudes con el formulario:

```
/rpc/?v=5&type=search&by=*field*&arg=*keywords*

```

donde `*keywords*` es el argumento de búsqueda y `*field*` es uno de los siguientes valores:

*   `name` (busca solo por nombre de paquete)
*   `name-desc` (busca por nombre y descripción del paquete)
*   `maintainer` (busca por mantenedor de paquetes)
*   `depends` (busca paquetes cuya «depends» dependen de palabras clave)
*   `makedepends` (busca paquetes cuya «makedepends» dependa de palabras clave)
*   `optdepends` (busca paquetes cuya «optdepends» dependa de palabras clave)
*   `checkdepends` (busca paquetes cuya «checkdepends» dependa de palabras clave)

El parámetro `by` se puede omitir y el valor predeterminado es `name-desc`. Los posibles tipos de retorno son `search` y `error`.

Si se realiza una búsqueda por mantenedor y el argumento de búsqueda se deja vacío, se devuelve una lista de paquetes huérfanos.

Ejemplos:

Buscar por `foobar`:

```
https://aur.archlinux.org/rpc/?v=5&type=search&arg=foobar

```

Buscar por paquetes mantenidos por `john`:

```
https://aur.archlinux.org/rpc/?v=5&type=search&by=maintainer&arg=john

```

Buscar por paquetes que tengan `foobar` como «makedepends»:

```
https://aur.archlinux.org/rpc/?v=5&type=search&by=makedepends&arg=foobar

```

Buscar con callback («devolución de llamada»):

```
https://aur.archlinux.org/rpc/?v=5&type=search&arg=foobar&callback=jsonp1192244621103

```

#### info

La información del paquete se puede realizar emitiendo solicitudes con el formulario:

```
/rpc/?v=5&type=info&arg[]=*pkg1*&arg[]=*pkg2*&…

```

donde `*pkg1*`, `*pkg2*`, … son las coincidencias exactas de los nombres de los paquetes, de los cuales se quieren recuperar los detalles del paquete.

Los posibles tipos de retorno son `multiinfo` y `error`.

Ejemplos:

Información para el paquete único `foobar`:

```
https://aur.archlinux.org/rpc/?v=5&type=info&arg[]=foobar

```

Información para varios paquetes `foobar` y `bar`:

```
https://aur.archlinux.org/rpc/?v=5&type=info&arg[]=foobar&arg[]=bar

```

### Tipos de retorno

La carga para la devolución es de un formato único y dispone actualmente de tres tipos principales. La respuesta siempre devolverá un tipo para que el usuario pueda determinar si el resultado de una operación fue un error o no.

El formato para la carga de devolución es:

```
{"version":5,"type":*ReturnType*,"resultcount":0,"results":*ReturnData*}

```

`*ReturnType*` es una cadena y el valor es uno de los siguientes:

*   `search`
*   `multiinfo`
*   `error`

#### return data

El tipo de `*ReturnData*` es una matriz de elementos de diccionario para `search` y `multiinfo` de `*ReturnType*`, y una matriz vacía para `error` de `*ReturnType*`.

Para `*ReturnType*` `*search*`, `*ReturnData*` puede contener los siguientes campos:

*   `ID`
*   `Name`
*   `PackageBaseID`
*   `PackageBase`
*   `Version`
*   `Description`
*   `URL`
*   `NumVotes`
*   `Popularity`
*   `OutOfDate`
*   `Maintainer`
*   `FirstSubmitted`
*   `LastModified`
*   `URLPath`

Para `*ReturnType*` `*info*` y `*multiinfo*`, `*ReturnData*` también puede contener adicionalmente los siguientes campos:

*   `Depends`
*   `MakeDepends`
*   `OptDepends`
*   `CheckDepends`
*   `Conflicts`
*   `Provides`
*   `Replaces`
*   `Groups`
*   `License`
*   `Keywords`

Los campos que no contienen un paquete se omitirán de la salida.

#### error

El tipo «error» tiene una cadena de respuesta de error como valor de retorno. Se puede devolver una respuesta de error desde un tipo de consulta `search` o `info`.

Ejemplo de `*ReturnType*` `error`:

```
{"version":5,"type":"error","resultcount":0,"results":[],"error":"Incorrect by field specified."}

```

#### search

El tipo «search» es el resultado devuelto por una operación de solicitud de búsqueda.

Ejemplo de `*ReturnType*` `search`:

```
{"version":5,"type":"search","resultcount":2,"results":[{"ID":206807,"Name":"cower-git", ...}]}

```

#### info

El tipo «info» es el resultado devuelto por una operación de solicitud de información.

Ejemplo de `*ReturnType*` `multiinfo`:

```
 {
    "version":5,
    "type":"multiinfo",
    "resultcount":1,
    "results":[{
        "ID":229417,
        "Name":"cower",
        "PackageBaseID":44921,
        "PackageBase":"cower",
        "Version":"14-2",
        "Description":"A simple AUR agent with a pretentious name",
        "URL":"http:\/\/github.com\/falconindy\/cower",
        "NumVotes":590,
        "Popularity":24.595536,
        "OutOfDate":null,
        "Maintainer":"falconindy",
        "FirstSubmitted":1293676237,
        "LastModified":1441804093,
        "URLPath":"\/cgit\/aur.git\/snapshot\/cower.tar.gz",
        "Depends":[
            "curl",
            "openssl",
            "pacman",
            "yajl"
        ],
        "MakeDepends":[
            "perl"
        ],
        "License":[
            "MIT"
        ],
        "Keywords":[]
    }]
 }

```

### jsonp

Si está trabajando con una página de JavaScript y necesita un mecanismo de devolución de llamada («callback») en formato [JSON](https://en.wikipedia.org/wiki/es:JSON "wikipedia:es:JSON"), que puede hacerlo uno mismo. Solo necesitamos proporcionar una variable de «callback» adicional. Esta devolución de llamada generalmente se maneja a través de la biblioteca javascript, he aquí un ejemplo:

Ejemplo de consulta:

```
https://aur.archlinux.org/rpc/?v=5&type=search&arg=foobar&callback=jsonp1192244621103

```

Ejemplo de resultado:

```
/**/jsonp1192244621103({"version":5,"type":"search","resultcount":1,"results":[{"ID":250608,"Name":"foobar2000","PackageBaseID":37068,"PackageBase":"foobar2000","Version":"1.3.9-1","Description":"An advanced freeware audio player (uses Wine).","URL":"http:\/\/www.foobar2000.org\/","NumVotes":39,"Popularity":0.425966,"OutOfDate":null,"Maintainer":"supermario","FirstSubmitted":1273255356,"LastModified":1448326415,"URLPath":"\/cgit\/aur.git\/snapshot\/foobar2000.tar.gz"}]})

```

Esto llamaría automáticamente a la función de JavaScript `jsonp1192244621103` con el parámetro establecido en los resultados de la llamada RPC.

## Limitaciones

*   Las solicitudes GET de HTTP están limitadas a un [URI](https://en.wikipedia.org/wiki/es:Identificador_de_recursos_uniforme "wikipedia:es:Identificador de recursos uniforme") de 8190 bytes de longitud máxima. Sin embargo, la instancia oficial de AUR que se ejecuta en un servidor [nginx](/index.php/Nginx "Nginx") con [HTTP/2](https://en.wikipedia.org/wiki/es:HTTP/2 "wikipedia:es:HTTP/2") utiliza el límite de 4443 bytes de [longitud máxima de URI predeterminada](https://nginx.org/en/docs/http/ngx_http_v2_module.html#http2_max_field_size). Las solicitudes de información con más de 200 paquetes aproximadamente como argumento deberán dividirse.
*   Las consultas de búsqueda deben tener al menos dos caracteres de longitud.
*   Las búsquedas fallarán si contienen 5000 o más resultados.
*   La tasa de API está limitada a un máximo de 4000 solicitudes por IP al día.

## Clientes de referencia

A veces las cosas son más fáciles de entender con ejemplos. Algunas implementaciones de referencia (jQuery, python, ruby) están disponibles en la siguiente URL: [https://github.com/cactus/random/tree/2b72a1723bfc8ae64eed6a3c40cb154accae3974/aurjson_examples](https://github.com/cactus/random/tree/2b72a1723bfc8ae64eed6a3c40cb154accae3974/aurjson_examples)