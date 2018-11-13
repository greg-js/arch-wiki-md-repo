**Estado de la traducción**
Este artículo es una traducción de [Poclbm](/index.php/Poclbm "Poclbm"), revisada por última vez el **2018-11-08**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Poclbm&diff=0&oldid=552088) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[Poclbm](https://github.com/m0mchil/poclbm) (Python OpenCL Bitcoin miner) es un script de Python que mina Bitcoins usando un dispositivo compatible con OpenCL.

## Contents

*   [1 Introducción](#Introducción)
*   [2 Instalación](#Instalación)
*   [3 Ejecutar el minero](#Ejecutar_el_minero)
*   [4 Ejecutándolo como servicio de systemd](#Ejecutándolo_como_servicio_de_systemd)

## Introducción

Minar Bitcoins es un proceso que utiliza el hardware de su ordenador, es decir, su GPU/CPU para generar "bloques" que se utilizan para verificar las transacciones en la red de Bitcoin. Actualmente un bloque generado le dará 50 BTC. Sin embargo, se reducirá a 25 BTC para finales de noviembre de 2012.

A medida que se generan más bloques, la dificultad aumenta, y a día de hoy (a partir de noviembre de 2012) el tiempo estimado para generar un bloque en un ordenador gaming promedio es de más de 2 años. Por lo tanto, no merece la pena intentar generar un bloque dado el nivel de consumo de electricidad. Pero tenga en cuenta que es algo aleatorio y, aún así (a pesar de la dificultad y el resto), en ocasiones puede tener suerte y generar un bloque con su ordenador gaming estándar. Sin embargo, es muy poco probable y no vale la pena el riesgo que supone esperar tantos meses. Probablemente termine deteniéndolo y pagando una enorme factura de electricidad sin haber generado nada. Pero existe una solución que se denomina **Pool Mining**.

Un pool es una red de ordenadores que minan en conjunto para generar un bloque, y la recompensa total se divide entre todas las personas que contribuyeron para generar el bloque, de modo que al usar un grupo obtendrá ingresos más pequeños pero regulares y con el hardware apropiado (ver más abajo) puede llegar a ser un negocio rentable.

Cuando se realiza la minería, la CPU no es ideal e incluso una tarjeta gráfica de gama baja superará a una CPU de gama alta, por lo que solo se usan GPUs para la minería, aunque, con la configuración correcta, la máquina utilizada para minar puede ser usada para otra cosa (por ejemplo un servidor web), y si solo está minando, entonces es plausible que quiera usar un CPU básico de un solo núcleo y una placa base de baja calidad. La RAM no se usa, por lo que 2 GB de RAM es más que suficiente.

**Nota:** Las tarjetas NVIDIA no son idóneas para la minería y desperdiciarán más dinero (en electricidad) que el que generarán, incluso aunque se use un pool, a si que a menos que lo haga para experimentar/divertirse, o si desea usar su ordenador como radiador (utilizo el mío en mi habitación y produce más calor que mi calentador eléctrico habitual) no vale la pena.

**Nota:** Las tarjetas ATI/AMD son la mejor opción para esto, tienen un menor precio y consumen menos electricidad mientras que tienen un rendimiento extremo (para minería) en comparación con las tarjetas NVIDIA (una única tarjeta ATI es más poderosa que mi 3x NVIDIA GTX580), así que si está haciendo esto con ánimo de lucro, necesitará tarjetas ATI.

Además, hay un fallo en algunos controladores (tanto ATI como NVIDIA) que hace que el minero use el 100% de la CPU en 2 núcleos (incluso si se mina con la GPU). No estoy seguro de qué causa esto, pero parece que también afecta a Windows por lo que tendrá que probarlo usted mismo.

## Instalación

Instale [poclbm-git](https://aur.archlinux.org/packages/poclbm-git/) desde [AUR](/index.php/AUR_(Espa%C3%B1ol) "AUR (Español)").

## Ejecutar el minero

Utilice el siguiente comando para iniciar el minero en todos los dispositivos OpenCL. Si recibe el siguiente error, verifique su configuración y asegúrese de que todos los paquetes y controladores necesarios están presentes:

**Sugerencia:** Asegúrese de tener su nombre de usuario y contraseña de pool disponibles. Puede obtenerlo registrándose en [https://mining.bitcoin.cz](https://mining.bitcoin.cz)

```
$ poclbm *nombre de usuario:contraseña@servidor:puerto*

```

El minero habrá comenzado y mostrará una tasa de hash (x MH/s). Para salir use el `Ctrl + C`. Si tan solo desea ejecutar el minero manualmente, eso es todo lo que necesita hacer.

## Ejecutándolo como servicio de systemd

Cree el archivo de servicio:

 `/etc/systemd/system/poclbm.service` 
```
[Unit]
Description=Python OpenCL Bitcoin miner
After=network.target

[Service]
ExecStart=/usr/bin/poclbm --verbose *<argumentos específicos del usuario>*

[Install]
WantedBy=multi-user.target
```

Los argumentos específicos del usuario deben adaptarse según se describe en [#Ejecutar el minero](#Ejecutar_el_minero). Luego [inicie](/index.php/Start_(Espa%C3%B1ol) "Start (Español)") el servicio usando *systemctl*.