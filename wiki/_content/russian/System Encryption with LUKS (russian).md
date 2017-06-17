Из проекта cryptsetup [wiki](https://gitlab.com/cryptsetup/cryptsetup/wikis/DMCrypt):

Device-mapper - это инфраструктура в ядре Linux 2.6 и 3.x, которая обеспечивает общий способ создания виртуальных уровней блочных устройств. Device-mapper обеспечивает прозрачное шифрование блочных устройств с использованием API-интерфейса ядра crypto. Пользователь может в основном указать один из симметричных шифров, режим шифрования, ключ (любого разрешенного размера), режим генерации iv, а затем пользователь может создать новое блочное устройство в / dev. Процесс записи и чтения на этом устройстве будет зашифрован. Вы можете подключить свою файловую систему к нему, как обычно, или к устройству dm-crypt с помощью другого устройства, такого как RAID или LVM. Базовая документация таблицы сопоставления dm-crypt поставляется с исходным кодом ядра, а последняя версия доступна в репозитории git.

## Contents

*   [1 Общие сценарии](#.D0.9E.D0.B1.D1.89.D0.B8.D0.B5_.D1.81.D1.86.D0.B5.D0.BD.D0.B0.D1.80.D0.B8.D0.B8)
*   [2 Подготовка устройств](#.D0.9F.D0.BE.D0.B4.D0.B3.D0.BE.D1.82.D0.BE.D0.B2.D0.BA.D0.B0_.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2)
*   [3 Шифрование устройства](#.D0.A8.D0.B8.D1.84.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2.D0.B0)
*   [4 Конфигурация системы](#.D0.9A.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D1.8F_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.8B)
*   [5 Шифрование подкачки](#.D0.A8.D0.B8.D1.84.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BF.D0.BE.D0.B4.D0.BA.D0.B0.D1.87.D0.BA.D0.B8)
*   [6 Детали](#.D0.94.D0.B5.D1.82.D0.B0.D0.BB.D0.B8)

## Общие сценарии

В этой части представлены общие сценарии использования «dm-crypt» для шифрования системных или отдельных точек монтирования файловой системы. Это означает отправную точку для ознакомления с различными практическими процедурами шифрования. Сценарии пересекаются с другими подстраницами, где это необходимо.

См. [Dm-crypt/Encrypting a non-root file system](/index.php/Dm-crypt/Encrypting_a_non-root_file_system "Dm-crypt/Encrypting a non-root file system"), если вам нужно зашифровать устройство, которое не используется для загрузки системы, например [partition](/index.php/Dm-crypt/Encrypting_a_non-root_file_system#Partition "Dm-crypt/Encrypting a non-root file system") или [loop device](/index.php/Dm-crypt/Encrypting_a_non-root_file_system#Loop_device "Dm-crypt/Encrypting a non-root file system").

См. [Dm-crypt/Encrypting an entire system](/index.php/Dm-crypt/Encrypting_an_entire_system "Dm-crypt/Encrypting an entire system"), если вы хотите зашифровать всю систему, в частности корневой раздел. Рассмотрены несколько сценариев, в том числе использование «dm-crypt» с расширением «LUKS», «простой» режим шифрования и шифрования и «LVM».

## Подготовка устройств

[Dm-crypt/Drive preparation](/index.php/Dm-crypt/Drive_preparation "Dm-crypt/Drive preparation") работает с такими операциями, как [безопасное стирание диска](/index.php/Dm-crypt/Drive_preparation#Secure_erasure_of_the_hard_disk_drive "Dm-crypt/Drive preparation") и «dm-crypt» для специфичного [разбиения на разделы](/index.php/Dm-crypt/Drive_preparation#Partitioning "Dm-crypt/Drive preparation").

## Шифрование устройства

[Dm-crypt/Device encryption](/index.php/Dm-crypt/Device_encryption "Dm-crypt/Device encryption") описывает, как вручную использовать dm-crypt для шифрования системы с помощью команды [cryptsetup](/index.php/Dm-crypt/Device_encryption#Cryptsetup_usage "Dm-crypt/Device encryption"). В нем описаны примеры [опций для шифрования с dm-crypt](/index.php/Dm-crypt/Device_encryption#Encryption_options_with_dm-crypt "Dm-crypt/Device encryption"), посвященные созданию [ключевых файлов](/index.php/Dm-crypt/Device_encryption#Keyfiles "Dm-crypt/Device encryption"), специфичные команды LUKS для [управления ключами](/index.php/Dm-crypt/Device_encryption#Key_management "Dm-crypt/Device encryption"), а также для [Резервное копирование и восстановление](/index.php/Dm-crypt/Device_encryption#Backup_and_restore "Dm-crypt/Device encryption").

## Конфигурация системы

[Dm-crypt/System configuration](/index.php/Dm-crypt/System_configuration "Dm-crypt/System configuration") показывает, как настроить [mkinitcpio](/index.php/Dm-crypt/System_configuration#mkinitcpio "Dm-crypt/System configuration"), [загрузчик](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration") и [Crypttab](/index.php/Crypttab "Crypttab") при шифровании системы.

## Шифрование подкачки

[Dm-crypt/Swap encryption](/index.php/Dm-crypt/Swap_encryption "Dm-crypt/Swap encryption") описывает, как добавить раздел подкачки в зашифрованную систему, если это необходимо. Раздел подкачки также должен быть зашифрован, чтобы защитить любые данные, выгруженные системой. В этой части описаны методы [без](/index.php/Dm-crypt_with_LUKS/Swap_Encryption#Without_suspend-to-disk_support "Dm-crypt with LUKS/Swap Encryption") и [с](/index.php/Dm-crypt_with_LUKS/Swap_Encryption#With_suspend-to-disk_support "Dm-crypt with LUKS/Swap Encryption") поддержкой спящего режима для диска.

## Детали

[Dm-crypt/Specialties](/index.php/Dm-crypt/Specialties "Dm-crypt/Specialties") занимается специальными операциями, такими как [Защита незашифрованного загрузочного раздела](/index.php/Dm-crypt/Specialties#Securing_the_unencrypted_boot_partition "Dm-crypt/Specialties"), [использование зашифрованных ключей GPG или OpenSSL](/index.php/Dm-crypt/Specialties#Using_GPG_or_OpenSSL_Encrypted_Keyfiles "Dm-crypt/Specialties"), метод [загрузки и разблокировки через сеть](/index.php/Dm-crypt/Specialties#Remote_unlocking_of_the_root_.28or_other.29_partition "Dm-crypt/Specialties"), так же для [настройка опции монтирования discard для функции TRIM в SSD дисках](/index.php/Dm-crypt/Specialties#Discard.2FTRIM_support_for_solid_state_drives_._28SSD.29 "Dm-crypt/Specialties") и разделы, посвященные [хукам шифрования при нескольких дисках](/index.php/Dm-crypt/Specialties#The_encrypt_hook_and_multiple_disks "Dm-crypt/Specialties").