[VirtualBox](https://www.virtualbox.org) - это [гипервизор](https://en.wikipedia.org/wiki/ru:%D0%93%D0%B8%D0%BF%D0%B5%D1%80%D0%B2%D0%B8%D0%B7%D0%BE%D1%80 интерфейс, а также можно не управлять ими или управлять с помощью [SDL](https://en.wikipedia.org/wiki/ru:Simple_DirectMedia_Layer "wikipedia:ru:Simple DirectMedia Layer") утилит командной строки.

Чтобы интегрировать в гостевую систему функции хост системы, такие как общие папки и общий буфер обмена, видео ускорение и режим бесшовной интеграции окон, для некоторых гостевых операционных систем предоставляются *дополнения гостевой ОС*.

## Contents

*   [1 Пошаговая установка на хост-компьютер под управлением Arch Linux](#.D0.9F.D0.BE.D1.88.D0.B0.D0.B3.D0.BE.D0.B2.D0.B0.D1.8F_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BD.D0.B0_.D1.85.D0.BE.D1.81.D1.82-.D0.BA.D0.BE.D0.BC.D0.BF.D1.8C.D1.8E.D1.82.D0.B5.D1.80_.D0.BF.D0.BE.D0.B4_.D1.83.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5.D0.BC_Arch_Linux)
    *   [1.1 Установка базовых пакетов](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.B1.D0.B0.D0.B7.D0.BE.D0.B2.D1.8B.D1.85_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2)
    *   [1.2 Установка модулей ядра VirtualBox](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BC.D0.BE.D0.B4.D1.83.D0.BB.D0.B5.D0.B9_.D1.8F.D0.B4.D1.80.D0.B0_VirtualBox)
        *   [1.2.1 Использование различных версий ядра Linux на хост-машине](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.80.D0.B0.D0.B7.D0.BB.D0.B8.D1.87.D0.BD.D1.8B.D1.85_.D0.B2.D0.B5.D1.80.D1.81.D0.B8.D0.B9_.D1.8F.D0.B4.D1.80.D0.B0_Linux_.D0.BD.D0.B0_.D1.85.D0.BE.D1.81.D1.82-.D0.BC.D0.B0.D1.88.D0.B8.D0.BD.D0.B5)
        *   [1.2.2 Обновление ядра Linux на хост-машине](#.D0.9E.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D1.8F.D0.B4.D1.80.D0.B0_Linux_.D0.BD.D0.B0_.D1.85.D0.BE.D1.81.D1.82-.D0.BC.D0.B0.D1.88.D0.B8.D0.BD.D0.B5)
        *   [1.2.3 Стороннее ядро на хост-машине](#.D0.A1.D1.82.D0.BE.D1.80.D0.BE.D0.BD.D0.BD.D0.B5.D0.B5_.D1.8F.D0.B4.D1.80.D0.BE_.D0.BD.D0.B0_.D1.85.D0.BE.D1.81.D1.82-.D0.BC.D0.B0.D1.88.D0.B8.D0.BD.D0.B5)
    *   [1.3 Загрузка модулей ядра VirtualBox](#.D0.97.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B0_.D0.BC.D0.BE.D0.B4.D1.83.D0.BB.D0.B5.D0.B9_.D1.8F.D0.B4.D1.80.D0.B0_VirtualBox)
    *   [1.4 Дополнительные модули VirtualBox](#.D0.94.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D0.BC.D0.BE.D0.B4.D1.83.D0.BB.D0.B8_VirtualBox)
    *   [1.5 Добавление пользователей в группу vboxusers](#.D0.94.D0.BE.D0.B1.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D0.B5.D0.B9_.D0.B2_.D0.B3.D1.80.D1.83.D0.BF.D0.BF.D1.83_vboxusers)
    *   [1.6 Образ диска с гостевыми дополнениями](#.D0.9E.D0.B1.D1.80.D0.B0.D0.B7_.D0.B4.D0.B8.D1.81.D0.BA.D0.B0_.D1.81_.D0.B3.D0.BE.D1.81.D1.82.D0.B5.D0.B2.D1.8B.D0.BC.D0.B8_.D0.B4.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B5.D0.BD.D0.B8.D1.8F.D0.BC.D0.B8)
    *   [1.7 Пакет дополнений](#.D0.9F.D0.B0.D0.BA.D0.B5.D1.82_.D0.B4.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B5.D0.BD.D0.B8.D0.B9)
    *   [1.8 Правильное использование в фронт-энде](#.D0.9F.D1.80.D0.B0.D0.B2.D0.B8.D0.BB.D1.8C.D0.BD.D0.BE.D0.B5_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.B2_.D1.84.D1.80.D0.BE.D0.BD.D1.82-.D1.8D.D0.BD.D0.B4.D0.B5)
*   [2 Пошаговая установка Arch Linux как гостевой ОС](#.D0.9F.D0.BE.D1.88.D0.B0.D0.B3.D0.BE.D0.B2.D0.B0.D1.8F_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_Arch_Linux_.D0.BA.D0.B0.D0.BA_.D0.B3.D0.BE.D1.81.D1.82.D0.B5.D0.B2.D0.BE.D0.B9_.D0.9E.D0.A1)
    *   [2.1 Установка Arch Linux в виртуальную машину](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_Arch_Linux_.D0.B2_.D0.B2.D0.B8.D1.80.D1.82.D1.83.D0.B0.D0.BB.D1.8C.D0.BD.D1.83.D1.8E_.D0.BC.D0.B0.D1.88.D0.B8.D0.BD.D1.83)
        *   [2.1.1 Установка в режиме EFI](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.B2_.D1.80.D0.B5.D0.B6.D0.B8.D0.BC.D0.B5_EFI)
    *   [2.2 Установка гостевых дополнений](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.B3.D0.BE.D1.81.D1.82.D0.B5.D0.B2.D1.8B.D1.85_.D0.B4.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B5.D0.BD.D0.B8.D0.B9)
    *   [2.3 Установка гостевых модулей ядра VirtualBox](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.B3.D0.BE.D1.81.D1.82.D0.B5.D0.B2.D1.8B.D1.85_.D0.BC.D0.BE.D0.B4.D1.83.D0.BB.D0.B5.D0.B9_.D1.8F.D0.B4.D1.80.D0.B0_VirtualBox)
        *   [2.3.1 Запуск гостевой ОС с официальным ядром](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.B3.D0.BE.D1.81.D1.82.D0.B5.D0.B2.D0.BE.D0.B9_.D0.9E.D0.A1_.D1.81_.D0.BE.D1.84.D0.B8.D1.86.D0.B8.D0.B0.D0.BB.D1.8C.D0.BD.D1.8B.D0.BC_.D1.8F.D0.B4.D1.80.D0.BE.D0.BC)
        *   [2.3.2 Запуск гостевой ОС со сторонним ядром](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.B3.D0.BE.D1.81.D1.82.D0.B5.D0.B2.D0.BE.D0.B9_.D0.9E.D0.A1_.D1.81.D0.BE_.D1.81.D1.82.D0.BE.D1.80.D0.BE.D0.BD.D0.BD.D0.B8.D0.BC_.D1.8F.D0.B4.D1.80.D0.BE.D0.BC)
    *   [2.4 Загрузка модулей ядра VirtualBox](#.D0.97.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B0_.D0.BC.D0.BE.D0.B4.D1.83.D0.BB.D0.B5.D0.B9_.D1.8F.D0.B4.D1.80.D0.B0_VirtualBox_2)
    *   [2.5 Запуск гостевых сервисов VirtualBox](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.B3.D0.BE.D1.81.D1.82.D0.B5.D0.B2.D1.8B.D1.85_.D1.81.D0.B5.D1.80.D0.B2.D0.B8.D1.81.D0.BE.D0.B2_VirtualBox)
    *   [2.6 Расшаривание директорий](#.D0.A0.D0.B0.D1.81.D1.88.D0.B0.D1.80.D0.B8.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.B4.D0.B8.D1.80.D0.B5.D0.BA.D1.82.D0.BE.D1.80.D0.B8.D0.B9)
        *   [2.6.1 Ручное монтирование](#.D0.A0.D1.83.D1.87.D0.BD.D0.BE.D0.B5_.D0.BC.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
        *   [2.6.2 Автомонтирование](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
        *   [2.6.3 Монтирование при загрузке](#.D0.9C.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.B8_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B5)
*   [3 Импорт/экспорт виртуальных машин VirtualBox в/из других гипервизоров](#.D0.98.D0.BC.D0.BF.D0.BE.D1.80.D1.82.2F.D1.8D.D0.BA.D1.81.D0.BF.D0.BE.D1.80.D1.82_.D0.B2.D0.B8.D1.80.D1.82.D1.83.D0.B0.D0.BB.D1.8C.D0.BD.D1.8B.D1.85_.D0.BC.D0.B0.D1.88.D0.B8.D0.BD_VirtualBox_.D0.B2.2F.D0.B8.D0.B7_.D0.B4.D1.80.D1.83.D0.B3.D0.B8.D1.85_.D0.B3.D0.B8.D0.BF.D0.B5.D1.80.D0.B2.D0.B8.D0.B7.D0.BE.D1.80.D0.BE.D0.B2)
    *   [3.1 Удаление дополнений гостевой ОС](#.D0.A3.D0.B4.D0.B0.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B4.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B5.D0.BD.D0.B8.D0.B9_.D0.B3.D0.BE.D1.81.D1.82.D0.B5.D0.B2.D0.BE.D0.B9_.D0.9E.D0.A1)
    *   [3.2 Использование правильного формата виртуального диска](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.B0.D0.B2.D0.B8.D0.BB.D1.8C.D0.BD.D0.BE.D0.B3.D0.BE_.D1.84.D0.BE.D1.80.D0.BC.D0.B0.D1.82.D0.B0_.D0.B2.D0.B8.D1.80.D1.82.D1.83.D0.B0.D0.BB.D1.8C.D0.BD.D0.BE.D0.B3.D0.BE_.D0.B4.D0.B8.D1.81.D0.BA.D0.B0)
        *   [3.2.1 Автоматические инструменты](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B5_.D0.B8.D0.BD.D1.81.D1.82.D1.80.D1.83.D0.BC.D0.B5.D0.BD.D1.82.D1.8B)
        *   [3.2.2 Ручное преобразование](#.D0.A0.D1.83.D1.87.D0.BD.D0.BE.D0.B5_.D0.BF.D1.80.D0.B5.D0.BE.D0.B1.D1.80.D0.B0.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
    *   [3.3 Создание конфигурации VM для гипервизора](#.D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BA.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D0.B8_VM_.D0.B4.D0.BB.D1.8F_.D0.B3.D0.B8.D0.BF.D0.B5.D1.80.D0.B2.D0.B8.D0.B7.D0.BE.D1.80.D0.B0)
*   [4 Управление виртуальными дисками](#.D0.A3.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B2.D0.B8.D1.80.D1.82.D1.83.D0.B0.D0.BB.D1.8C.D0.BD.D1.8B.D0.BC.D0.B8_.D0.B4.D0.B8.D1.81.D0.BA.D0.B0.D0.BC.D0.B8)
    *   [4.1 Форматы, поддерживаемые VirtualBox](#.D0.A4.D0.BE.D1.80.D0.BC.D0.B0.D1.82.D1.8B.2C_.D0.BF.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.B8.D0.B2.D0.B0.D0.B5.D0.BC.D1.8B.D0.B5_VirtualBox)
    *   [4.2 Преобразование виртуальных дисков разных форматов](#.D0.9F.D1.80.D0.B5.D0.BE.D0.B1.D1.80.D0.B0.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.B2.D0.B8.D1.80.D1.82.D1.83.D0.B0.D0.BB.D1.8C.D0.BD.D1.8B.D1.85_.D0.B4.D0.B8.D1.81.D0.BA.D0.BE.D0.B2_.D1.80.D0.B0.D0.B7.D0.BD.D1.8B.D1.85_.D1.84.D0.BE.D1.80.D0.BC.D0.B0.D1.82.D0.BE.D0.B2)
        *   [4.2.1 VMDK в VDI и VDI в VMDK](#VMDK_.D0.B2_VDI_.D0.B8_VDI_.D0.B2_VMDK)
        *   [4.2.2 VHD в VDI и VDI в VDH](#VHD_.D0.B2_VDI_.D0.B8_VDI_.D0.B2_VDH)
        *   [4.2.3 QCOW2 в VDI и VDI в QCOW2](#QCOW2_.D0.B2_VDI_.D0.B8_VDI_.D0.B2_QCOW2)
    *   [4.3 Монтирование виртуальных дисков](#.D0.9C.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.B2.D0.B8.D1.80.D1.82.D1.83.D0.B0.D0.BB.D1.8C.D0.BD.D1.8B.D1.85_.D0.B4.D0.B8.D1.81.D0.BA.D0.BE.D0.B2)
        *   [4.3.1 VDI](#VDI)
    *   [4.4 Сжатие виртуальных дисков](#.D0.A1.D0.B6.D0.B0.D1.82.D0.B8.D0.B5_.D0.B2.D0.B8.D1.80.D1.82.D1.83.D0.B0.D0.BB.D1.8C.D0.BD.D1.8B.D1.85_.D0.B4.D0.B8.D1.81.D0.BA.D0.BE.D0.B2)
    *   [4.5 Увеличение размера виртуальных дисков](#.D0.A3.D0.B2.D0.B5.D0.BB.D0.B8.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D1.80.D0.B0.D0.B7.D0.BC.D0.B5.D1.80.D0.B0_.D0.B2.D0.B8.D1.80.D1.82.D1.83.D0.B0.D0.BB.D1.8C.D0.BD.D1.8B.D1.85_.D0.B4.D0.B8.D1.81.D0.BA.D0.BE.D0.B2)
    *   [4.6 Замена виртуального диска из файла .vbox вручную](#.D0.97.D0.B0.D0.BC.D0.B5.D0.BD.D0.B0_.D0.B2.D0.B8.D1.80.D1.82.D1.83.D0.B0.D0.BB.D1.8C.D0.BD.D0.BE.D0.B3.D0.BE_.D0.B4.D0.B8.D1.81.D0.BA.D0.B0_.D0.B8.D0.B7_.D1.84.D0.B0.D0.B9.D0.BB.D0.B0_.vbox_.D0.B2.D1.80.D1.83.D1.87.D0.BD.D1.83.D1.8E)
    *   [4.7 Клонирование виртуального диска и назначение ему нового UUID](#.D0.9A.D0.BB.D0.BE.D0.BD.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.B2.D0.B8.D1.80.D1.82.D1.83.D0.B0.D0.BB.D1.8C.D0.BD.D0.BE.D0.B3.D0.BE_.D0.B4.D0.B8.D1.81.D0.BA.D0.B0_.D0.B8_.D0.BD.D0.B0.D0.B7.D0.BD.D0.B0.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B5.D0.BC.D1.83_.D0.BD.D0.BE.D0.B2.D0.BE.D0.B3.D0.BE_UUID)
*   [5 Расширенная настройка](#.D0.A0.D0.B0.D1.81.D1.88.D0.B8.D1.80.D0.B5.D0.BD.D0.BD.D0.B0.D1.8F_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [5.1 Управление запуском виртуальной машины](#.D0.A3.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA.D0.BE.D0.BC_.D0.B2.D0.B8.D1.80.D1.82.D1.83.D0.B0.D0.BB.D1.8C.D0.BD.D0.BE.D0.B9_.D0.BC.D0.B0.D1.88.D0.B8.D0.BD.D1.8B)
        *   [5.1.1 Запуск виртуальный машин как сервиса systemd](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.B2.D0.B8.D1.80.D1.82.D1.83.D0.B0.D0.BB.D1.8C.D0.BD.D1.8B.D0.B9_.D0.BC.D0.B0.D1.88.D0.B8.D0.BD_.D0.BA.D0.B0.D0.BA_.D1.81.D0.B5.D1.80.D0.B2.D0.B8.D1.81.D0.B0_systemd)
        *   [5.1.2 Запуск виртуальной машины по горячей клавише](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.B2.D0.B8.D1.80.D1.82.D1.83.D0.B0.D0.BB.D1.8C.D0.BD.D0.BE.D0.B9_.D0.BC.D0.B0.D1.88.D0.B8.D0.BD.D1.8B_.D0.BF.D0.BE_.D0.B3.D0.BE.D1.80.D1.8F.D1.87.D0.B5.D0.B9_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D1.88.D0.B5)
    *   [5.2 Использование конкретных устройств в виртуальной машине](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BA.D0.BE.D0.BD.D0.BA.D1.80.D0.B5.D1.82.D0.BD.D1.8B.D1.85_.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2_.D0.B2_.D0.B2.D0.B8.D1.80.D1.82.D1.83.D0.B0.D0.BB.D1.8C.D0.BD.D0.BE.D0.B9_.D0.BC.D0.B0.D1.88.D0.B8.D0.BD.D0.B5)
        *   [5.2.1 Использование USB веб-камеры/микрофона](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_USB_.D0.B2.D0.B5.D0.B1-.D0.BA.D0.B0.D0.BC.D0.B5.D1.80.D1.8B.2F.D0.BC.D0.B8.D0.BA.D1.80.D0.BE.D1.84.D0.BE.D0.BD.D0.B0)
        *   [5.2.2 Обнаружение веб-камер и прочих USB устройств](#.D0.9E.D0.B1.D0.BD.D0.B0.D1.80.D1.83.D0.B6.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B2.D0.B5.D0.B1-.D0.BA.D0.B0.D0.BC.D0.B5.D1.80_.D0.B8_.D0.BF.D1.80.D0.BE.D1.87.D0.B8.D1.85_USB_.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2)
    *   [5.3 Доступ к гостевому серверу](#.D0.94.D0.BE.D1.81.D1.82.D1.83.D0.BF_.D0.BA_.D0.B3.D0.BE.D1.81.D1.82.D0.B5.D0.B2.D0.BE.D0.BC.D1.83_.D1.81.D0.B5.D1.80.D0.B2.D0.B5.D1.80.D1.83)
    *   [5.4 D3D ускорение в гостевой Windows](#D3D_.D1.83.D1.81.D0.BA.D0.BE.D1.80.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B2_.D0.B3.D0.BE.D1.81.D1.82.D0.B5.D0.B2.D0.BE.D0.B9_Windows)
    *   [5.5 VirtualBox c USB-ключом](#VirtualBox_c_USB-.D0.BA.D0.BB.D1.8E.D1.87.D0.BE.D0.BC)
    *   [5.6 Запуск установленного Arch Linux внутри VirtualBox](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.BD.D0.BE.D0.B3.D0.BE_Arch_Linux_.D0.B2.D0.BD.D1.83.D1.82.D1.80.D0.B8_VirtualBox)
        *   [5.6.1 Убедитесь, что система наименования разделов не изменяется](#.D0.A3.D0.B1.D0.B5.D0.B4.D0.B8.D1.82.D0.B5.D1.81.D1.8C.2C_.D1.87.D1.82.D0.BE_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D0.B0_.D0.BD.D0.B0.D0.B8.D0.BC.D0.B5.D0.BD.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F_.D1.80.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB.D0.BE.D0.B2_.D0.BD.D0.B5_.D0.B8.D0.B7.D0.BC.D0.B5.D0.BD.D1.8F.D0.B5.D1.82.D1.81.D1.8F)
        *   [5.6.2 Убедитесь в корректности образа mkinitcpio](#.D0.A3.D0.B1.D0.B5.D0.B4.D0.B8.D1.82.D0.B5.D1.81.D1.8C_.D0.B2_.D0.BA.D0.BE.D1.80.D1.80.D0.B5.D0.BA.D1.82.D0.BD.D0.BE.D1.81.D1.82.D0.B8_.D0.BE.D0.B1.D1.80.D0.B0.D0.B7.D0.B0_mkinitcpio)
        *   [5.6.3 Создание конфигурации виртуальной машины для загрузки с физического диска](#.D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BA.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D0.B8_.D0.B2.D0.B8.D1.80.D1.82.D1.83.D0.B0.D0.BB.D1.8C.D0.BD.D0.BE.D0.B9_.D0.BC.D0.B0.D1.88.D0.B8.D0.BD.D1.8B_.D0.B4.D0.BB.D1.8F_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B8_.D1.81_.D1.84.D0.B8.D0.B7.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.BE.D0.B3.D0.BE_.D0.B4.D0.B8.D1.81.D0.BA.D0.B0)
            *   [5.6.3.1 Создайте потоковый(raw) образ .vmdk](#.D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D0.B9.D1.82.D0.B5_.D0.BF.D0.BE.D1.82.D0.BE.D0.BA.D0.BE.D0.B2.D1.8B.D0.B9.28raw.29_.D0.BE.D0.B1.D1.80.D0.B0.D0.B7_.vmdk)
            *   [5.6.3.2 Создание файла конфигурации виртуальной машины](#.D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5_.D1.84.D0.B0.D0.B9.D0.BB.D0.B0_.D0.BA.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D0.B8_.D0.B2.D0.B8.D1.80.D1.82.D1.83.D0.B0.D0.BB.D1.8C.D0.BD.D0.BE.D0.B9_.D0.BC.D0.B0.D1.88.D0.B8.D0.BD.D1.8B)
        *   [5.6.4 Установка дополнений гостевой ОС](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.B4.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B5.D0.BD.D0.B8.D0.B9_.D0.B3.D0.BE.D1.81.D1.82.D0.B5.D0.B2.D0.BE.D0.B9_.D0.9E.D0.A1)
    *   [5.7 Физическая установка системы Arch Linux из VirtualBox](#.D0.A4.D0.B8.D0.B7.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B0.D1.8F_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.8B_Arch_Linux_.D0.B8.D0.B7_VirtualBox)
    *   [5.8 Перемещение физически установленного Windows в виртуальную машину](#.D0.9F.D0.B5.D1.80.D0.B5.D0.BC.D0.B5.D1.89.D0.B5.D0.BD.D0.B8.D0.B5_.D1.84.D0.B8.D0.B7.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.BD.D0.BE.D0.B3.D0.BE_Windows_.D0.B2_.D0.B2.D0.B8.D1.80.D1.82.D1.83.D0.B0.D0.BB.D1.8C.D0.BD.D1.83.D1.8E_.D0.BC.D0.B0.D1.88.D0.B8.D0.BD.D1.83)
        *   [5.8.1 Задачи в Windows](#.D0.97.D0.B0.D0.B4.D0.B0.D1.87.D0.B8_.D0.B2_Windows)
        *   [5.8.2 Задачи в GNU/Linux](#.D0.97.D0.B0.D0.B4.D0.B0.D1.87.D0.B8_.D0.B2_GNU.2FLinux)
        *   [5.8.3 Исправление MBR и загрузчика Microsoft](#.D0.98.D1.81.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_MBR_.D0.B8_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D1.87.D0.B8.D0.BA.D0.B0_Microsoft)
        *   [5.8.4 Известные ограничения](#.D0.98.D0.B7.D0.B2.D0.B5.D1.81.D1.82.D0.BD.D1.8B.D0.B5_.D0.BE.D0.B3.D1.80.D0.B0.D0.BD.D0.B8.D1.87.D0.B5.D0.BD.D0.B8.D1.8F)
*   [6 Возможные проблемы](#.D0.92.D0.BE.D0.B7.D0.BC.D0.BE.D0.B6.D0.BD.D1.8B.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B)
    *   [6.1 VERR_ACCESS_DENIED](#VERR_ACCESS_DENIED)
    *   [6.2 Клавиатура и мышка заблокированы виртуальной машиной](#.D0.9A.D0.BB.D0.B0.D0.B2.D0.B8.D0.B0.D1.82.D1.83.D1.80.D0.B0_.D0.B8_.D0.BC.D1.8B.D1.88.D0.BA.D0.B0_.D0.B7.D0.B0.D0.B1.D0.BB.D0.BE.D0.BA.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D1.8B_.D0.B2.D0.B8.D1.80.D1.82.D1.83.D0.B0.D0.BB.D1.8C.D0.BD.D0.BE.D0.B9_.D0.BC.D0.B0.D1.88.D0.B8.D0.BD.D0.BE.D0.B9)
    *   [6.3 Не могу отправить комбинацию CTRL+ALT+Fn в виртуальную машину](#.D0.9D.D0.B5_.D0.BC.D0.BE.D0.B3.D1.83_.D0.BE.D1.82.D0.BF.D1.80.D0.B0.D0.B2.D0.B8.D1.82.D1.8C_.D0.BA.D0.BE.D0.BC.D0.B1.D0.B8.D0.BD.D0.B0.D1.86.D0.B8.D1.8E_CTRL.2BALT.2BFn_.D0.B2_.D0.B2.D0.B8.D1.80.D1.82.D1.83.D0.B0.D0.BB.D1.8C.D0.BD.D1.83.D1.8E_.D0.BC.D0.B0.D1.88.D0.B8.D0.BD.D1.83)
    *   [6.4 Исправление проблем в ISO-образах](#.D0.98.D1.81.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC_.D0.B2_ISO-.D0.BE.D0.B1.D1.80.D0.B0.D0.B7.D0.B0.D1.85)
    *   [6.5 VirtualBox GUI не видит мою тему GTK 2x/3x](#VirtualBox_GUI_.D0.BD.D0.B5_.D0.B2.D0.B8.D0.B4.D0.B8.D1.82_.D0.BC.D0.BE.D1.8E_.D1.82.D0.B5.D0.BC.D1.83_GTK_2x.2F3x)
    *   [6.6 OpenBSD не работает при недоступных инструкциях виртуализации](#OpenBSD_.D0.BD.D0.B5_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D0.B5.D1.82_.D0.BF.D1.80.D0.B8_.D0.BD.D0.B5.D0.B4.D0.BE.D1.81.D1.82.D1.83.D0.BF.D0.BD.D1.8B.D1.85_.D0.B8.D0.BD.D1.81.D1.82.D1.80.D1.83.D0.BA.D1.86.D0.B8.D1.8F.D1.85_.D0.B2.D0.B8.D1.80.D1.82.D1.83.D0.B0.D0.BB.D0.B8.D0.B7.D0.B0.D1.86.D0.B8.D0.B8)
    *   [6.7 VBOX_E_INVALID_OBJECT_STATE (0x80BB0007)](#VBOX_E_INVALID_OBJECT_STATE_.280x80BB0007.29)
    *   [6.8 Подсистема USB не работает в хост-машине или гостевой ОС](#.D0.9F.D0.BE.D0.B4.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D0.B0_USB_.D0.BD.D0.B5_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D0.B5.D1.82_.D0.B2_.D1.85.D0.BE.D1.81.D1.82-.D0.BC.D0.B0.D1.88.D0.B8.D0.BD.D0.B5_.D0.B8.D0.BB.D0.B8_.D0.B3.D0.BE.D1.81.D1.82.D0.B5.D0.B2.D0.BE.D0.B9_.D0.9E.D0.A1)
    *   [6.9 Ошибка создания сетевого интерфейса "host-only"](#.D0.9E.D1.88.D0.B8.D0.B1.D0.BA.D0.B0_.D1.81.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D1.8F_.D1.81.D0.B5.D1.82.D0.B5.D0.B2.D0.BE.D0.B3.D0.BE_.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D1.84.D0.B5.D0.B9.D1.81.D0.B0_.22host-only.22)
    *   [6.10 WinXP: глубина цвета не может превышать 16 цветов](#WinXP:_.D0.B3.D0.BB.D1.83.D0.B1.D0.B8.D0.BD.D0.B0_.D1.86.D0.B2.D0.B5.D1.82.D0.B0_.D0.BD.D0.B5_.D0.BC.D0.BE.D0.B6.D0.B5.D1.82_.D0.BF.D1.80.D0.B5.D0.B2.D1.8B.D1.88.D0.B0.D1.82.D1.8C_16_.D1.86.D0.B2.D0.B5.D1.82.D0.BE.D0.B2)
    *   [6.11 Использование последовательных портов в гостевой ОС](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BF.D0.BE.D1.81.D0.BB.D0.B5.D0.B4.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D1.8B.D1.85_.D0.BF.D0.BE.D1.80.D1.82.D0.BE.D0.B2_.D0.B2_.D0.B3.D0.BE.D1.81.D1.82.D0.B5.D0.B2.D0.BE.D0.B9_.D0.9E.D0.A1)
    *   [6.12 Windows 8.x ошибка 0x000000C4](#Windows_8.x_.D0.BE.D1.88.D0.B8.D0.B1.D0.BA.D0.B0_0x000000C4)
    *   [6.13 Windows 8 VM вылетает при загрузке с ошибкой "ERR_DISK_FULL"](#Windows_8_VM_.D0.B2.D1.8B.D0.BB.D0.B5.D1.82.D0.B0.D0.B5.D1.82_.D0.BF.D1.80.D0.B8_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B5_.D1.81_.D0.BE.D1.88.D0.B8.D0.B1.D0.BA.D0.BE.D0.B9_.22ERR_DISK_FULL.22)
    *   [6.14 Гостевая ОС Linux выдает искажённый или запаздывающий звук](#.D0.93.D0.BE.D1.81.D1.82.D0.B5.D0.B2.D0.B0.D1.8F_.D0.9E.D0.A1_Linux_.D0.B2.D1.8B.D0.B4.D0.B0.D0.B5.D1.82_.D0.B8.D1.81.D0.BA.D0.B0.D0.B6.D1.91.D0.BD.D0.BD.D1.8B.D0.B9_.D0.B8.D0.BB.D0.B8_.D0.B7.D0.B0.D0.BF.D0.B0.D0.B7.D0.B4.D1.8B.D0.B2.D0.B0.D1.8E.D1.89.D0.B8.D0.B9_.D0.B7.D0.B2.D1.83.D0.BA)
    *   [6.15 Гостевая ОС зависает после запуска Xorg](#.D0.93.D0.BE.D1.81.D1.82.D0.B5.D0.B2.D0.B0.D1.8F_.D0.9E.D0.A1_.D0.B7.D0.B0.D0.B2.D0.B8.D1.81.D0.B0.D0.B5.D1.82_.D0.BF.D0.BE.D1.81.D0.BB.D0.B5_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA.D0.B0_Xorg)
    *   [6.16 Исчезновение пунктов меню и ошибка "NS_ERROR_FAILURE"](#.D0.98.D1.81.D1.87.D0.B5.D0.B7.D0.BD.D0.BE.D0.B2.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.83.D0.BD.D0.BA.D1.82.D0.BE.D0.B2_.D0.BC.D0.B5.D0.BD.D1.8E_.D0.B8_.D0.BE.D1.88.D0.B8.D0.B1.D0.BA.D0.B0_.22NS_ERROR_FAILURE.22)
    *   [6.17 "Указанный путь не существует. Проверьте путь и попробуйте еще раз." Ошибка в гостевой ОС Windows](#.22.D0.A3.D0.BA.D0.B0.D0.B7.D0.B0.D0.BD.D0.BD.D1.8B.D0.B9_.D0.BF.D1.83.D1.82.D1.8C_.D0.BD.D0.B5_.D1.81.D1.83.D1.89.D0.B5.D1.81.D1.82.D0.B2.D1.83.D0.B5.D1.82._.D0.9F.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D1.8C.D1.82.D0.B5_.D0.BF.D1.83.D1.82.D1.8C_.D0.B8_.D0.BF.D0.BE.D0.BF.D1.80.D0.BE.D0.B1.D1.83.D0.B9.D1.82.D0.B5_.D0.B5.D1.89.D0.B5_.D1.80.D0.B0.D0.B7..22_.D0.9E.D1.88.D0.B8.D0.B1.D0.BA.D0.B0_.D0.B2_.D0.B3.D0.BE.D1.81.D1.82.D0.B5.D0.B2.D0.BE.D0.B9_.D0.9E.D0.A1_Windows)
    *   [6.18 Не работают 64-битные гостевые ОС](#.D0.9D.D0.B5_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D1.8E.D1.82_64-.D0.B1.D0.B8.D1.82.D0.BD.D1.8B.D0.B5_.D0.B3.D0.BE.D1.81.D1.82.D0.B5.D0.B2.D1.8B.D0.B5_.D0.9E.D0.A1)
*   [7 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Пошаговая установка на хост-компьютер под управлением Arch Linux

Для запуска виртуальной машины под VirtualBox на хост-компьютере под управлением Arch Linux, выполните следующие действия по установке пакетов.

### Установка базовых пакетов

Установите пакет [virtualbox](https://www.archlinux.org/packages/?name=virtualbox). [virtualbox-host-dkms](https://www.archlinux.org/packages/?name=virtualbox-host-dkms) будет установлен в качестве необходимой зависимости. Также нужно установить пакеты с заголовками для установленных ядер [[1]](https://lists.archlinux.org/pipermail/arch-dev-public/2016-March/027808.html):

*   [linux](https://www.archlinux.org/packages/?name=linux) kernel: [linux-headers](https://www.archlinux.org/packages/?name=linux-headers)
*   [linux-lts](https://www.archlinux.org/packages/?name=linux-lts) kernel: [linux-lts-headers](https://www.archlinux.org/packages/?name=linux-lts-headers)
*   [linux-zen](https://www.archlinux.org/packages/?name=linux-zen) kernel: [linux-zen-headers](https://www.archlinux.org/packages/?name=linux-zen-headers)
*   [linux-grsec](https://www.archlinux.org/packages/?name=linux-grsec) kernel: [linux-grsec-headers](https://www.archlinux.org/packages/?name=linux-grsec-headers)

Вы можете установить [qt4](https://www.archlinux.org/packages/?name=qt4) в качестве опциональной зависимости для использования графического интерфейса, который базируется на [Qt](/index.php/Qt "Qt"). Это не обязательно, если вы хотите использовать VirtualBox только через консоль. [Смотрите ниже, чтобы узнать различия](#.D0.9F.D1.80.D0.B0.D0.B2.D0.B8.D0.BB.D1.8C.D0.BD.D0.BE.D0.B5_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.B2_.D1.84.D1.80.D0.BE.D0.BD.D1.82-.D1.8D.D0.BD.D0.B4.D0.B5).

### Установка модулей ядра VirtualBox

Чтобы полностью виртуализировать гостевую ОС, VirtualBox предоставляет следующие [модули ядра](/index.php/Kernel_modules_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Kernel modules (Русский)"): `vboxdrv`, `vboxnetadp`, `vboxnetflt`, и `vboxpci`. Они должны быть добавлены к вашему хост ядру.

Бинарная совместимость модулей ядра зависит от API ядра, на котором они были собраны. API может не совпадать в разных версиях ядра. Чтобы избежать проблем совместимости и багов, каждый раз при обновлении ядра Linux рекомендуется перекомпилировать модули ядра с обновленным ядром. Вместе с обновлением ядра в репозиториях Arch Linux обновляются также и модули Virtualbox, так что достаточно обновиться через пакетный менеджер.

Если вы используете ядро из [официального репозитория](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)") или стороннее (скомпилированное самостоятельно или установленное из [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)")), то необходимо тем же способом переустановить ядро.

#### Использование различных версий ядра Linux на хост-машине

*   Если вы используете ядро [linux](https://www.archlinux.org/packages/?name=linux), убедитесь, что пакет [virtualbox-host-modules](https://www.archlinux.org/packages/?name=virtualbox-host-modules) установлен. По умолчанию последняя версия этого пакета устанавливается как зависимость [virtualbox](https://www.archlinux.org/packages/?name=virtualbox).
*   Если вы используете LTS версию ядра ([linux-lts](https://www.archlinux.org/packages/?name=linux-lts)), тогда вам нужно установить пакет [virtualbox-host-modules-lts](https://aur.archlinux.org/packages/virtualbox-host-modules-lts/). Пакет [virtualbox-host-modules](https://www.archlinux.org/packages/?name=virtualbox-host-modules) после этого можно удалить.
*   Если вы используете ядро [linux-ck](https://aur.archlinux.org/packages/linux-ck/), установите пакет [virtualbox-ck-host-modules](https://aur.archlinux.org/packages/virtualbox-ck-host-modules/).

#### Обновление ядра Linux на хост-машине

После обновления ядра выполните команду

```
# sudo /usr/bin/rcvboxdrv

```

для рекомпиляции модулей ядра.

#### Стороннее ядро на хост-машине

Если вы используете или планируете использовать самостоятельно собранное ядро, вы должны знать, что VirtualBox не требует каких-либо модулей виртуализации (например, virtio, KVM, ...). Модули ядра VirtualBox обеспечивают все необходимое для нормальной работы. Таким образом, вы можете отключить в вашем ядре *.config*-файл модулей виртуализации, если они не требуются другим гипервизорам (например, Xen, KVM или QEMU).

Пакет `virtualbox-host-modules` отлично работает с пользовательской конфигурацией стокового ядра Arch Linux, такого как [linux-ck](https://aur.archlinux.org/packages/linux-ck/). `virtualbox-host-modules` поставляется с официальным ядром Arch Linux ([linux](https://www.archlinux.org/packages/?name=linux)) в зависимостях, и если вы используете иное ядро, необходимо установить [virtualbox-host-dkms](https://www.archlinux.org/packages/?name=virtualbox-host-dkms).

Если вы используете самостоятельно собранное ядро, версия которого не совпадает с версией стокового ядра Arch Linux , нужно установить [virtualbox-host-dkms](https://www.archlinux.org/packages/?name=virtualbox-host-dkms). Он поставляется в комплекте с исходниками модулей ядра VirtualBox.

Пакет [virtualbox-host-dkms](https://www.archlinux.org/packages/?name=virtualbox-host-dkms) требует компиляции. Проверьте наличие заголовков ядра, соответствующих вашей версии пользовательского ядра, чтобы избежать ошибки `Your kernel headers for kernel *your custom kernel version* cannot be found at /usr/lib/modules/*your custom kernel version*/build or /usr/lib/modules/*your custom kernel version*/source`

*   Если вы используете самостоятельно собранное ядро и использовали `make modules_install` для установки модулей, директории `/usr/lib/modules/*your custom kernel version*/build` и `(...)/source` будут символическими ссылками на исходники ядра. Они могут использоваться в качестве заголовков ядра в случае необходимости.
*   Если вы используете ядро из [AUR](/index.php/AUR "AUR") репозитория, убедитесь, что установлен пакет [linux-headers](https://www.archlinux.org/packages/?name=linux-headers).

После того, как [virtualbox-host-dkms](https://www.archlinux.org/packages/?name=virtualbox-host-dkms) установится, сгенерируйте модули ядра для пользовательского ядра следующей командой:

```
# dkms install vboxhost/*virtualbox-host-source version* -k *your custom kernel version*/*your architecture*

```

**Совет:** Используйте эту команду вместо предыдущей, если вы не хотите её адаптировать: `# dkms install vboxhost/$(pacman -Q virtualbox|awk '{print $2}'|sed 's/\-.\+//') -k $(uname -rm|sed 's/\ /\//')` 

Чтобы автоматически перекомпилировать модули ядра VirtualBox, когда их исходники обновится (т.е. повысится версия пакета [virtualbox-host-dkms](https://www.archlinux.org/packages/?name=virtualbox-host-dkms)) и чтобы не повторять впоследствии вручную `dkms install`, включите `dkms` сервис командой:

```
# systemctl enable dkms.service

```

При включенной службе `dkms` для обновления модулей можно перезагрузить компьютер. Если же вы не хотите включать эту службу, то нужно выполнять команду `dkms install` каждый раз при обновлении [virtualbox-host-dkms](https://www.archlinux.org/packages/?name=virtualbox-host-dkms). В противном случае модули не обновятся, и есть немалая возможность получить нерабочий VirtualBox.

Однако, если вы не хотите включать этот сервис (например, для оптимизации systemd) можно также использовать [initramfs hook](/index.php/Mkinitcpio "Mkinitcpio"), который будет автоматически запускать `dkms install` во время загрузки. Он требует перезагрузки для перекомпиляции модулей VirtualBox. Чтобы включить этот хук, нужно установить пакет [vboxhost-hook](https://aur.archlinux.org/packages/vboxhost-hook/) из [AUR](/index.php/AUR "AUR") и добавить `vboxhost` в `/etc/mkinitcpio.conf`. Опять же, убедитесь, что заголовки Linux доступны для нового ядра: в противном случае компиляция не удастся.

**Совет:** Ровно как и команда `dkms`, `vboxhost` хук выведет ошибку, если что-то пойдет не так во время перекомпиляции модулей VirtualBox.

### Загрузка модулей ядра VirtualBox

Среди используемых [модулей ядра](/index.php/Kernel_modules_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Kernel modules (Русский)") VirtualBox, есть обязательный модуль `vboxdrv`, который должен быть загружен перед стартом любой виртуальной машины. Он может быть загружен автоматически при старте Arch Linux, или, при необходимости, его можно загрузить вручную.

Для загрузки модуля вручную выполните следующую команду:

```
# modprobe vboxdrv

```

Для автоматической загрузки модуля VirtualBox при старте, посмотрите [Модули ядра#Автоматическое управление модулями](/index.php/Kernel_modules_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.BE.D0.B5_.D1.83.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BC.D0.BE.D0.B4.D1.83.D0.BB.D1.8F.D0.BC.D0.B8 "Kernel modules (Русский)") и создайте файл `*.conf` (например `virtualbox.conf`) в каталоге `/etc/modules-load.d/` с записью:

 `/etc/modules-load.d/virtualbox.conf`  `vboxdrv` 

### Дополнительные модули VirtualBox

Следующие модули не являются обязательными, но рекомендуются, если вы не хотите проблем с некоторыми конфигурациями (подробнее смотрите ниже): `vboxnetadp`, `vboxnetflt` и `vboxpci`.

*   `vboxnetadp` и `vboxnetflt` необходимы, если вы собираетесь использовать ["Локальную виртуальную сеть"](https://www.virtualbox.org/manual/ch06.html#network_hostonly). Точнее, `vboxnetadp` нужен для создания интерфейса в глобальных настройках VirtualBox, и `vboxnetflt` нужен для запуска виртуальной машины с использованием этого интерфейса.

*   `vboxpci` необходим, когда вашей виртуальной машине нужно получить доступ к PCI устройству на вашей машине.

Для работы данных модулей выполните команду

```
# pacman -S net-tools

```

И создайте файл `vbox-other-modules.conf` в каталоге `/etc/modules-load.d/` с записью

 `/etc/modules-load.d/vbox-other-modules.conf`  `vboxnetadp vboxnetflt vboxpci` 
**Примечание:** Если модули ядра VirtualBox были загружены в ядро пока вы обновляли модули, то вы должны загрузить их вручную для использования новой, обновленной версии. Что бы это сделать, запустите
```
# vboxreload

```

VirtualBox использует `ifconfig` и `route`, чтобы назначить IP и маршрут до интерфейса хоста, настроенного с помощью `VBoxManage hostonlyif` или с помощью GUI *Settings > Network > Host-only Networks > Edit host-only network (space) > Adapter*.

### Добавление пользователей в группу vboxusers

Чтобы использовать USB-порты хост-системы в виртуальных машинах, нужно добавить в [группу](/index.php/Groups_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Groups (Русский)") `vboxusers` имена пользователей, которые смогут получить доступ к USB-портам. Новая группа не будет автоматически применяться к существующим сеансам. Пользователь должен перелогиниться или добавить пользователя в новую группу в текущей сессии командой `newgrp` или `sudo -u $USER -s`. Для добавления текущего пользователя в группу `vboxusers` нужно выполнить:

```
# gpasswd -a $USER vboxusers

```

### Образ диска с гостевыми дополнениями

Для корректной работы VirtualBox рекомендуется установить пакет [virtualbox-guest-iso](https://www.archlinux.org/packages/?name=virtualbox-guest-iso) в хост-системе. Этот пакет создаёт образ диска, который может быть использован для установки гостевых дополнений в гостевых системах, отличных от Arch Linux. *.iso* образ будет находиться в `/usr/lib/virtualbox/additions/VBoxGuestAdditions.iso` и может быть установлен вручную после подключения образа в виртуальной машине.

### Пакет дополнений

Начиная с версии VirtualBox 4.0, компоненты, не распространяющиеся под лицензией GPL были отделены от основной части приложения. Несмотря на то, что данные компоненты выпущены под несвободной лицензией и **доступны только для личного использования**, вам может понадобиться установка Oracle Extension Pack, который обеспечивает [дополнительный функционал](https://www.virtualbox.org/manual/ch01.html#intro-installing). [virtualbox-ext-oracle](https://aur.archlinux.org/packages/virtualbox-ext-oracle/) пакет доступен на [AUR](/index.php/AUR "AUR"), а нестабильная версия может быть найдена в репозитории [seblu](/index.php/Unofficial_user_repositories#seblu "Unofficial user repositories").

Если вы предпочитаете использовать ручной способ, можно скачать пакет дополнений вручную и установить его с помощью графического интерфейса (*Настройки > Расширения*) или с помощью команды `VBoxManage extpack install <.vbox-extpack>`. Предварительно убедитесь, что у вас установлен инструментарий (например, [Polkit](/index.php/Polkit "Polkit"), gksu и т.д.) для предоставления привилегированного доступа к VirtualBox, так как установка этого пакета [требует прав суперпользователя](https://www.virtualbox.org/ticket/8473).

### Правильное использование в фронт-энде

Теперь вы готовы использовать VirtualBox. Поздравляем!

Вы можете использовать несколько удобных команд VirtualBox:

*   Если вы хотите использовать VirtualBox в командной строке (только запускать и изменять настройки существующих виртуальных машин), вы можете использовать команду `VBoxSDL`. VBoxSDL создаёт простое окно, которое содержит только *чистую* виртуальную машину, без меню или других элементов управления (фрейм-буфер).
*   Если вы хотите использовать VirtualBox в командной строке без любого GUI-интерфейса (например, на сервере) для создания, запуска и настройки виртуальных машин, используйте `VBoxHeadless`, который не производит никакого видимого вывода на хост-машине, а только предоставляет данные VRDP.

Если вы установили [qt4](https://www.archlinux.org/packages/?name=qt4) из дополнительных зависимостей, у вас будет приятный GUI-интерфейс.

Наконец, вы можете использовать [PhpVirtualBox](/index.php/PhpVirtualBox "PhpVirtualBox") для управления виртуальными машинами из веб-интерфейса.

Обратитесь к [руководству VirtualBox](https://www.virtualbox.org/manual), чтобы узнать, как создавать виртуальные машины.

**Важно:** Если вы собираетесь хранить образы виртуальных дисков в файловой системе [Btrfs](/index.php/Btrfs "Btrfs") , то перед созданием каких-либо образов вы должны отключить журналирование [Copy-on-Write](/index.php/Btrfs#Copy-on-Write_.28CoW.29 "Btrfs") для каталога с образами.

## Пошаговая установка Arch Linux как гостевой ОС

### Установка Arch Linux в виртуальную машину

**Примечание:** Хостам с ОС Windows, возможно, придется отключить Hyper-V для того, чтобы использовать возможности виртуализации устройств и создания 64-битных виртуальных машин в VirtualBox. Чтобы узнать, как отключить или снова включить Hyper-V, [посмотрите пост на StackOverflow](http://superuser.com/questions/684966/switch-off-hyper-v-without-disable-functionality-in-windows-8-1).

Загрузите установочный носитель Arch через один из виртуальных дисков виртуальной машины. Затем совершите установку базовой системы Arch, как описано в [руководстве по установке](/index.php/Installation_guide_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Installation guide (Русский)"), без установки графических драйверов: мы будем устанавливать драйвера, поставляемые VirtualBox на следующем этапе.

#### Установка в режиме EFI

Если вы хотите установить Arch Linux в режиме EFI внутри VirtualBox, в настройках виртуальной машины, перейдите в закладку *Настройки*, и установите флажок *Enable EFI (special OSes only)*. После выбора ядра из меню установочного носителя Arch Linux, установка будут висеть в течение минуты-двух, и после этого будет загружено ядро . Подождите и не прекращайте установку.

При загрузке в режиме EFI, VirtualBox будет пытаться выполнить `/EFI/BOOT/BOOTX64.EFI` из ESP. Если первый вариант не удается, VirtualBox будет пытаться выполнить сценарий оболочки EFI `startup.nsh` из корня ESP. Если вы не хотите вручную запускать загрузчик из оболочки EFI каждый раз, вы должны будете переместить свой загрузчик в этот путь по умолчанию. Не заморачивайтесь с VirtualBox Boot Manager (доступен по `F2` при загрузке): EFI данные будут добавлены в него вручную при загрузке или [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr) будет сохранять их после перезагрузки, [но терять после закрытия виртуальной машины](https://www.virtualbox.org/ticket/11177).

### Установка гостевых дополнений

После завершения установки гостевой системы, установите [дополнения гостевой ОС](https://www.virtualbox.org/manual/ch04.html), которые включают драйверы и приложения, оптимизирующие гостевую операционную систему. Они могут быть установлены с помощью [virtualbox-guest-utils](https://www.archlinux.org/packages/?name=virtualbox-guest-utils), которая прикреплена к [virtualbox-guest-modules](https://www.archlinux.org/packages/?name=virtualbox-guest-modules) как необходимая зависимость.

**Примечание:** Метод, описанный в [VirtualBox руководстве](https://www.virtualbox.org/manual/ch04.html#idp54932560) не работает на гостевой Arch Linux, в результате `Unable to determine your Linux distribution` несколько раз повторено, как сообщение об ошибке. Если Вы уже попробовали этот первый метод и вы используете правильное описанное выше решение впоследствии, это не удастся. Вы получите ошибку `/usr/bin/VBox* exists in filesystem` и `/usr/lib/VBox* exists in filesystem`. Решение заключается в удалении конфликтующих файлов: `# rm /usr/bin/VBox* /usr/lib/VBox*` Эти файлы на самом деле являются символическими ссылками на места, где были установлены гостевые дополнения; По умолчанию, это `/opt/VBoxGuestAdditions-*номер версии*`. Удалите и эти файлы `# rm -r /opt/VBoxGuestAdditions-*номер версии*`,так как они не нужны. Теперь вы можете перезапустить установку правильным, вышеописанным способом.

### Установка гостевых модулей ядра VirtualBox

#### Запуск гостевой ОС с официальным ядром

*   Если вы используете ядро [linux](https://www.archlinux.org/packages/?name=linux), убедитесь, что пакет [virtualbox-guest-modules](https://www.archlinux.org/packages/?name=virtualbox-guest-modules) установлен. [virtualbox-guest-modules](https://www.archlinux.org/packages/?name=virtualbox-guest-modules) устанавливается как зависимость пакета [virtualbox-guest-utils](https://www.archlinux.org/packages/?name=virtualbox-guest-utils).
*   Если вы используете LTS ядро ([linux-lts](https://www.archlinux.org/packages/?name=linux-lts)), установите пакет [virtualbox-guest-modules-lts](https://aur.archlinux.org/packages/virtualbox-guest-modules-lts/). Пакет [virtualbox-guest-modules](https://www.archlinux.org/packages/?name=virtualbox-guest-modules) может быть удалён по вашему желанию.
*   Если вы используете ядро [linux-ck](https://aur.archlinux.org/packages/linux-ck/), скомпилируйте пакет [virtualbox-ck-guest-modules](https://aur.archlinux.org/packages/virtualbox-ck-guest-modules/). Пакет [virtualbox-guest-modules](https://www.archlinux.org/packages/?name=virtualbox-guest-modules) также может быть удалён.

#### Запуск гостевой ОС со сторонним ядром

Этот шаг установки очень похож на настройку модулей ядра в разделе Vitualbox для хоста, описанную выше. Обратитесь к [этому разделу](#Install_the_VirtualBox_kernel_modules) для получения дополнительной информации и замените все [virtualbox-host-modules](https://www.archlinux.org/packages/?name=virtualbox-host-modules), [virtualbox-host-dkms](https://www.archlinux.org/packages/?name=virtualbox-host-dkms) и [vboxhost-hook](https://aur.archlinux.org/packages/vboxhost-hook/) на [virtualbox-guest-modules](https://www.archlinux.org/packages/?name=virtualbox-guest-modules), [virtualbox-guest-dkms](https://www.archlinux.org/packages/?name=virtualbox-guest-dkms) и [vboxguest-hook](https://aur.archlinux.org/packages/vboxguest-hook/) соответственно.

### Загрузка модулей ядра VirtualBox

Для загрузки модуля вручную выполните:

```
# modprobe -a vboxguest vboxsf vboxvideo

```

Чтобы загрузить модуль VirtualBox во время загрузки системы, обратитесь к [Загрузка ядра#Автоматическое управление модулями](/index.php/Kernel_modules_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.BE.D0.B5_.D1.83.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BC.D0.BE.D0.B4.D1.83.D0.BB.D1.8F.D0.BC.D0.B8 "Kernel modules (Русский)") и создайте `*.conf` файл (например, `virtualbox.conf`) в директории `/etc/modules-load.d/` с следующим содержанием:

 `/etc/modules-load.d/virtualbox.conf` 
```
vboxguest
vboxsf
vboxvideo
```

Кроме того, команда

```
# systemctl enable vboxservice 

```

включает автозагрузку модулей и синхронизацию времени хоста и гостевой ОС.

### Запуск гостевых сервисов VirtualBox

После довольно непростой установки с модулями ядра VirtualBox, необходимо обеспечить взаимодействие гостевой ОС и хоста посредством сервисов. Гостевой сервис - на самом деле просто исполняемый файл, обращающийся к `VBoxClient`, который будет взаимодействовать с вашей X Window System. `VBoxClient` управляет следующими функциями:

*   Общий буфер обмена и перетаскивания между принимающей стороной и гостевой ОС;
*   Бесшовный оконный режим;
*   Гостевой дисплей автоматически изменяется в соответствии с размером окна гостевой ОС;
*   Проверка версии VirtualBox, установленной на хосте.

Все эти особенности могут быть включены независимо следующими параметрами:  $ VBoxClient --clipboard --draganddrop --seamless --display --checkhostversion

Как ссылка, `VBoxClient-all` bash скрипт позволяет использовать все эти функции. Вы должны установить `VBoxClient`, который будет автоматически загружен в качестве [DE](/index.php/Desktop_environment_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Desktop environment (Русский)") или [оконного менеджера](/index.php/Window_manager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Window manager (Русский)")

На практике,

*   Если вы используете [DE](/index.php/Desktop_environment_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Desktop environment (Русский)"), вам просто нужно установить флажок или добавить `/usr/sbin/VBoxClient-all`} в разделе автозапуска вашей DE (DE обычно устанавливают флаг на *.desktop* файлы в `~/.config/autostart`, см. [настройку автозапуска](/index.php/Desktop_entries "Desktop entries") для более подробной информации);
*   Если у вас нет каких-либо DE, добавьте следующую строку в начале [~/.xinitrc](/index.php/Xinitrc_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xinitrc (Русский)") перед любыми `exec` функциями:

 `~/.xinitrc`  `/usr/bin/VBoxClient-all` 

VirtualBox также может синхронизировать время между хостом и гостевой ОС. Чтобы сделать это, выполните `VBoxService` с правами суперпользователя. Чтобы установить автоматический запуск этого кода при загрузке, выполните:

```
# systemctl enable vboxservice

```

Теперь у вас есть рабочая гостевая Arch Linux. Поздравляем!

Если вы хотите расшарить директории между вашим компьютером и гостевым Arch Linux, читайте дальше.

### Расшаривание директорий

Общие папки управляются в хосте через настройки виртуальной машины, доступной через графический интерфейс VirtualBox, на вкладке *Shared Folders*. Там путь к директории и имя точки монтирования определены как *Имя папки* и аргументы, такие как *Read-only*, *Auto-mount* и *Make permanent* Эти параметры могут быть определены через утилиту `VBoxManage`. См. [для более подробной информации](https://www.virtualbox.org/manual/ch04.html#sharedfolders).

Независимо от того, какой метод вы будете использовать, чтобы смонтировать директорию, требуются некоторые начальные действия.

Чтобы избежать проблемы `/sbin/mount.vboxsf: mounting failed with the error: No such device`, убедитесь, что модуль ядра `vboxsf` загружен правильно. Он должен быть загружен, поскольку мы включили все гостевые модули ядра ранее.

Два дополнительных шага необходимы для того, чтобы точки монтирования должны быть доступны из пользователей кроме root-а:

*   Пакет [virtualbox-guest-utils](https://www.archlinux.org/packages/?name=virtualbox-guest-utils) создает группу `vboxsf`;
*   Ваше имя пользователя должно быть в этой группе, используйте команду `gpasswd -a $USER vboxsf`, чтобы добавить свое имя пользователя и запустите `newgrp`, чтобы применить изменения немедленно.

#### Ручное монтирование

Выполните следующую команду для монтирования директории в гостевой Arch Linux:

```
# mount -t vboxsf *имя_расшариваемой_директории* *точка_монтирования_в_гостевой_ОС*

```

Файловая система `vboxsf` предоставляет и другие способы, просмотреть которые можно выполнив:

```
# mount.vboxsf

```

Например, если пользователь не добавлен в *vboxsf* группу, мы могли бы использовать эту команду, чтобы смонтировать директорию в гостевой ОС:

```
# mount -t vboxsf -o uid=1000,gid=1000 home /mnt/

```

Где *UID* и *GID* являются значениями, соответствующими пользователям, которым мы хотим дать доступ к монтированию директории. Эти значения можно узнать из вывода команды `id`, выполненной из сессии этого пользователя.

#### Автомонтирование

Чтобы функция автоматического монтирования заработала, вы должны включить флажок в графическом интерфейсе или использовать дополнительный аргумент `--automount` при команде `VBoxManage общая_директория`

Теперь общая директория должна появиться в `/media/sf_*имя_расшаренной_директории*`.

Вы можете использовать символические ссылки, если хотите иметь более удобный доступ:

```
$ ln -s /media/sf_*имя_расшаренной_директории* ~/*мои_документы*

```

#### Монтирование при загрузке

Вы можете монтировать директории с помощью [fstab](/index.php/Fstab_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Fstab (Русский)"). Во избежание проблем с systemd, необходимо добавить в `/etc/fstab` строчку `comment=systemd.automount`. Таким образом, общие папки монтируются только тогда, когда доступны точки подключения, а не во время запуска. Это может избежать некоторых проблем, особенно если гостевая ОС еще не загружена, когда systemd уже начал читать fstab и монтировать разделы.

```
desktop   /media/desktop    vboxsf  uid=user,gid=group,rw,dmode=700,fmode=600,comment=systemd.automount 0 0

```

mount.vboxsf [может не поддерживать](https://www.virtualbox.org/ticket/10676%7C) *nofail* аргумент:

```
desktop   /media/desktop    vboxsf  uid=user,gid=group,rw,dmode=700,fmode=600,nofail 0 0

```

## Импорт/экспорт виртуальных машин VirtualBox в/из других гипервизоров

Если вы планируете использовать виртуальную машину на другом гипервизоре или хотите импортировать в VirtualBox виртуальную машину, созданную в другом гипервизоре, вы можете быть заинтересованы в чтении следующих шагов.

### Удаление дополнений гостевой ОС

Гостевые дополнения доступны в большинстве гипервизоров: VirtualBox поставляется с гостевыми дополнениями, VMware с VMware Tools, Parallels с инструментами Parallels, и т.д. Это дополнительные компоненты, предназначенные для установки внутри виртуальной машины после гостевой операционной системы, состоящие из драйверов устройств и системных приложений, которые оптимизируют гостевую операционной системы для повышения производительности и удобства использования. [Читать подробнее](https://www.virtualbox.org/manual/ch04.html).

Если у вас установлены дополнения в вашей виртуальной машине - удалите их в первую очередь. Ваша гостевая ОС, особенно если это ОС из семейства Windows, может вести себя странно, аварийно или не загрузиться вообще, если вы используете специальные драйверы одного гипервизора на другом.

### Использование правильного формата виртуального диска

От этого шага будет зависеть способность преобразовывать образ диска виртуальной в другие форматы - непосредственно или конвейерным методом.

#### Автоматические инструменты

Некоторые компании предоставляют инструменты, которые предлагают возможность создания виртуальных машин с операционной системой Windows или GNU / Linux, расположенной в виртуальной машине или даже в оригинальной установке. С таким продуктом вам не нужно применять этот и следующие шаги, и можно далее не читать.

*   *[Parallels Transporter](Http://www.parallels.com/products/transporter)* - не бесплатный, продукт от Parallels Inc. Это решение в основном заключается в части программного обеспечения под названием *агент*, который будет установлен в гостевой ОС, которую вы хотите импортировать / преобразовать. Затем, Parallels Transporter, *который работает только на OS X* , создаст виртуальную машину с этим *агентом*, который контактирует либо по USB или по сети Ethernet.
*   *[VMware vCenter Converter](Https://www.vmware.com/products/converter/)* - бесплатен при регистрации на Webiste VMware, работает почти так же, как Parallels Transporter, но часть программного обеспечения, которая собирает данные для создания виртуальной машины работает только на платформе Windows.

#### Ручное преобразование

Во-первых, ознакомьтесь с [форматами, поддерживаемыми Virtualbox](#.D0.A4.D0.BE.D1.80.D0.BC.D0.B0.D1.82.D1.8B.2C_.D0.BF.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.B8.D0.B2.D0.B0.D0.B5.D0.BC.D1.8B.D0.B5_VirtualBox) и [форматами других гипервизоров](https://en.wikipedia.org/wiki/Comparison_of_platform_virtual_machines#Image_type_compatibility "wikipedia:Comparison of platform virtual machines").

*   Импорт и экспорт виртуальной машины из/в формат VMware не является проблемой, если вы используете формат диска VMDK или OVF, в противном случае преобразования [VMDK в VDI и VDI в VMDK](#VMDK_.D0.B2_VDI_.D0.B8_VDI_.D0.B2_VMDK) можно осуществить вышеописанным VMware vCenter Converter.

*   Импорт и экспорт из/в QEMU почти не проблема: некоторые форматы QEMU поддерживает непосредственно VirtualBox и преобразование между [QCOW2 в VDI и VDI в QCOW2](#QCOW2_.D0.B2_VDI_.D0.B8_VDI_.D0.B2_QCOW2) по-прежнему доступны в случае необходимости.

*   Импорт и экспорт из/в Parallels гипервизора является трудный задачей: Parallels поддерживает только свой собственный формат жесткого диска (даже стандартные форматы и портативный формат OVF не поддерживается!).

*   Чтобы экспортировать виртуальную машину для Parallels, вам нужно будет использовать инструмент описанной выше Parallels - Transporter.
*   Чтобы импортировать виртуальную машину в VirtualBox, вы должны будете использовать VMware vCenter Converter , чтобы преобразовать виртуальную машину в формат VMware в первую очередь - а затем используйте инструмент для миграции с VMware.

### Создание конфигурации VM для гипервизора

Каждый гипервизор имеет свой собственный файл конфигурации виртуальной машины: `.vbox` для VirtualBox, `.vmx` для VMware, `config.pvs` файл, расположенный в виртуальной машине (`.pvm` файл), и т.д. Вы можете, таким образом, создать новую виртуальную машину в новом гипервизоре и указать его конфигурацию как можно ближе относительно начальной виртуальной машины.

Обратите пристальное внимание на интерфейс прошивки (BIOS или UEFI), используемый для установки гостевой операционной системы. В то время как опция доступна выбирать между этими 2 интерфейсов на VirtualBox и на Parallels решений, на VMware, вам придется вручную добавить следующую строку в ваш *.vmx* файл.

 `ArchLinux_vm.vmx`  `firmware = "efi"` 

Наконец, настройте ваш гипервизор, для использования существующего виртуального диска, который вы преобразовали и запустите виртуальную машину.

**Совет:**

*   В VirtualBox, если вы не хотите просмотривать весь графический интерфейс, чтобы найти нужное место где можно добавить новый виртуальный диск устройства, вы можете [Заменить виртуальный диск вручную из файла .vbox](#.D0.97.D0.B0.D0.BC.D0.B5.D0.BD.D0.B0_.D0.B2.D0.B8.D1.80.D1.82.D1.83.D0.B0.D0.BB.D1.8C.D0.BD.D0.BE.D0.B3.D0.BE_.D0.B4.D0.B8.D1.81.D0.BA.D0.B0_.D0.B8.D0.B7_.D1.84.D0.B0.D0.B9.D0.BB.D0.B0_.vbox_.D0.B2.D1.80.D1.83.D1.87.D0.BD.D1.83.D1.8E), или использовать `VBoxManage storageattach`, описанный в [увеличении вируального диска](#.D0.A3.D0.B2.D0.B5.D0.BB.D0.B8.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D1.80.D0.B0.D0.B7.D0.BC.D0.B5.D1.80.D0.B0_.D0.B2.D0.B8.D1.80.D1.82.D1.83.D0.B0.D0.BB.D1.8C.D0.BD.D1.8B.D1.85_.D0.B4.D0.B8.D1.81.D0.BA.D0.BE.D0.B2) или в [руководстве VirtualBox](https://www.virtualbox.org/manual/ch08.html#vboxmanage-storageattach)
*   Кроме того, в продуктах VMware, вы можете заменить местоположение текущего местоположения виртуального диска путем адаптации *.vmdk* местоположения файла в *.vmx* конфигурационном файле.

## Управление виртуальными дисками

### Форматы, поддерживаемые VirtualBox

VirtualBox поддерживает следующие форматы виртуальных дисков:

*   VDI: Virtual Disk Image является собственным стандартои VirtualBox, используемыи по умолчанию, когда вы создаете виртуальную машину в VirtualBox.

*   VMDK: изначально разработан VMware для своих продуктов.Спецификация была закрытым исходным кодом, но сейчас стало открытым форматом, который полностью поддерживается VirtualBox. Этот формат дает возможность разбивать себя на несколько файлов по 2 Гб. Эта функция особенно полезна, если вы хотите сохранить виртуальную машину на компьютерах, которые не поддерживают очень большие файлы. Другие форматы, за исключением формата HDD от Parallels, не обеспечивают такую эквивалентную функцию.

*   VHD: Virtual Hard Disk - формат, используемый в Microsoft в Windows Virtual PC и Hyper-V. Если вы собираетесь использовать любой из этих продуктов Microsoft, вы должны будете выбрать этот формат.

**Совет:** Начиная с Windows 7, этот формат может быть установлен непосредственно без каких-либо дополнительных приложений.

*   VHDX (только для чтения): Это расширенная версия формата виртуального жесткого диска, разработанного Microsoft, которая была выпущена на 2012-09-04 с Hyper-V 3.0 при переходе на Windows Server 2012\. Эта новая версия имеет повышенную производительность (лучшее расположение блоков), большие размеры блоков и поддержку журнала. VirtualBox [поддерживает этот формат только для чтения](https://www.virtualbox.org/manual/ch15.html#idp63002176).

*   Версия 2 HDD: Формат HDD разработан Parallels Inc и используются в их гипервизоре, например Parallels Desktop для Mac. Новые версии этого формата (т.е. 3 и 4) не поддерживаются из-за отсутствия документации для этого форматф.
    **Примечание:** Существуют споры в отношении поддержки версии 2 формата. Официальное руководство VirtualBox [сообщает, что поддерживается только 2 версия](https://www.virtualbox.org/manual/ch05.html#vdidetails), авторы Википедии утверждают,что [частично может работать и первая версия](https://en.wikipedia.org/wiki/Comparison_of_platform_virtual_machines#_Image_type_compatibility "wikipedia:Comparison of platform virtual machines"). Приветствуется помощь, если вы можете выполнить некоторые тесты с первой версией формата HDD.

*   QED: Формат Enhanced Disk QEMU - старый формат для QEMU, свободный и открытый. Этот формат был разработан в 2010 году таким образом, чтобы обеспечить превосходную альтернативу qcow2 и другим форматам. Этот формат имеет полностью асинхронный ввод / вывод, хорошую целостность данных, откат файлов и разреженные файлы. Формат QED поддерживается только для совместимости с виртуальными машинами, созданными в старых версиях QEMU.

*   QCOW: QEMU CoW - нынешний формат для QEMU.Формат QCOW поддерживает прозрачное сжатие на основе ZLIB и шифрование (последнее имеет недостаток, и не рекомендуется к сипользованию). QCOW доступен в двух версиях: QCOW и qcow2\. Последний, как правило, заменяет первый. QCOW [в настоящее время поддерживается VirtualBox](https://www.virtualbox.org/manual/ch15.html#idp63002176). Qcow2 поставляется в двух версиях: qcow2 0.10 и qcow2 1.1 (по умолчанию используемый при создании виртуального диска с QEMU). VirtualBox не поддерживает qcow2.

*   OVF: Open Virtualization Format является открытым форматом, который был разработан для обеспечения взаимодействия и распределения виртуальных машин между различными гипервизоров. VirtualBox поддерживает все версии этого формата через [`VBoxManage` импорт / экспорт](https://www.virtualbox.org/manual/ch08.html#idp55423424), но с [https: //www.virtualbox.org/manual/ch14.html#KnownProblems известными ограничениями].

*   RAW: Это режим, когда виртуальный диск скидывается непосредственно на диск без определенного формата файл контейнера. VirtualBox поддерживает эту функцию несколькими способами: преобразование RAW диск [к определенному формату](https://www.virtualbox.org/manual/ch08.html#idp59139136), или [клонированием диска в формате RAW](https://www.virtualbox.org/manual/ch08.html#VBoxManage-clonevdi), или непосредственно через файл VMDK, [который указывает на физический диск или просто файл](https://www.virtualbox.org/manual/ch09.html#idp57804112).

### Преобразование виртуальных дисков разных форматов

#### VMDK в VDI и VDI в VMDK

VirtualBox может конвертировать VDI в VMDK и обратно с использованием [`VBoxManage clonehd`](https://www.virtualbox.org/manual/ch08.html#vboxmanage-clonevdi).

VMDK в VDI:

```
$ VBoxManage clonehd *source.vmdk* *destination.vdi* --format VDI

```

VDI в VMDK:

```
$ VBoxManage clonehd *source.vdi* *destination.vmdk* --format VMDK

```

#### VHD в VDI и VDI в VDH

VirtualBox также может конвертировать VHD в VDI и наоборот с использованием [`VBoxManage clonehd`](https://www.virtualbox.org/manual/ch08.html#vboxmanage-clonevdi):

VHD в VDI:

```
$ VBoxManage clonehd *source.vhd* *destination.vdi* --format VDI

```

VDI в VHD:

```
$ VBoxManage clonehd *source.vdi* *destination.vhd* --format VHD

```

#### QCOW2 в VDI и VDI в QCOW2

[`VBoxManage clonehd`](https://www.virtualbox.org/manual/ch08.html#vboxmanage-clonevdi) не может конвертировать QEMU форматы и необходимо воспользоваться иными инструментами. Команда `qemu-img` из пакета [qemu](https://www.archlinux.org/packages/?name=qemu) может осуществлять преобразования QCOW2<=>VDI.
**Примечание:** `qemu-img` также обрабатывает кучу других форматов. В соответствии выводу `qemu-img --help`, `qemu-img` поддерживает данные форматы : "*vvfat vpc vmdk vhdx vdi ssh sheepdog sheepdog sheepdog raw host_cdrom host_floppy host_device file qed qcow2 qcow parallels nbd nbd nbd iscsi dmg tftp ftps ftp https http cow cloop bochs blkverify blkdebug'".*

QCOW2 в VDI:

```
$ qemu-img convert -pO vdi *source.qcow2* *destination.vdi*

```

VDI в QCOW2:

```
$ qemu-img convert -pO qcow2 *source.vdi* *destination.qcow2*

```

Так как QCOW2 предостовляется в двух версиях (0.10 и 1.1) (см. [форматы, поддерживаемые VirtualBox](#.D0.A4.D0.BE.D1.80.D0.BC.D0.B0.D1.82.D1.8B.2C_.D0.BF.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.B8.D0.B2.D0.B0.D0.B5.D0.BC.D1.8B.D0.B5_VirtualBox). Используйте параметр `-o compat=` для выбора версии.

```
$ qemu-img convert -pO qcow2 *source.vdi* *destination.qcow2* -o compat=0.10

```

или

```
$ qemu-img convert -pO qcow2 *source.vdi* *destination.qcow2* -o compat=1.1

```

**Совет:** Параметр `-p` отображает прогресс выполнения преобразования.

### Монтирование виртуальных дисков

#### VDI

Монтирование образов VDI работает только с образами фиксированного размера (т.е. статичными образами); динамические образы (динамическое выделение размера) монтируются довольно-таки не просто.

Если необходимо смещение раздела (в VDI), добавьте значение `offData` в `32256` (например, 69632 + 32256 = 101888):

```
$ VBoxManage internalcommands dumphdinfo <storage.vdi> | grep "offData"

```

Теперь cмонтируем:

```
# mount -t ext4 -o rw,noatime,noexec,loop,offset=101888 <storage.vdi> /mntpoint/

```

Вы также можете использовать скрипт [mount.vdi](https://github.com/pld-linux/VirtualBox/blob/master/mount.vdi), который можно использовать (и даже установить скрипт в `/usr/bin/`:

```
# mount -t vdi -o fstype=ext4,rw,noatime,noexec *vdi_file_location* */mnt/*

```

Также можно использовать модули ядра [qemu](https://www.archlinux.org/packages/?name=qemu) , которые выполняют эту же функцию [attrib](http://bethesignal.org/blog/2011/01/05/how-to-mount-virtualbox-vdi-image/):

```
# modprobe nbd max_part=16
# qemu-nbd -c /dev/nbd0 <storage.vdi>
# mount /dev/nbd0p1 /mnt/dir/
# # to unmount:
# umount /mnt/dir/
# qemu-nbd -d /dev/nbd0

```

Если файлы раздела не распространяются, попробуйте использовать `partprobe /dev/nbd0`. В противном случае, VDI раздел может быть отображен непосредственно в файл с помощью `qemu-nbd -P 1 -c /dev/nbd0 <storage.vdi>`.

### Сжатие виртуальных дисков

Сжатие работает только с файлами `.vdi` и в основном состоит из следующих действий:

Загрузите виртуальную машину и удалите все ненужное вручную или с помощью специальных средств, например [bleachbit](https://www.archlinux.org/packages/?name=bleachbit) ([доступна для ОС Windows](http://bleachbit.sourceforge.net/download/windows)).

Затирание свободного места нулями может быть выполнено следующими инструментами:

*   Если вы пользовались Bleachbit, просто установите галочку *System > Free disk space* в графическом интерфейсе, выполните команду `bleachbit -c system.free_disk_space`;
*   В UNIX-based системах, выполните команду `dd` или, предпочтительно, [dcfldd](https://www.archlinux.org/packages/?name=dcfldd) (см. [здесь](http://superuser.com/a/355322) информацию об отличиях):

	 `# dcfldd if=/dev/zero of=*/fillfile* bs=4M` 

	Когда `fillfile` достигает лимита раздела, вам будет выдано сообщение вида `1280 blocks (5120Mb) written.dcfldd:: No space left on device`. Это означает, что все пространство пользователя и незарезервированные блоки раздела будут затерты. Используя эту команду от суперпользователя, важно убедится в том, что все свободные блоки затерты. По умолчанию некий процент блоков ФС зарезервирован для супер-пользователя (см. вывод `-m` аргумента при команде `mkfs.ext4` или используйте `tune2fs -l` чтобы увидеть, сколько места зарезервировано под приложения запущенные от root).

	Когда вышеописанный процесс будет завершён, вы можете удалить созданный вами файл `*fillfile*`.

*   В ОС Windows есть два инструмента:

*   `sdelete` - [Sysinternals Suite](http://technet.microsoft.com/en-us/sysinternals/bb842062.aspx), выполните `sdelete -s *c:*` для каждого виртуального диска;
*   Для любителей PowerShell есть скрипт [PowerShell solution](http://blog.whatsupduck.net/2012/03/powershell-alternative-to-sdelete.html). Его также необходимо отдельно выполнять для каждого виртуального диска.

	 `PS> ./Write-ZeroesToFreeSpace.ps1 -Root *c:\* -PercentFree 0` 

**Примечание:** Этот скрипт должен быть запущен в среде PowerShell от имени администратора. По дефолту скрипты не запускаются из-за ограничений политик безопасности. Необходимо установить необходимое значение параметра `Get-ExecutionPolicy` в политиках безопасности: `Set-ExecutionPolicy RemoteSigned`.

Перезагрузите виртуальную машину. После выполнения задач и перезагрузки виртуальной машины рекомендуется провести проверку диска.

*   В UNIX-based системах можно использовать `fsck`;

*   В GNU/Linux системах, в том числе Arch Linux, вы можете установить проверку диска при загрузке вручную [в параметрах загрузки ядра](/index.php/Fsck#Forcing_the_check "Fsck");

*   В Windows системах:

*   `chkdsk *c:* /F` где `*c:*` заменяется на имя проверяемого диска;
*   или `FsckDskAll` [отсюда](http://therightstuff.de/2009/02/14/ChkDskAll-ChkDsk-For-All-Drives.aspx), который основан на `chkdsk`, но не требует перезапуска для каждого отдельного диска;

Теперь удалите нули из `vdi` файлов с помощью `[VBoxManage modifyhd](https://www.virtualbox.org/manual/ch08.html#vboxmanage-modifyvdi)`:

```
$ VBoxManage modifyhd *your_disk.vdi* --compact

```

**Примечание:** Если в вашей виртуальной машине есть снимки, вам необходимо выполнить команду для всех ваших `.vdi` файлов.

### Увеличение размера виртуальных дисков

Если вы выходите за рамки пространства жесткого диска, которое выбрали при создании виртуальной машины, проблему можно решить по совету из руководства VirtualBox [`VBoxManage modifyhd`](https://www.virtualbox.org/manual/ch08.html#VBoxManage-modifyvdi). Эта команда работает только для динамически расширяемых дисков VDI и VHD . Если вы хотите изменить размер фиксированного виртуального диска, можете использовать нижеописанный трюк, который работает и на виртуальной машине Windows, и в UNIX-подобных системах.

Во-первых, создайте новый виртуальный диск рядом с тем, который вы хотите увеличить:

 $ VBoxManage createhd -filename *new.vdi* --size *10000*

где размер указан в MiB, в этом примере 10000MiB ~ = 10GiB, *new.vdi* - имя создаваемого нового виртуального диска.

Далее старый виртуальный диск должен быть клонирован в новый(это может занять длительной время):

 $ VBoxManage clonehd *old.vdi* *ew.vdi* --existing

**Примечание:** По умолчанию, эта команда использует *Standard* (что соответствует динамическому выделению) формату файла диска, и, следовательно, не будет использовать тот же формат в качестве формата исходного виртуального диска. Если ваш *old.vdi* имеет фиксированный размер, и вы хотите, чтобы новый диск был тоже фиксированным, добавьте параметр `--variant Fixed`.

Отключите старый диск и установите новый, обязательно заменив все выделенные курсивом аргументы на свои:

```
$ VBoxManage storageattach *VM_name* --storagectl *SATA* --port *0* --medium none
$ VBoxManage storageattach *VM_name* --storagectl *SATA* --port *0* --medium *new.vdi* --type hdd

```

Чтобы получить имя контроллера диска и номер порта, вы можете использовать команду `VBoxManage showvminfo *VM_name*`. Среди вывода вы получите такой результат (то, что вы ищете выделено курсивом):

```
[...]
Storage Controller Name (0):            IDE
Storage Controller Type (0):            PIIX4
Storage Controller Instance Number (0): 0
Storage Controller Max Port Count (0):  2
Storage Controller Port Count (0):      2
Storage Controller Bootable (0):        on
Storage Controller Name (1):            SATA
Storage Controller Type (1):            IntelAhci
Storage Controller Instance Number (1): 0
Storage Controller Max Port Count (1):  30
Storage Controller Port Count (1):      1
Storage Controller Bootable (1):        on
IDE (1, 0): Empty
*SATA* (*0*, 0): /home/wget/IT/Virtual_machines/GNU_Linux_distributions/ArchLinux_x64_EFI/Snapshots/{6bb17af7-e8a2-4bbf-baac-fbba05ebd704}.vdi (UUID: 6bb17af7-e8a2-4bbf-baac-fbba05ebd704)
[...]
```

Скачайте [GParted LiveCD](http://gparted.org/download.php) и установите его в качестве виртуального привода , загрузите вашу виртуальную машину, используйте увеличение / перемещение ваших разделов. По окончании работы отмонтируйте GParted LiveCD и перезагрузите машину.

**Примечание:** На GPT дисках, увеличение размера диска приведет к созданию резервной копии заголовка GPT в месте, отличном от конца устройства. GParted попросит, чтобы исправить проблему, нажать на *исправить* два раза. На дисках MBR такой проблемы не возникнет.

Наконец, отключите старый виртуальный диск в VirtualBox и удалите его:

```
$ VBoxManage closemedium disk *old.vdi*
$ rm *old.vdi*

```

### Замена виртуального диска из файла .vbox вручную

Если вы думаете, что редактирование простого *XML* файла более удобно, чем возня с GUI или `VBoxManage` и вы хотите заменить (или добавить) виртуальный диск в вашей виртуальной машине, просто замените GUID, местоположение файла и формат для ваших нужд в конфигурационном файле *.vbox*, соответствующем вашей виртуальной машине:

 `ArchLinux_vm.vbox`  `<HardDisk uuid="*{670157e5-8bd4-4f7b-8b96-9ee412a712b5}*" location="*ArchLinux_vm.vdi*" format="*VDI*" type="Normal"/>` 

в `<AttachedDevice>` (суб-тег `<StorageController>`) замените старый GUID на новый.

 `ArchLinux_vm.vbox` 
```
<AttachedDevice type="HardDisk" port="0" device="0">
  <Image uuid="*{670157e5-8bd4-4f7b-8b96-9ee412a712b5}*"/>
</AttachedDevice>
```

**Примечание:** Если вы не знаете GUID диска который вы хотите добавить, вы можете использовать `VBoxManage showhdinfo *file*`. Если раньше вы использовали `VBoxManage clonehd`, для копирования или конвертирования виртуальных дисков, он выводит GUID после завершения копирования / преобразования. Применение случайного GUID не работает, так как каждый [UUID хранится внутри любого образа диска](http://www.virtualbox.org/manual/ch05.html#cloningvdis).

### Клонирование виртуального диска и назначение ему нового UUID

UUID широко используются VirtualBox. Каждая виртуальная машина и каждый виртуальный диск виртуальной машины должны иметь разные UUID. Когда вы запускаете виртуальную машину в VirtualBox, он будет отслеживать все UUID. См [`VBoxManage list`](http://www.virtualbox.org/manual/ch08.html#vboxmanage-list), чтобы просмотреть список элементов, зарегистрированных в VirtualBox.

Если вы клонировали виртуальный диск вручную путем копирования файла виртуального диска, необходимо будет назначить новый UUID клонированному виртуальному диску. Вы можете использовать этот диск в той же виртуальной машине или даже в другой (если он уже открыт и таким образом зарегистрирован в VirtualBox).

Вы можете использовать эту команду, чтобы назначить новый UUID для вашего виртуального диска:

```
$ VBoxManage internalcommands sethduuid */path/to/disk.vdi*

```

**Совет:** В будущем, чтобы избежать копирования виртуального диска и назначения нового UUID вручную, используйте `[VBoxManage clonehd](http://www.virtualbox.org/manual/ch08.html#vboxmanage-clonevdi)`.

**Примечание:** Все указанные команды поддерживают [все форматы виртуальных дисков, поддерживаемые VirtualBox](#.D0.A4.D0.BE.D1.80.D0.BC.D0.B0.D1.82.D1.8B.2C_.D0.BF.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.B8.D0.B2.D0.B0.D0.B5.D0.BC.D1.8B.D0.B5_VirtualBox).

## Расширенная настройка

### Управление запуском виртуальной машины

#### Запуск виртуальный машин как сервиса systemd

 `/etc/systemd/system/vboxvmservice@.service` 
```
[Unit]
Description=VBox Virtual Machine %i Service
Requires=systemd-modules-load.service
After=systemd-modules-load.service

[Service]
User=*username*
Group=vboxusers
ExecStart=/usr/bin/VBoxHeadless -s %i
ExecStop=/usr/bin/VBoxManage controlvm %i savestate

[Install]
WantedBy=multi-user.target
```

**Примечание:** Замените `*username*` на имя вашего пользователя и добавьте его в группу `vboxusers`. Убедитесь, что это именно тот пользователь, который управляет созданием VM. Иначе ничего не получится

**Примечание:** Если у вас есть несколько машин запускаемых `Systemd`, и они завершаются некорректно, попробуйте добавить `RemainAfterExit=true` и `KillMode=none` в конец `[Service]` секции.

Для запуска VM начиная с следующей загрузки, выполните:

```
# systemctl enable vboxvmservice@*your_virtual_machine_name*

```

Для запуска же в текущий момент времени выполните:

```
# systemctl start vboxvmservice@*your_virtual_machine_name*

```

VirtualBox 4.2 [предоставляет](http://lifeofageekadmin.com/how-to-set-your-virtualbox-vm-to-automatically-startup/) для UNIX-like систем также другие способы автозапуска, без использования сервисов systemd.

#### Запуск виртуальной машины по горячей клавише

Может быть полезно запускать виртуальные машины непосредственно с клавиатуры вместо использования интерфейса VirtualBox (GUI или CLI). Для этого, вы можете просто определить ключевые привязки в `.xbindkeysrc`. Обратитесь к [Xbindkeys](/index.php/Xbindkeys_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xbindkeys (Русский)") для более подробной информации.

Например, запуск по `Fn+F3`:

```
"VBoxManage startvm 'Windows 7'"
m:0x0 + c:244
XF86Battery

```

**Примечание:** Если у вас есть пробел в имени виртуальной машины, то заключите его в одинарные апострофы как сделано в вышеуказанном примере.

### Использование конкретных устройств в виртуальной машине

#### Использование USB веб-камеры/микрофона

**Примечание:** Вам понадобятся установленные гостевые дополнения, прежде чем следовать приведенному ниже примеру. См. [Дополнения гостевой ОС](#.D0.9E.D0.B1.D1.80.D0.B0.D0.B7_.D0.B4.D0.B8.D1.81.D0.BA.D0.B0_.D1.81_.D0.B3.D0.BE.D1.81.D1.82.D0.B5.D0.B2.D1.8B.D0.BC.D0.B8_.D0.B4.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B5.D0.BD.D0.B8.D1.8F.D0.BC.D0.B8) для более подробной информации.

1.  Убедитесь, что виртуальная машина не работает, а веб-камера / микрофон не используется.
2.  Вызовите главное окно VirtualBox и перейдите к настройкам для Arch машины. Перейдите в раздел USB.
3.  Убедитесь, что стоит галочка "Включить USB-контроллер". Также убедитесь, что выбран пункт "Разрешить USB 2.0 (EHCI) контроллер"
4.  Нажмите кнопку "Добавить фильтр с устройства" (кабельное со значком «+»).
5.  Выберите USB веб-камеру/микрофон из списка.
6.  Нажмите кнопку ОК и запустите VM.

#### Обнаружение веб-камер и прочих USB устройств

Убедитесь, что вы фильтруете любые устройства, (кроме клавиатур или мышей), чтобы они не запускались при загрузке -это гарантирует, что ОС Windows обнаружит устройство при запуске.

### Доступ к гостевому серверу

Для доступа к [Apache серверу](https://en.wikipedia.org/wiki/Apache_HTTP_Server "wikipedia:Apache HTTP Server") в виртуальной машине только с хост-машины, выполните:

```
$ VBoxManage setextradata GuestName "VBoxInternal/Devices/*pcnet*/0/LUN#0/Config/Apache/HostPort" *8888*
$ VBoxManage setextradata GuestName "VBoxInternal/Devices/*pcnet*/0/LUN#0/Config/Apache/GuestPort" *80*
$ VBoxManage setextradata GuestName "VBoxInternal/Devices/*pcnet*/0/LUN#0/Config/Apache/Protocol" TCP

```

Where 8888 is the port the host should listen on and 80 is the port the VM will send Apache's signal on. Где 8888 порт должна слушать хост-система, а VM шлет сигнал Apache на 80 порт.

Чтобы использовать порт ниже, чем 1024 на хост-машине, изменения должны быть внесены в брандмауэр на этом хосте. Он также может быть настроен на работу с SSH или иных услуг путем изменения «Apache» с соответствующими сервисами и портами.

**Примечание:** `pcnet` относится к сетевой карте виртуальной машины. Если вы используете карту Intel в VM, необходимо изменить `pcnet` на `e1000`.

### D3D ускорение в гостевой Windows

Последние версии Virtualbox имеют поддержку ускорения OpenGL внутри гостевой ОС. Эта функция может быть включена галочкой в настройках машины (при установленных дополнениях гостевой ОС VirtualBox). Тем не менее, большинство игр под Windows используют Direct3D (часть DirectX), а не OpenGL, и, таким образом, этот метод не поможет. Тем не менее возможно получить ускоренное Direct3D в гостевой Windows, за счет заимствования D3D библиотеки из Wine, который переводит инструкции d3d под OpenGL, который и занимается ускорением. Эти библиотеки теперь являются частью дополнений гостевой ОС.

После включения OpenGL ускорения, как описано выше, перезагрузите гостевую ОС в безопасном режиме (нажмите F8 до появления экрана для Windows, но после исчезновения экрана Virtualbox), и установите дополнения гостевой ОС, во время установки установите галочку *Включить поддержку Direct3D*. Перезагрузитесь обратно в нормальный режим, и вы получите ускоренный Direct3D.

**Примечание:** Этот хак может может не работать для некоторых игр, в зависимости от того, какую аппаратную проверку они делают и какие части D3D они используют

**Примечание:** Хак был проверено на Windows XP, 7 и 8,1\. Если метод не работает на версии Windows, пожалуйста, добавьте эту информацию здесь.

### VirtualBox c USB-ключом

При использовании VirtualBox с USB-ключом, например, для запуска установленной машины с ISO-образа, вы вручную должны создать VDMK-файлы существующих приводов. Тем не менее, как только новые файлы VMDK сохраняться и вы перейдёте на другую машину, у вас могут снова возникнуть проблемы. Чтобы избавиться от этой проблемы, можно использовать следующий скрипт для запуска VirtualBox. Этот сценарий будет убирать старые файлов VMDK и создавать новые:

```
#!/bin/bash

# Erase old VMDK entries
rm ~/.VirtualBox/*.vmdk

# Clean up VBox-Registry
sed -i '/sd/d' ~/.VirtualBox/VirtualBox.xml

# Remove old harddisks from existing machines
find ~/.VirtualBox/Machines -name \*.xml | while read file; do
  line=`grep -e "type\=\"HardDisk\"" -n $file | cut -d ':' -f 1`
  if [ -n "$line" ]; then
    sed -i ${line}d $file
    sed -i ${line}d $file
    sed -i ${line}d $file
  fi
  sed -i "/rg/d" $file
done

# Delete prev-files created by VirtualBox
find  ~/.VirtualBox/Machines -name \*-prev -exec rm '{}' \;

# Recreate VMDKs
ls -l /dev/disk/by-uuid | cut -d ' ' -f 9,11 | while read ln; do
  if [ -n "$ln" ]; then
    uuid=`echo "$ln" | cut -d ' ' -f 1`
    device=`echo "$ln" | cut -d ' ' -f 2 | cut -d '/' -f 3 | cut -b 1-3`

    # determine whether drive is mounted already
    checkstr1=`mount | grep $uuid`
    checkstr2=`mount | grep $device`
    checkstr3=`ls ~/.VirtualBox/*.vmdk | grep $device`
    if [[ -z "$checkstr1" && -z "$checkstr2" && -z "$checkstr3" ]]; then
      VBoxManage internalcommands createrawvmdk -filename ~/.VirtualBox/$device.vmdk -rawdisk /dev/$device -register
    fi
  fi
done

# Start VirtualBox
VirtualBox

```

Обратите внимание, что ваш пользователь должен быть добавлен в группу `disk`, чтобы создать VMDKs из существующих приводов.

### Запуск установленного Arch Linux внутри VirtualBox

Если у вас есть дуалбут системы между Arch Linux и другими операционных системами, он может быстро стать утомительным для переключения туда-сюда, если вам нужно работать в обоих. Кроме того, с помощью виртуальных машин, у вас есть только крошечный фрагмент власти компьютера, который может привести к проблемам при работе на проектах, требующих производительности.

Это руководство позволит вам использовать в виртуальной машине, вашу родную установку Arch Linux, когда вы используете свою вторую операционную систему. Таким образом, вы сохраняете возможность запуска каждой операционной систему изначально, но есть возможность запустить установленный физически Arch Linux внутри виртуальной машины.

#### Убедитесь, что система наименования разделов не изменяется

В зависимости от настроек вашего жесткого диска, файлы устройств, представляющих свои жесткие диски могут выглядеть по-разному когда вы будете запускать установку Arch Linux - изначально или в виртуальной машине. Эта проблема возникает, например, при использовании [FakeRAID](/index.php/RAID#Implementation "RAID"). Поддельные RAID устройстве, будут перемещены в `/dev/mapper/` при запуске дистрибутива GNU/Linux , в то время как будут устройства по-прежнему доступны по отдельности. Тем не менее, в вашей виртуальной машине может оказаться без отображения в `/dev/sdaX` например, потому что драйвера, управляющие поддельными RAID в вашей локальной операционной системе (например, Windows) абстрагируются под поддельные RAID устройства.

Чтобы обойти эту проблему, мы должны будем использовать схему адресации, работающую в обеих системах. Это может быть достигнуто с помощью [UUIDs](/index.php/Fstab#UUIDs "Fstab") в файле `/etc/fstab`. Убедитесь, что ваш [fstab](/index.php/Fstab_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Fstab (Русский)") использует UUID - в противном случае решайте эту проблему. Читайте [Fstab](/index.php/Fstab "Fstab") и [Устойчивое именование разделов](/index.php/Persistent_block_device_naming "Persistent block device naming").

`/etc/fstab` не является единственным местом, где используются UUID. Менеджеры загрузчиков тоже их используют. Убедитесь, что они действительно используют UUID-ы.

	[GRUB Legacy](/index.php/GRUB_Legacy_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GRUB Legacy (Русский)")

Если вы все еще используете [GRUB Legacy](/index.php/GRUB_Legacy_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GRUB Legacy (Русский)"), может быть настало время его [обновить](/index.php/GRUB_Legacy#Upgrading_to_GRUB2 "GRUB Legacy"), так как этот пакет в настоящее время удален из официальных репозиториев Arch Linux. Если вы хотите сохранить его, отредактируйте `/boot/grub/menu.lst` и замените `root=/dev/sdXX` в загрузочной записи Arch Linux на Linux UUID `/dev/disk/by-uuid/`, соответствующий корневому разделу.

```
title  Arch Linux
root
kernel /vmlinuz-linux root=*/dev/disk/by-uuid/0a3407de-014b-458b-b5c1-848e92a327a3* ro vga=773
initrd /initramfs-linux-vbox.img

```

Предварительно создайте резервную копию файла на случай ошибок.

	[GRUB](/index.php/GRUB_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GRUB (Русский)")

Если вы работаете с самой последней версией [GRUB](/index.php/GRUB_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GRUB (Русский)"); у вас нет проблем. Это ещё одна причина для перехода на GRUB 2.

**Важно:**

*   Убедитесь, что ваш хост-раздел доступна только для чтения с вашей виртуальной машины Arch Linux. Это позволит избежать риска повреждения.
*   Вы никогда не должны позволять VirtualBox загружаться с момента загрузки вашей второй операционной системы, которая используется в качестве хоста для этой виртуальной машины! Возьмите, таким образом, за правило - особенно если ваша загрузка производится по умолчанию в другую операционную систему. Установите более большой тайм-аут или переместите систему ниже в порядке предпочтений.

#### Убедитесь в корректности образа mkinitcpio

Убедитесь, что в конфигурации вашего [mkinitcpio](/index.php/Mkinitcpio_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Mkinitcpio (Русский)") есть [хук](/index.php/Mkinitcpio_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.97.D0.B0.D0.BF.D1.80.D0.B5.D1.82_.D0.BE.D0.B1.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D1.87.D0.B8.D0.BA.D0.BE.D0.B2 "Mkinitcpio (Русский)") `block`:

 `/etc/mkinitcpio.conf` 
```
[...]
HOOKS="base udev autodetect modconf *block* filesystems keyboard fsck"
[...]
```

Если это не так, добавьте хук и сгенерируйте свой initramfs, с помощью команды `# mkinitcpio -p linux`, что [описано здесь более подробно](/index.php/Mkinitcpio_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BE.D0.B1.D1.80.D0.B0.D0.B7.D0.B0 "Mkinitcpio (Русский)").

#### Создание конфигурации виртуальной машины для загрузки с физического диска

##### Создайте потоковый(raw) образ .vmdk

Теперь нам нужно создать новую виртуальную машину, которая будет использовать [RAW диск](https://www.virtualbox.org/manual/ch09.html#rawdisk) в качестве виртуального диска, для этого мы будем использовать файл ~ 1Kib VMDK, которые будет сбрасываться на физический диск. VirtualBox не имеет этой опции в графическом интерфейсе, так что мы должны использовать консоль и внутреннюю команду из `VBoxManage`.

Загрузите хост, который будет использовать виртуальную машину Arch Linux.Команда должны быть адаптированы в соответствии с вашей хост-машиной.

	На хосте GNU/Linux

Существует 3 способа этого достичь: вход от суперпользователя, изменение прав доступа к устройству командой `chmod`, добавление пользователя в группу `disk`. Последний путь является более элегантным. Реализуем таким образом:

```
# gpasswd -a *your_user* disk

```

Применить новые параметры сейчас же:

```
$ newgrp

```

Теперь вы можете использовать следующую команду:

```
$ VBoxManage internalcommands createrawvmdk -filename */path/to/file.vmdk* -rawdisk */dev/sdb* -register 

```

Адаптируйте команду для ваших потребностей.

	На хосте с Windows

Откройте окно командной строки (необходимо запускать от имени администратора).
**Совет:** В Windows откройте меню Пуск / стартовый экран, введите `cmd`, и нажмите `Ctrl+Shift+Enter`, это ярлык для запуска выбранной программы с правами администратора.

В Windows наименование дисков отлично от UNIX. Используйте эту команду, чтобы определить значения в вашей системе Windows, и их расположение:

 `# wmic diskdrive get name,size,model` 
```
Model                               Name                Size
WDC WD40EZRX-00SPEB0 ATA Device     \\.\PHYSICALDRIVE1  4000783933440
KINGSTON SVP100S296G ATA Device     \\.\PHYSICALDRIVE0  96024821760
Hitachi HDT721010SLA360 ATA Device  \\.\PHYSICALDRIVE2  1000202273280
Innostor Ext. HDD USB Device        \\.\PHYSICALDRIVE3  1000202273280
```

В этом примере Windows называет диски `\\.\PhysicalDriveX`, Где X представляет собой число от 0, `\\.\PHYSICALDRIVE1` может быть сопоставим с `/dev/sdb` из терминологии Linux.

Для использования в командной строке `VBoxManage` в Windows, вы должны изменить текущую папку в папку установки VirtualBox, обычно это `cd C:\Program Files\Oracle\VirtualBox\`

```
# .\VBoxManage.exe internalcommands createrawvmdk -filename C:\file.vmdk -rawdisk \\.\PHYSICALDRIVE1

```

или использовать абсолютный путь:

```
# "C:\Program Files\Oracle\VirtualBox\VBoxManage.exe" internalcommands createrawvmdk -filename C:\file.vmdk -rawdisk \\.\PHYSICALDRIVE1

```

	На другой хост-OS

Есть и другие ограничения, касающиеся вышеприведенной команды, когда она используется в других операционных системах - таких как OS X. Прочитайте [внимательно руководство](https://www.virtualbox.org/manual/ch09.html#rawdisk), если это вас беспокоит.

##### Создание файла конфигурации виртуальной машины

**Примечание:**

*   Для использования команды VBoxManage в Windows, вам нужно сначало изменить текущую директорию в папку установки VirtualBox :

```
cd C:\Program Files\Oracle\VirtualBox\

```

*   Windows делает использование обратного слеша вместо слеша, пожалуйста, замените все вхождения / на \ в командах, которые вы будете использовать.

После этого мы должны создать новую машину (замените *VM_name* ная ваш вариант) и зарегистрировать её в VirtualBox.

```
$ VBoxManage createvm -name *VM_name* -register

```

Затем виртуальный диск должен быть подключен к машине. Это будет зависеть от того, находится ли корень в вашей оригинальной установке Arch Linux на IDE или контроллере SATA.

Если вам нужен контроллер IDE:

```
$ VBoxManage storagectl *VM_name* --name "IDE Controller" --add ide
$ VBoxManage storageattach machineA --storagectl "IDE Controller" --port 0 --device 0 --type hdd --medium /path/to/file.vmdk

```

В противном случае:

```
$ VBoxManage storagectl *VM_name* --name "SATA Controller" --add sata
$ VBoxManage storageattach machineA --storagectl "SATA Controller" --port 0 --device 0 --type hdd --medium /path/to/file.vmdk

```

В то время как вы продолжаете использовать интерфейс командной строки, рекомендуется использовать VirtualBox GUI, чтобы персонализировать настройки виртуальной машины. Необходимо указать аппаратную конфигурацию как можно ближе к родной машине: включение ускорения 3D, увеличение видеопамяти, установка сетевого интерфейса и т.д.

#### Установка дополнений гостевой ОС

Наконец, вы можете легко интегрировать Arch Linux с хост-системой и синхронизировать буфер обмена между двумя ОС. Обратитесь к [установке гостевых дополнений](#.D0.9E.D0.B1.D1.80.D0.B0.D0.B7_.D0.B4.D0.B8.D1.81.D0.BA.D0.B0_.D1.81_.D0.B3.D0.BE.D1.81.D1.82.D0.B5.D0.B2.D1.8B.D0.BC.D0.B8_.D0.B4.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B5.D0.BD.D0.B8.D1.8F.D0.BC.D0.B8) для этого.

**Важно:** Для [Xorg (Русский)](/index.php/Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xorg (Русский)"), чтобы работать в родной и в виртуальной машине, так как очевидно, он должен использовать другой драйвер, то лучше, если не будет `/etc/X11/xorg.conf` - так как Xorg будет собирать все, что необходимо на лету. Однако, если вам действительно нужно свою собственную конфигурацию Xorg, может быть, стоит установить используемые по умолчанию цели Systemd к `multi-user.target` с `# systemctl isolate graphical.target` (более [подробно](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.98.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D1.82.D0.B5.D0.BA.D1.83.D1.89.D0.B5.D0.B9_.D1.86.D0.B5.D0.BB.D0.B8 "Systemd (Русский)")). Таким образом, графический интерфейс будет отключен (т.е. Xorg не запустится) и после входа в систему вы сможете выполнить `startx` вручную с пользовательским `xorg.conf`.

### Физическая установка системы Arch Linux из VirtualBox

В некоторых случаях это может быть полезно для установки родной системы Arch Linux из другой операционной системы: один из способов достижения этой цели является выполнение установки через VirtualBox на [жёсткий диск](http://www.virtualbox.org/manual/ch09.html#rawdisk). Если существующая операционная система на основе Linux, вы можете рассмотреть [установку из существующего Linux](/index.php/Install_from_existing_Linux_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Install from existing Linux (Русский)") вместо этого.

Этот сценарий очень похож на [Запуск установленного ArchLinux в VirtualBox](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.BD.D0.BE.D0.B3.D0.BE_Arch_Linux_.D0.B2.D0.BD.D1.83.D1.82.D1.80.D0.B8_VirtualBox), но будет реализовывать эти шаги в другом порядке: начать с создания [.vmdk образа жёсткого диска](#.D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D0.B9.D1.82.D0.B5_.D0.BF.D0.BE.D1.82.D0.BE.D0.BA.D0.BE.D0.B2.D1.8B.D0.B9.28raw.29_.D0.BE.D0.B1.D1.80.D0.B0.D0.B7_.vmdk), а затем [создавать файл конфигурации виртуальной машины](#.D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5_.D1.84.D0.B0.D0.B9.D0.BB.D0.B0_.D0.BA.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D0.B8_.D0.B2.D0.B8.D1.80.D1.82.D1.83.D0.B0.D0.BB.D1.8C.D0.BD.D0.BE.D0.B9_.D0.BC.D0.B0.D1.88.D0.B8.D0.BD.D1.8B).

Теперь вы должны иметь рабочую конфигурацию виртуальной машины, чей виртуальный VMDK-диск связан с реальным диском. Процесс установки точно такой же, как и описанный в [пошаговой установке ArchLinux в VirtualBox](#.D0.9F.D0.BE.D1.88.D0.B0.D0.B3.D0.BE.D0.B2.D0.B0.D1.8F_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_Arch_Linux_.D0.BA.D0.B0.D0.BA_.D0.B3.D0.BE.D1.81.D1.82.D0.B5.D0.B2.D0.BE.D0.B9_.D0.9E.D0.A1), но сначала [убедитесь в постоянной схеме наименования разделов](#.D0.A3.D0.B1.D0.B5.D0.B4.D0.B8.D1.82.D0.B5.D1.81.D1.8C.2C_.D1.87.D1.82.D0.BE_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D0.B0_.D0.BD.D0.B0.D0.B8.D0.BC.D0.B5.D0.BD.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F_.D1.80.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB.D0.BE.D0.B2_.D0.BD.D0.B5_.D0.B8.D0.B7.D0.BC.D0.B5.D0.BD.D1.8F.D0.B5.D1.82.D1.81.D1.8F) и [корректности образа mkinitcpio](#.D0.A3.D0.B1.D0.B5.D0.B4.D0.B8.D1.82.D0.B5.D1.81.D1.8C_.D0.B2_.D0.BA.D0.BE.D1.80.D1.80.D0.B5.D0.BA.D1.82.D0.BD.D0.BE.D1.81.D1.82.D0.B8_.D0.BE.D0.B1.D1.80.D0.B0.D0.B7.D0.B0_mkinitcpio).

**Важно:**

*   Для BIOS и MBR дисков: не устанавливайте загрузчик внутри виртуальной машины - он не будет работать, так как MBR не связан с MBR вашей реальной машины, и виртуальный диск отображается только в реальном разделе без MBR
*   Для UEFI систем без [CSM](https://en.wikipedia.org/wiki/Unified_Extensible_Firmware_Interface#Compatibility_Support_Module "wikipedia:Unified Extensible Firmware Interface") и GPT дискa установка не будет работать вообще, так как:

*   [ESP](https://en.wikipedia.org/wiki/EFI_system_partition "wikipedia:EFI system partition") не отображается на виртуальный диск и Arch Linux требует, чтобы ядро Linux было на нём, чтобы загрузиться в качестве приложения EFI (смотрите статью [EFISTUB (Русский)](/index.php/EFISTUB_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "EFISTUB (Русский)"))
*   и efivars, если вы устанавливаете Arch Linux через VirtualBox, используя режим EFI, не загрузит ни одну из ваших реальных систем: записи Bootmanager не смогут быть зарегистрированы

*   Вот почему рекомендуется создавать разделы в родной установке. В противном случае разделы не будут приниматься во внимание в MBR / GPT таблице разделов

После завершения установки загрузите компьютер сперва с установочного носителя GNU/Linux (будь то Arch Linux или нет), выполните [chroot](/index.php/Installation_guide_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Chroot "Installation guide (Русский)") в установленной Arch Linux и установите и настройте [загрузчик](/index.php/Installation_guide_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.97.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D1.87.D0.B8.D0.BA "Installation guide (Русский)").

### Перемещение физически установленного Windows в виртуальную машину

Если вы хотите перенести существующую Windows на виртуальную машину, которая будет использоваться с VirtualBox на GNU/Linux, этот вариант использования для вас. В этом разделе описан перенос только Windows с использованием схемы MSDOS/Intel разделов. Ваш Windows должен находиться на первом после MBR разделе. Работа в других разделах доступна, но были не тестировалась (см [Известные ограничения](#.D0.98.D0.B7.D0.B2.D0.B5.D1.81.D1.82.D0.BD.D1.8B.D0.B5_.D0.BE.D0.B3.D1.80.D0.B0.D0.BD.D0.B8.D1.87.D0.B5.D0.BD.D0.B8.D1.8F) для более подробной информации)

**Важно:** Если вы используете OEM версию Windows, этот процесс является неправомочным по конечной пользовательской лицензии. Действительно, лицензия OEM, как правило, указывает, что Windows Install связана с аппаратными средствами. Сделайте так, что бы у вас был полный Windows Install или полная лицензия, прежде чем продолжить. Если у вас есть полная лицензию для Windows, но последний не приходит в объеме, ни в качестве специальной лицензии на нескольких компьютерах, это означает, что вы должны будете удалить родную установку после операции клонирования в VM.

Несколько задач необходимо выполнить внутри вашей Windows, а затем в хост-машине GNU/Linux.

#### Задачи в Windows

Первые три следующих моменты происходит от [этой устаревшей вики-страницы VirtualBox](https://www.virtualbox.org/wiki/Migrate_Windows#HAL), но обновляются здесь.

*   Удалите проверку IDE/ATA контроллеров (только Windows XP): Windows запоминает IDE/ATA после установки, и не будет загружаться, если он обнаружит что они изменились.Решение, предложенное Microsoft является повторным использованием того же контроллера или использовать один из той-же серии, что невозможно сделать, поскольку мы используем виртуальную машину. [MergeIDE](https://www.virtualbox.org/wiki/Migrate_Windows#HardDiskSupport), немецкий инструмент, разработан как другое решением, предложенное Microsoft. Решение в основном состоит в принятии всех IDE/ATA драйверов контроллера IDE, поддерживаемые Windows XP от первоначального архива драйвера, их установке и регистрации в реестре через Regedit.

*   Используйте правильный тип слоя абстрагирования оборудования (старые 32-битный Windows): Microsoft использует с 3 версии по умолчанию: `Hal.dll` (Standard PC), `Halacpi.dll` (ACPI HAL) и `halaacpi.dll` (ACPI HAL с IO APIC). Ваша Windows-установка могла устанавитmся с первого или второго варианта. В этом случае, пожалуйста, [отключите *Enable IO/APIC* в расширенных возможностях VirtualBox](https://www.virtualbox.org/manual/ch08.html#idp56927888).

*   Отключите драйвер AGP устройства (только устаревшие версии ОС Windows): Если у вас есть файлы `agp440.sys` или `intelppm.sys` внутри `C:\Windows\System32\drivers\`, то удалите его. Так как VirtualBox использует PCI виртуальную графическую карту, это может вызвать проблемы, когда используется драйвер AGP.

*   Создайте диск восстановления ОС Windows: В следующих шагах, если что-то испортится, вам нужно будет восстановить установку Windows. Убедитесь, что у вас есть установочного носителя под рукой, или создайте через *Создать диск восстановления* в Vista SP1, *Создать диск восстановления системы* в Windows 7 или *Создать диск восстановления* в Windows 8.x).

#### Задачи в GNU/Linux

*   Уменьшите родной размер раздела Windows, для чего нужен `ntfsresize` из пакета [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g). Вы определяете размер, который будет равен размере VDI, который будет создан на следующем шаге. Если этот размер будет слишком мал, вы можете сломать ваш Windows и он может не загружаться вообще.

	Включите параметр `--no-action` для тестового запуска:

	 `# ntfsresize --no-action --size *52Gi* */dev/sda1*` 

	Если только предыдущий тест прошел успешно, необходимо выполнить следующую команду снова, только без вышеупомянутого параметра `--no-action`.

*   Установите VirtualBox на ваш GNU/Linux-хост (см. [подробнее](#.D0.9F.D0.BE.D1.88.D0.B0.D0.B3.D0.BE.D0.B2.D0.B0.D1.8F_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BD.D0.B0_.D1.85.D0.BE.D1.81.D1.82-.D0.BA.D0.BE.D0.BC.D0.BF.D1.8C.D1.8E.D1.82.D0.B5.D1.80_.D0.BF.D0.BE.D0.B4_.D1.83.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5.D0.BC_Arch_Linux) ).

*   Создайте образ диска для Windows от начала диска до конца первого раздела, на котором находится Windows. Копирование с начала диска необходимо потому, что пространство MBR в начале привода должно быть перенесено на виртуальный диск вместе с самим Windows. В этом примере следующие два раздела `sda2` и `sda3` будут позже удалены из таблицы разделов и загрузчик MBR будет обновляться.

	 `# sectnum=$(( $(cat /sys/block/''sda/sda1''/start) + $(cat /sys/block/''sda/sda1''/size) ))` 

Использование `cat /sys/block/*sda/sda1*/size` выведет количество секторов первого раздела диска `sda`. Адаптируйте команду, если это вам нужно.

	 `# dd if=''/dev/sda'' bs=512 count=$sectnum | VBoxManage convertfromraw stdin ''windows.vdi'' $(( $sectnum * 512 ))` 

	Мы должны показать размер в байтах, `$(( $sectnum * 512 ))` преобразует номера секторов в байты.

*   Так как вы создали свой образ диска с правами администратора, установите права доступа на образ диска: `# chown $USER:users windows.vdi`.

*   Создайте Ваш файл конфигурации виртуальной машины - используйте виртуальный диск, созданный ранее в качестве основного виртуального жесткого диска.

*   Постарайтесь загрузиться с виртуальной машины Windows (может работать). Во-первых, хотя бы отключите восстановление дисков из процесса загрузки, так как это может помешать (и, вероятно, будет мешать) загрузиться в безопасном режиме.

*   Попытка загрузить виртуальную машину в безопасном режиме (нажмите клавишу F8 до логотипа Windows) ... при возникновении вопросов о загрузке, читайте [Исправление MBR и загрузчика Microsoft](#.D0.98.D1.81.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_MBR_.D0.B8_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D1.87.D0.B8.D0.BA.D0.B0_Microsoft). В безопасном режиме вероятно будут установлен драйверы. Кроме того, установите Дополнения гостевой ОС через меню *Devices* > *Insert Guest Additions CD image...*. Если новое диалоговое окно не отображается, перейдите к компакт-дискам и запустите программу установки вручную.

*   Наконец-то у вас есть необходимый Windows в виртуальной машине. Ознакомьтесь с [известными ограничениями](#.D0.98.D0.B7.D0.B2.D0.B5.D1.81.D1.82.D0.BD.D1.8B.D0.B5_.D0.BE.D0.B3.D1.80.D0.B0.D0.BD.D0.B8.D1.87.D0.B5.D0.BD.D0.B8.D1.8F).

#### Исправление MBR и загрузчика Microsoft

Если ваша виртуальная машина с Windows отказывается загружаться, вам, возможно, потребуется применить следующие изменения в вашей виртуальной машине.

*   Начальная загрузка GNU/Live внутри виртуальной машины, прежде чем загрузится ОС Windows .

*   Удалить другие записи разделы с MBR виртуального диска. В самом деле, так как мы скопировали MBR и только раздел Windows, записи, относящихся к другим разделам по-прежнему присутствуют в MBR, но разделы ведь больше не доступны. Используйте `fdisk`, чтобы добиться этого, например.

```
fdisk ''/dev/sda''
Command (m for help): a
Partition number (''1-3'', default ''3''): ''1''
```

*   Запишите обновленную таблицу разделов на диск (это будет пересозданием MBR) с помощью `m` команды в окружении `fdisk`.

*   Используйте [testdisk](https://www.archlinux.org/packages/?name=testdisk) (см. [здесь](http://www.cgsecurity.org/index.html?testdisk.html) для более подробной информации), чтобы добавить общий MBR:

	 `# testdisk > *Disk /dev/sda...'* > [Proceed] >  [Intel] Intel/PC partition > [MBR Code] Write TestDisk MBR to first sector > Write a new copy of MBR code to first sector? (Y/n) > Y > Write a new copy of MBR code, confirm? (Y/N) > A new copy of MBR code has been written. You have to reboot for the change to take effect. > [OK]` 

*   С новым MBR и обновленной таблицей разделов, ваша виртуальная машина с Windows должна загрузиться. Если вы все еще сталкиваетесь с вопросами, загрузите диск восстановления Windows с предыдущей стадии, и внутри вашей среды Windows RE, выполняйте команды [описанные здесь](http://support.microsoft.com/kb/927392).

#### Известные ограничения

*   Ваша виртуальная машина может иногда зависать и забивать оперативную память, это может быть вызвано конфликтующими драйверами , установленными внутри виртуальной машины Windows. Удачи вам найти их!
*   Дополнительное ПО ожидало драйвер,который не может установиться из-за невозможности отключения / деинсталляции старого драйвера.
*   Ваша Windows должна находиться в первом разделе для описанного выше процесса, чтобы заработать. Если это требование не выполнено, система может работать, но это не было испытаны. Это потребует либо копирования MBR и редактирования в шестнадцатеричном коде, см. [VirtualBox: загрузка клонированного диска](http://superuser.com/questions/237782/virtualbox-booting-cloned-disk/253417#253417) или потребуется исправить таблицу разделов [вручную](http://gparted.org/h2-fix-msdos-pt.php) или восстанавливать Windows с диска восстановления, созданного в предыдущем шаге. Рассмотрим нашу установку окна на втором раздела; мы скопируем MBR, второму разделу, где лужит образ диска `VBoxManage convertfromraw` необходимо общее количество байтов, которые будут записаны: Вычислим как сумму размера MBR (начало первого раздела) плюс размер второго (Windows) раздела.`{ dd if=/dev/sda bs=512 count=$(cat /sys/block/sda/sda1/start) ; dd if=/dev/sda2 bs=512 count=$(cat /sys/block/sda/sda2/size) ; } | VBoxManage convertfromraw stdin windows.vdi $(( ($(cat /sys/block/sda/sda1/start) + $(cat /sys/block/sda/sda2/size)) * 512 ))`.

## Возможные проблемы

### VERR_ACCESS_DENIED

Чтобы получить доступ к образу vdmk, расположенного на хосте под Windows, запустите VirtualBox GUI от имени администратора.

### Клавиатура и мышка заблокированы виртуальной машиной

Это означает, что ваша виртуальная машина захватила ввод клавиатуры и мышки. Просто нажмите правый `Ctrl` и ваши устройства ввода будут доступны в основной системе.

Для того, чтобы управление мышкой возвращалось основной ОС при выходе курсора за границы окна виртуальной машины, без нажатия каких-либо клавиш, и для возможности бесшовной интеграции, установите гостевое дополнение на виртуальную машину. Читайте шаг [#Установка гостевых дополнений](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.B3.D0.BE.D1.81.D1.82.D0.B5.D0.B2.D1.8B.D1.85_.D0.B4.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B5.D0.BD.D0.B8.D0.B9) если вы новичок в Arch Linux, или читайте официальную справку VirtualBox.

### Не могу отправить комбинацию CTRL+ALT+Fn в виртуальную машину

Если в вашей виртуальной машине установлен дистрибутив GNU/Linux и вы хотите открыть новую оболочку TTY нажатием `Ctrl+Alt+F2` или выйти из X сессии с помощью `Ctrl+Alt+Backspace`, просто нажав это сочетание клавиш без какой-либо адаптации, гостевая машина его не получит и основная ОС (если это тоже дистрибутив GNU/Linux) распознает это сочетание клавиш. Для отправки `Ctrl+Alt+F2` на виртуальную машину нужно просто нажать ваш *Host Key* (обычно это правый `Ctrl`) и одновременно нажать `F2`.

### Исправление проблем в ISO-образах

В то время как VirtualBox монтирует оригинальный образы ISO без проблем, есть такие форматы образов, которые не могут надежно быть преобразованы в ISO. Например, ccd2iso игнорирует .ccd и .sub файлы, что может привести к созданию образа диска с разбитыми файлами.

В этом случае вам придется использовать [CDemu](/index.php/CDemu "CDemu") для Linux внутри VirtualBox или любую другую утилиту, предназначенную для монтирования образов дисков.

### VirtualBox GUI не видит мою тему GTK 2x/3x

Смотрите [Единый интерфейс GTK/QT приложений](/index.php/Uniform_look_for_Qt_and_GTK_applications_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Uniform look for Qt and GTK applications (Русский)") для получения информации о настройке GUI Qt в GTK-окружениях.

### OpenBSD не работает при недоступных инструкциях виртуализации

В то время как OpenBSD отлично работает на других гипервизорах без включенной виртуализации (VT-х AMD-V), виртуальная машина с OpenBSD работает в VirtualBox без этих инструкций некорректно, выдавая кучу ошибок сегментации. Запуская VirtualBox с аргументом *-norawr0* [можно избавиться от этой проблемы](https://www.virtualbox.org/ticket/3947). Вы можете сделать это следующим образом:

```
$ VBoxSDL -norawr0 -vm *имя_OpenBSD_VM*

```

### VBOX_E_INVALID_OBJECT_STATE (0x80BB0007)

Это может произойти при некорректном завершении виртуальной машины. Разблокировка машины тривиальна:

```
$ VBoxManage controlvm *virtual_machine_name* poweroff

```

### Подсистема USB не работает в хост-машине или гостевой ОС

Ваш пользователь должен быть в группе `vboxusers`, и вы должны установить [пакет дополнений](#.D0.9F.D0.B0.D0.BA.D0.B5.D1.82_.D0.B4.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B5.D0.BD.D0.B8.D0.B9), если хотите иметь поддержку USB 2\. Тогда вы сможете включить USB 2 в настройках виртуальной машины и добавить один или несколько фильтров для устройств, которые будут иметь доступ из гостевой ОС.

Иногда, на старых Linux-хостах, подсистема USB не распознается автоматически и выдает ошибку `Could not load the Host USB Proxy service: VERR_NOT_FOUND` или при невидимом USB-диске в хост-машине, [даже когда пользователь находится в группе **vboxusers**](HTTPS://bbs.archlinux.org/viewtopic.php?id=121377,). Эта проблема происходит из-за того, что VirtualBox переключается с *usbfs* на *sysfs* с версии 3.0.8\. Если хост-машина не распознаёт этого изменения, вы можете вернуться к старому поведению, определив следующую переменную окружения в любом файле, которые конфигурирует вашу оболочку (например, в `~/.bashrc`, если вы используете *bash*):

 `~/.bashrc`  `VBOX_USB=usbfs` 

Затем убедитесь, что, окружающая среда приняла это изменение (перелогиньтесь, запустите новый экземпляр оболочки или перезагрузитесь).

Также убедитесь, что ваш пользователь состоит в группе `storage`.

### Ошибка создания сетевого интерфейса "host-only"

Убедитесь в том, что все модули ядра VirtualBox загружены (см. [Загрузка модулей ядра VirtualBox](#.D0.97.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B0_.D0.BC.D0.BE.D0.B4.D1.83.D0.BB.D0.B5.D0.B9_.D1.8F.D0.B4.D1.80.D0.B0_VirtualBox)).

### WinXP: глубина цвета не может превышать 16 цветов

Если Вы работаете в 16-битной глубине цвета, то значки будут отображаться некорректно. Тем не менее, при попытке изменить глубину цвета на более высокий уровень, система может ограничить вас с более низким разрешением или просто не позволит вам изменить глубину вообще. Чтобы это исправить, запустите `regedit` в Windows и добавьте следующий ключ реестра для виртуальной машины Windows XP:

```
[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services]
"ColorDepth"=dword:00000004

```

Затем обновите глубину цвета в "Свойствах рабочего стола". Если ничего не происходит, заставьте экран перерисоваться (например, нажмите`Host+f`).

### Использование последовательных портов в гостевой ОС

Проверьте наличие прав для доступа к последовательным портам:

```
$ /bin/ls -l /dev/ttyS*
crw-rw---- 1 root uucp 4, 64 Feb  3 09:12 /dev/ttyS0
crw-rw---- 1 root uucp 4, 65 Feb  3 09:12 /dev/ttyS1
crw-rw---- 1 root uucp 4, 66 Feb  3 09:12 /dev/ttyS2
crw-rw---- 1 root uucp 4, 67 Feb  3 09:12 /dev/ttyS3

```

Добавьте пользователя в группу `uucp`

```
# gpasswd -a $USER uucp 

```

и перелогиньтесь.

### Windows 8.x ошибка 0x000000C4

Если вы получаете этот код ошибки при загрузке, даже при выбранном типе OS Win 8, попробуйте включить инструкцию процессора `CMPXCHG16B`:

```
$ vboxmanage setextradata *virtual_machine_name* VBoxInternal/CPUM/CMPXCHG16B 1

```

### Windows 8 VM вылетает при загрузке с ошибкой "ERR_DISK_FULL"

Если ваша Windows 8 не запускается, VirtualBox выдаёт ошибку что виртуальный диск заполнен, но тем не менее вы уверены что диск не является заполненным, откройте настройки виртуальной машины *Настройки>Память>Контроллер: SATA* и выберите *Use Host I/O Cache*.

### Гостевая ОС Linux выдает искажённый или запаздывающий звук

Аудио драйвер AC97 в ядре linux иногда неправильно считывает время из Virtual Box, что приводит к различным искажениям звука. Для исправления проблемы, создайте файл `/etc/modprobe.d` со следующим содержанием:

```
options snd-intel8x0 ac97_clock=48000

```

### Гостевая ОС зависает после запуска Xorg

Неисправные или отсутствующие драйверы могут привести к остановке после запуска Xorg, см., например, [[2]](https://bbs.archlinux.org/viewtopic.php?pid=1167838) и [[3]](https://bbs.archlinux.org/viewtopic.PHP?ID=156079). Попробуйте отключить 3D-ускорение в *Настройки> Дисплей*, и проверьте, все ли драйверы [Xorg](/index.php/Xorg "Xorg") установлены.

### Исчезновение пунктов меню и ошибка "NS_ERROR_FAILURE"

Если после первого запуска машины вы столкнулись с такой ошибкой:

```
Failed to open a session for the virtual machine debian.
Could not open the medium '/home/.../VirtualBox VMs/debian/debian.qcow'.
QCow: Reading the L1 table for image '/home/.../VirtualBox VMs/debian/debian.qcow' failed (VERR_EOF).
VD: error VERR_EOF opening image file '/home/.../VirtualBox VMs/debian/debian.qcow' (VERR_EOF).

Result Code: 
NS_ERROR_FAILURE (0x80004005)
Component: 
Medium

```

Выйдите из VirtualBox, удалите все файлы новой машины и из файла конфигурации VirtualBox удалите последнюю строку в `MachineRegistry` меню:

 `~/.config/VirtualBox/VirtualBox.xml` 
```
...
<MachineRegistry>
  <MachineEntry uuid="{00000000-0000-0000-0000-000000000000}" src="/home/void/VirtualBox VMs/debian/debian.vbox"/>
  <MachineEntry uuid="{00000000-0000-0000-0000-000000000000}" src="/home/void/VirtualBox VMs/ubuntu/ubuntu.vbox"/>
  ~~<MachineEntry uuid="{00000000-0000-0000-0000-000000000000}" src="/home/void/VirtualBox VMs/lastvmcausingproblems/lastvmcausingproblems.qcow"/>~~
</MachineRegistry>
...
```

Это иногда происходит при выборе *QCOW*/*QCOW2*/*QED* формата виртуального диска.

### "Указанный путь не существует. Проверьте путь и попробуйте еще раз." Ошибка в гостевой ОС Windows

Это сообщение об ошибке часто появляется при работе с расширением .exe который требует привелегий администратора из общей папки в гостевой Windows. См. [отчет об ошибке](https://www.virtualbox.org/ticket/5732).

Есть несколько способов обойти ошибку:

1.  Отключить UAC с помощью Панель управления -> Центр поддержки -> "Settings Change User Account Control" из левой боковой панели -> Установить ползунок "Никогда не уведомлять» -> OK и перезагрузить ОС
2.  Скопируйте файл из папки общего доступа в гостевую ОС и запустите оттуда

### Не работают 64-битные гостевые ОС

При запуске клиента VM, если никакие 64-битные варианты не доступны, убедитесь что ваши возможности виртуализации процессора (обычно с именем `VT-X`) включены в BIOS.

## Смотрите также

*   [Руководство пользователя VirtualBox](https://www.virtualbox.org/manual/UserManual.html)
*   [Википедия:VirtualBox](https://ru.wikipedia.org/wiki/VirtualBox)