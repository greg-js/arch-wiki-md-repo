Related articles

*   [Arch Linux](/index.php/Arch_Linux "Arch Linux")
*   [The Arch Way](/index.php/The_Arch_Way "The Arch Way")

Halaman ini berisi tentang perbandingan antara Archlinux dengan distribusi GNU/Linux lain serta sistem operasi yang menyerupai UNIX. Sehingga Anda dapat tahu apakah Archlinux adalah sistem operasi yang cocok untuk Anda atau tidak.Namun,mencoba secara langsung Archlinux adalah cara terbaik untuk membandingkan Archlinux dengan sistem operasi lainnya.

## Contents

*   [1 Source-based (Berbasis kode sumber)](#Source-based_.28Berbasis_kode_sumber.29)
    *   [1.1 Gentoo](#Gentoo)
    *   [1.2 Sorcerer/Lunar-Linux/Source Mage](#Sorcerer.2FLunar-Linux.2FSource_Mage)
*   [2 Minimalis](#Minimalis)
    *   [2.1 LFS](#LFS)
    *   [2.2 CRUX](#CRUX)
    *   [2.3 Slackware](#Slackware)
*   [3 Grafikal](#Grafikal)
    *   [3.1 Ubuntu](#Ubuntu)
    *   [3.2 Fedora](#Fedora)
    *   [3.3 Mandriva](#Mandriva)
    *   [3.4 SUSE](#SUSE)
    *   [3.5 PCLinuxOS](#PCLinuxOS)
*   [4 Keluarga *BSDs](#Keluarga_.2ABSDs)
    *   [4.1 FreeBSD](#FreeBSD)
    *   [4.2 NetBSD](#NetBSD)
    *   [4.3 OpenBSD](#OpenBSD)
*   [5 Lainnya](#Lainnya)
    *   [5.1 Debian GNU/Linux](#Debian_GNU.2FLinux)
    *   [5.2 Frugalware](#Frugalware)
*   [6 Pranala eksternal](#Pranala_eksternal)

## Source-based (Berbasis kode sumber)

Distro yang berbasis kode sumber sangat portabel, memberi keuntungan dalam mengontrol dan mengompilasi keseluruhan sistem operasi dan aplikasi-aplikasinya untuk sebagian arsitektur mesin dan skema pemakaian, namun membutuhkan waktu saat proses kompilasi. Basis dan keseluruhan paket Arch dikompilasi untuk arsitektur i686 dan x86_64, menawarkan peningkatan performa yang potensial diantara distro berbasis binari i386/i486/i586, dengan tambahan keuntungan instalasi yang fleksibel/*expedient*.

### Gentoo

Baik Archlinux dan Linux Gentoo, keduanya memakai sistem *rolling release*, yang berarti bahwa paket-paket tersedia bagi distribusi dalam waktu yang singkat setelah pengembang merilis versi vanilanya. Paket Gentoo dibangun dari kode sumber secara langsung sedangkan paket Arch berupa binari *pre-built*. Ini membuat sistem Archlinux lebih cepat dibangun dan dimutakhirkan, dan membuat Linux Gentoo menjadi lebih siap dikustomisasi. Arch mendukung i686 dan x86_64 sedangkan Gentoo mendukung arsitektur x86, ppc, sparc, alpha, amd64, arm, mips, hppa, s390, sh, dan itanium. Karena kedua instalasi Gentoo dan Arch hanya memasang sistem dasar, keduanya disebut sangat mudah dikustomisasi. Pengguna Gentoo akan merasa nyaman dengan sebagian besar aspek Archlinux.

### Sorcerer/Lunar-Linux/Source Mage

Sorcerer/Lunar-Linux/Source Mage (SLS) adalah distro-distro yang semuanya berbasis kode sumber, banyak serupa dengan Gentoo, tetapi aslinya saling terkait antara yang satu dengan yang lainnya. Distro SLS memakai suatu set berkas skrip sederhana untuk membuat deskripsi-deskripsi paket, dan menggunakan berkas konfigurasi global untuk mengonfigurasikan proses kompilasi, serupa seperti [Arch Build System](/index.php/Arch_Build_System "Arch Build System"). Perangkat-perangkat SLS melakukan pengecekan dependensi seutuhnya (termasuk menangani fitur-fitur opsional) dan penelusuran paket (dan *uninstalling/upgrading*). Tidak tersedia paket-paket binari untuk tiap keluarga SLS, meskipun mereka semua bisa *roll back* kembali ke paket-paket yang terpasang dengan mudah.

Instalasi melibatkan pemasangan sistem dasar (seperti Arch: dioptimasi untuk i686, CLI dan menu ncurses, hanya perangkat-perangkat utama), lalu dilanjutkan dengan merekompilasi sistem dasar (sesuai pilihan). Tidak ada WM/DE/DM standar, dan Xorg tidak termasuk dalam instalasi dasar. Beberapa alternatif server X tersedia (X.Org 6.8 atau 7, XFree86).

SLS memiliki riwayat yang sangat komplikatif. Mungkin tulisan terbaik tentang hal itu dapat ditemukan di [the SourceMage wiki](http://wiki.sourcemage.org/SourceMage/History).

## Minimalis

Distro-distro minimalis tepat dibandingkan dengan Arch, memiliki beberapa kesamaan. Semuanya bisa disebut sederhana/*simple* dari sudut pandang teknis.

### LFS

LFS, (atau Linux From Scratch) berupa sebagai dokumentasi. Buku tersebut menginstruksikan pengguna bagaimana mewujudkan suatu set paket dasar yang minimal untuk suatu sistem GNU/Linux yang fungsional, serta bagaimana mengompilasi dan mengonfigurasikan secara manual dari *scratch*. LFS adalah seminimal yang didapatkan, serta menawarkan suatu proses edukasi dan kebaikan dari penyusunan sebuah sistem dasar. Arch menyediakan paket-paket yang sangat serupa, plus init ala BSD, sedikit perangkat ekstra dan pengelola paket [pacman](/index.php/Pacman "Pacman") yang penuh fungsi sebagai sistem dasar, sudah dikompilasi untuk i686/x86-64\. LFS tidak menyediakan repositori daring (dalam jaringan/*online*); kode sumber diperoleh manual, dikompilasi dan di-*install* dengan **make**. (Beberapa metode manual pengelolaan paket tersedia, seperti disebutkan di LFS Hints) Bersama dengan sistem dasar Arch minimal, komunitas Arch dan pengembang menyediakan dan memelihara ratusan paket binari yang siap dipasang via pacman dan skrip [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") untuk digunakan dalam [Arch Build System](/index.php/Arch_Build_System "Arch Build System"). Arch juga memasukkan perangkat [makepkg](/index.php/Makepkg "Makepkg") untuk memudahkan penyusunan dan kustomisasi paket `.pkg.tar.gz`, siap dipasang oleh pacman. Judd Vinet membangun Arch dari *scratch*, lalu menulisnya di C. Dulu, Arch kadang dideskripsikan dengan lelucon *Linux, with a nice package manager (Linux, dengan pengelola paket yang baik).*

### CRUX

Arch dikembangkan independen, dibangun dari *scratch* dan tidak berbasis distribusi GNU/Linux manapun. Sebelum membuat Arch, Judd Vinet lebih memilih dan memakai CRUX, sebuah distro minimalis yang dibuat oleh Per Lidén. Diinspirasi secara alami dari ide-ide bersama CRUX, Arch dibangun dari *scratch*, dan [pacman](/index.php/Pacman "Pacman") lalu ditulis dengan bahasa C. Keduanya memiliki beberapa prinsip panduan: singkatnya, keduanya dioptimasi untuk arsitektur tertentu, minimalis dan berorientasi K.I.S.S. Keduanya menerapkan sistem menyerupai *ports*, memakai sistem init ala *BSD, dan seperti juga *BSD, keduanya menyediakan lingkungan dasar yang minimal untuk dibangun kemudian. Arch memiliki pacman, yang menangani pengelolaan paket sistem binari dan berfungsi baik dengan [Arch Build System](/index.php/Arch_Build_System "Arch Build System"). CRUX memakai sistem kontribusi komunitas yang disebut prt-get, yang dikombinasikan dengan sistem *ports* mereka sendiri, menangani masalah dependensi, tetapi menyusun semua paket dari kode sumber (meskipun instalasi dasar CRUX adalah binari i686). Arch mendukung x86-64 dan i686 secara resmi, sedangkan CRUX hanya i686.

Arch memakai sistem *rolling-release* dan memiliki repositori paket binari di [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"). CRUX menyediakan lebih sedikit paket yang didukung resmi oleh sistem *ports* selain repositori komunitas.

### Slackware

Si perkasa Slackware dan Arch nampak serupa. Dalam hal keduanya adalah distribusi yang sederhana. Terfokus pada eleganisme dan minimalisme. Slackware terkenal karena sifat generik/*non-branding* dan sepenuhnya memakai paket-paket vanilla/asli versi pengembang, termasuk kernel. Arch umumnya hanya menambal untuk menghindari ketidaksinkronan dan menjaga fungsionalitas, jika memang diperlukan. Keduanya memakai skrip init ala BSD. Arch menyediakan sistem manajemen paket via [pacman](/index.php/Pacman "Pacman"), yang mana tidak serupa dengan perangkat standar Slackware, menawarkan resolusi dependensi otomatis dan memungkinkan pemutakhiran sistem otomatis. Para pengguna Slackware umumnya lebih menyukai metode resolusi dependensi manual, menyesuaikan dengan level kontrol sistem yang ada di tangan mereka. Arch bersistem *rolling release*. Slackware lebih konservatif dalam siklus rilis, lebih mengutamakan paket yang terbukti stabil. Arch lebih *bleeding edge* dalam hal ini. Arch menawarkan [Arch Build System](/index.php/Arch_Build_System "Arch Build System"), sebuah sistem menyerupai ports yang aktual. Sistem (*unofficial*) Slackbuild sangat serupa dengan konsep [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"). Para pengguna Slackware umumnya akan merasa nyaman dengan banyak aspek di Arch.

## Grafikal

Kadang disebut distro *newbie*, distro berbasis grafis memiliki banyak kesamaan, meskipun Arch agak berbeda darinya. Arch mungkin menjadi pilihan yang baik jika kamu ingin mempelajari GNU/Linux dengan membangunnya dari sistem dasar yang sangat minimal, sebagai perbandingan instalasi Arch memasang sangat sedikit paket. Distro berbasis grafis mengutamakan penyertaan *installer* GUI (seperti Anaconda milik Fedora) dan perangkat konfigurasi sistem GUI (seperti YaST-nya SUSE). Perbedaan spesifik antar distro dijelaskan di bawah.

Sometimes called "newbie" distros, the graphical distros share a lot of similarities, though Arch is quite different from them. Arch may be a better choice if you want to learn about GNU/Linux by building up from a very minimal base, as an installation of Arch installs very few packages in comparison. Graphical distros tend to ship with GUI installers (like Fedora's Anaconda) and GUI system-configuration tools (like SUSE's YaST). Specific differences between distros are described below.

### Ubuntu

Ubuntu adalah sebuah distro besar berbasis Debian yang populer disponsori oleh Canonical Ltd. secara komersial, sedangkan Arch adalah sistem yang dikembangkan independen dari *scratch*. Kedua proyek memiliki tujuan yang berbeda dan ditargetkan untuk basis pengguna yang berlainan. Arch didesain bagi pengguna yang berkeyakinan untuk mampu menerima pendekatan *do-it-yourself*, sedangkan Ubuntu menyediakan sistem yang mampu melakukan autokonfigurasi yang lebih menekankan distribusi untuk semua. Jika kamu ingin menyelesaikan sesuatu dengan lebih cepat dan tidak ingin berkutat dengan keruwetan sistem, Ubuntu lebih cocok. Arch disajikan sebagai desain minimalis dari awal instalasi, memberi seluruh kuasa pada pengguna untuk melakukan kustomisasi agar sesuai dengan keinginan spesifik pengguna itu sendiri. Umumnya, para pengembang dan pengoprek akan lebih menyukai Arch dibanding Ubuntu, meskipun beberapa pengguna Arch mengklaim memulai dari Ubuntu dan akhirnya bermigrasi ke Arch. Ubuntu memiliki siklus rilis tiap 6 bulan, sedangkan Arch adalah sebuah sistem *rolling release*. Arch menawarkan sistem paket menyerupai *ports*, disebut [Arch Build System](/index.php/Arch_Build_System "Arch Build System"), sedangkan Ubuntu tidak. Kedua komunitas memiliki perbedaan di beberapa hal. Komunitas Arch jauh lebih kecil dan sangat proaktif; sebuah persentase yang besar berkontribusi ke distro. Sebaliknya, komunitas Ubuntu cukup besar dan oleh karenanya dapat ditoleransi banyaknya persentase jumlah pengguna yang tidak berkontribusi pada pengembangan, paket atau pemeliharaan.

### Fedora

Fedora adalah distribusi turunan Red Hat dan terus menjadi salah satu distribusi paling populer saat ini. Ada banyak komunitas, paket *pre-built* dan dukungan yang tersedia. Paket-paket Fedora berbasis RPM, memakai YUM sebagai pengelola paket. Arch memakai [pacman](/index.php/Pacman "Pacman") untuk mengelola paket-paket `.pkg.tar.gz`. Fedora dikenal tidak mencoba untuk mendukung format media MP3 terkait isu paten. Arch lebih lunak dalam memandang MP3 dan format media lain. Fedora menawarkan *installer* berbasis teks dan grafis. Arch tidak menawarkan *installer* grafis, tapi justru, memakai *installer* berbasis ncurses, menyerahkan konfigurasi manual ke pengguna. Fedora memiliki siklus rilis terjadwal. Arch adalah sistem *rolling-release*. Pendekatan desain Arch lebih kepada ringan, elegan, dan minimalis dibanding otomatis/autokonfigurasi. Fedora memberi inovasi dan banyak menarik minat komunitas terkait integrasi paket-paket kompilasi SELinux dan GCJ untuk melepas ketergantungan pada paket JRE milik Sun. Fedora tidak mendukung JFS dan ReiserFS secara langsung.

### Mandriva

Linux Mandriva (awalnya Linux Mandrake) lahir tahun 1998 dengan tujuan membuat GNU/Linux mudah bagi siapa saja. Berbasis RPM dan paket manajer *urpmi*. Lagi, Arch memilih pendekatan yang lebih sederhana, berbasis teks dan lebih mengandalkan konfigurasi manual dan lebih ditujukan ke pengguna tingkat menengah ke atas.

### SUSE

SUSE mengemuka terkait perangkat konfigurasi yang sangat baik, YaST, yang merupakan *one-stop shop* bagi semua kebutuhan pengguna. Arch tidak menawarkan fasilitas serupa karena bertentangan dengan [The Arch Way](/index.php/The_Arch_Way "The Arch Way"). SUSE, oleh karenanya, lebih luas disarankan karena lebih cocok bagi pengguna yang kurang berpengalaman, atau bagi mereka yang menginginkan lingkungan berbasis GUI, konfigurasi otomatis dan diharapkan berfungsi langsung/*out of the box*.

### PCLinuxOS

PCLinuxOS (PCLOS) adalah sebuah distro populer yang berbasis Mandriva menyediakan sebuah lingkungan desktop yang komplit, didesain untuk ramah pengguna dan dideskripsikan sebagai *sederhana/simple*, yang mana definisi *simple* tersebut berbeda dengan definisi yang Arch pakai. Arch didesain sebagai sistem dasar yang dikustomasi dari dasar dan ditujukan lebih kepada para pengguna tingkat lanjut. Pengguna PCLOS memakai pengelola paket apt sebagai pelengkap paket-paket RPM. Arch memakai pengelola paket [pacman](/index.php/Pacman "Pacman") yang dikembangkan sendiri dengan paket-paket `.pkg.tar.gz`. PCLOS sangat kental nuansa GUI-nya, menyediakan perangkat konfigurasi perangkat keras/*hardware* dan antarmuka pengelola paket Synaptic, dan diklaim memiliki sedikit atau bahkan tanpa perlu memakai terminal/*console* lagi. Arch berorientasi *command-line* dan didesain dengan pendekatan yang lebih sederhana untuk konfigurasi sistem, pengelolaan dan pemeliharaan. PCLOS merekomendasikan RAM 256MB sebagai bagian kebutuhan sistem minimal. Untuk menjadi ringan/*lightweight', Arch dapat berjalan di atas sistem dengan memori rendah, memerlukan RAM hanya 64MB untuk memasang sistem dasar i686, dan berjalan sangat lancar di atas sistem yang lebih modern.*

## Keluarga *BSDs

Arch dan *BSD keduanya menawarkan sistem dasar yang terintegrasi erat dan *ports* dikombinasikan dengan paket-paket binari yang tersedia. Keluarga BSD datang dari Berkeley <tt>UNIX</tt>. Sehingga, keluarga *BSD bukanlah distro GNU/Linux, tapi lebih pada sistem operasi yang menyerupai <tt>UNIX</tt>.

### FreeBSD

Arch dan [FreeBSD](http://www.freebsd.org/about.html) menawarkan perangkat lunak yang dapat disusun memakai binari atau dikompilasi memakai sistem *ports*. Keduanya memakai sistem init yang serupa. FreeBSD lebih sebagai sebuah desain sistem secara keseluruhan, dibandingkan dengan distro GNU/Linux, dimana tiap aplikasi di-*port* ke FreeBSD dan dipastikan berfungsi di tiap proses. Keduanya memakai berkas `/etc/rc.conf` sebagai konfigurasi utama. Lisensi FreeBSD lebih protektif bagi *coder*, dibandingkan dengan GPL, yang kontras dilihat dari sisi proteksi terhadap *code* itu sendiri. Arch dirilis di bawah GPL. Di FreeBSD, seperti Arch, keputusan diserahkan pada pengguna, *power user*. Ini mungkin perbandingan paling menarik bagi Arch karena serupa *head-to-head* dalam modernitas paket dan komunitas yang bisa dihitung, cerdas, aktif, *no-nonsense*. Kedua sistem memiliki banyak persamaan dan para pengguna FreeBSD umumnya akan merasa nyaman dengan banyak aspek di Arch.

### NetBSD

NetBSD adalah sistem operasi *open source* menyerupai <tt>UNIX</tt> yang bebas, aman, dan sangat portabel, tersedia untuk lebih dari 50 arsitektur mesin, dari mesin 64-bit Opteron dan sistem desktop sampai perangkat genggam/*hand-held* dan *embedded devices*. Desain rapi dan fitur tingkat lanjut menjadikannya sempurna di lingkungan produksi dan riset, serta didukung pengguna dengan kelengkapan sumber kode. Banyak aplikasi dengan mudah tersedia melalui pkgsrc, *the NetBSD Packages Collection*. Arch tidak berjalan di banyak perangkat seperti yang NetBSD mampu, tapi untuk sebuah sistem i686, Arch menawarkan lebih banyak aplikasi. Juga, metode instalasi standar di pkgsrc adalah melalui kompilasi kode sumber dimana Arch menawarkan paket-paket binari. Arch punya banyak kesamaan dengan NetBSD; keduanya memakai berkas `/etc/rc.conf` sebagai alat konfigurasi utama, mereka sangat minimalis dan ringan, keduanya menawarkan sistem *ports*, binari, dan sama-sama aktif, komunitas dan pengembang yang *no-nonsense*. Arch juga meminjam konsep sistem init *BSD.

### OpenBSD

Proyek OpenBSD memproduksi sebuah sistem operasi menyerupai <tt>UNIX</tt> yang bebas, *multi-platform* berbasis 4.4BSD. Usaha mereka fokus pada portabilitas, standardisasi, kesesuaian kode, keamanan yang proaktif, dan kriptografi terintegrasi. Sebaliknya, Arch lebih fokus pada kesederhanaan, elegan, minimalisme dan perangkat lunak terkini/*bleeding edge*. OpenBSD mendukung emulasi banyak program mulai dari SVR4 (Solaris), FreeBSD, GNU/Linux, BSD/OS, SunOS dan HP-UX. OpenBSD mendeskripsikan diri sebagai *perhaps the #1 security OS*.

Dibandingkan dengan Arch, OpenBSD menawarkan instalasi paket dasar yang kecil, elegan, memakai sistem *ports* dan sistem pemaketan untuk memudahkan instalasi dan pengelolaan program yang bukan bawaan sistem operasi dasar. Kontras dengan sistem GNU/Linux seperti Arch, tapi umum terdapat di sistem operasi berbasis BSD, kernel OpenBSD dan programnya, seperti *shell* dan perangkat-perangkat umum (misalnya ls, cp, cat dan ps), dikembangkan bersama di satu repositori sumber.

## Lainnya

Sistem operasi berikut masuk dalam kategori 'lain'.

### Debian GNU/Linux

Debian adalah suatu proyek dan komunitas yang sangat besar dan memiliki fitur cabang *stable*, *testing*, dan *unstable*, menawarkan lebih dari 20.000 paket-paket binari. Arch tidak membagi paket-paket mereka ke dalam kategori *-dev* dan *-common* seperti yang Debian lakukan, oleh karena itu, repositori Arch akan nampak lebih kecil. Debian memiliki sikap yang lebih keras pada perangkat lunak bebas. Arch lebih lunak dalam pemakaian paket-paket *non-free* seperti yang didefinisikan oleh GNU. Pendekatan desain Debian lebih fokus pada stabilitas dan pengujian yang ketat. Arch lebih fokus pada filosofi kesederhanaan, minimalisme, dan menawarkan perangkat lunak *bleeding edge*. Paket-paket Arch lebih mutakhir/baru/terkini dibanding Debian Stable dan Testing, setara dengan Debian Unstable. Baik Debian dan Arch menawarkan sistem manajemen paket yang disegani. Arch adalah sebuah *rolling release*, sedangkan Debian Stable dirilis dengan paket-paket *frozen*. Debian tersedia untuk banyak arsitektur, seperti alpha, arm, hppa, i386, x86_64, ia64, m68k, mips, mipsel, powerpc, s390, dan sparc, sedangkan Arch hanya i686 dan x86_64\. Arch menyediakan dukungan yang lebih untuk membangun sistem sesuai selera pengguna, memasang paket-paket dari kode sumber lain, dengan sistem pembangunan paket menyerupai *ports*. Debian tidak menyediakan sistem *ports*, mengandalkan hanya repositori binari dalam jumlah besar. Instalasi sistem Arch hanya menawarkan suatu paket dasar minimal, yang dipaparkan transparan selama konfigurasi sistem, sedangkan metode Debian menawarkan pendekatan yang lebih otomatis juga beberapa metode instalasi alternatif. Debian memanfaatkan SysVinit, sedangkan Arch memakai init yang lebih sederhana ala *BSD.

### Frugalware

Arch berorientasi berbasis teks dan *command-line*. Frugalware mengadopsi [pacman](/index.php/Pacman "Pacman") milik Arch sebagai pengelola paket, tetapi memakai *bzipped tarballs*. Sebaliknya, Arch memakai *gzipped tarballs*, dengan tujuan memudahkan instalasi. Frugalware pada dasarnya tidak mendukung sistem berkas JFS. Frugalware tidak lagi berbasis Slackware tetapi lebih sebagai distro tersendiri, dan dipromosikan sebagai sebuah distro i686\. Arch dasarnya adalah sistem yang berbeda, diinstal sebagai lingkungan dasar yang minimal dan diperlengkap dengan pacman sesuai kebutuhan dan pilihan penggunanya. Frugalware diinstal dari DVD, dengan pilihan perangkat lunak dan lingkungan desktop yang sudah tersedia bagi pengguna. Frugalware memiliki siklus rilis terjadwal. Lagi, Arch lebih fokus pada kesederhanaan, minimalisme, kesesuaian kode dan kemutakhiran dengan model rolling-release.

## Pranala eksternal

*   [DistroWatch.com](http://distrowatch.com/)