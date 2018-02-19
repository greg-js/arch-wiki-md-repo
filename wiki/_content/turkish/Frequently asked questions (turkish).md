Related articles

*   [Arch terminology](/index.php/Arch_terminology "Arch terminology")
*   [Arch User Repository#FAQ](/index.php/Arch_User_Repository#FAQ "Arch User Repository")
*   [General troubleshooting](/index.php/General_troubleshooting "General troubleshooting")

## Contents

*   [1 Genel](#Genel)
    *   [1.1 Arch Linux nedir?](#Arch_Linux_nedir.3F)
    *   [1.2 Neden Arch Linux kullanmak istemeyeyim ?](#Neden_Arch_Linux_kullanmak_istemeyeyim_.3F)
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
*   [2 Package management](#Package_management)
    *   [2.1 I've found an error with Package X. What should I do?](#I.27ve_found_an_error_with_Package_X._What_should_I_do.3F)
    *   [2.2 Arch packages need to use a unique naming convention. ".pkg.tar.gz" and ".pkg.tar.xz" are too long and/or confusing](#Arch_packages_need_to_use_a_unique_naming_convention._.22.pkg.tar.gz.22_and_.22.pkg.tar.xz.22_are_too_long_and.2For_confusing)
    *   [2.3 Pacman needs a library so other applications can easily access package information](#Pacman_needs_a_library_so_other_applications_can_easily_access_package_information)
    *   [2.4 Pacman needs feature X!](#Pacman_needs_feature_X.21)
    *   [2.5 I just installed Package X. How do I start it?](#I_just_installed_Package_X._How_do_I_start_it.3F)
    *   [2.6 Why is there only a single version of each shared library in the official repositories?](#Why_is_there_only_a_single_version_of_each_shared_library_in_the_official_repositories.3F)
    *   [2.7 What if I run a full system upgrade and there will be an update for a shared library, but not for the apps that depend on it?](#What_if_I_run_a_full_system_upgrade_and_there_will_be_an_update_for_a_shared_library.2C_but_not_for_the_apps_that_depend_on_it.3F)
    *   [2.8 Is it possible that there's a major kernel update in the repository, and that some of the driver packages haven't been updated?](#Is_it_possible_that_there.27s_a_major_kernel_update_in_the_repository.2C_and_that_some_of_the_driver_packages_haven.27t_been_updated.3F)
    *   [2.9 What to do before upgrading?](#What_to_do_before_upgrading.3F)
    *   [2.10 A package update was released, but pacman says the system is up to date](#A_package_update_was_released.2C_but_pacman_says_the_system_is_up_to_date)
    *   [2.11 Upstream project *X* has released a new version. How long will it take for the Arch package to update to that new version?](#Upstream_project_X_has_released_a_new_version._How_long_will_it_take_for_the_Arch_package_to_update_to_that_new_version.3F)
*   [3 Installation](#Installation)
    *   [3.1 Arch needs an installer. Maybe a GUI installer?](#Arch_needs_an_installer._Maybe_a_GUI_installer.3F)
    *   [3.2 I installed Arch, and now I am at a shell! What now?](#I_installed_Arch.2C_and_now_I_am_at_a_shell.21_What_now.3F)
    *   [3.3 Which desktop environment or window manager should I use?](#Which_desktop_environment_or_window_manager_should_I_use.3F)
    *   [3.4 What makes Arch unique amongst other "minimal" distributions?](#What_makes_Arch_unique_amongst_other_.22minimal.22_distributions.3F)
*   [4 64-bit](#64-bit)
    *   [4.1 İşlemcimin x86_64 mimarisine sahip olup olmadığını nasıl öğrenebilirim ?](#.C4.B0.C5.9Flemcimin_x86_64_mimarisine_sahip_olup_olmad.C4.B1.C4.9F.C4.B1n.C4.B1_nas.C4.B1l_.C3.B6.C4.9Frenebilirim_.3F)

## Genel

### Arch Linux nedir?

Detaylı bilgi için [Arch Linux](/index.php/Arch_Linux "Arch Linux") sayfasını ziyaret edin.

### Neden Arch Linux kullanmak istemeyeyim ?

Arch Linux'u kullanmak **istemiyeceğiniz** durumlar olabilir, bunlardan bazıları:

*   'kendi işini kendin hallet' ileksinde bir GNU/Linux dağıtımı için zamanınız, yetkinliğiniz ve isteğiniz yoksa.
*   x86_64 işlemci mimarisi dışında bir işlemci mimarisine sahipseniz.
*   bir işletim sisteminin kendi işini görmesi, kendi kendine ayarlarını yapması veya bazı varsayılan yazılımları ve masaüstü ortamınıda beraberinde getirmesi gerektirdiğini inanıyorsanız.
*   yuvarlanan sürüm yapısına sahip olan bir GNU/Linux dağıtımı istemiyorsanız.
*   şuanda kullandığınız işletim sisteminden memnunsanız.

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

Şuradaki [tadından yenmicek](http://www.linuxjournal.com/article/2770) olan yazıyı eğer merakınız tavan yaptıysa okuyabilirsiniz!

### Bütün boş alan nereye gitti ?

Bu sorunun cevabı kurmuş olduğunuz sisteminize bağlıdır. Burada bazı sorunun cevabı için [yardımcı olabilecek](/index.php/List_of_applications#Disk_usage_display "List of applications") uygulamaları bulabilirsiniz.

## Package management

See the [pacman](/index.php/Pacman "Pacman"), [pacman/Tips and tricks](/index.php/Pacman/Tips_and_tricks "Pacman/Tips and tricks") and [Official repositories](/index.php/Official_repositories "Official repositories") pages for more answers.

### I've found an error with Package X. What should I do?

First, you need to figure out if this error is something the Arch team can fix. Sometimes it's not (e.g. Firefox crashes may be the fault of the Mozilla team); this is called an *upstream error*. If it is an Arch problem, there is a series of steps you can take:

1.  Search the forums for information. See if anyone else has noticed it.
2.  Post a [bug report](/index.php/Bug_report "Bug report") with detailed information at [https://bugs.archlinux.org](https://bugs.archlinux.org).
3.  If you'd like, write a forum post detailing the problem and the fact that you have reported it already. This will help prevent a lot of people from reporting the same error.

### Arch packages need to use a unique naming convention. ".pkg.tar.gz" and ".pkg.tar.xz" are too long and/or confusing

This has been discussed on the Arch mailing list. Some proposed a `.pac` file extension. As far as is currently known, there is no plan to change the package extension. As Tobias Kieslich, one of the Arch devs, put it, "*A package **is** a gzipped* [xz] *tarball! And it can be opened, investigated and manipulated by any tar-capable application. Moreover, the mime-type is automatically detected correctly by most applications.*"

### Pacman needs a library so other applications can easily access package information

Pacman is a front-end to [libalpm](https://www.archlinux.org/pacman/libalpm.3.html)—the "Arch Linux Package Management" library—which allows alternative front-ends, like a GUI front-end, to be written.

### Pacman needs feature X!

If you think an idea has merit, you may choose to discuss it on [pacman-dev](https://lists.archlinux.org//listinfo/pacman-dev/). Also check [https://bugs.archlinux.org](https://bugs.archlinux.org) for existing feature requests.

However, the best way to get a feature added to pacman or Arch Linux is to implement it yourself. The patch or code may or may not be officially accepted, but perhaps others will appreciate, test and contribute to your effort.

### I just installed Package X. How do I start it?

If you're using a desktop environment like [KDE](/index.php/KDE "KDE") or [GNOME](/index.php/GNOME "GNOME"), the program should automatically show up in your menu. If you're trying to run the program from a terminal and do not know the binary name, use:

```
$ pacman -Qlq *package_name* | grep /usr/bin/

```

### Why is there only a single version of each shared library in the official repositories?

Several distributions, such as Debian, have different versions of shared libraries packaged as different packages: `libfoo1`, `libfoo2`, `libfoo3` and so on. In this way it is possible to have applications compiled against different versions of `libfoo` installed on the same system.

In case of a distribution like Arch, only the latest stable versions of packages are officially supported. By dropping support for outdated software, package maintainers are able to spend more time ensuring that the newest versions work as expected. As soon as a new version of a shared library becomes available from upstream, it is added to the repositories and affected packages are rebuilt to use the new version.

### What if I run a full system upgrade and there will be an update for a shared library, but not for the apps that depend on it?

This scenario should not happen at all. Assuming an application called `foobaz` is in one of the official repositories and builds successfully against a new version of a shared library called `libbaz`, it will be updated along with `libbaz`. If, however, it doesn't build successfully, `foobaz` package will have a versioned dependency (e.g. *libbaz 1.5*), and will be removed by pacman during `libbaz` upgrade, due to a conflict.

If `foobaz` is a package that you built yourself and installed from AUR, you should try rebuilding `foobaz` against the new version of `libbaz`. If the build fails, report the bug to the `foobaz` developers.

### Is it possible that there's a major kernel update in the repository, and that some of the driver packages haven't been updated?

No, it is not possible. Major kernel updates (e.g. *linux 3.5.0-1* to *linux 3.6.0-1*) are always accompanied by rebuilds of all supported kernel driver packages. On the other hand, if you have an unsupported driver package installed on your system, such as [catalyst](https://aur.archlinux.org/packages/catalyst/), then a kernel update might break things for you if you do not rebuild it for the new kernel. Users are responsible for updating any unsupported driver packages that they have installed.

### What to do before upgrading?

Follow the [System maintenance#Upgrading the system](/index.php/System_maintenance#Upgrading_the_system "System maintenance") section.

### A package update was released, but pacman says the system is up to date

*pacman* mirrors are not synced immediately. It may take over 24 hours before an update is available to you. The only options are be patient or use another mirror. [MirrorStatus](https://www.archlinux.org/mirrors/status/) can help you identify an up-to-date mirror.

### Upstream project *X* has released a new version. How long will it take for the Arch package to update to that new version?

Package updates will be released when they are ready. The specific amount of time can be as short as a few hours after upstream releases a minor bugfix update to as long as several weeks after a large package group's major update. The amount of time from an upstream's new version to Arch releasing a new package depends on the specific packages and the availability of the package maintainers. Additionally, some packages spend some time in the [testing](/index.php/Testing "Testing") repository, so this can prolong the time before a package is updated. [Package maintainers](/index.php/Package_maintainer "Package maintainer") attempt to work quickly to bring stable updates to the repositories. If you find a package in the official repositories that is out of date, go to that package's page at the [package website](https://www.archlinux.org/packages/) and flag it.

## Installation

### Arch needs an installer. Maybe a GUI installer?

Since installation doesn't occur often (read the rest of this article to know more about what *rolling release* means), it is not a high priority for developers or users. The [Installation guide](/index.php/Installation_guide "Installation guide") has been fully updated to use the command-line method. If you're still interested in using an installer, consider using [Archboot](/index.php/Archboot "Archboot").

### I installed Arch, and now I am at a shell! What now?

See [General recommendations](/index.php/General_recommendations "General recommendations").

### Which desktop environment or window manager should I use?

Since many are available to you, use the one you like the most to fit your needs. Have a look at the [Desktop environment](/index.php/Desktop_environment "Desktop environment") and [Window manager](/index.php/Window_manager "Window manager") articles.

### What makes Arch unique amongst other "minimal" distributions?

See [Arch compared to other distributions](/index.php/Arch_compared_to_other_distributions "Arch compared to other distributions").

## 64-bit

### İşlemcimin x86_64 mimarisine sahip olup olmadığını nasıl öğrenebilirim ?

Eğer işlemciniz [x86_64](https://en.wikipedia.org/wiki/X86-64 "wikipedia:X86-64") mimarisiyle uyumluysa, `/proc/cpuinfo` dosyasında `lm` bayrağını barındıracaktır . Örneğin,

```
$ grep -w lm /proc/cpuinfo

```

Windows altında çalışan makinelerde [CPU-Z](http://www.cpuid.com/cpuz.php) uygulamasını kullanarak işlemcinin 64-bit olup olmadığını kolaylıkla bulunabilir.