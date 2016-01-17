# PulseAudio/Troubleshooting (Русский)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

**Эта страница нуждается в сопроводителе**

Статья не гарантирует актуальность информации. Помогите русскоязычному сообществу поддержкой подобных страниц. См. [Команда переводчиков ArchWiki](/index.php/%D0%9A%D0%BE%D0%BC%D0%B0%D0%BD%D0%B4%D0%B0_%D0%BF%D0%B5%D1%80%D0%B5%D0%B2%D0%BE%D0%B4%D1%87%D0%B8%D0%BA%D0%BE%D0%B2_ArchWiki "Команда переводчиков ArchWiki")

**Состояние перевода:** На этой странице представлен перевод статьи [PulseAudio/Troubleshooting](/index.php/PulseAudio/Troubleshooting "PulseAudio/Troubleshooting"). Дата последней синхронизации: 31 декабря 2015‎. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=PulseAudio/Troubleshooting&diff=0&oldid=411367).

Смотрите основную статью [PulseAudio (Русский)](/index.php/PulseAudio_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PulseAudio (Русский)").

## Contents

*   [1 Звук](#.D0.97.D0.B2.D1.83.D0.BA)
    *   [1.1 Автоматический бесшумный режим](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B9_.D0.B1.D0.B5.D1.81.D1.88.D1.83.D0.BC.D0.BD.D1.8B.D0.B9_.D1.80.D0.B5.D0.B6.D0.B8.D0.BC)
    *   [1.2 Аудиоустройство с отключенным звуком](#.D0.90.D1.83.D0.B4.D0.B8.D0.BE.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2.D0.BE_.D1.81_.D0.BE.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.BD.D1.8B.D0.BC_.D0.B7.D0.B2.D1.83.D0.BA.D0.BE.D0.BC)
    *   [1.3 Приложение с отключенным звуком](#.D0.9F.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D0.B5_.D1.81_.D0.BE.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.BD.D1.8B.D0.BC_.D0.B7.D0.B2.D1.83.D0.BA.D0.BE.D0.BC)
    *   [1.4 Настройка громкости не работает должным образом](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.B3.D1.80.D0.BE.D0.BC.D0.BA.D0.BE.D1.81.D1.82.D0.B8_.D0.BD.D0.B5_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D0.B5.D1.82_.D0.B4.D0.BE.D0.BB.D0.B6.D0.BD.D1.8B.D0.BC_.D0.BE.D0.B1.D1.80.D0.B0.D0.B7.D0.BE.D0.BC)
    *   [1.5 Громкость приложений меняется, когда регулируется Общая громкость](#.D0.93.D1.80.D0.BE.D0.BC.D0.BA.D0.BE.D1.81.D1.82.D1.8C_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D0.B9_.D0.BC.D0.B5.D0.BD.D1.8F.D0.B5.D1.82.D1.81.D1.8F.2C_.D0.BA.D0.BE.D0.B3.D0.B4.D0.B0_.D1.80.D0.B5.D0.B3.D1.83.D0.BB.D0.B8.D1.80.D1.83.D0.B5.D1.82.D1.81.D1.8F_.D0.9E.D0.B1.D1.89.D0.B0.D1.8F_.D0.B3.D1.80.D0.BE.D0.BC.D0.BA.D0.BE.D1.81.D1.82.D1.8C)
    *   [1.6 Звук становится каждый раз громче, как только запускается новое приложение](#.D0.97.D0.B2.D1.83.D0.BA_.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.B8.D1.82.D1.81.D1.8F_.D0.BA.D0.B0.D0.B6.D0.B4.D1.8B.D0.B9_.D1.80.D0.B0.D0.B7_.D0.B3.D1.80.D0.BE.D0.BC.D1.87.D0.B5.2C_.D0.BA.D0.B0.D0.BA_.D1.82.D0.BE.D0.BB.D1.8C.D0.BA.D0.BE_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA.D0.B0.D0.B5.D1.82.D1.81.D1.8F_.D0.BD.D0.BE.D0.B2.D0.BE.D0.B5_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D0.B5)
    *   [1.7 На звуковой карте M-Audio Audiophile 2 496 звук только Mono](#.D0.9D.D0.B0_.D0.B7.D0.B2.D1.83.D0.BA.D0.BE.D0.B2.D0.BE.D0.B9_.D0.BA.D0.B0.D1.80.D1.82.D0.B5_M-Audio_Audiophile_2_496_.D0.B7.D0.B2.D1.83.D0.BA_.D1.82.D0.BE.D0.BB.D1.8C.D0.BA.D0.BE_Mono)
    *   [1.8 Нет звука ниже определённого уровня](#.D0.9D.D0.B5.D1.82_.D0.B7.D0.B2.D1.83.D0.BA.D0.B0_.D0.BD.D0.B8.D0.B6.D0.B5_.D0.BE.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D1.91.D0.BD.D0.BD.D0.BE.D0.B3.D0.BE_.D1.83.D1.80.D0.BE.D0.B2.D0.BD.D1.8F)
    *   [1.9 Тихая громкость внутреннего микрофона](#.D0.A2.D0.B8.D1.85.D0.B0.D1.8F_.D0.B3.D1.80.D0.BE.D0.BC.D0.BA.D0.BE.D1.81.D1.82.D1.8C_.D0.B2.D0.BD.D1.83.D1.82.D1.80.D0.B5.D0.BD.D0.BD.D0.B5.D0.B3.D0.BE_.D0.BC.D0.B8.D0.BA.D1.80.D0.BE.D1.84.D0.BE.D0.BD.D0.B0)
    *   [1.10 Клиенты изменяют основной выход звука (т. е. переход громкости к 100% после запущенного приложения)](#.D0.9A.D0.BB.D0.B8.D0.B5.D0.BD.D1.82.D1.8B_.D0.B8.D0.B7.D0.BC.D0.B5.D0.BD.D1.8F.D1.8E.D1.82_.D0.BE.D1.81.D0.BD.D0.BE.D0.B2.D0.BD.D0.BE.D0.B9_.D0.B2.D1.8B.D1.85.D0.BE.D0.B4_.D0.B7.D0.B2.D1.83.D0.BA.D0.B0_.28.D1.82._.D0.B5._.D0.BF.D0.B5.D1.80.D0.B5.D1.85.D0.BE.D0.B4_.D0.B3.D1.80.D0.BE.D0.BC.D0.BA.D0.BE.D1.81.D1.82.D0.B8_.D0.BA_100.25_.D0.BF.D0.BE.D1.81.D0.BB.D0.B5_.D0.B7.D0.B0.D0.BF.D1.83.D1.89.D0.B5.D0.BD.D0.BD.D0.BE.D0.B3.D0.BE_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F.29)
    *   [1.11 Нет звука после возобновления из спящего режима](#.D0.9D.D0.B5.D1.82_.D0.B7.D0.B2.D1.83.D0.BA.D0.B0_.D0.BF.D0.BE.D1.81.D0.BB.D0.B5_.D0.B2.D0.BE.D0.B7.D0.BE.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D1.8F_.D0.B8.D0.B7_.D1.81.D0.BF.D1.8F.D1.89.D0.B5.D0.B3.D0.BE_.D1.80.D0.B5.D0.B6.D0.B8.D0.BC.D0.B0)
    *   [1.12 Каналы ALSA отключены, когда наушники подсоединены/отсоединены неправильно](#.D0.9A.D0.B0.D0.BD.D0.B0.D0.BB.D1.8B_ALSA_.D0.BE.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D1.8B.2C_.D0.BA.D0.BE.D0.B3.D0.B4.D0.B0_.D0.BD.D0.B0.D1.83.D1.88.D0.BD.D0.B8.D0.BA.D0.B8_.D0.BF.D0.BE.D0.B4.D1.81.D0.BE.D0.B5.D0.B4.D0.B8.D0.BD.D0.B5.D0.BD.D1.8B.2F.D0.BE.D1.82.D1.81.D0.BE.D0.B5.D0.B4.D0.B8.D0.BD.D0.B5.D0.BD.D1.8B_.D0.BD.D0.B5.D0.BF.D1.80.D0.B0.D0.B2.D0.B8.D0.BB.D1.8C.D0.BD.D0.BE)
*   [2 Микрофон](#.D0.9C.D0.B8.D0.BA.D1.80.D0.BE.D1.84.D0.BE.D0.BD)
    *   [2.1 PulseAudio не обнаруживает микрофон](#PulseAudio_.D0.BD.D0.B5_.D0.BE.D0.B1.D0.BD.D0.B0.D1.80.D1.83.D0.B6.D0.B8.D0.B2.D0.B0.D0.B5.D1.82_.D0.BC.D0.B8.D0.BA.D1.80.D0.BE.D1.84.D0.BE.D0.BD)
    *   [2.2 PulseAudio использует неправильный микрофон](#PulseAudio_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D1.83.D0.B5.D1.82_.D0.BD.D0.B5.D0.BF.D1.80.D0.B0.D0.B2.D0.B8.D0.BB.D1.8C.D0.BD.D1.8B.D0.B9_.D0.BC.D0.B8.D0.BA.D1.80.D0.BE.D1.84.D0.BE.D0.BD)
    *   [2.3 Нет микрофона на ThinkPad T400/T500/T420](#.D0.9D.D0.B5.D1.82_.D0.BC.D0.B8.D0.BA.D1.80.D0.BE.D1.84.D0.BE.D0.BD.D0.B0_.D0.BD.D0.B0_ThinkPad_T400.2FT500.2FT420)
    *   [2.4 Нет микрофона на Acer Aspire One](#.D0.9D.D0.B5.D1.82_.D0.BC.D0.B8.D0.BA.D1.80.D0.BE.D1.84.D0.BE.D0.BD.D0.B0_.D0.BD.D0.B0_Acer_Aspire_One)
    *   [2.5 Статический шум в записи микрофона](#.D0.A1.D1.82.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B9_.D1.88.D1.83.D0.BC_.D0.B2_.D0.B7.D0.B0.D0.BF.D0.B8.D1.81.D0.B8_.D0.BC.D0.B8.D0.BA.D1.80.D0.BE.D1.84.D0.BE.D0.BD.D0.B0)
        *   [2.5.1 Определение звуковых карт в системе (1/5)](#.D0.9E.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B7.D0.B2.D1.83.D0.BA.D0.BE.D0.B2.D1.8B.D1.85_.D0.BA.D0.B0.D1.80.D1.82_.D0.B2_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D0.B5_.281.2F5.29)
        *   [2.5.2 Определить частоту дискретизации звуковой карты (2/5)](#.D0.9E.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D0.B8.D1.82.D1.8C_.D1.87.D0.B0.D1.81.D1.82.D0.BE.D1.82.D1.83_.D0.B4.D0.B8.D1.81.D0.BA.D1.80.D0.B5.D1.82.D0.B8.D0.B7.D0.B0.D1.86.D0.B8.D0.B8_.D0.B7.D0.B2.D1.83.D0.BA.D0.BE.D0.B2.D0.BE.D0.B9_.D0.BA.D0.B0.D1.80.D1.82.D1.8B_.282.2F5.29)
        *   [2.5.3 Установка частоты дескритизации в настройках PulseAudio (3/5)](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D1.87.D0.B0.D1.81.D1.82.D0.BE.D1.82.D1.8B_.D0.B4.D0.B5.D1.81.D0.BA.D1.80.D0.B8.D1.82.D0.B8.D0.B7.D0.B0.D1.86.D0.B8.D0.B8_.D0.B2_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0.D1.85_PulseAudio_.283.2F5.29)
        *   [2.5.4 Перезапустите PulseAudio для применения новых настроек (4/5)](#.D0.9F.D0.B5.D1.80.D0.B5.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D1.82.D0.B8.D1.82.D0.B5_PulseAudio_.D0.B4.D0.BB.D1.8F_.D0.BF.D1.80.D0.B8.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D1.8F_.D0.BD.D0.BE.D0.B2.D1.8B.D1.85_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B5.D0.BA_.284.2F5.29)
        *   [2.5.5 Наконец, проверьте запись и её воспроизведение (5/5)](#.D0.9D.D0.B0.D0.BA.D0.BE.D0.BD.D0.B5.D1.86.2C_.D0.BF.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D1.8C.D1.82.D0.B5_.D0.B7.D0.B0.D0.BF.D0.B8.D1.81.D1.8C_.D0.B8_.D0.B5.D1.91_.D0.B2.D0.BE.D1.81.D0.BF.D1.80.D0.BE.D0.B8.D0.B7.D0.B2.D0.B5.D0.B4.D0.B5.D0.BD.D0.B8.D0.B5_.285.2F5.29)
    *   [2.6 Нет микрофона в Steam или Skype с enable-remixing = no](#.D0.9D.D0.B5.D1.82_.D0.BC.D0.B8.D0.BA.D1.80.D0.BE.D1.84.D0.BE.D0.BD.D0.B0_.D0.B2_Steam_.D0.B8.D0.BB.D0.B8_Skype_.D1.81_enable-remixing_.3D_no)
*   [3 Качество звука](#.D0.9A.D0.B0.D1.87.D0.B5.D1.81.D1.82.D0.B2.D0.BE_.D0.B7.D0.B2.D1.83.D0.BA.D0.B0)
    *   [3.1 Включить отмену Эха/Шума](#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B8.D1.82.D1.8C_.D0.BE.D1.82.D0.BC.D0.B5.D0.BD.D1.83_.D0.AD.D1.85.D0.B0.2F.D0.A8.D1.83.D0.BC.D0.B0)
    *   [3.2 Глюки, пропуски или потрескивания](#.D0.93.D0.BB.D1.8E.D0.BA.D0.B8.2C_.D0.BF.D1.80.D0.BE.D0.BF.D1.83.D1.81.D0.BA.D0.B8_.D0.B8.D0.BB.D0.B8_.D0.BF.D0.BE.D1.82.D1.80.D0.B5.D1.81.D0.BA.D0.B8.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F)
    *   [3.3 Определение номера фрагмента по умолчанию и размера буфера в PulseAudio](#.D0.9E.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BD.D0.BE.D0.BC.D0.B5.D1.80.D0.B0_.D1.84.D1.80.D0.B0.D0.B3.D0.BC.D0.B5.D0.BD.D1.82.D0.B0_.D0.BF.D0.BE_.D1.83.D0.BC.D0.BE.D0.BB.D1.87.D0.B0.D0.BD.D0.B8.D1.8E_.D0.B8_.D1.80.D0.B0.D0.B7.D0.BC.D0.B5.D1.80.D0.B0_.D0.B1.D1.83.D1.84.D0.B5.D1.80.D0.B0_.D0.B2_PulseAudio)
        *   [3.3.1 Поиск параметров вашего аудиоустройства (1/4)](#.D0.9F.D0.BE.D0.B8.D1.81.D0.BA_.D0.BF.D0.B0.D1.80.D0.B0.D0.BC.D0.B5.D1.82.D1.80.D0.BE.D0.B2_.D0.B2.D0.B0.D1.88.D0.B5.D0.B3.D0.BE_.D0.B0.D1.83.D0.B4.D0.B8.D0.BE.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2.D0.B0_.281.2F4.29)
        *   [3.3.2 Вычисление размера вашего фрагмента в миллисекундах и количества фрагментов (2/4)](#.D0.92.D1.8B.D1.87.D0.B8.D1.81.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D1.80.D0.B0.D0.B7.D0.BC.D0.B5.D1.80.D0.B0_.D0.B2.D0.B0.D1.88.D0.B5.D0.B3.D0.BE_.D1.84.D1.80.D0.B0.D0.B3.D0.BC.D0.B5.D0.BD.D1.82.D0.B0_.D0.B2_.D0.BC.D0.B8.D0.BB.D0.BB.D0.B8.D1.81.D0.B5.D0.BA.D1.83.D0.BD.D0.B4.D0.B0.D1.85_.D0.B8_.D0.BA.D0.BE.D0.BB.D0.B8.D1.87.D0.B5.D1.81.D1.82.D0.B2.D0.B0_.D1.84.D1.80.D0.B0.D0.B3.D0.BC.D0.B5.D0.BD.D1.82.D0.BE.D0.B2_.282.2F4.29)
        *   [3.3.3 Редактирование конфигурационного файла PulseAudio (3/4)](#.D0.A0.D0.B5.D0.B4.D0.B0.D0.BA.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BA.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D0.BE.D0.BD.D0.BD.D0.BE.D0.B3.D0.BE_.D1.84.D0.B0.D0.B9.D0.BB.D0.B0_PulseAudio_.283.2F4.29)
        *   [3.3.4 Перезапуск демона PulseAudio (4/4)](#.D0.9F.D0.B5.D1.80.D0.B5.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.B4.D0.B5.D0.BC.D0.BE.D0.BD.D0.B0_PulseAudio_.284.2F4.29)
    *   [3.4 Прерывистый звук с аналогового объемного звучания](#.D0.9F.D1.80.D0.B5.D1.80.D1.8B.D0.B2.D0.B8.D1.81.D1.82.D1.8B.D0.B9_.D0.B7.D0.B2.D1.83.D0.BA_.D1.81_.D0.B0.D0.BD.D0.B0.D0.BB.D0.BE.D0.B3.D0.BE.D0.B2.D0.BE.D0.B3.D0.BE_.D0.BE.D0.B1.D1.8A.D0.B5.D0.BC.D0.BD.D0.BE.D0.B3.D0.BE_.D0.B7.D0.B2.D1.83.D1.87.D0.B0.D0.BD.D0.B8.D1.8F)
    *   [3.5 Тормозит звук](#.D0.A2.D0.BE.D1.80.D0.BC.D0.BE.D0.B7.D0.B8.D1.82_.D0.B7.D0.B2.D1.83.D0.BA)
    *   [3.6 Искажённый звук](#.D0.98.D1.81.D0.BA.D0.B0.D0.B6.D1.91.D0.BD.D0.BD.D1.8B.D0.B9_.D0.B7.D0.B2.D1.83.D0.BA)
*   [4 Hardware and Cards](#Hardware_and_Cards)
    *   [4.1 No HDMI sound output after some time with the monitor turned off](#No_HDMI_sound_output_after_some_time_with_the_monitor_turned_off)
    *   [4.2 No cards](#No_cards)
    *   [4.3 Starting an application interrupts other app's sound](#Starting_an_application_interrupts_other_app.27s_sound)
    *   [4.4 The only device shown is "dummy output" or newly connected cards aren't detected](#The_only_device_shown_is_.22dummy_output.22_or_newly_connected_cards_aren.27t_detected)
    *   [4.5 No HDMI 5/7.1 Selection for Device](#No_HDMI_5.2F7.1_Selection_for_Device)
    *   [4.6 Failed to create sink input: sink is suspended](#Failed_to_create_sink_input:_sink_is_suspended)
    *   [4.7 Simultaneous output to multiple sound cards / devices](#Simultaneous_output_to_multiple_sound_cards_.2F_devices)
    *   [4.8 Simultaneous output to multiple sinks on the same sound card not working](#Simultaneous_output_to_multiple_sinks_on_the_same_sound_card_not_working)
    *   [4.9 Some profiles like SPDIF are not enabled by default on the card](#Some_profiles_like_SPDIF_are_not_enabled_by_default_on_the_card)
*   [5 Bluetooth](#Bluetooth)
    *   [5.1 Отключение поддержки Bluetooth](#.D0.9E.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.BA.D0.B8_Bluetooth)
    *   [5.2 Bluetooth headset replay problems](#Bluetooth_headset_replay_problems)
    *   [5.3 Автоматическое переключение на Bluetooth или USB-гарнитуру](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.BE.D0.B5_.D0.BF.D0.B5.D1.80.D0.B5.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BD.D0.B0_Bluetooth_.D0.B8.D0.BB.D0.B8_USB-.D0.B3.D0.B0.D1.80.D0.BD.D0.B8.D1.82.D1.83.D1.80.D1.83)
    *   [5.4 Устройство сопряжено, но не проигрывает звук](#.D0.A3.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2.D0.BE_.D1.81.D0.BE.D0.BF.D1.80.D1.8F.D0.B6.D0.B5.D0.BD.D0.BE.2C_.D0.BD.D0.BE_.D0.BD.D0.B5_.D0.BF.D1.80.D0.BE.D0.B8.D0.B3.D1.80.D1.8B.D0.B2.D0.B0.D0.B5.D1.82_.D0.B7.D0.B2.D1.83.D0.BA)
*   [6 Applications](#Applications)
    *   [6.1 Flash content](#Flash_content)
    *   [6.2 Ошибка с правами доступа](#.D0.9E.D1.88.D0.B8.D0.B1.D0.BA.D0.B0_.D1.81_.D0.BF.D1.80.D0.B0.D0.B2.D0.B0.D0.BC.D0.B8_.D0.B4.D0.BE.D1.81.D1.82.D1.83.D0.BF.D0.B0)
    *   [6.3 Audacity](#Audacity)
*   [7 Other Issues](#Other_Issues)
    *   [7.1 Bad configuration files](#Bad_configuration_files)
    *   [7.2 Can't update configuration of sound device in pavucontrol](#Can.27t_update_configuration_of_sound_device_in_pavucontrol)
    *   [7.3 Failed to create sink input: sink is suspended](#Failed_to_create_sink_input:_sink_is_suspended_2)
    *   [7.4 Pulse overwrites ALSA settings](#Pulse_overwrites_ALSA_settings)
    *   [7.5 Prevent Pulse from restarting after being killed](#Prevent_Pulse_from_restarting_after_being_killed)
    *   [7.6 Daemon startup failed](#Daemon_startup_failed)
        *   [7.6.1 Outputs by PulseAudio error status check utilities](#Outputs_by_PulseAudio_error_status_check_utilities)
    *   [7.7 Daemon already running](#Daemon_already_running)
    *   [7.8 Subwoofer stops working after end of every song](#Subwoofer_stops_working_after_end_of_every_song)
    *   [7.9 Unable to select surround configuration other than "Surround 4.0"](#Unable_to_select_surround_configuration_other_than_.22Surround_4.0.22)
    *   [7.10 Realtime scheduling](#Realtime_scheduling)
    *   [7.11 pactl "invalid option" error with negative percentage arguments](#pactl_.22invalid_option.22_error_with_negative_percentage_arguments)
    *   [7.12 Fallback device is not respected](#Fallback_device_is_not_respected)

## Звук

Здесь Вы найдете некоторые подсказки по проблемам звука и почему Вы ничего не можете услышать.

### Автоматический бесшумный режим

Автоматический бесшумный режим может быть включен изначально. Его можно легко отключить с помощью `alsamixer`.

Для подробностей смотрите [http://superuser.com/questions/431079/how-to-disable-auto-mute-mode](http://superuser.com/questions/431079/how-to-disable-auto-mute-mode)

Для сохранения текущих настроек, как опций по умолчанию, выполните от имени суперпользователя (root) `alsactl store`

### Аудиоустройство с отключенным звуком

Если нет звука при использовании [ALSA](/index.php/ALSA "ALSA"), попытайтесь включить звуковую карту. Чтобы сделать это, запустите `alsamixer`, и убедитесь, что каждый столбец имеет под ним зелёное значение `00` (можно переключать путём нажатия `m`):

$ alsamixer-c 0

**Обратите внимание:** alsamixer не скажет Вам, какое устройство вывода установлено как значение по умолчанию. Одна из возможных причин отсутствия звука после установки состоит в том, что PulseAudio обнаруживает неправильное устройство вывода как значение по умолчанию. Установите [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol) и проверьте, существует ли какой-нибудь вывод на панели pavucontrol, например, при проигрывании файла _.wav_.

### Приложение с отключенным звуком

Если у определенного приложения отключен звук, или он тихий, в то время как все остальные приложения в порядке. Это может произойти из-за индивидуальной настройки `sink-input`. Выполните с приложением, у которого нарушен звук:

```
$ pacmd list-sink-inputs

```

Найдите и запишите `index` соответствия `sink input`.`properties:` `application.name` и `application.process.binary`, среди прочего, должны помочь здесь. Убедитесь, что присутствуют нормальные настройки, в частности те `muted` и `volume`. Если у устройства вывода отключен звук, его можно включить:

```
$ pacmd set-sink-input-mute <index> false

```

Если нужна корректировка громкости, она может быть установлена на 100%:

```
$ pacmd set-sink-input-volume <index> 0x10000

```

**Обратите внимание:** Если `pacmd` выдаёт `0 sink input(s)`, перепроверьте, что приложение воспроизводит звук. Если звук всё ещё отсутствует, проверьте, что другие приложения показывают как устройство вывода.

### Настройка громкости не работает должным образом

Проверьте: `/usr/share/pulseaudio/alsa-mixer/paths/analog-output.conf.common`

Если громкость, кажется, не постепенно увеличивается/постепенно уменьшается должным образом используя `alsamixer` или `amixer`, это может быть связано с PulseAudio, имеющего большее число инкрементов (65537, чтобы быть точным). Попытайтесь использовать большие значения при изменении громкости (например, `amixer set Master 655+`).

### Громкость приложений меняется, когда регулируется Общая громкость

Это вызвано тем, что PulseAudio использует "плоскую регулировку громкости" (flat-volumes) по умолчанию, вместо относительной регулировки громкости, по сравнению с абсолютной общей регулировкой громкостью. Если это поведение вызывает неудобства, относительная громкость может быть включена путем отключения плоской громкости в файле настроек демона PulseAudio:

 `/etc/pulse/daemon.conf or ~/.config/pulse/daemon.conf` 

```
flat-volumes = no

```

и затем перезапустите PulseAudio выполнив:

```
$ pulseaudio -k
$ pulseaudio --start

```

### Звук становится каждый раз громче, как только запускается новое приложение

По-умолчанию, кажется, как будто изменение громкости в приложении меняет общую громкость системы, а не только соответствующего приложения. Следовательно, настройки приложения громкости на старте заставляют системную громкость "прыгать".

Исправьте это путем отключения "плоской громкости", как продемонстрировано в предыдущем разделе. Когда Pulse после нескольких секунд вернёт приложению "не изменять больше глобальную громкость", и установит собственный уровень громкости приложения.

**Обратите внимание:** Ранее установленный и удаленный pulseaudio-equalizer может оставить настройки в `~/.config/pulse/default.pa` или `~/.pulse/default.pa`, которые также могут доставить неприятности увеличения звука. Закомментируйте эти настройки, при необходимости.

### На звуковой карте M-Audio Audiophile 2 496 звук только Mono

Добавьте следующее:

 `/etc/pulseaudio/default.pa` 

```
load-module module-alsa-sink sink_name=delta_out device=hw:M2496 format=s24le channels=10 channel_map=left,right,aux0,aux1,aux2,aux3,aux4,aux5,aux6,aux7
load-module module-alsa-source source_name=delta_in device=hw:M2496 format=s24le channels=12 channel_map=left,right,aux0,aux1,aux2,aux3,aux4,aux5,aux6,aux7,aux8,aux9
set-default-sink delta_out
set-default-source delta_in

```

### Нет звука ниже определённого уровня

Известная проблема (не исправление): [https://bugs.launchpad.net/ubuntu/+source/pulseaudio/+bug/223133](https://bugs.launchpad.net/ubuntu/+source/pulseaudio/+bug/223133)

Если звук не играет, когда громкость PulseAudio регулируется ниже определенного уровня, попробуйте установить `ignore_dB=1` в `/etc/pulse/default.pa`:

 `/etc/pulse/default.pa` 

```
load-module module-udev-detect ignore_dB=1

```

Однако следует помнить, что это может привести к ошибке предотвращения PulseAudio чтобы включить колонки, когда наушники или другие аудио устройства выключены.

### Тихая громкость внутреннего микрофона

Если у вас низкая громкость звука, на внутреннем микрофоне ноутбука, попытайтесь установить:

 `/etc/pulse/default.pa` 

```
set-source-volume 1 300000

```

### Клиенты изменяют основной выход звука (т. е. переход громкости к 100% после запущенного приложения)

Если изменение громкости в конкретных приложениях или просто запуск приложения изменяет громкость воспроизведения, это происходит скорее всего из-за режима "плоская громкость" в PulseAudio. Перед отключением, пользователи KDE должны попытаться снизить громкость их системы уведомлений в _System Settings -> Application and System Notifications -> Manage Notifications_ ( _Системные настройки -> приложения и уведомлений системы -> Управление Уведомлениями_ на вкладке _Настройки воспроизведения_), на что-то разумное. Тут не поможет изменение _звуков событий_, громкости в KMix или другом приложении громкости микшера. Это должно заставить режим "плоской громкости" работать как задумано, если он не работает, некоторые другие приложения, скорее всего, запрашивают громкость 100%, когда что-то воспроизводят. Если все остальное не помогает, вы можете попробовать отключить "плоскую громкость":

 `/etc/pulse/daemon.conf` 

```
flat-volumes = no

```

Затем перезапустите демон PulseAudio:

```
# pulseaudio -k
# pulseaudio --start

```

### Нет звука после возобновления из спящего режима

Если звук обычно работает, но не работает после спящего режима, попытайтесь "перезагрузить" PulseAudio путем выполнения:

```
$ /usr/bin/pasuspender /bin/true

```

Это лучше, чем убить, и перезапустить его (`pulseaudio -k` сопровождаемый `pulseaudio --start`), потому что это уже не повредит запущенные приложения.

Если вышеупомянутое действие решает Вашу проблему, Вы можете автоматизировать это путем создания файла службы systemd.

1\. Создайте шаблонный файл службы в `/etc/systemd/system/resume-fix-pulseaudio@.service`:

```
[Unit]
Description=Fix PulseAudio after resume from suspend
After=suspend.target

[Service]
User=%I
Type=oneshot
Environment="XDG_RUNTIME_DIR=/run/user/%U"
ExecStart=/usr/bin/pasuspender /bin/true

[Install]
WantedBy=suspend.target

```

2\. Включите его для своей учетной записи пользователя

```
# systemctl enable resume-fix-pulseaudio@Здесь_ваше_имя_пользователя.service

```

3\. Перезагрузите systemd

```
# systemctl --system daemon-reload

```

### Каналы ALSA отключены, когда наушники подсоединены/отсоединены неправильно

Когда вы отключаете наушники или подключаете их, звук остается отключенным в alsamixer на неправильном канале, из-за его установки на 0%, вы сможете исправить это, открыв `/etc/pulse/default.pa` и закомментировав строку:

```
load-module module-switch-on-port-available

```

## Микрофон

### PulseAudio не обнаруживает микрофон

Определите номер карты и номер устройства Вашего микрофона:

```
 $ arecord -l
 **** List of CAPTURE Hardware Devices ****
 card 0: PCH [HDA Intel PCH], device 0: ALC269VC Analog [ALC269VC Analog]
 Subdevices: 1/1
 Subdevice #0: subdevice #0

```

В нотации hw:CARD,DEVICE, Вы определили вышеупомянутое устройство как `hw:0,0`.

Затем отредактируйте {`/etc/pulse/default.pa` и вставьте строку `load-module`, определяющую Ваше устройство следующим образом:

```
  load-module module-alsa-source device=hw:0,0
  # the line above should be somewhere before the line below
 .ifexists module-udev-detect.so

```

Наконец, перезапустите pulseaudio для применения новых настроек:

```
  $ pulseaudio -k ; pulseaudio -D

```

Если все работает правильно, то Вы должны увидеть, что микрофон обнаруживается при выполнении `pavucontrol` (на вкладке `Input Devices` ).

### PulseAudio использует неправильный микрофон

Если PulseAudio использует неправильный микрофон, и изменение Устройства ввода данных с Pavucontrol не помогало, смотрите alsamixer. Кажется, что Pavucontrol не всегда устанавливает входной источник правильно.

```
$ alsamixer

```

Нажмите `F6` и выберите свою звуковую карту, например, HDA Intel. Теперь нажмите `F5` для отображения всех элементов. Попытайтесь найти элемент: `Input Source`. С помощью клавиш Вверх / Вниз вы можете изменить источник входного сигнала.

Теперь попробуйте, правильный ли микрофон используется для записи.

### Нет микрофона на ThinkPad T400/T500/T420

Выплните:

```
alsamixer -c 0

```

Включите звук и максимизируйте громкость "Internal Mic" (внутреннего микрофона).

После того, как вы увидите устройство с помощью:

```
arecord -l

```

Вам возможно нужно скорректировать настройки. Микрофон и аудиоразъем являются дуплексными. Установите настройки внутреннего аудио pavucontrol в _Analog Stereo Duplex_ (_Аналоговому Дуплексу Стерео_).

### Нет микрофона на Acer Aspire One

Установите pavucontrol, отсоедините каналы микрофона и выключите левый на 0. Ссылка: [http://getsatisfaction.com/jolicloud/topics/deaf_internal_mic_on_acer_aspire_one#reply_2108048](http://getsatisfaction.com/jolicloud/topics/deaf_internal_mic_on_acer_aspire_one#reply_2108048)

### Статический шум в записи микрофона

Если мы получаем статический шум в записях Skype, gnome-sound-recorder, arecord, и т.д., то в этом случае частота дискретизации звуковой карты является неправильной. Именно поэтому в записях микрофона Linux существует статический шум. Для того чтобы это исправить, мы должны установить уровень выборки (sampling rate) в `/etc/pulse/daemon.conf` для звукового оборудования.

#### Определение звуковых карт в системе (1/5)

Для этого потребуются установленые и необходимые пакеты [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils):

 `$ arecord —list-devices` 

```

**** List of CAPTURE Hardware Devices ****
card 0: Intel [HDA Intel], device 0: ALC888 Analog [ALC888 Analog]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
card 0: Intel [HDA Intel], device 2: ALC888 Analog [ALC888 Analog]
  Subdevices: 1/1
  Subdevice #0: subdevice #0

```

`hw:0,0` является звуковой картой.

#### Определить частоту дискретизации звуковой карты (2/5)

 `arecord -f dat -r 60000 -D hw:0,0 -d 5 test.wav` 

```
"Recording WAVE 'test.wav' : Signed 16 bit Little Endian, Rate 60000 Hz, Stereo
Warning: rate is not accurate (requested = 60000Hz, **got = 96000Hz**)
please, try the plug plugin
```

заметьте, `got = 96000 Гц`. Это максимальная частота дискретизации нашей карты.

#### Установка частоты дескритизации в настройках PulseAudio (3/5)

Уровень дескритизации, по умолчанию, в PulseAudio:

 `$ grep "default-sample-rate" /etc/pulse/daemon.conf`  `; default-sample-rate = 44100` 

`44100` отключен, и должен быть изменен на `96000`:

```
# sed 's/; default-sample-rate = 44100/default-sample-rate = 96000/g' -i /etc/pulse/daemon.conf

```

#### Перезапустите PulseAudio для применения новых настроек (4/5)

```
$ pulseaudio -k
$ pulseaudio --start

```

#### Наконец, проверьте запись и её воспроизведение (5/5)

Давайте запишем речь с помощью микрофона в течение, 10 секунд. Удостоверьтесь, что микрофон не отключен.

```
$ arecord -f cd -d 10 test-mic.wav

```

После 10 секунд, давайте проиграем запись:

```
$ aplay test-mic.wav

```

Теперь, надеюсь, больше нет никакого статического шума на записи с микрофона

### Нет микрофона в Steam или Skype с enable-remixing = no

Когда Вы устанавите `enable-remixing = no` в `/etc/pulse/daemon.conf`, Вы можете обнаружить, что Ваш микрофон перестал работать в определенных приложениях, как Skype или Steam. Это происходит потому, что эти приложения получают микрофон как моно, только потому что отключен remixing, Pulseaudio больше не будет делать «remixing» Вашего стереомикрофона в моно.

Чтобы исправить это, вы должны сказать PulseAudio, что сделать за вас:

1\. Найти имя источника

```
# pacmd list-sources

```

Пример вывода отредактирован для краткости, имя которое вам нужно, выделено жирным:

```
   index: 2
       name: <**alsa_input.pci-0000_00_14.2.analog-stereo**>
       driver: <module-alsa-card.c>
       flags: HARDWARE HW_MUTE_CTRL HW_VOLUME_CTRL DECIBEL_VOLUME LATENCY DYNAMIC_LATENCY

```

2\. Добавить правило переназначения в `/etc/pulse/default.pa`, используйте имя, которое Вы нашли предыдущей командой, здесь мы будем использовать **alsa_input.pci-0000_00_14.2.analog-stereo** в качестве примера:

 `/etc/pulse/default.pa` 

```
### Remap microphone to mono
load-module module-remap-source master=alsa_input.pci-0000_00_14.2.analog-stereo master_channel_map=front-left,front-right channels=2 channel_map=mono,mono

```

3\. Перезапустите Pulseaudio

```
# pulseaudio -k

```

**Обратите внимание:** Pulseaudio может не запуститься, если Вы не вышли из программы, использовавшей микрофон (например, если Вы протестировали в Steam, прежде, чем изменить файл), тогда Вы должны выйти из приложения, и вручную запустить Pulseaudio

```
# pulseaudio --start

```

## Качество звука

### Включить отмену Эха/Шума

Arch не загружает по умолчанию модуль аннулирования эха Pulseaudio, поэтому, мы должны включить его `/etc/pulse/default.pa`. Сначала Вы можете проверить, пресутствует ли модуль с помощью `pacmd` и вводом `list-modules`. Если Вы не можете найти строку {`list-modules` Вы должны добавить

 `/etc/pulse/default.pa ` 

```
###  Включить отмену Эха/Шума
load-module module-echo-cancel

```

затем перезапустите Pulseaudio

```
pulseaudio -k
pulseaudio --start

```

и проверьте, активируется ли модуль, путем запуска `pavucontrol`. Под `Recoding` устройством ввода, должно показать `Echo-Cancel Source Stream from"`

### Глюки, пропуски или потрескивания

Более новая реализация звукового сервера PulseAudio использует звуковой планировщик на основе таймера, вместо традиционного подхода управления прерываниями.

Основанное на таймере планирование может представлять проблемы в некоторых драйверах ALSA. С другой стороны, другие драйверы могли бы глючить без него, проверьте и посмотрите что работает на вашей системе.

Для выключения основанного на таймере планирования добавьте `tsched=0` в `/etc/pulse/default.pa`:

 `/etc/pulse/default.pa`  `load-module module-udev-detect tsched=0` 

Затем перезапустите сервер PulseAudio:

```
pulseaudio -k
pulseaudio --start

```

Наоборот, для включения основанного на таймере планирования, если он уже не включен по умолчанию.

Если Вы используете Intel [IOMMU](https://en.wikipedia.org/wiki/IOMMU "wikipedia:IOMMU") и испытываете глюки и/или пропуски, добавьте `intel_iommu=igfx_off` к Вашей командной строке ядра.

Некоторым звуковым картам Intel использующим модуль `snd-hda-intel` нужны опции `vid=8086 pid=8ca0 snoop=0`. Для постоянной их установки создайте/измените следующий файл, включая строку ниже.

 `/etc/modprobe.d/sound.conf`  `options snd-hda-intel vid=8086 pid=8ca0 snoop=0` 

Сообщите о любых таких картах [PulseAudio Broken Sound Driver page](http://www.freedesktop.org/wiki/Software/PulseAudio/Backends/ALSA/BrokenDrivers/)

### Определение номера фрагмента по умолчанию и размера буфера в PulseAudio

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**Эта статья или раздел нуждается в улучшении грамматики, форматирования или стиля.**

**Причина:** Скопировано из темы Linux Mint с некоторыми дополнениями (обсуждение: [Talk:PulseAudio/Troubleshooting (Русский)#](https://wiki.archlinux.org/index.php/Talk:PulseAudio/Troubleshooting_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)))

#### Поиск параметров вашего аудиоустройства (1/4)

Чтобы узнать какие настройки буферизации имеет ваша звуковая карта, выполните:

```
$ echo autospawn = no >> ~/.config/pulse/client.conf
$ pulseaudio -k
$ LANG=C timeout --foreground -k 10 -s kill 10 pulseaudio -vvvv 2>&1 | grep device.buffering -B 10
$ sed -i '$d' ~/.config/pulse/client.conf

```

Вы увидите примерно следующий вывод для каждой звуковой карты, обнаруженной PulseAudio:

```
I: [pulseaudio] source.c:     alsa.long_card_name = "HDA Intel at 0xfa200000 irq 46"
I: [pulseaudio] source.c:     alsa.driver_name = "snd_hda_intel"
I: [pulseaudio] source.c:     device.bus_path = "pci-0000:00:1b.0"
I: [pulseaudio] source.c:     sysfs.path = "/devices/pci0000:00/0000:00:1b.0/sound/card0"
I: [pulseaudio] source.c:     device.bus = "pci"
I: [pulseaudio] source.c:     device.vendor.id = "8086"
I: [pulseaudio] source.c:     device.vendor.name = "Intel Corporation"
I: [pulseaudio] source.c:     device.product.name = "82801I (ICH9 Family) HD Audio Controller"
I: [pulseaudio] source.c:     device.form_factor = "internal"
I: [pulseaudio] source.c:     device.string = "front:0"
I: [pulseaudio] source.c:     device.buffering.buffer_size = "768000"
I: [pulseaudio] source.c:     device.buffering.fragment_size = "384000"

```

Обратите внимание на то, что значения buffer_size и fragment_size релевантны соответствующей звуковой карте.

#### Вычисление размера вашего фрагмента в миллисекундах и количества фрагментов (2/4)

Частота дискретизации и битовая глубина PulseAudio по умолчанию установлены на `44100Hz` @ `16 bits`.

При такой конфигурации нам нужен битрейт `44100`*`16` = `705600` битов в секунду. Для стерео - `1411200 bps`.

Давайте взглянем на параметры, которые мы нашли в предыдущем шаге:

```
device.buffering.buffer_size = "768000" => 768000/1411200 = 0.544217687075s = 544 msecs
device.buffering.fragment_size = "384000" => 384000/1411200 = 0.272108843537s = 272 msecs

```

#### Редактирование конфигурационного файла PulseAudio (3/4)

 `/etc/pulse/daemon.conf` 

```
; default-fragments = X
; default-fragment-size-msec = Y

```

В предыдущем шаге мы рассчитали размер фрагмента. Узнать количество фрагментов также просто: buffer_size/fragment_size. Ответ в нашем случае будет равен (`544/272`) `2`:

 `/etc/pulse/daemon.conf` 

```
; default-fragments = **2**
; default-fragment-size-msec = **272**
```

#### Перезапуск демона PulseAudio (4/4)

```
$ pulseaudio -k
$ pulseaudio --start

```

Для получения дополнительной информации смотрите: [тему на форуме Linux Mint](http://forums.linuxmint.com/viewtopic.php?f=42&t=44862)

### Прерывистый звук с аналогового объемного звучания

Канал низкочастотных эфектов (НЭ) не ремикширован по-умолчанию. Чтобы включить его, нужно изменить следующее в `/etc/pulse/daemon.conf`:

 `/etc/pulse/daemon.conf` 

```
enable-lfe-remixing = yes

```

### Тормозит звук

Эта проблема возникает из-за неправильного размера буфера. Сначала убедитесь, что переменные {ic|default-fragments}} и `default-fragment-size-msec` не установлены на нестандартные значения в файле `/etc/pulse/daemon.conf`. Если это не помогло, попробуйте установить эти переменные на следующие значения:

 `/etc/pulse/daemon.conf` 

```
default-fragments = 5
default-fragment-size-msec = 2
```

### Искажённый звук

Искажённый звук может быть вызван неправильно настроенной частотой дискретизации. Попробуйте следующие настройки:

 `/etc/pulse/daemon.conf`  `default-sample-rate = 48000` 

и перезапустите сервер PulseAudio.

Если искажённый звук возникает в приложениях, использующих [OpenAL](https://en.wikipedia.org/wiki/ru:OpenAL "wikipedia:ru:OpenAL"), поменяйте частоту дискретизации в `/etc/openal/alsoft.conf`:

 `/etc/openal/alsoft.conf`  `frequency = 48000` 

Установка PCM volume выше 0 dB может вызвать [клиппинг](https://en.wikipedia.org/wiki/ru:%D0%9A%D0%BB%D0%B8%D0%BF%D0%BF%D0%B8%D0%BD%D0%B3_(%D0%B0%D1%83%D0%B4%D0%B8%D0%BE) "wikipedia:ru:Клиппинг (аудио)"). Запуск `alsamixer` позволит вам обнаружить и исправить проблему. Обратите внимание, что ALSA не может [корректно экспортировать](http://www.freedesktop.org/wiki/Software/PulseAudio/Documentation/User/PulseAudioStoleMyVolumes) информацию о dB в PulseAudio. Попробуйте следующее:

 `/etc/pulse/default.pa`  `load-module module-udev-detect ignore_dB=1` 

и перезапустите сервер PulseAudio. Смотрите также [#No sound below a volume cutoff](#No_sound_below_a_volume_cutoff).

## Hardware and Cards

### No HDMI sound output after some time with the monitor turned off

The monitor is connected via HDMI/DisplayPort, and the audio jack is plugged in the headphone jack of the monitor, but PulseAudio insists that it is unplugged:

 `pactl list sinks` 

```
...
hdmi-output-0: HDMI / DisplayPort (priority: 5900, not available)
...

```

This leads to no sound coming from HDMI output. A workaround for this is to switch to another VT and back again. If that doesn't work, try: turn off your monitor, switch to another VT, turn on your monitor, and switch back. This problem has been reported by ATI/Nvidia/Intel users.

### No cards

If PulseAudio starts, run `pacmd list`. If no cards are reported, make sure that the ALSA devices are not in use:

```
$ fuser -v /dev/snd/*
$ fuser -v /dev/dsp

```

Make sure any applications using the pcm or dsp files are shut down before restarting PulseAudio.

### Starting an application interrupts other app's sound

If you have trouble with some applications (eg. Teamspeak, Mumble) interrupting sound output of already running applications (eg. Deadbeaf), you can solve this by commenting out the line `load-module module-role-cork` in `/etc/pulse/default.pa` like shown below:

 `/etc/pulse/default.pa` 

```
### Cork music/video streams when a phone stream is active
# load-module module-role-cork

```

Then restart pulseaudo by using your normal user account with

```
pulseaudio -k
pulseaudio --start

```

### The only device shown is "dummy output" or newly connected cards aren't detected

This may be caused by settings in `~/.asoundrc` overriding the system wide settings in `/etc/asound.conf`. This can be prevented by commenting out the last line of `~/.asoundrc` like so:

 `~/.asoundrc` 

```
# </home/_yourusername_/.asoundrc.asoundconf>

```

Maybe some program is monopolizing the audio device:

 `# fuser -v /dev/snd/*` 

```
                     USER       PID  ACCESS COMMAND
/dev/snd/controlC0:  root        931 F....  timidity
                     bob        1195 F....  panel-6-mixer
/dev/snd/controlC1:  bob        1195 F....  panel-6-mixer
                     bob        1215 F....  pulseaudio
/dev/snd/pcmC0D0p:   root        931 F...m  timidity
/dev/snd/seq:        root        931 F....  timidity
/dev/snd/timer:      root        931 f....  timidity

```

That means timidity blocks PulseAudio from accessing the audio devices. Just killing timidity will make the sound work again.

If it doesn't help or you see nothing in the output, deleting the [timidity++](https://www.archlinux.org/packages/?name=timidity%2B%2B) package and restarting your system will help to get rid of the "dummy output".

Another reason is [FluidSynth](/index.php/FluidSynth "FluidSynth") conflicting with PulseAudio as discussed in [this thread](https://bbs.archlinux.org/viewtopic.php?id=154002). One solution is to remove the package [fluidsynth](https://www.archlinux.org/packages/?name=fluidsynth).

Alternatively you could modify the _fluidsynth_ configuration file `/etc/conf.d/fluidsynth` and change the driver to PulseAudio, then restart _fluidsynth_ and PulseAudio:

 `/etc/conf.d/fluidsynth` 

```
AUDIO_DRIVER=pulseaudio
OTHER_OPTS='-m alsa_seq-r 48000'
```

### No HDMI 5/7.1 Selection for Device

If you are unable to select 5/7.1 channel output for a working HDMI device, then turning off "stream device reading" in `/etc/pulse/default.pa` might help.

See [#Fallback device is not respected](#Fallback_device_is_not_respected).

### Failed to create sink input: sink is suspended

If you do not have any output sound and receive dozens of errors related to a suspended sink in your `journalctl -b` log, then backup first and then delete your user-specific pulse folders:

```
$ rm -r ~/.pulse ~/.pulse-cookie ~/.config/pulse

```

### Simultaneous output to multiple sound cards / devices

Simultaneous output to two different devices can be very useful. For example, being able to send audio to your A/V receiver via your graphics card's HDMI output, while also sending the same audio through the analogue output of your motherboard's built-in audio. This is much less hassle than it used to be (in this example, we are using GNOME desktop).

Using [paprefs](https://www.archlinux.org/packages/?name=paprefs), simply select "Add virtual output device for simultaneous output on all local sound cards" from under the "Simultaneous Output" tab. Then, under GNOME's "sound settings", select the simultaneous output you have just created.

If this doesn't work, try adding the following to `~/.asoundrc`:

```
pcm.dsp {
   type plug
   slave.pcm "dmix"
}

```

**Tip:** Simultaneous output can also be achieved manually using alsamixer. Disable "auto mute" item, then unmute other output sources you want to hear and increase their volume.

### Simultaneous output to multiple sinks on the same sound card not working

This can be useful for users who have multiple sound sources and want to play them on different sinks/outputs. An example use-case for this would be if you play music and also voice chat and want to output music to speakers (in this case Digital S/PDIF) and voice to headphones. (Analog)

This is sometimes auto detected by PulseAudio but not always. If you know that your sound card can output to both Analog and S/PDIF at the same time and PulseAudio does not have this option in it's profiles in pavucontrol, or veromix then you probably need to create a configuration file for your sound card.

More in detail you need to create a profile-set for your specific sound card. This is done in two steps mostly.

*   Create udev rule to make PulseAudio choose your PulseAudio configuration file specific to the sound card.
*   Create the actual configuration.

Create a pulseadio udev rule.

**Note:** This is only an example for Asus Xonar Essence STX. Read [udev](/index.php/Udev "Udev") to find out the correct values.

**Note:** Your configuration file should have lower number than the original PulseAudio rule to take effect.

 `/usr/lib/udev/rules.d/90-pulseaudio-Xonar-STX.rules` 

```
ACTION=="change", SUBSYSTEM=="sound", KERNEL=="card*", \
ATTRS{subsystem_vendor}=="0x1043", ATTRS{subsystem_device}=="0x835c", ENV{PULSE_PROFILE_SET}="asus-xonar-essence-stx.conf" 

```

Now, create a configuration file. If you bother, you can start from scratch and make it saucy. However you can also use the default configuration file, rename it, and then add your profile there that you know works. Less pretty but also faster.

To enable multiple sinks for Asus Xonar Essence STX you need only to add this in.

**Note:** `asus-xonar-essence-stx.conf` also includes all code/mappings from `default.conf`.

 `/usr/share/pulseaudio/alsa-mixer/profile-sets/asus-xonar-essence-stx.conf` 

```
[Profile analog-stereo+iec958-stereo]
description = Analog Stereo Duplex + Digital Stereo Output
input-mappings = analog-stereo
output-mappings = analog-stereo iec958-stereo
skip-probe = yes

```

This will auto-profile your Asus Xonar Essence STX with default profiles and add your own profile so you can have multiple sinks.

You need to create another profile in the configuration file if you want to have the same functionality with AC3 Digital 5.1 output.

[See PulseAudio article about profiles](http://www.freedesktop.org/wiki/Software/PulseAudio/Backends/ALSA/Profiles/)

### Some profiles like SPDIF are not enabled by default on the card

Some profiles like IEC-958 (i.e. S/PDIF) may not be enabled by default on the selected sink. Each time the system starts up, the card profile is disabled and the pulseaudio daemon cannot select it. You have to add the profile selection to you default.pa file. Verify the card and profile name with :

```
$ pacmd list-cards

```

Then edit the config to add the profile

 `~/.config/pulse/default.pa` 

```
## Replace with your card name and the profile you want to activate
set-card-profile alsa_card.pci-0000_00_1b.0 output:iec958-stereo+input:analog-stereo

```

Pulse audio will add this profile the pool of available profiles

## Bluetooth

### Отключение поддержки Bluetooth

Если вы не используете Bluetooth, вы можете обнаружить следующую ошибку в журнале:

```
bluez5-util.c: GetManagedObjects() failed: org.freedesktop.DBus.Error.ServiceUnknown: The name org.bluez was not provided by any .service files

```

Чтобы отключить поддержку Bluetooth в PulseAudio, убедитесь, что следующие строчки закомментированы в используемом файле конфигурации (`~/.config/pulse/default.pa` или `/etc/pulse/default.pa`):

 `~/.config/pulse/default.pa` 

```
### Automatically load driver modules for Bluetooth hardware
#.ifexists module-bluetooth-policy.so
#load-module module-bluetooth-policy
#.endif

#.ifexists module-bluetooth-discover.so
#load-module module-bluetooth-discover
#.endif

```

### Bluetooth headset replay problems

Некоторые пользователи [сообщают](https://bbs.archlinux.org/viewtopic.php?id=117420) о больших задержках или даже отсутствии звука, когда по Bluetooth-соединению не передаются никакие данные. Это вызвано модулем `module-suspend-on-idle`, который автоматически приостанавливает устройства ввода/вывода при простое. Так как это может вызвать проблемы с гарнитурой, можно отключить соответствующий модуль.

Для отключения загрузки модуля `module-suspend-on-idle` закомментируйте следующую строчку в используемом файле конфигурации (`~/.config/pulse/default.pa` или `/etc/pulse/default.pa`):

 `~/.config/pulse/default.pa` 

```
### Automatically suspend sinks/sources that become idle for too long
#load-module module-suspend-on-idle

```

И перезагрузите PulseAudio для применения изменений.

### Автоматическое переключение на Bluetooth или USB-гарнитуру

Добавьте следующие строчки в файл конфигурации:

 `/etc/pulse/default.pa` 

```
# automatically switch to newly-connected devices
load-module module-switch-on-connect

```

### Устройство сопряжено, но не проигрывает звук

[Смотрите раздел в статье Bluetooth](/index.php/Bluetooth#My_device_is_paired_but_no_sound_is_played_from_it "Bluetooth")

Начиная с PulseAudio 2.99 и bluez 4.101, вы должны **избегать** использования интерфейса Socket. НЕ используйте:

 `/etc/bluetooth/audio.conf` 

```
[General]
Enable=Socket

```

Если вы имеете проблемы с A2DP и PA 2.99, убедитесь, что у вас установлена библиотека [sbc](https://www.archlinux.org/packages/?name=sbc).

## Applications

### Flash content

Since Adobe Flash does not directly support PulseAudio, the recommended way is to [configure ALSA to use the virtual PulseAudio sound card](/index.php/PulseAudio#ALSA "PulseAudio").

If Flash audio is lagging, you may try to have Flash access ALSA directly. See [PulseAudio#ALSA/dmix without grabbing hardware device](/index.php/PulseAudio#ALSA.2Fdmix_without_grabbing_hardware_device "PulseAudio") for details.

### Ошибка с правами доступа

 `pulseaudio --start` 

```
E: [autospawn] core-util.c: Failed to create secure directory (/run/user/1000/pulse): Operation not permitted
W: [autospawn] lock-autospawn.c: Cannot access autospawn lock.
E: [pulseaudio] main.c: Failed to acquire autospawn lock
```

Известные програмы меняют права доступа для `/run/user_user id_/pulse` когда используется [Polkit](/index.php/Polkit "Polkit"):

*   [sakis3g](https://aur.archlinux.org/packages/sakis3g/)<sup><small>AUR</small></sup>

В качестве обходного пути можно использовать [gksu](https://www.archlinux.org/packages/?name=gksu) или [kdesu](https://www.archlinux.org/packages/?name=kdesu) в [desktop entry](/index.php/Desktop_entry "Desktop entry") или добавить `_username_ ALL=NOPASSWD: /usr/bin/_program_name_` в [sudoers](/index.php/Sudo_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0 "Sudo (Русский)") для запуска [sudo](https://www.archlinux.org/packages/?name=sudo) или `gksudo` без запроса пароля. Другой способ лежит через раскомментирование и установки `daemonize = yes` в `/etc/pulse/daemon.conf`.  
Также стоит посмотреть [эту ветку форума (англ)](https://bbs.archlinux.org/viewtopic.php?id=135955).

### Audacity

When starting Audacity you may find that your headphones no longer work. This can be because Audacity is trying to use them as a recording device. To fix this, open Audacity, then set its recording device to `pulse:Internal Mic:0`.

Under some circumstances, playback may be distorted, very fast, or freeze, as discussed in the [Audacity Wiki's Linux Issues page](http://wiki.audacityteam.org/wiki/Linux_Issues#ALSA_and_other_sound_systems).

The solution proposed in this page may work: start Audacity with:

```
$ env PULSE_LATENCY_MSEC=30 audacity

```

If the solution above does not fix this issue, one may wish to temporarily disable pulseaudio while running Audacity by using the `pasuspender` command:

```
$ pasuspender -- audacity

```

Then, be sure to select the appropriate ALSA input and output devices in Audacity.

See also [#Setting the default fragment number and buffer size in PulseAudio](#Setting_the_default_fragment_number_and_buffer_size_in_PulseAudio).

## Other Issues

### Bad configuration files

After starting PulseAudio, if the system outputs no sound, it may be necessary to delete the contents of `~/.config/pulse` and/or `~/.pulse`. PulseAudio will automatically create new configuration files on its next start.

### Can't update configuration of sound device in pavucontrol

[pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol) is a handy GUI utility for configuring PulseAudio. Under its 'Configuration' tab, you can select different profiles for each of your sound devices e.g. analogue stereo, digital output (IEC958), HDMI 5.1 Surround etc.

However, you may run into an instance where selecting a different profile for a card results in the pulse daemon crashing and auto restarting without the new selection "sticking". If this occurs, use the other useful GUI tool, [paprefs](https://www.archlinux.org/packages/?name=paprefs), to check under the "Simultaneous Output" tab for a virtual simultaneous device. If this setting is active (checked), it will prevent you changing any card's profile in pavucontrol. Uncheck this setting, then adjust your profile in pavucontrol prior to re-enabling simultaneous output in paprefs.

### Failed to create sink input: sink is suspended

If you do not have any output sound and receive dozens of errors related to a suspended sink in your `journalctl -b` log, then backup first and then delete your user-specific pulse folders:

```
$ rm -r ~/.pulse ~/.pulse-cookie ~/.config/pulse

```

### Pulse overwrites ALSA settings

PulseAudio usually overwrites the ALSA settings — for example set with alsamixer — at start-up, even when the ALSA daemon is loaded. Since there seems to be no other way to restrict this behaviour, a workaround is to restore the ALSA settings again after PulseAudio has started. Add the following command to `.xinitrc` or `.bash_profile` or any other [autostart](/index.php/Autostart "Autostart") file:

```
restore_alsa() {
 while [ -z "$(pidof pulseaudio)" ]; do
  sleep 0.5
 done
 alsactl -f /var/lib/alsa/asound.state restore 
}
restore_alsa &

```

### Prevent Pulse from restarting after being killed

Sometimes you may wish to temporarily disable Pulse. In order to do so you will have to prevent Pulse from restarting after being killed.

 `~/.config/pulse/client.conf` 

```
# Disable autospawning the PulseAudio daemon
autospawn = no
```

### Daemon startup failed

Try resetting PulseAudio:

```
$ rm -rf /tmp/pulse* ~/.pulse* ~/.config/pulse
$ pulseaudio -k
$ pulseaudio --start

```

*   Check that options for sinks are set up correctly.

*   If you configured in default.pa to load and use the OSS modules then check with [lsof](https://www.archlinux.org/packages/?name=lsof) that `/dev/dsp` device is not used by another application.

*   LXDE may have a problem with closing all applications after the user logged out to fix it look [Incorrect logout handling](/index.php/LXDM#Incorrect_logout_handling "LXDM").

*   Set a preferred working resample method. Use `pulseaudio --dump-resample-methods` to see a list with all available resample methods you can use.

*   To get details about currently appeared unfixed errors or just get status of daemon use commands like `pax11publish -d` and `pulseaudio -v` where `v` option can be used multiple time to set verbosity of log output equal to the `--log-level[=LEVEL]` option where LEVEL is from 0 to 4\. See the [Outputs by PulseAudio error status check utilities](/index.php/PulseAudio#Outputs_by_PulseAudio_error_status_check_utilities "PulseAudio") section.

See also man pages for [pax11publish](http://linux.die.net/man/1/pax11publish) and [pulseaudio](http://linux.die.net/man/1/pulseaudio) for more details.

#### Outputs by PulseAudio error status check utilities

If the `pax11publish -d` shows error like:

```
N: [pulseaudio] main.c: User-configured server at "user", refusing to start/autospawn.

```

then run `pax11publish -r` command then could be also good to logout and login again. This manual cleanup is always required when using LXDM because it does not restart the X server on logout; see [LXDM#PulseAudio](/index.php/LXDM#PulseAudio "LXDM").

If the `pulseaudio -vvvv` command shows error like:

```
E: [pulseaudio] module-udev-detect.c: You apparently ran out of inotify watches, probably because Tracker/Beagle took them all away. I wished people would do their homework first and fix inotify before using it for watching whole directory trees which is something the current inotify is certainly not useful for. Please make sure to drop the Tracker/Beagle guys a line complaining about their broken use of inotify.

```

This can be resolved temporary by:

```
$ echo 100000 > /proc/sys/fs/inotify/max_user_watches

```

For permanent use save settings in the _99-sysctl.conf_ file:

 `/etc/sysctl.d/99-sysctl.conf` 

```
# Increase inotify max watchs per user
fs.inotify.max_user_watches = 100000
```

**Warning:** It may cause much bigger consumption of memory by kernel.

**See also**

*   [proc_sys_fs_inotify](http://www.linuxinsight.com/proc_sys_fs_inotify.html) and [dnotify, inotify](http://lwn.net/Articles/604686/)- more details about _inotify/max_user_watches_
*   [reasonable amount of inotify watches with Linux](http://stackoverflow.com/questions/535768/what-is-a-reasonable-amount-of-inotify-watches-with-linux?answertab=votes#tab-top)
*   [inotify](http://linux.die.net/man/7/inotify) - man page

### Daemon already running

On some systems, PulseAudio may be started multiple times. journalctl will report:

```
[pulseaudio] pid.c: Daemon already running.

```

Make sure to use only one method of autostarting applications. [pulseaudio](https://www.archlinux.org/packages/?name=pulseaudio) includes these files:

*   `/etc/X11/xinit/xinitrc.d/pulseaudio`
*   `/etc/xdg/autostart/pulseaudio.desktop`
*   `/etc/xdg/autostart/pulseaudio-kde.desktop`

Also check user autostart files and directories, such as [xinitrc](/index.php/Xinitrc "Xinitrc"), `~/.config/autostart/` etc.

### Subwoofer stops working after end of every song

Known issue: [https://bugs.launchpad.net/ubuntu/+source/pulseaudio/+bug/494099](https://bugs.launchpad.net/ubuntu/+source/pulseaudio/+bug/494099)

To fix this, must edit: `/etc/pulse/daemon.conf` and enable `enable-lfe-remixing` :

 `/etc/pulse/daemon.conf` 

```
enable-lfe-remixing = yes

```

### Unable to select surround configuration other than "Surround 4.0"

If you're unable to set 5.1 surround output in pavucontrol because it only shows "Analog Surround 4.0 Output", open the ALSA mixer and change the output configuration there to 6 channels. Then restart pulseaudio, and pavucontrol will list many more options.

### Realtime scheduling

If rtkit does not work, you can manually set up your system to run PulseAudio with real-time scheduling, which can help performance. To do this, add the following lines to `/etc/security/limits.conf`:

```
@pulse-rt - rtprio 9
@pulse-rt - nice -11

```

Afterwards, you need to add your user to the `pulse-rt` group:

```
# gpasswd -a <user> pulse-rt

```

### pactl "invalid option" error with negative percentage arguments

`pactl` commands that take negative percentage arguments will fail with an 'invalid option' error. Use the standard shell '--' pseudo argument to disable argument parsing before the negative argument. _e.g._ `pactl set-sink-volume 1 -- -5%`.

### Fallback device is not respected

PulseAudio does not have a true default device. Instead it uses a ["fallback"](http://www.freedesktop.org/wiki/Software/PulseAudio/Documentation/User/DefaultDevice/), which only applies to new sound streams. This means previously run applications are not affected by the newly set fallback device.

[gnome-control-center](https://www.archlinux.org/packages/?name=gnome-control-center), [mate-media-pulseaudio](https://www.archlinux.org/packages/?name=mate-media-pulseaudio)<sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): replaced by [mate-media](https://www.archlinux.org/packages/?name=mate-media)]</sup> and [paswitch](https://aur.archlinux.org/packages/paswitch/)<sup><small>AUR</small></sup> handle this gracefully. Alternatively:

1\. Move the old streams in [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol) manually to the new sound card.

2\. Stop Pulse, erase the "stream-volumes" in `~/.config/pulse` and/or `~/.pulse` and restart Pulse. This also resets application volumes.

3\. Disable stream device reading. This may be not wanted when using different soundcards with different applications.

 `/etc/pulse/default.pa` 

```
load-module module-stream-restore restore_device=false

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=PulseAudio/Troubleshooting_(Русский)&oldid=415781](https://wiki.archlinux.org/index.php?title=PulseAudio/Troubleshooting_(Русский)&oldid=415781)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Русский](/index.php/Category:%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9 "Category:Русский")
*   [Sound (Русский)](/index.php/Category:Sound_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Category:Sound (Русский)")

Hidden category:

*   [Pages with broken package links](/index.php/Category:Pages_with_broken_package_links "Category:Pages with broken package links")