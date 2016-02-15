## Contents

*   [1 Introducción a Modalias](#Introducci.C3.B3n_a_Modalias)
    *   [1.1 ¿Qué es ese 'modalias' del que habla?](#.C2.BFQu.C3.A9_es_ese_.27modalias.27_del_que_habla.3F)
    *   [1.2 ¿Qué es un archivo modalias?](#.C2.BFQu.C3.A9_es_un_archivo_modalias.3F)
    *   [1.3 ¿Cómo se usa esta información?](#.C2.BFC.C3.B3mo_se_usa_esta_informaci.C3.B3n.3F)
    *   [1.4 ¿De dónde viene este archivo modules.alias?](#.C2.BFDe_d.C3.B3nde_viene_este_archivo_modules.alias.3F)
    *   [1.5 ¿Cómo funciona hwdetect?](#.C2.BFC.C3.B3mo_funciona_hwdetect.3F)
    *   [1.6 ¿Cómo funciona udev?](#.C2.BFC.C3.B3mo_funciona_udev.3F)
    *   [1.7 Vea también](#Vea_tambi.C3.A9n)

# Introducción a Modalias

Este documento servirá como introducción acerca de cómo el núcleo Linux y sus módulos detectan y reconocen el hardware, y de cómo se traduce esto a un archivo virtual de sysfs llamado 'modalias'

## ¿Qué es ese 'modalias' del que habla?

Modalias es un pequeño truco por parte de sysfs para exportar información acerca del hardware a un archivo llamado 'modalias'. Este archivo contiene simplemente la información que presenta el hardware normal con un determinado formato. Echemos un vistazo antes de continuar a este ejemplo:

```
$ cat /sys/devices/pci0000:00/0000:00:1f.1/modalias
     pci:v00008086d000024DBsv0000103Csd0000006Abc01sc01i8A

```

No se preocupe, todo se aclarará pronto.

## ¿Qué es un archivo modalias?

Como se describió antes, un archivo modalias simplemente expone la información que un determinado elemento de hardware le comunica al núcleo. Este archivo especifica una estructura para mostrar dicha información. Volvamos al ejemplo anterior:

```
$ cat /sys/devices/pci0000:00/0000:00:1f.1/modalias
  pci:v00008086d000024DBsv0000103Csd0000006Abc01sc01i8A

```

¿Qué diablos es esto? ¿Qué significa? Analicémoslo por partes. Primero, el nombre del archivo.

```
/sys/devices/pci0000:00/0000:00:1f.1/modalias

```

*   **pci0000:00** es la id para el primer bus PCI. En la mayoría de los casos será el único bus PCI que tenga, pero es posible que se pueda extender a **pci0000:01** o **pci0000:02** - los datos exactos no son importantes, ya que es una apuesta bastante segura lo de que sólo tenga un bus PCI (_PISTA:_ ejecute ls /sys/devices/pci* para comprobarlo)
*   **0000:00:1f.1** es el índice del dispositivo dado en el bus PCI. Específicamente, se trata del bus 0000:00 y tiene un índice **1f.1**
*   Todo esto es muy poco importante, a menos que quiera saber de donde vienen todos esos números. Por completar, si analiza la salida de _lspci_ verá la misma información:

```
$ lspci
  00:1f.1 IDE interface: Intel Corp.: Unknown device 24db (rev 02)

```

Ahora, echemos una mirada al contenido del archivo modalias para el dispositivo 00:1f.1:

```
pci:v00008086d000024DBsv0000103Csd0000006Abc01sc01i8A

```

Bien, ¡podemos ver pci! Recocemos eso, pero qué es todo ese galimatías del final? Ese galimatías son en realidad datos estructurados. Reconocerá un esquema repetitivo letra/número. Troceemos los datos para que sean más fáciles de leer:

```
v  00008086
d  000024DB
sv 0000103C
sd 0000006A
bc 01
sc 01
i  8A

```

Cada uno de estos identificadores, y sus correspondientes números hexadecimales representan parte de la información que un dispositivo dado expone. Para empezar, **v** es la _id del fabricante_ y **d** es la _id del dispositivo_ - estos son números muy estandarizados, y son esos mismos números los que utilizan **hwd** y otras herramientas similares para consultar un dispositivo. Incluso puede encontrar sitios web para hacer consultas sobre hardware específico basadas en las id del fabricante y del dispositivo, por ejemplo [http://www.pcidatabase.com/](http://www.pcidatabase.com/)

También se pueden ver estos números aquí:

```
$ lspci -n
  00:1f.1 Class 0101: 8086:24db (rev 02)

```

¿Ve cómo 8086:24db coincide con los _v_ y _d_ anteriores?

Para más exactitud, **sv** y **sd** son las versiones de "subsistema" de tanto el fabricante como del dispositivo. La mayor parte de las veces estos son ignorados. Se utilizan principalmente por los desarrolladores de hardware para distinguir pequeñas diferencias en el funcionamiento interno que no suponen cambios en el dispositivo entendido como un todo.

**bc** (clase base) y **sc** (sub clase) se utilizan para crear la "Class" listada por lspci, y ordenados "bcsc". Se trata de la clase de dispositivo, que es bastante genérica. En este caso, la "clase" es consultada en la salida normal de lspci. Podemos ver que "Class 0101" se corresponde con "Interfaz IDE" (lspci también consulta los id del fabricante y del dispositivo - 8086 se corresponde con "Intel Corp." y 24DB con 'Dispositivo desconocido ("Unknown Device").

**i** es el "Interfaz de programación", y solamente tienen sentido para un reducido número de clases de dispositivos.

## ¿Cómo se usa esta información?

Bien, ahora sabemos qué es toda esta información. Un puñado de números intrigantes que expone cada dispositivo. Todo correcto. ¿Pero qué importancia tiene esto cuando hablamos de módulos?

Una cosa que la gente tiende a dejar de lado, es todo el trabajo que hace **depmod**. Cuando ejecuta depmod, éste construye una serie de archivos de "mapeado" en /lib/modules/`uname -r` que le dicen a modprobe cómo manejar ciertas cosas que tiene que hacer. En este caso podemos ignorar casi todas ellas. La importante es **modules.alias**. Este archivo contiene alias, o nombres secundarios para los módulos. Como muestra, veamos los alias de por ejemplo, snd_intel8x0m:

```
$ grep snd_intel8x0m /lib/modules/`uname -r`/modules.alias
  alias pci:v00008086d00002416sv*sd*bc*sc*i* snd_intel8x0m
  alias pci:v00008086d00002426sv*sd*bc*sc*i* snd_intel8x0m
  alias pci:v00008086d00002446sv*sd*bc*sc*i* snd_intel8x0m
  alias pci:v00008086d00002486sv*sd*bc*sc*i* snd_intel8x0m
  alias pci:v00008086d000024C6sv*sd*bc*sc*i* snd_intel8x0m
  alias pci:v00008086d000024D6sv*sd*bc*sc*i* snd_intel8x0m
  alias pci:v00008086d0000266Dsv*sd*bc*sc*i* snd_intel8x0m
  alias pci:v00008086d000027DDsv*sd*bc*sc*i* snd_intel8x0m
  alias pci:v00008086d00007196sv*sd*bc*sc*i* snd_intel8x0m
  alias pci:v00001022d00007446sv*sd*bc*sc*i* snd_intel8x0m
  alias pci:v00001039d00007013sv*sd*bc*sc*i* snd_intel8x0m
  alias pci:v000010DEd000001C1sv*sd*bc*sc*i* snd_intel8x0m
  alias pci:v000010DEd00000069sv*sd*bc*sc*i* snd_intel8x0m
  alias pci:v000010DEd00000089sv*sd*bc*sc*i* snd_intel8x0m
  alias pci:v000010DEd000000D9sv*sd*bc*sc*i* snd_intel8x0m

```

¡Hey, un momento! ¡Sabemos qué es eso! ¡Es la información sobre las id del fabricante/dispositivo de antes!

Sí, así es. Es un formato bastante sencillo "alias <algo> <modulo real>". De hecho, puede crear alias para todo lo que quiera. Se puede añadir "alias boogabooga snd_intel8x0m" y hacer después "modprobe boogabooga" con seguridad.

El "*" indica que coincidirá con cualquier cosa, de forma muy parecida a la expansión de nombres de archivo (_ls somedir/*_). Como se dijo antes, la mayor parte de los alias ignoran sv, sd, bc, sc, e i usando la coincidencia con "*".

## ¿De dónde viene este archivo modules.alias?

Vale, ahora puede estar pensando "Bien, hwd consulta las cosas basándose en una tabla de dispositivos, ¿qué hace diferente a esto?"

La diferencia estriba en que esta tabla de consulta no es estática. No se mantiene a mano. De hecho, se construye dinámicamente cuando ejecuta depmod. "De dónde viene esta información?", preguntará? Pues desde los **propios módulos**. Si lo piensa, cada módulo específico debería saber cuál es el hardware que conoce, ya que ha sido programado específicamente para dicho hardware. Esto es, los desarrolladores del módulo _nvidia_ saben que su módulo sólo funciona para las tarjetas gráficas ("clase") de Nvidia ("fabricante"). De hecho, exporta en realidad esta información. Dice "Hey, yo puedo trabajar con esto:".

```
$ modinfo nvidia
  filename:       /lib/modules/2.6.14-ARCH/kernel/drivers/video/nvidia.ko
  license:        NVIDIA
  alias:          char-major-195-*
  vermagic:       2.6.14-ARCH SMP preempt 686 gcc-4.1
  depends:        agpgart
  alias:          pci:v000010DEd*sv*sd*bc03sc00i00*

```

Como puede ver por los alias listados, busca específicamente por el fabricante "10DE" (Nvidia) y bc/sc 0300 (que lo más probable es que sea 'graphics cards'). De hecho, si consulta el modinfo de **snd_intel8x0m**:

```
$ modinfo snd_intel8x0m
  filename:       /lib/modules/2.6.14-ARCH/kernel/sound/pci/snd-intel8x0m.ko
  author:         Jaroslav Kysela <perex@suse.cz>
  description:    Intel 82801AA,82901AB,i810,i820,i830,i840,i845,MX440; SiS 7013; NVidia MCP/2/2S/3 modems
  license:        GPL
  vermagic:       2.6.14-ARCH SMP preempt 686 gcc-4.1
  depends:        snd-ac97-codec,snd-pcm,snd-page-alloc,snd
  alias:          pci:v00008086d00002416sv*sd*bc*sc*i*
  alias:          pci:v00008086d00002426sv*sd*bc*sc*i*
  alias:          pci:v00008086d00002446sv*sd*bc*sc*i*
  alias:          pci:v00008086d00002486sv*sd*bc*sc*i*
  alias:          pci:v00008086d000024C6sv*sd*bc*sc*i*
  alias:          pci:v00008086d000024D6sv*sd*bc*sc*i*
  alias:          pci:v00008086d0000266Dsv*sd*bc*sc*i*
  alias:          pci:v00008086d000027DDsv*sd*bc*sc*i*
  alias:          pci:v00008086d00007196sv*sd*bc*sc*i*
  alias:          pci:v00001022d00007446sv*sd*bc*sc*i*
  alias:          pci:v00001039d00007013sv*sd*bc*sc*i*
  alias:          pci:v000010DEd000001C1sv*sd*bc*sc*i*
  alias:          pci:v000010DEd00000069sv*sd*bc*sc*i*
  alias:          pci:v000010DEd00000089sv*sd*bc*sc*i*
  alias:          pci:v000010DEd000000D9sv*sd*bc*sc*i*

```

Muestra los alias encontrados anteriormente mediante grep en el archivo de alias. Estos alias exportados por cada módulo, son recogidos por depmod y mezclados dinámicamente en el archivo modules.alias. No hay cambios manuales en una tabla de consulta, si no que se construye al vuelo. Cada módulo sabe con exactitud con qué puede trabajar, y en consecuencia depmod puede utilizar esa información para ayudar en la carga de módulos.

## ¿Cómo funciona hwdetect?

hwdetect es la herramienta específica de Arch que carga módulos en base a estos modalias. Todo lo que hacer es volcar estos modalias en el sistema, y ejecutar "modprobe --show-depends <alias>" para cada uno de ellos. Esto construye una lista con todos los módulos con los que puede trabajar su hardware. Es así de simple. Por supuesto, hay correcciones hechas para ciertas cositas que no son detectadas correctamente.

En esencia, se hace lo siguiente:

```
modprobe -a $(find /sys/devices -name modalias -exec cat {} +)

```

Por supuesto, esto no es *exacto*, ya que hwdetect carga también dispositivos pnp y módulos de disco, que no son exportados mediante modalias. No obstante, la configuración de modalias hace que todo esto sea sencillo y directo.

## ¿Cómo funciona udev?

Ahora, puede estar usted pensando, "Eso tiene sentido, encuentras simplemente todos los modalias del sistema y los cargas, pero ¿cómo funciona esto cuando insertas un nuevo dispositivo? ¿Tengo que recorrer todo el sistema de nuevo?"

No. udev está estrechamente ligado a sysfs (el sistema de ficheros que expone los modalias en primer lugar). De hecho, cargar módulos basándose en los modalias cuando se inserta un nuevo dispositivo (o cuando udev se inicia por primera vez en el arranque), es extremadamente sencillo:

```
DRIVER!="?*", ENV{MODALIAS}=="?*", RUN{builtin}="kmod load $env{MODALIAS}"

```

Sí, eso es todo. Es una sola línea. Esta sencilla línea, que forma parte de las reglas udev por defecto que reemplazan a hotplug. Sorprendente, ¿no es verdad?

## Vea también

Este artículo muestra otras plantillas modalias, por ejemplo para usb, dmi y subtipos acpy (en Inglés)

*   [Modalias strings - a practical way to map "stuff" to hardware](http://people.skolelinux.org/pere/blog/Modalias_strings___a_practical_way_to_map__stuff__to_hardware.html) por Petter Reinholdtsen