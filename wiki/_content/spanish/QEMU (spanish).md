QEMU es un Emulador y virtualizador genérico y de código abierto.

Cuando es utilizado como emulador de hardware, QEMU puede correr Sistemas Operativos y programas hechos para una máquina (ejem. una placa ARM), en una máquina diferente (ej. tu propia PC), mediante la traducción dinámica se consigue muy buen rendimiento.

Cuando es utilizado como un virtualizador, QEMU alcanza un funcionamiento cercano al nativo, al ejecutar el código de guest directamente en el CPU. QEMU soporta la virtualización utilizando el hipervisor Xen o el módulo KVM del kernel Linux. Al usar KVM, QEMU puede virtualizar las plataformas x86, PowerPC y S390.

## Instalando QEMU

Dependiendo de tus necesidades, puedes elegir entre instalar los paquetes [qemu](https://www.archlinux.org/packages/?name=qemu) o [qemu-kvm](https://www.archlinux.org/packages/?name=qemu-kvm), ambos en el repositorio [extra]. [qemu](https://www.archlinux.org/packages/?name=qemu) incluye soporte para emular un amplio rango de arquitecturas, mientras que [qemu-kvm](https://www.archlinux.org/packages/?name=qemu-kvm) sólo admite la virtualización de la arquitectura del sistema principal utilizando [KVM](/index.php/KVM "KVM"). Es altamente recomendable utilizar KVM siempre que sea posible.