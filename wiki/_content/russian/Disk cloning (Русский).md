Клонирование диска, представляет собой процесс создания образа раздела или всего жёсткого диска. Это может быть полезно как для копирования диска с других компьютеров, так и для резервного копирования/восстановления.

## Contents

*   [1 Программное Обеспечение Для Клонирования](#.D0.9F.D1.80.D0.BE.D0.B3.D1.80.D0.B0.D0.BC.D0.BC.D0.BD.D0.BE.D0.B5_.D0.9E.D0.B1.D0.B5.D1.81.D0.BF.D0.B5.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.94.D0.BB.D1.8F_.D0.9A.D0.BB.D0.BE.D0.BD.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F)
    *   [1.1 Клонирование Диска в Arch](#.D0.9A.D0.BB.D0.BE.D0.BD.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.94.D0.B8.D1.81.D0.BA.D0.B0_.D0.B2_Arch)
    *   [1.2 Клонирование Диска без Arch](#.D0.9A.D0.BB.D0.BE.D0.BD.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.94.D0.B8.D1.81.D0.BA.D0.B0_.D0.B1.D0.B5.D0.B7_Arch)
*   [2 Внешние Ссылки](#.D0.92.D0.BD.D0.B5.D1.88.D0.BD.D0.B8.D0.B5_.D0.A1.D1.81.D1.8B.D0.BB.D0.BA.D0.B8)

## Программное Обеспечение Для Клонирования

### Клонирование Диска в Arch

Основанная на ncurses, программа [PartImage](https://en.wikipedia.org/wiki/Partimage "wikipedia:Partimage"), находится в репозитории community. Интерфейс программы иниутивно не понятен, но она работает. На данный момент, программ клонирования дисков, основанных на GTK/QT в Linux нет. Другой вариант использовать dd, это маленькая CLI утилита для создания образа/файла. В википедии есть список различных версий dd, специально созданный для этих целей [wikipedia:Dd_(Unix)#Recovery-oriented_variants_of_dd](https://en.wikipedia.org/wiki/Dd_(Unix)#Recovery-oriented_variants_of_dd "wikipedia:Dd (Unix)"). [dd_rescue](http://www.garloff.de/kurt/linux/ddrescue/) эффективно работает с повреждёнными дисками, копируя ошибки в свободные сектора и после снова повторяет попытку копирования ошибочного сектора.

### Клонирование Диска без Arch

Если Вы хотите сделать резервную копию или размножить установленный Arch, Вам скорее всего лучше загрузится в чём-нибудь другом и клонировать партиции там. Некоторые рекомендации:

*   [PartedMagic](http://partedmagic.com/wiki/PartedMagic.php) имеет очень приятый Live CD/USB с PartImage и другими средствами восстановления.
*   [Mindi](http://www.mondorescue.org/) является Linux дистрибутивом, созданным, специально для резервного копирования и клонирования дисков. Он, поставляется со своей собственной программой клонирования - Mondo Rescue.
*   [Acronis True Image](https://en.wikipedia.org/wiki/Acronis_True_Image "wikipedia:Acronis True Image") является коммерческой утилитой для клонирования дисков под Windows. Она позволяет создать Live CD (в Windows), так что вам не нужна установленная рабочая копия Windows на машине, чтобы её использовать.

## Внешние Ссылки

*   [Wikipedia entry on Disk cloning](https://en.wikipedia.org/wiki/List_of_disk_cloning_software "wikipedia:List of disk cloning software")
*   [Arch Linux forum thread](https://bbs.archlinux.org/viewtopic.php?id=4329)