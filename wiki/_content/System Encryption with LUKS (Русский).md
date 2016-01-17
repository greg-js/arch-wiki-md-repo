# System Encryption with LUKS (Русский)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

**Эта страница нуждается в сопроводителе**

Статья не гарантирует актуальность информации. Помогите русскоязычному сообществу поддержкой подобных страниц. См. [Команда переводчиков ArchWiki](/index.php/%D0%9A%D0%BE%D0%BC%D0%B0%D0%BD%D0%B4%D0%B0_%D0%BF%D0%B5%D1%80%D0%B5%D0%B2%D0%BE%D0%B4%D1%87%D0%B8%D0%BA%D0%BE%D0%B2_ArchWiki "Команда переводчиков ArchWiki")

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

**Эта статья или раздел нуждается в [переводе](/index.php/ArchWiki:Contributing_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.9F.D0.B5.D1.80.D0.B5.D0.B2.D0.BE.D0.B4 "ArchWiki:Contributing (Русский)")**

**Примечания:** пожалуйста, используйте первый аргумент шаблона для указания дополнительной информации. (обсуждение: [Talk:System Encryption with LUKS (Русский)#](https://wiki.archlinux.org/index.php/Talk:System_Encryption_with_LUKS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)))

## Введение

### Зачем вообще шифровать?

Шифровать харды надо для того, что бы не дать злоумышленникам полазить в ваших личных файлах. Например ноутбук могут стырить и файлы будут доступны злоумышленникам, или сдать ноут в сервисный центр - тогда работающие там бородатые тунеядцы будут лазить по вашим личным фотографиям. Конечно могут быть и более серьезные мотивы, как например на ваших дисках лежит серьезный компромат на крупные корпорации.

**Важно:** Having encrypted partitions does not protect you from all possible attacks. The encryption is only as good as your key management, and there are other ways to break into computers while they are running. Read the [caveats](/index.php/System_Encryption_with_LUKS_for_dm-crypt#Caveats "System Encryption with LUKS for dm-crypt") section below!

Retrieved from "[https://wiki.archlinux.org/index.php?title=System_Encryption_with_LUKS_(Русский)&oldid=415644](https://wiki.archlinux.org/index.php?title=System_Encryption_with_LUKS_(Русский)&oldid=415644)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Security (Русский)](/index.php/Category:Security_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Category:Security (Русский)")
*   [File systems (Русский)](/index.php/Category:File_systems_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Category:File systems (Русский)")
*   [Русский](/index.php/Category:%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9 "Category:Русский")