Desde la versón 2.6.16.2-1 del paquete kernel26 oficial de Arch, IPv6 ya no se compila directamente en el kernel, sino como un módulo aparte. Es común que sus características no sean necesarias, a la vez que, si se descarga, se puede obtener cierta mejora de rendimiento (muchos programas tratarán de usar primero las direcciones IPs en formato IPv6, sin percatarse de que tu conexión no es IPv6) y liberar algo de memoria (250K, esto es un gran módulo).

El módulo `ipv6` se carga durante el arranque del sistema. Hay varios programas que cargarán el módulo ipv6 si detectan que está disponible. De hecho, cargan `net-pf-10`, que es un alias del módulo `ipv6`. Simplemente añadiendo las siguientes líneas en el fichero `/etc/modprobe.d/modprobe.conf`, inhabilitarás la carga automática de `ipv6`.

```
# Inhabilitar la carga automática de IPv6
alias net-pf-10 off

```

Si más tarde necesitas cargar el módulo, podrías hacerlo manualmente ejecutando el siguiente comando como root:

```
modprobe ipv6

```