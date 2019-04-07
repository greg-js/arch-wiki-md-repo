Ссылки по теме

*   [Rng-tools](/index.php/Rng-tools "Rng-tools")

**Состояние перевода:** На этой странице представлен перевод статьи [Haveged](/index.php/Haveged "Haveged"). Дата последней синхронизации: 6 декабря 2018\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Haveged&diff=0&oldid=558163).

[haveged](http://www.issihosts.com/haveged/) — проект, разрабатывающий простой в использовании и непредсказуемый [генератор случайных чисел](/index.php/Random_number_generator "Random number generator"), основанный на алгоритме HAVEGE. Haveged был создан для предотвращения низкого уровня энтропии в устройстве Linux для генерации случайных чисел, что может случиться под некоторыми рабочими нагрузками, особенно на headless-серверах.

**Важно:** Качество сгенерированной энтропии не гарантируется и иногда оспаривается (см. [LCE: Do not play dice with random numbers](https://lwn.net/Articles/525459/) и [Is it appropriate to use haveged as a source of entropy on virtual machines?](http://security.stackexchange.com/questions/34523/is-it-appropriate-to-use-haveged-as-a-source-of-entropy-on-virtual-machines)). Используйте haveged на свой риск или используйте его в паре с аппаратным генератором случайных чисел с помощью [rng-tools](https://www.archlinux.org/packages/?name=rng-tools) (см. секцию [#Альтернативы](#Альтернативы))

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Установка](#Установка)
*   [2 Просмотр доступной энтропии](#Просмотр_доступной_энтропии)
*   [3 Альтернативы](#Альтернативы)
*   [4 Виртуальные машины](#Виртуальные_машины)
*   [5 Смотрите также](#Смотрите_также)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [haveged](https://www.archlinux.org/packages/?name=haveged).

[Запустите](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Запустите") и [включите](/index.php/%D0%92%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Включите") службу `haveged.service`.

## Просмотр доступной энтропии

Если вы не уверены, нужен ли вам haveged, запустите следующую команду:

```
# cat /proc/sys/kernel/random/entropy_avail

```

Эта команда покажет количество собранной на сервере энтропии. Если её довольно мало (<1000), то, вероятно, стоит установить haveged. Иначе криптографические приложения не будут работать до тех пор, пока не появится достаточно энтропии. К примеру, может снизится скорость беспроводного соединения в случае, если сервер используется в качестве [программной точки доступа](/index.php/Software_access_point_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Software access point (Русский)").

Воспользуйтесь этой командой снова, чтобы проверить, насколько haveged увеличил пул энтропии после установки.

## Альтернативы

Если у вас нет определённой причины не доверять каким-либо аппаратным генераторам случайных чисел в вашей системе, вы должны сначала попробовать использовать их с [rng-tools](/index.php/Rng-tools "Rng-tools") и если этого окажется недостаточно (или у вас нет доступного аппаратного генератора случайных чисел), тогда используйте haveged.

## Виртуальные машины

Как обсуждалось в [Is it appropriate to use haveged as a source of entropy on virtual machines?](http://security.stackexchange.com/questions/34523/is-it-appropriate-to-use-haveged-as-a-source-of-entropy-on-virtual-machines), качество энтропии, генерируемой haveged, может быть спорным в виртуальной среде. Haveged полагается на инструкцию rdtsc, которая может быть виртуализирована, из-за чего понизится уровень энтропии. В некоторых гипервизорах есть возможность отключить виртуализацию rdtsc, что, в теории, позволит haveged более качественно генерировать энтропию.

Чтобы отключить виртуализацию инструкции rdtsc в VMware ESXi, добавьте параметр `monitor_control.virtual_rdtsc = "FALSE"` в конфигурационный файл .vmx виртуальной машины. VMware рекомендует использовать данный параметр в случаях измерений, для которых требуется надёжный источник реального времени в виртуальной машине. [[1]](http://www.vmware.com/files/pdf/Timekeeping-In-VirtualMachines.pdf)

## Смотрите также

*   [Официальный веб-сайт](http://www.issihosts.com/haveged)
*   [Статья DigitalOcean по настройке haveged](https://www.digitalocean.com/community/tutorials/how-to-setup-additional-entropy-for-cloud-servers-using-haveged)