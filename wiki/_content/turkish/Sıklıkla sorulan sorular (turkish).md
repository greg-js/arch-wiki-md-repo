## Contents

*   [1 Genel](#Genel)
    *   [1.1 Arch Linux nedir?](#Arch_Linux_nedir.3F)
    *   [1.2 Niçin Arch Linux kullanmamalıyım?](#Ni.C3.A7in_Arch_Linux_kullanmamal.C4.B1y.C4.B1m.3F)
    *   [1.3 Arch hangi işlemci mimarilerini destekliyor?](#Arch_hangi_i.C5.9Flemci_mimarilerini_destekliyor.3F)
    *   [1.4 Arch ARM mimarisini destekliyor mu?](#Arch_ARM_mimarisini_destekliyor_mu.3F)
*   [2 64-bit](#64-bit)
    *   [2.1 İşlemcimin x86_64 mimarisine sahip olduğunu nasıl anlarım?](#.C4.B0.C5.9Flemcimin_x86_64_mimarisine_sahip_oldu.C4.9Funu_nas.C4.B1l_anlar.C4.B1m.3F)
    *   [2.2 Neden 64-bit?](#Neden_64-bit.3F)
    *   [2.3 İşletim sistemini yeniden kurmadan i636 kurulumundan x86_64 kurulumuna geçebilir miyim?](#.C4.B0.C5.9Fletim_sistemini_yeniden_kurmadan_i636_kurulumundan_x86_64_kurulumuna_ge.C3.A7ebilir_miyim.3F)

## Genel

### Arch Linux nedir?

Bilgi için [Arch Linux](/index.php/Arch_Linux "Arch Linux") sayfasını ziyaret edin.

### Niçin Arch Linux kullanmamalıyım?

Arch'ı "kullanmamayı" tercih edebileceğiniz sebepler:

*   arch power user'ları(gelişmiş kullanıcıları) hedefleyen bir GNU/Linux dağıtımıdır. kullanmayı öğrenmek için yeterli yetenek, zaman veya isteğiniz olmayabilir.
*   x86_64 mimarisi haricinde bir mimariye sahipsinizdir.
*   sadece ama sadece açık kaynak yazılımlara destek veren ve sadece ama sadece açık kaynak yazılım sunan bir dağıtım kullanmak konusunda ısrarcısınızdır.
*   basit bir kullanıcısınızdır. işletim sisteminin tüm ayarları sizin için sağlamasını ve yardımcı olmasını istiyorsunuzdur.
*   rolling release -yuvarlanan yayım, her daim en güncel- bir dağıtım kullanmak istemiyorsunuzdur.
*   hali hazırda kullandığınız işletim sisteminizden memnunsunuzdur.

### Arch hangi işlemci mimarilerini destekliyor?

Arch sadece x86_64(amd64 olarak da adlandırılabilir) mimarisini destekler. i636(x86,32 bit) desteği Kasım 2017 itibariyle sonlandırılmıştır. Daha fazla bilgi için:[[1]](https://www.archlinux.org/news/the-end-of-i686-support/). Eğer hâlâ i636 bir kuruluma ve x86_64 mimariye sahip bir işlemciye sahipseniz, [#İşletim sistemini yeniden kurmadan i636 kurulumundan x86_64 kurulumuna geçebilir miyim?](#.C4.B0.C5.9Fletim_sistemini_yeniden_kurmadan_i636_kurulumundan_x86_64_kurulumuna_ge.C3.A7ebilir_miyim.3F) başlığına yönelin. Eğer işlemciniz desteklemiyorsa [Arch Linux 32](https://archlinux32.org/) projesine geçiş yapmayı göz önünde bulundurun.

### Arch ARM mimarisini destekliyor mu?

Resmi olarak hayır. Ama bazı ARM mimarileri için Arch Linux portu geliştiren [Arch Linux ARM](http://archlinuxarm.org/) projesine bakabilirsiniz.

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