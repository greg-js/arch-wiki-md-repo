**Состояние перевода:** На этой странице представлен перевод статьи [Haveged](/index.php/Haveged "Haveged"). Дата последней синхронизации: 2017-08-17\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Haveged&diff=0&oldid=485546).

The [haveged project](http://www.issihosts.com/haveged/) is an attempt to provide an easy-to-use, unpredictable [random number generator](/index.php/Random_number_generator "Random number generator") based upon an adaptation of the HAVEGE algorithm. Haveged was created to remedy low-entropy conditions in the Linux random device that can occur under some workloads, especially on headless servers.

**Warning:** The quality of the generated entropy is not guaranteed and sometimes contested (see [LCE: Do not play dice with random numbers](https://lwn.net/Articles/525459/) and [Is it appropriate to use haveged as a source of entropy on virtual machines?](http://security.stackexchange.com/questions/34523/is-it-appropriate-to-use-haveged-as-a-source-of-entropy-on-virtual-machines)). Use it at your own risk or use it with a hardware based random number generator with the [rng-tools](https://www.archlinux.org/packages/?name=rng-tools) (see [#Alternative](#Alternative) section)

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Просмотр энтропии](#.D0.9F.D1.80.D0.BE.D1.81.D0.BC.D0.BE.D1.82.D1.80_.D1.8D.D0.BD.D1.82.D1.80.D0.BE.D0.BF.D0.B8.D0.B8)
*   [3 Альтернативы](#.D0.90.D0.BB.D1.8C.D1.82.D0.B5.D1.80.D0.BD.D0.B0.D1.82.D0.B8.D0.B2.D1.8B)
*   [4 Виртуальные машины](#.D0.92.D0.B8.D1.80.D1.82.D1.83.D0.B0.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D0.BC.D0.B0.D1.88.D0.B8.D0.BD.D1.8B)
*   [5 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [haveged](https://www.archlinux.org/packages/?name=haveged).

[Запустите](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Запустите") и [включите](/index.php/%D0%92%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Включите") сервис `haveged.service`.

## Просмотр энтропии

Если вы не уверены, нужен ли haveged, запустите:

```
# cat /proc/sys/kernel/random/entropy_avail

```

Эта команда покажет количество собранной на сервере энтропии. Если её мало (<1000), то следует установить haveged. Иначе криптографические приложения не будут работать до тех пор, пока не будет достаточно энтропии. К примеру, может быть понижена скорость соединения в случае, если сервер используется в качестве [программной точки доступа](/index.php/Software_access_point_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Software access point (Русский)").

Вы можете запустить эту команду до и после установки Haveged, чтобы убедиться в возросшей энтропии.

## Альтернативы

Unless you have a specific reason to not trust any hardware random number generator on your system, you should try to use them with the [rng-tools](/index.php/Rng-tools "Rng-tools") first and if it turns out not to be enough (or if you do not have a hardware random number generator available), then use Haveged.

## Виртуальные машины

As discussed at [Is it appropriate to use haveged as a source of entropy on virtual machines?](http://security.stackexchange.com/questions/34523/is-it-appropriate-to-use-haveged-as-a-source-of-entropy-on-virtual-machines), it can be contested whether haveged provides quality entropy within a virtual environment. Haveged relies on the rdtsc instruction, which may be virtualized within a virtual machine resulting in lower quantity entropy. On some hypervisors, it is possible to disable the virtualization of rdtsc, which would in theory allow haveged to provide higher quality entropy.

To disable the virtualization of the rdtsc instruction in VMware ESXi, add the setting `monitor_control.virtual_rdtsc = "FALSE"` to the virtual machine’s .vmx configuration file. VMware recommends the setting for use when performing measurements that require a precise source of real time in the virtual machine. [[1]](http://www.vmware.com/files/pdf/Timekeeping-In-VirtualMachines.pdf)

## Смотрите также

*   [http://www.issihosts.com/haveged](http://www.issihosts.com/haveged)
*   [http://www.digitalocean.com/community/tutorials/how-to-setup-additional-entropy-for-cloud-servers-using-haveged](http://www.digitalocean.com/community/tutorials/how-to-setup-additional-entropy-for-cloud-servers-using-haveged)