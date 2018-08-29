Related articles

*   [Arch terminology](/index.php/Arch_terminology "Arch terminology")
*   [Arch User Repository#FAQ](/index.php/Arch_User_Repository#FAQ "Arch User Repository")
*   [General troubleshooting](/index.php/General_troubleshooting "General troubleshooting")

## Contents

*   [1 Genel](#Genel)
    *   [1.1 Arch Linux nedir?](#Arch_Linux_nedir.3F)
    *   [1.2 Arch Linux'u neden kullanmak istemeyeyim ?](#Arch_Linux.27u_neden_kullanmak_istemeyeyim_.3F)
    *   [1.3 Arch ARM mimarili işlemcileri destekliyor mu ?](#Arch_ARM_mimarili_i.C5.9Flemcileri_destekliyor_mu_.3F)
    *   [1.4 Arch Linux FHS'yi takip ediyor mu?](#Arch_Linux_FHS.27yi_takip_ediyor_mu.3F)
    *   [1.5 GNU/Linux için tamamen acemiyim. Gerçekten Arch Linux kullanmalımıyım ?](#GNU.2FLinux_i.C3.A7in_tamamen_acemiyim._Ger.C3.A7ekten_Arch_Linux_kullanmal.C4.B1m.C4.B1y.C4.B1m_.3F)
    *   [1.6 Arch Linux kullanım olarak nasıl tasarlandı ? Bir sunucu olarak mı ? Bir iş istasyonu olarak mı ? Yoksa normal masaüstü kullanımı için mi ?](#Arch_Linux_kullan.C4.B1m_olarak_nas.C4.B1l_tasarland.C4.B1_.3F_Bir_sunucu_olarak_m.C4.B1_.3F_Bir_i.C5.9F_istasyonu_olarak_m.C4.B1_.3F_Yoksa_normal_masa.C3.BCst.C3.BC_kullan.C4.B1m.C4.B1_i.C3.A7in_mi_.3F)
    *   [1.7 Arch'ı gerçekten beğendim, fakat geliştirici ekibinin X özelliğini uygulaması lazım](#Arch.27.C4.B1_ger.C3.A7ekten_be.C4.9Fendim.2C_fakat_geli.C5.9Ftirici_ekibinin_X_.C3.B6zelli.C4.9Fini_uygulamas.C4.B1_laz.C4.B1m)
    *   [1.8 Yeni sürüm ne zaman ulaşılabilir olur ?](#Yeni_s.C3.BCr.C3.BCm_ne_zaman_ula.C5.9F.C4.B1labilir_olur_.3F)
    *   [1.9 Arch Linux kararlı bir dağıtım mı ? Sık bir şekilde bozulma meydana gelir mi ?](#Arch_Linux_kararl.C4.B1_bir_da.C4.9F.C4.B1t.C4.B1m_m.C4.B1_.3F_S.C4.B1k_bir_.C5.9Fekilde_bozulma_meydana_gelir_mi_.3F)
    *   [1.10 Arch'ın daha çok basında olmasına ihtiyacı var (reklam vb.)](#Arch.27.C4.B1n_daha_.C3.A7ok_bas.C4.B1nda_olmas.C4.B1na_ihtiyac.C4.B1_var_.28reklam_vb..29)
    *   [1.11 Arch'ın daha fazla geliştiriciye ihtiyacı var](#Arch.27.C4.B1n_daha_fazla_geli.C5.9Ftiriciye_ihtiyac.C4.B1_var)
    *   [1.12 Neden internetim diğer işletim sistemlerine göre daha yavaş ?](#Neden_internetim_di.C4.9Fer_i.C5.9Fletim_sistemlerine_g.C3.B6re_daha_yava.C5.9F_.3F)
    *   [1.13 Niçin Arch benim tüm RAM kapasitemi kullanıyor ?](#Ni.C3.A7in_Arch_benim_t.C3.BCm_RAM_kapasitemi_kullan.C4.B1yor_.3F)
    *   [1.14 Bütün boş alan nereye gitti ?](#B.C3.BCt.C3.BCn_bo.C5.9F_alan_nereye_gitti_.3F)
*   [2 Paket yönetimi](#Paket_y.C3.B6netimi)
    *   [2.1 X pakette hata buldum. Ne yapmalıyım?](#X_pakette_hata_buldum._Ne_yapmal.C4.B1y.C4.B1m.3F)
    *   [2.2 Arch paketlerinin karmaşık isimlendirme kuralı var. ".pkg.tar.gz" ve ".pkg.tar.xz" çok uzun ve/veya kafa karıştırıcı](#Arch_paketlerinin_karma.C5.9F.C4.B1k_isimlendirme_kural.C4.B1_var._.22.pkg.tar.gz.22_ve_.22.pkg.tar.xz.22_.C3.A7ok_uzun_ve.2Fveya_kafa_kar.C4.B1.C5.9Ft.C4.B1r.C4.B1c.C4.B1)
    *   [2.3 Pacman'in diğer uygulamalar tarafından kolayca paket bilgilerine erişilmesini sağlayan bir kütüphaneye ihtiyacı var](#Pacman.27in_di.C4.9Fer_uygulamalar_taraf.C4.B1ndan_kolayca_paket_bilgilerine_eri.C5.9Filmesini_sa.C4.9Flayan_bir_k.C3.BCt.C3.BCphaneye_ihtiyac.C4.B1_var)
    *   [2.4 Pacman'in X özelliğe ihtiyacı var!](#Pacman.27in_X_.C3.B6zelli.C4.9Fe_ihtiyac.C4.B1_var.21)
    *   [2.5 X paketini yükledim. Nasıl başlatacağım?](#X_paketini_y.C3.BCkledim._Nas.C4.B1l_ba.C5.9Flataca.C4.9F.C4.B1m.3F)
    *   [2.6 Neden her paylaşımlı kütüphanenin resmi depolarda tek bir sürümü var?](#Neden_her_payla.C5.9F.C4.B1ml.C4.B1_k.C3.BCt.C3.BCphanenin_resmi_depolarda_tek_bir_s.C3.BCr.C3.BCm.C3.BC_var.3F)
    *   [2.7 What if I run a full system upgrade and there will be an update for a shared library, but not for the apps that depend on it?](#What_if_I_run_a_full_system_upgrade_and_there_will_be_an_update_for_a_shared_library.2C_but_not_for_the_apps_that_depend_on_it.3F)
    *   [2.8 Is it possible that there's a major kernel update in the repository, and that some of the driver packages haven't been updated?](#Is_it_possible_that_there.27s_a_major_kernel_update_in_the_repository.2C_and_that_some_of_the_driver_packages_haven.27t_been_updated.3F)
    *   [2.9 Yükseltmeden önce ne yapmalı?](#Y.C3.BCkseltmeden_.C3.B6nce_ne_yapmal.C4.B1.3F)
    *   [2.10 Bir sistem güncellemesi yayınlandı, ancak pacman sistemin güncel olduğunu söylüyor](#Bir_sistem_g.C3.BCncellemesi_yay.C4.B1nland.C4.B1.2C_ancak_pacman_sistemin_g.C3.BCncel_oldu.C4.9Funu_s.C3.B6yl.C3.BCyor)
    *   [2.11 Upstream project *X* has released a new version. How long will it take for the Arch package to update to that new version?](#Upstream_project_X_has_released_a_new_version._How_long_will_it_take_for_the_Arch_package_to_update_to_that_new_version.3F)
*   [3 Kurulum](#Kurulum)
    *   [3.1 Arch'ın bir kurulum sihirbazına ihtiyacı var. Belki grafiksel kullanıcı arayüzlü bir sihirbaz?](#Arch.27.C4.B1n_bir_kurulum_sihirbaz.C4.B1na_ihtiyac.C4.B1_var._Belki_grafiksel_kullan.C4.B1c.C4.B1_aray.C3.BCzl.C3.BC_bir_sihirbaz.3F)
    *   [3.2 Arch'ı kurdum, ve şu anda kabuk ekranındayım. Ne yapmam gerekiyor?](#Arch.27.C4.B1_kurdum.2C_ve_.C5.9Fu_anda_kabuk_ekran.C4.B1nday.C4.B1m._Ne_yapmam_gerekiyor.3F)
    *   [3.3 Hangi masaüstü ortamı veya pencere yöneticisini kullanmalıyım?](#Hangi_masa.C3.BCst.C3.BC_ortam.C4.B1_veya_pencere_y.C3.B6neticisini_kullanmal.C4.B1y.C4.B1m.3F)
    *   [3.4 Arch'ı diğer "minimal" dağıtımlardan ayıran nedir?](#Arch.27.C4.B1_di.C4.9Fer_.22minimal.22_da.C4.9F.C4.B1t.C4.B1mlardan_ay.C4.B1ran_nedir.3F)
*   [4 64-bit](#64-bit)
    *   [4.1 İşlemcimin x86_64 mimarisine sahip olduğunu nasıl anlarım?](#.C4.B0.C5.9Flemcimin_x86_64_mimarisine_sahip_oldu.C4.9Funu_nas.C4.B1l_anlar.C4.B1m.3F)
    *   [4.2 Neden 64-bit?](#Neden_64-bit.3F)
    *   [4.3 İşletim sistemini yeniden kurmadan i636 kurulumundan x86_64 kurulumuna geçebilir miyim?](#.C4.B0.C5.9Fletim_sistemini_yeniden_kurmadan_i636_kurulumundan_x86_64_kurulumuna_ge.C3.A7ebilir_miyim.3F)

## Genel

### Arch Linux nedir?

Detaylı bilgi için [Arch Linux](/index.php/Arch_Linux "Arch Linux") sayfasını ziyaret edin.

### Arch Linux'u neden kullanmak istemeyeyim ?

Arch Linux'u kullanmak **istemeyeceğiniz** durumlar olabilir, bunlardan bazıları:

*   'kendin yap' ilkesinde bir GNU/Linux dağıtımı için zamanınız, yetkinliğiniz ve isteğiniz yoksa.
*   x86_64 işlemci mimarisi dışında bir işlemci mimarisine sahipseniz.
*   bir işletim sisteminin kendi işini görmesi, kendi kendine ayarlarını yapması veya bazı varsayılan yazılımları ve masaüstü ortamınıda beraberinde getirmesi gerektirdiğini inanıyorsanız.
*   yuvarlanan sürüm yapısına sahip olan bir GNU/Linux dağıtımı istemiyorsanız.
*   şu anda kullandığınız işletim sisteminden memnunsanız.

Arch Linux kullanmayı birdaha gözden geçirmelisiniz.

### Arch ARM mimarili işlemcileri destekliyor mu ?

Hayır, fakat [Arch Linux ARM](http://archlinuxarm.org/) projesi birçok ARM platformlarına Arch Linux'u çalıştırma imkanı sağlıyor. Lütfen bakınız [[1]](http://ix.io/73w/irc).

### Arch Linux [FHS](http://refspecs.linuxfoundation.org/FHS_3.0/fhs/index.html)'yi takip ediyor mu?

**Not:** FHS yani *file system hierarchy* inglizce olarak Türkçesi ise *dosya sistemi hiyerarşisi* olarak adlandırılır.

Arch Linux [systemd](/index.php/Systemd "Systemd") servis yöneticisini kullanarak işletim sistemleri için *file system hierarchy* yapısını takip etmektedir. Klasörlendirme ve isimlemdirme için ayrıca bakınız [file-hierarchy(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/file-hierarchy.7). `/bin`, `/sbin` ve `/usr/sbin` sembolik bağıntı olarak `/usr/bin`'e ve `/lib`, `/lib64`'da sembolik bağıntı olarak `/usr/lib`'e bağlıdır.

### GNU/Linux için tamamen acemiyim. Gerçekten Arch Linux kullanmalımıyım ?

Öncelikle bilmen gerekir ki Arch Linux tasarım olarak DIY (Do-It-Yourself) yani 'kendi işini kendin hallet' olarak tasarlanmıştır. Yani acemi olarak Arch kullanmak istersen, yeni bir sisteme adepte olmak ve bu yeni sistemi öğrenmek için zamanının bir çoğunda bu işlemleri gerçekleştirken isteyerek yapman gerekir çünkü sistemi bir bütün olarak kullanabilir hale getiren kişi kullanıcı(yani siz) olacaktır.

Herhangi bir şekilde yardım istemeden önce sorununla alakalı konuyu Google vasıtasıyla kendin bağımsız olarak göz atmanda yada forumda ve Arch Wiki tarafından sağlanan zengin içeriklere bakman beklenmektedir. Herşeyden önce bilmelisinki bu kaynakların ulaşabilir olmasının bir sebebi var. Binlerce gönüllü insan buradaki değerli bilgileri birleştirmek için ciddi bir zaman harcadığını belirtmek isteriz.

Lütfen [Arch terminolojisi](/index.php/Arch_terminology#RTFM "Arch terminology") ve [Yükleme rehberine](/index.php/Installation_guide "Installation guide") bir gözat.

### Arch Linux kullanım olarak nasıl tasarlandı ? Bir sunucu olarak mı ? Bir iş istasyonu olarak mı ? Yoksa normal masaüstü kullanımı için mi ?

Arch herhangi bir şekilde bir kullanım tarzı baz alınarak tasarlanmadı yahut *kullanıcı* tiplerine göre tasarlanmıştır. Arch'ın kullanımında kendi işini kendin hallet ilkesinden zevk alan, kendi özel ihtiyaçları veya spesifik durumlara uygun halde sistemin çalışmasını sağlamak isteyen yetkin kullanıcıları hedef alır. Bundan dolayı seçimler kullanıcıya kaldığı için Arch istenilen hertürlü amaç için sanal olarak kullanılabilir. Bir çok kullanıcı Arch'ı masaüstü yada iş istasyonu olarak kullanıyor. **Örneğin** archlinux.org sunucu olarak Arch Linux kullanmaktadır.

### Arch'ı gerçekten beğendim, fakat geliştirici ekibinin X özelliğini uygulaması lazım

Komüniteye dahil olarak çözümlerini ve geliştirdğin kodları paylaşarak destekleyebilirsin. Hem kömünite tarafından hem geliştirici ekibi tarafından beğenilirse ileri dönük zamanda birleştirilme ihtimali var.

### Yeni sürüm ne zaman ulaşılabilir olur ?

Arch Linux sürümleri basit yükleme ve kurtarma için canlı ortam oluşturur ve bu oluşum sağlanırken [base](https://www.archlinux.org/groups/x86_64/base/) grubu ve başka diğer paketleri içerir. Sürümler genellikle her ayın ilk yarısında yayımlanır.

### Arch Linux kararlı bir dağıtım mı ? Sık bir şekilde bozulma meydana gelir mi ?

Yuvarlanan sistemin kararlı olması tamamen **kullanıcının** sorumluluğundadır. Kullanıcı sistemi güncellemek istediği zaman gerekli değişiklikleri ve birleştirmeleri yapması zorunludur. Arch Linux 'kendi işini kendin hallet' ilkesinni benimseyen bir dağıtım olduğu için yardım istendiği zaman bozulma şikayetleri düzgün bilgilendirilmemiş ve üretken olmayan olarak değerlendirilecektir çünkü bunlardan kesinlikle Arch geliştiricileri sorumlu değillerdir.

Bu konuda belirtilen görüşleri ve ipuçları için lütfen [Sistem bakımı](/index.php/System_maintenance "System maintenance") sayfasını ziyaret ediniz.

### Arch'ın daha çok basında olmasına ihtiyacı var (reklam vb.)

Arch kendi yağında kavrulan bir dağıtımdır ve gerekli miktarda basında da yer almaktadır. Arch Linux'un hedefi çok büyük olmak değildir aksine organik ve yönetilbilirliği yüksek şekilde büyüyen bir kullanıcı havuzuna sahiptir.

### Arch'ın daha fazla geliştiriciye ihtiyacı var

Doğru olabilir. Gönüllü olarak katkıda bulanabilirsiniz. [Forumlar](https://bbs.archlinux.org), [IRC kanalları](/index.php/IRC_channels "IRC channels") ve [mail listesi](https://mailman.archlinux.org/mailman/listinfo/) ziyaret ederek ne yapılması gerektiğine bakın.

### Neden internetim diğer işletim sistemlerine göre daha yavaş ?

Ağınızı düzgün bir şekilde yapılandırdığınıza emin misiniz ? [Ağ yapılandırmaları](/index.php/Network_configuration "Network configuration") sayfasına gözatmanızda bir fayda var.

Bilmenizde yarar var ki Arch Linux [trafik yapılandırmaları](https://en.wikipedia.org/wiki/Traffic_shaping "wikipedia:Traffic shaping") aktif olarak gelmemektedir. Bundan dolayı bir uygulama internetinizi tam kapasite olarak kullanabilir.

### Niçin Arch benim tüm RAM kapasitemi kullanıyor ?

Temel olarak, kullanılmayan RAM harcanan RAM'dir.

Bir çok yeni kullanıcı bir önceki hafıza kullanımlarına göre Linux çekirdeğinin nasıl farklı kullandığını fark edicekelerdir. Veriye ulaşmada RAM depolama aygıtlarına göre daha hızlı ulaştığından sebeple, çekirdek o anlık ulaşılmış olan veriyi önbellekleme işlemini yapar. Önbelleklenen veri sadece sistemde yeterli miktarda bellek kullanımı yapamadığında ve yeni veriler yüklenmesi gerektiğinde temizlenmektedir.

Bu farklılığı `free` komutunu kullanarak gözlemleye biliriz:

 `$ free -h` 
```
              total        used        free      shared  buff/cache   available
Mem:           2.8G        1.1G        283M        224M        1.4G        1.2G
Swap:          3.0G        881M        2.1G

```

"free" ve "available" arasındaki bellek farkının ne kadar önemli olduğunu bilmemiz gerekiyor. Yukarıda verilen örnekte, 2.8G RAM kapasitesine sahip olan bir dizüstü görünüşe göre hemen hemen tüm belleği kullanıyor gibi ve sadece 283M boş kapasitesi var. Dikkat etmek gerekir ki 1.4G olan "buff/cache". Yani hala 1.2G ulaşılabilir yeni uygulamaları açabilecek, swap yapmadan kullanbileceğimiz bir bellek var. Detaylı bilgi için `man free(1)`. Sonuç olarak tüm fındık fıstığı sistem kullandığı için performansımızı daha elverişli hale getirmiş oluyoruz :)

Şuradaki [tadından yenmeyecek](http://www.linuxjournal.com/article/2770) olan yazıyı eğer merakınız tavan yaptıysa okuyabilirsiniz!

### Bütün boş alan nereye gitti ?

Bu sorunun cevabı kurmuş olduğunuz sisteminize bağlıdır. Burada bazı sorunun cevabı için [yardımcı olabilecek](/index.php/List_of_applications#Disk_usage_display "List of applications") uygulamaları bulabilirsiniz.

## Paket yönetimi

Daha fazla cevap için [pacman](/index.php/Pacman "Pacman"), [pacman/İpuçları ve püf noktaları](/index.php/Pacman/Tips_and_tricks "Pacman/Tips and tricks") ve [Resmi depolar](/index.php/Official_repositories "Official repositories") sayfalarına göz atın.

### X pakette hata buldum. Ne yapmalıyım?

İlk olarak, bu hatanın Arch ekibi tarafından düzeltilebilecek bir hata olduğuna emin olmalısın. Öyle olmadığı durumda (örn. Firefox'un Mozilla ekibinin hatasından dolayı çökmesi); bu hatalara *giriş hatası* denir. Eğer bu bir Arch problemi ise, yapabileceğiniz bir kaç adım söz konusu:

1.  Bilgi için forumlarda arama yapın. Birinin bu konuda bildirim yapıp yapmadığını kontrol edin.
2.  [https://bugs.archlinux.org](https://bugs.archlinux.org) adresine detaylı bilgi ile birlikte bir [hata bildirimi](/index.php/Bug_report "Bug report") yapın.
3.  Eğer istersen, sorunu detaylandırıp halihazırda raporladığına dair bilgi vereceğin bir forum gönderisi oluşturabilirsin. Bu, aynı hatayı bir çok kişi tarafından verilmesinin önüne geçecektir.

### Arch paketlerinin karmaşık isimlendirme kuralı var. ".pkg.tar.gz" ve ".pkg.tar.xz" çok uzun ve/veya kafa karıştırıcı

Bu Arch mailing listesinde tartışılmıştı. `.pac` uzantısı desteklendi. Ancak yakın bir zamanda paket uzantısını değiştirmek gibi bir planımız yok. Arch geliştiricilerinden Tobias Kieslich'e göre, "*Bir paket, gziplenmiş [xz] bir tar arşividir! Ve bu herhangi bir tar uyumlu uygulama tarafından açılabilir, incelenebilir ve manipüle edilebilir. Dahası, mime-type'ları çoğu uygulama tararfından otomatik algılanabilir.*"

### Pacman'in diğer uygulamalar tarafından kolayca paket bilgilerine erişilmesini sağlayan bir kütüphaneye ihtiyacı var

Pacman [libalpm](https://www.archlinux.org/pacman/libalpm.3.html) - "Arch Linux Paket Yönerimi" kütüphanesinin bir ön yüzüdür. Bu kütüphane alternatif ön yüzler geliştirilmesine de müsade etmektedir. Mesela bir grafiksel kullanıcı arayüz önyüzü, yazılabilir.

### Pacman'in X özelliğe ihtiyacı var!

Eğer fikrinin kayda değer olduğunu düşünüyorsan, bunu [pacman-dev](https://lists.archlinux.org//listinfo/pacman-dev/)'de tartışabilirsin. Ayrıca halihazırda bulunan özellik istekleri için de [https://bugs.archlinux.org](https://bugs.archlinux.org) sayfasını ziyaret edebilirsin.

Aslında, pacman'e veya Arch Linux'a özellik eklemenin en iyi yolu kendiniz yazmanızdır. Bu yama veya kod belki kabul edilebilir veya reddedilebilir, ama diğerleri bundan memnun olabilir, test edebilir ve harcadığınız emeğe katkıda bulunabilirler.

### X paketini yükledim. Nasıl başlatacağım?

Eğer [KDE](/index.php/KDE "KDE") veya [GNOME](/index.php/GNOME "GNOME") gibi bir masaüstü ortamı kullanıyorsanız, program menüde otomatik olarak gösterilecektir. Eğer programı uçbirimden çalıştırmak istiyorsanız ve ikili dosyanın adını bilmiyorsanız, şu komutu uygulayın:

```
$ pacman -Qlq *package_name* | grep /usr/bin/

```

### Neden her paylaşımlı kütüphanenin resmi depolarda tek bir sürümü var?

Debian gibi bir kaç dağıtımda, paylaşımlı kütüphanelerin farklı sürümleri bulunur. `libfoo1`, `libfoo2`, `libfoo3` ve daha fazlası. Bu durumda uygulamaların aynı sistemde `libfoo`nun farklı sürümleri ile derlenmesi söz konusu.

Arch gibi dağıtımlarda ise, sadece en son kararlı sürüm resmi olarak desteklenir. By dropping support for outdated software, package maintainers are able to spend more time ensuring that the newest versions work as expected. As soon as a new version of a shared library becomes available from upstream, it is added to the repositories and affected packages are rebuilt to use the new version.

### What if I run a full system upgrade and there will be an update for a shared library, but not for the apps that depend on it?

This scenario should not happen at all. Assuming an application called `foobaz` is in one of the official repositories and builds successfully against a new version of a shared library called `libbaz`, it will be updated along with `libbaz`. If, however, it doesn't build successfully, `foobaz` package will have a versioned dependency (e.g. *libbaz 1.5*), and will be removed by pacman during `libbaz` upgrade, due to a conflict.

If `foobaz` is a package that you built yourself and installed from AUR, you should try rebuilding `foobaz` against the new version of `libbaz`. If the build fails, report the bug to the `foobaz` developers.

### Is it possible that there's a major kernel update in the repository, and that some of the driver packages haven't been updated?

No, it is not possible. Major kernel updates (e.g. *linux 3.5.0-1* to *linux 3.6.0-1*) are always accompanied by rebuilds of all supported kernel driver packages. On the other hand, if you have an unsupported driver package installed on your system, such as [catalyst](https://aur.archlinux.org/packages/catalyst/), then a kernel update might break things for you if you do not rebuild it for the new kernel. Users are responsible for updating any unsupported driver packages that they have installed.

### Yükseltmeden önce ne yapmalı?

[Sistem bakımı#Sistemi yükseltmek](/index.php/System_maintenance#Upgrading_the_system "System maintenance") kısmını takip edin.

### Bir sistem güncellemesi yayınlandı, ancak pacman sistemin güncel olduğunu söylüyor

*pacman* yansımaları anında senkronize olmaz. Güncellemenin sizin için hazır olması 24 saate kadar sürebilir. Sabırlı olun veya başka yansımaları deneyin. [Bu sayfadan](https://www.archlinux.org/mirrors/status/) güncel yansımalara erişebilirsiniz.

### Upstream project *X* has released a new version. How long will it take for the Arch package to update to that new version?

Package updates will be released when they are ready. The specific amount of time can be as short as a few hours after upstream releases a minor bugfix update to as long as several weeks after a large package group's major update. The amount of time from an upstream's new version to Arch releasing a new package depends on the specific packages and the availability of the package maintainers. Additionally, some packages spend some time in the [testing](/index.php/Testing "Testing") repository, so this can prolong the time before a package is updated. [Package maintainers](/index.php/Package_maintainer "Package maintainer") attempt to work quickly to bring stable updates to the repositories. If you find a package in the official repositories that is out of date, go to that package's page at the [package website](https://www.archlinux.org/packages/) and flag it.

## Kurulum

### Arch'ın bir kurulum sihirbazına ihtiyacı var. Belki grafiksel kullanıcı arayüzlü bir sihirbaz?

Kurulum işleminin sık yapılması gerekmediği için (makalenin devamını okuyun ve *yuvarlanan sürüm*ün ne anlama geldiğini öğrenin), bu kullanıcıların veya geliştiricilerin yüksek bir önceliği değildir. [Kurulum rehberi](/index.php/Installation_guide_(T%C3%BCrk%C3%A7e) "Installation guide (Türkçe)") komut satırı metodunu kullanmak üzere sürekli olarak güncelleniyor.

### Arch'ı kurdum, ve şu anda kabuk ekranındayım. Ne yapmam gerekiyor?

[Genel öneriler](/index.php/General_recommendations_(T%C3%BCrk%C3%A7e) "General recommendations (Türkçe)")'e göz atın.

### Hangi masaüstü ortamı veya pencere yöneticisini kullanmalıyım?

Size en uygun olanı seçin. [Masaüstü ortamı](/index.php/Desktop_environment "Desktop environment") ve [Pencere yöneticisi](/index.php/Window_manager "Window manager") makalelerine göz atın.

### Arch'ı diğer "minimal" dağıtımlardan ayıran nedir?

[Diğer dağıtımlarla karşılaştırıldığında Arch](/index.php/Arch_compared_to_other_distributions "Arch compared to other distributions")'a göz atın.

## 64-bit

### İşlemcimin x86_64 mimarisine sahip olduğunu nasıl anlarım?

Eğer işlemciniz [x86_64](https://en.wikipedia.org/wiki/X86-64 "wikipedia:X86-64") mimarisine sahipse,`/proc/cpuinfo` içinde `lm` flag'i olacaktır. Aşağıdaki komutun çıktısı ile bunu öğrenebilirsiniz,

```
$ grep -w lm /proc/cpuinfo

```

Windows üzerinde ise ücretsiz bir yazılım olan [CPU-Z](http://www.cpuid.com/cpuz.php) ile işlemcinizin x86_64 mimarisine sahip olup olmadığını öğrenebilirsiniz. "AMD64" ve Intel'in 64 bit çözümü olan "EM64T" mimarisine sahip olan bir işlemci x86_64 komut setini ve kütüphanelerini çalıştırabilir.

### Neden 64-bit?

Çoğu durumda daha hızlıdır ve [Address space layout randomization (ASLR)](https://en.wikipedia.org/wiki/Address_space_layout_randomization "wikipedia:Address space layout randomization") özelliği ve [Position-independent code (PIC)](https://en.wikipedia.org/wiki/Position-independent_code "wikipedia:Position-independent code") , [NX Bit](https://en.wikipedia.org/wiki/NX_Bit "wikipedia:NX Bit") özellikleri ile daha güvenlidir. Ayrıca bilgisayarınız 4 GB'tan daha fazla RAM'e sahipse x86_64 komut setini çalıştıramayan bir işlemci bunu algılayamaz.

Ek olarak yazılımcılar da yavaş yavaş 32 bit desteğini gevşetip, çekmeye başladılar. 32 bit yazılımın yakın bir gelecekte var olmayacağını söyleyebiliriz.

### İşletim sistemini yeniden kurmadan i636 kurulumundan x86_64 kurulumuna geçebilir miyim?

Hayır. Tüm paketleriniz yeni mimari için tekrardan kurulması gerekiyor ve buna dahil olarak konfigürasyon değişiklerine ihtiyaç duymanız da muhtemel. Ama, bu işlem sırasında hard diskinizi formatlamanız ya da yeniden biçimlendirmeniz gerekmiyor. Yani hali hazırda bulunan verilerinizi yeni kuruluma aktarabilirsiniz. Bunun için verilerinizi kaybetmeden yeni kuruluma geçmenize yardımcı olacak bir [forum konusu](https://bbs.archlinux.org/viewtopic.php?id=64485) mevcut.

Veya sisteminizi 64-bit kurulum ISO'su ile açıp, diskinizden 32-bit kütüphanelerini içermeyen her şeyi kopyalayabilirsiniz. (örneğin: `/home` & `/etc`), and install.

Şu başlığı da okumak isteyebilirsiniz: [migrating between architectures](/index.php/Migrating_between_architectures "Migrating between architectures").