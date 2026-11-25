RANGKUMAN MATERI TEORI SISTEM TERDISTRIBUSI DAN TERDESENTRALISASI
PERTEMUAN 3
A. IDENTITAS MATERI
Mata Kuliah: Teori Sistem Terdistribusi dan Terdesentralisasi (Kode: FIF25002T / 3 SKS)
Program Studi: S1 Informatika
Universitas: Universitas Teknologi Digital Indonesia (UTDI)
Pertemuan: 3
Topik Materi: Sinkronisasi dan Koordinasi pada Sistem Terdistribusi
Dosen Pengampu: Dr. Bambang Purnomosidi D. P.
Sumber Materi: `03--sinkronisasi-sistem-terdistribusi.pdf`
AI yang Digunakan: Gemini
Format Dokumen: Markdown (`README.md`)
---
B. TUJUAN PEMBELAJARAN
Berdasarkan materi perkuliahan, tujuan pembelajaran pada pertemuan ini adalah:
Memahami dan mampu menjelaskan mengapa diperlukan sinkronisasi untuk koordinasi pada sistem terdistribusi.
Memahami dan mampu menjelaskan berbagai tantangan sinkronisasi untuk koordinasi pada sistem terdistribusi.
Memahami dan mampu menjelaskan sinkronisasi waktu fisik dan bisa menyebutkan serta menjelaskan berbagai algoritma dan protokolnya.
Memahami dan mampu menjelaskan sinkronisasi waktu logis dan bisa menyebutkan dan menjelaskan beberapa algoritma terkait.
Memahami dan mampu menjelaskan masalah mutual exclusion pada sistem terdistribusi dan berbagai algoritma untuk hal tersebut.
Memahami dan mampu menjelaskan mengapa terdapat masalah pemilihan koordinator dalam sistem terdistribusi dan menjelaskan bagaimana masalah tersebut dipecahkan.
Memahami dan mampu memberikan berbagai contoh studi kasus nyata di industri untuk sinkronisasi dan koordinasi.
---
C. RANGKUMAN MATERI
1. Pengertian dan Pentingnya Sinkronisasi
Sinkronisasi merupakan koordinasi proses, data, dan sumber daya di berbagai node untuk memastikan operasi yang konsisten dan andal. Sinkronisasi mengatasi tantangan dalam menjaga konsistensi data, mengelola proses konkuren, serta mencapai perilaku sistem yang koheren di berbagai node dalam jaringan, sehingga sistem dapat beroperasi dengan lancar, mencegah konflik data (data race), dan menyediakan layanan yang andal serta efisien.
Contoh permasalahan race condition / data race pada sistem terdistribusi yang dicontohkan dalam materi adalah pada perangkat lunak E-Commerce:
Produk X memiliki jumlah stok `10`.
User A dan User B masing-masing akan membeli `1` produk X.
Proses A membaca stok produk X (`10` $\rightarrow$ aman), lalu Proses B juga membaca stok produk X (`10` $\rightarrow$ aman).
Proses A membeli X dan mengurangi stok menjadi `9`, kemudian Proses B juga membeli X dan mengurangi stok menjadi `9`.
Realitasnya terjadi 2 pembelian sehingga seharusnya stok X = `8`, tetapi pencatatan di perangkat lunak menunjukkan 2 pembelian dengan stok X = `9`.
Sinkronisasi menjadi penting karena mendukung:
Integritas data: mencegah data race maupun race conditions.
Sinkronisasi state: menjaga state aplikasi tetap sinkron di semua node, misalnya pada online multiplayer game (mengirimkan posisi pemain, kesehatan, dan inventaris terbaru ke semua klien) dan aplikasi web (menyinkronkan data keranjang belanja pengguna antara browser dan basis data di berbagai perangkat serta sesi).
Koordinasi tasks.
Pengelolaan resources.
Memastikan mekanisme recovery, antara lain dengan me-maintain state.
Utilisasi yang efisien: mencegah operasi redundan.
Load balancing.
Mencegah deadlock.
Memungkinkan scalable operations.
Materi juga membedakan antara Data Race dan Race Condition:
Fitur / Parameter	Data Race	Race Condition
Fokus utama	Akses memori secara bersamaan (concurrent memory access)	Urutan dan waktu eksekusi instruksi (timing & execution sequence)
Level	Low-level (Instrumen CPU / Akses Memori fisik)	High-level (Alur logika aplikasi / Business logic)
Syarat terjadi	1) Ada minimal 2 thread mengakses memori yang sama; 2) Minimal 1 akses adalah operasi write; 3) Tidak ada sinkronisasi (tanpa mutex/lock)	Terjadi ketika kebenaran program bergantung pada urutan eksekusi yang tidak bisa diprediksi
Dampak utama	Undefined behavior, korupsi memori, data tidak konsisten	Output salah, bug logika bisnis (misalnya saldo minus atau eksekusi ganda)
Solusi	Menggunakan Mutex / Lock atau tipe data Atomic	Desain ulang alur kontrol (misalnya Atomic Check-and-Act atau Database Transaction Lock)
Selain itu, materi menampilkan contoh skrip multithreading Python (`multithreads-example.py`) menggunakan modul `threading` dan `time` untuk menjalankan beberapa task konkuren (`A` hingga `E`) dengan `start()` dan `join()`, serta ilustrasi deadlock pada jaringan terdistribusi di mana proses saling menunggu sumber daya yang sedang dialokasikan ke proses lain.
[MODIFIKASI] Contoh kasus e-commerce, increment memori (`x = 10`), dan penarikan saldo bank memperlihatkan bagaimana akses konkuren tanpa kendali urutan maupun penguncian dapat merusak akurasi data atau logika bisnis.
2. Tantangan dari Sinkronisasi
Tantangan yang dihadapi dalam melakukan sinkronisasi pada sistem terdistribusi meliputi:
Network latency dan partitioning
Skalabilitas
Fault-tolerant system
Concurrency control
Data consistency
Sinkronisasi waktu
[MODIFIKASI] Tantangan-tantangan tersebut saling berkaitan karena keterlambatan jaringan, partisi, dan kegagalan komponen dapat memengaruhi konsistensi data serta ketepatan koordinasi antar-node.
3. Sinkronisasi Waktu Fisik
Sinkronisasi waktu fisik adalah proses penyelarasan atau sinkronisasi real-time clock / jam nyata dari sistem terdistribusi dengan standar umum untuk memastikan kesamaan waktu yang konsisten. Mekanisme ini penting untuk korelasi log, penjadwalan event, dan menjaga konsistensi sistem, serta dilakukan dengan protokol dan/atau sinkronisasi dengan sumber berbasis perangkat keras atomic clock dan/atau GPS yang disinkronisasikan dengan atomic clock.
Standar waktu yang dijelaskan dalam materi meliputi:
GMT (Greenwhich Mean Time): sudah tidak digunakan.
UTC (Universal Coordinated Time): didefinisikan oleh ITU (International Telecommunication Union), digunakan sebagai standar sejak tahun 1963, dan berbasis pada TAI (International Atomic Time / Temps Atomique International).
LTC (Coordinated Lunar Time): masih dalam proses pengembangan.
Sumber atomic clock berada pada satelit yang mengorbit (sekitar 30 satelit), antara lain:
GPS Satellites (Earth Orbit): dioperasikan oleh The U.S. Space Force (31 satelit GPS di Medium Earth Orbit / MEO).
Deep Space Atomic Clock (DSAC): diluncurkan oleh NASA pada 2019 di wahana Orbital Test Bed pada orbit rendah Bumi untuk menguji stabilitas.
International Space Station (ISS): misi The Atomic Clock Ensemble in Space (ACES) untuk menempatkan cold-atom clock di orbit rendah Bumi.
Ground Control: pengelolaan master clock di darat dilakukan di U.S. Naval Observatory (Washington, D.C.) dan Schriever Space Force Base (Colorado).
Alur sinkronisasi waktu fisik digambarkan mulai dari master atomic clock $\leftrightarrow$ atomic clock di GPS $\leftrightarrow$ GPS dongle (seperti U-Blox G-7020 melalui daemon `gpsd` dan shared memory RAM) $\leftrightarrow$ Linux server (NTP/PTP) $\leftrightarrow$ client (Linux, Windows, Mac, mobile phone, dll.).
Protokol dan implementasi sinkronisasi waktu fisik yang dibahas dalam materi:
Network Time Protocol (NTP): diperkenalkan tahun 1985 (dikembangkan oleh David L. Mills, Harlan Stenn, dan Network Time Foundation, standar RFC 5905). Contoh implementasinya adalah chrony (`chronyd` dan `chronyc`), yang mendukung sinkronisasi melalui server NTP, reference clock (seperti penerima GPS), maupun input manual, serta dapat berjalan di Linux, FreeBSD, NetBSD, macOS, dan illumos.
Precision Time Protocol (PTP): standar IEEE (IEEE 1588-2002, IEEE 1588-2008 / PTPv2 dengan konsep profile dan adaptasi gPTP / IEEE 802.1AS untuk AVB dan TSN, serta IEEE 1588-2019). Implementasinya di Linux antara lain linuxptp (seperti `ptp4l` untuk Boundary/Ordinary/Transparent Clock dan `phc2sys` untuk menyinkronkan clock), dengan syarat NIC mendukung hardware timestamping (dapat diperiksa melalui `ethtool -T`).
[MODIFIKASI] Sinkronisasi waktu fisik menggabungkan sumber waktu berpresisi tinggi seperti atomic clock dan GPS dengan protokol jaringan seperti NTP atau PTP agar stempel waktu antar mesin lebih selaras.
4. Sinkronisasi Waktu Logis
Sinkronisasi waktu logis merupakan metode yang digunakan dalam sistem terdistribusi untuk menetapkan urutan sebab akibat dari kejadian (causal order of events) dan tidak terkait dengan sinkronisasi dengan waktu fisik di dunia nyata. Prinsip transitivitas menyatakan bahwa jika A terjadi sebelum B dan B terjadi sebelum C, maka A terjadi sebelum C.
Selain Lamport Logical Clock (Leslie Lamport), materi membahas Vector Clocks:
Vector memiliki ukuran dinamis, sedangkan array memiliki ukuran tetap.
Pada kondisi awal untuk 3 proses (A, B, C), masing-masing dimulai dengan `[0, 0, 0]` sesuai posisi indeksnya (A di indeks 0, B di indeks 1, C di indeks 2).
Setiap event / action (baik internal event maupun send/receive message) menambahkan `1` ke spot proses terkait, dan saat menerima pesan dilakukan pembaruan element-wise max.
Aturan urutan: A terjadi sebelum B jika semua angka pada clock A $\le$ semua angka pada clock B dan minimal 1 lebih kecil; bersifat concurrent (independen) jika tidak semua komponen $\le$.
Materi juga menampilkan contoh implementasi Python `vclocks.py` untuk proses `P0`, `P1`, dan `P2`.
[MODIFIKASI] Vector clocks memungkinkan pelacakan hubungan sebab-akibat atau independensi (concurrent) antar kejadian lintas proses secara lebih rinci dibandingkan jam logis skalar tunggal.
5. Tantangan Mutual Exclusion
Mutual exclusion adalah prinsip dalam ilmu komputer yang memastikan hanya satu proses atau thread yang dapat mengakses sumber daya bersama (shared resource, seperti printer, file, atau database) pada satu waktu untuk mencegah konflik dan menjaga integritas data. Bagian kode yang mengakses sumber daya bersama disebut Critical Section (CS).
Empat prinsip utama dalam mutual exclusion meliputi:
Mutual Exclusion: hanya 1 proses yang bekerja pada sumber daya bersama.
Progress: jika tidak ada CS yang bekerja pada sumber daya bersama, maka sumber daya bersama bisa diakses.
Bounded Waiting: tidak ada proses yang menunggu selamanya (waits forever).
Fairness: requests dilayani sesuai dengan urutan yang wajar (reasonable).
Tiga pendekatan algoritma mutual exclusion pada sistem terdistribusi yang dibahas:
Algoritma	Mekanisme Kerja	Kelebihan	Kekurangan
1. Centralized Algorithm	Satu node menjadi koordinator yang memberi izin akses CS jika bebas dan mengizinkan akses berikutnya saat dilepaskan	Sederhana, biaya rendah	Single point of failure, kemungkinan bottleneck
2. Ricart - Agrawala	Terdistribusi penuh (tanpa koordinator); proses mengirim pesan permintaan berstempel waktu dan masuk CS setelah semua proses lain menjawab OK ($2 \times (N - 1)$ pesan: $N - 1$ dikirim dan minimal $N - 1$ dibalas)	Fault tolerant	Overhead pesan tinggi
3. Token-Based Algorithm	Token unik beredar antar proses; proses harus memegang token untuk masuk CS, dan jika hilang perlu mekanisme pemulihan	Hanya 1 pesan per entri CS	Deteksi kehilangan token sulit
[MODIFIKASI] Setiap pendekatan mutual exclusion memiliki trade-off tersendiri antara kesederhanaan, jumlah pesan jaringan, ketahanan terhadap kegagalan, serta risiko bottleneck atau kehilangan token.
6. Pemilihan Koordinator
Dalam sistem terdistribusi, beberapa node (proses) mungkin memerlukan satu koordinator untuk mengelola sumber daya bersama, menyinkronkan operasi, dan membuat keputusan global. Ketika koordinator gagal atau node baru bergabung, sistem harus memilih pemimpin baru secara otomatis.
Algoritma dan mekanisme yang dapat digunakan untuk pemilihan koordinator antara lain:
Bully Algorithm
Ring Algorithm
Raft atau Paxos (berbasis konsensus)
Contoh penerapan di industri yang disebutkan dalam materi:
Apache ZooKeeper menggunakan Zab (ZooKeeper Atomic Broadcast, mirip Paxos).
Kubernetes menggunakan Raft (melalui etcd).
[MODIFIKASI] Pemilihan koordinator secara otomatis memastikan keberlangsungan koordinasi dan pengambilan keputusan global ketika pemimpin lama gagal atau topologi node berubah.
---
D. CONTOH PENERAPAN DAN ANALISIS
Berdasarkan materi perkuliahan, terdapat beberapa contoh penerapan sinkronisasi dan koordinasi pada sistem terdistribusi.
1. Pengelolaan Stok Produk pada Sistem E-Commerce
Konsep yang digunakan:
Sinkronisasi, concurrency control, dan pencegahan race condition / data race.
Cara kerja:
Dua pengguna (User A dan User B) secara bersamaan membaca jumlah stok produk X yang bernilai `10` dan masing-masing melakukan pembelian 1 unit sehingga mengurangi stok menjadi `9`.
[MODIFIKASI] Karena kedua proses membaca nilai awal yang sama sebelum pembaruan tersimpan secara konsisten, salah satu pengurangan stok tertimpa sehingga hasil pencatatan tidak sesuai dengan jumlah pembelian aktual.
Alasan penggunaan:
Menunjukkan perlunya sinkronisasi agar akses konkuren terhadap data bersama tidak menimbulkan inkonsistensi stok atau kesalahan logika transaksi.
Hubungan dengan materi pertemuan:
Contoh ini menggambarkan secara langsung dampak ketiadaan mekanisme sinkronisasi dan kontrol konkurensi pada aplikasi terdistribusi.
2. Sinkronisasi Waktu Menggunakan chrony (NTP) dan linuxptp (PTP) pada Linux
Konsep yang digunakan:
Sinkronisasi waktu fisik menggunakan protokol NTP dan PTP.
Cara kerja:
Daemon `chronyd` berjalan di atas layanan jaringan/lokal untuk menyelaraskan clock sistem dengan sumber waktu NTP dan dipantau melalui `chronyc` (`sources` dan `tracking`), sedangkan implementasi PTP (`ptp4l` dan `phc2sys`) digunakan untuk sinkronisasi presisi tinggi sesuai standar IEEE 1588.
[MODIFIKASI] Penggunaan perangkat lunak seperti `chrony` dan `linuxptp` membantu menjaga keselarasan waktu mesin terhadap pergeseran jam lokal serta memanfaatkan dukungan perangkat keras bila tersedia.
Alasan penggunaan:
Menjaga kesamaan waktu yang konsisten untuk korelasi log, penjadwalan event, dan koordinasi sistem.
Hubungan dengan materi pertemuan:
Contoh ini merepresentasikan implementasi praktis sinkronisasi waktu fisik pada sistem operasi Linux dalam materi.
3. Pelacakan Urutan Kejadian Antar Proses dengan Vector Clocks
Konsep yang digunakan:
Sinkronisasi waktu logis menggunakan Vector Clocks untuk menentukan urutan sebab-akibat (causal order) dan independensi (concurrent).
Cara kerja:
Setiap proses (`A`, `B`, `C` atau `P0`, `P1`, `P2`) mempertahankan vektor nilai clock yang diawali `[0, 0, 0]`, menaikkan nilai pada indeksnya sendiri saat terjadi event, dan melakukan pembaruan element-wise max saat menerima pesan.
[MODIFIKASI] Pembandingan nilai antar vektor memungkinkan sistem mengidentifikasi apakah suatu kejadian mendahului kejadian lain atau berlangsung secara independen tanpa bergantung pada jam fisik.
Alasan penggunaan:
Menetapkan urutan kejadian secara logis dan kausal di lingkungan terdistribusi.
Hubungan dengan materi pertemuan:
Contoh ini memperluas konsep logical clock dari pertemuan sebelumnya ke arah pelacakan kausalitas multikomponen melalui vector clocks.
4. Koordinasi dan Pemilihan Koordinator pada Kubernetes dan Apache ZooKeeper
Materi menyebutkan penggunaan mekanisme konsensus dan pemilihan koordinator pada sistem infrastruktur terdistribusi.
Aspek	Kubernetes (via etcd)	Apache ZooKeeper
Protokol / mekanisme terkait	Raft	Zab (ZooKeeper Atomic Broadcast, mirip Paxos)
Peran dalam materi	Contoh sistem yang menggunakan Raft (berbasis konsensus) untuk koordinasi/pemilihan koordinator	Contoh sistem yang menggunakan Zab untuk koordinasi/pemilihan koordinator
Konteks kebutuhan	Menjaga keselarasan koordinasi dan keputusan global saat terjadi kegagalan atau perubahan node	Menjaga keselarasan koordinasi dan keputusan global saat terjadi kegagalan atau perubahan node
[MODIFIKASI] Pemanfaatan protokol berbasis konsensus seperti Raft dan Zab membantu proses-proses terdistribusi mencapai kesepakatan serta menetapkan koordinator secara teratur ketika node mengalami perubahan atau gangguan.
---
E. PENGGUNAAN AI
Dalam penyusunan rangkuman materi Pertemuan 3 ini, AI digunakan sebagai alat bantu untuk membaca, memahami, mengelompokkan, dan menyusun kembali materi perkuliahan ke dalam format laporan Markdown.
AI yang digunakan:
Gemini.
Prompt yang digunakan:
AI diberikan instruksi untuk meneliti file materi perkuliahan Pertemuan 3 (`03--sinkronisasi-sistem-terdistribusi.pdf`) dan menyusun rangkuman laporan dengan mengikuti struktur dan susunan yang sama persis dengan template laporan yang diberikan.
Instruksi yang diberikan mencakup:
Membaca dan meneliti seluruh halaman PDF materi Pertemuan 3.
Menyusun rangkuman secara runtut berdasarkan isi dan konsep yang terdapat di dalam materi perkuliahan tanpa mengarang informasi di luar materi sumber.
Menyamakan seluruh susunan laporan dari bagian A sampai G sesuai template yang diberikan, termasuk mencantumkan bagian `[MODIFIKASI]` pada setiap poin rangkuman maupun analisis.
Membedakan informasi dari materi sumber dengan tambahan penjelasan menggunakan tanda `[MODIFIKASI]`.
Menghasilkan dokumen Markdown yang siap digunakan sebagai `README.md` di repository GitHub.
Bagian yang disesuaikan:
AI membantu menyusun penjelasan materi berdasarkan slide perkuliahan, mengelompokkan subtopik agar sistematis, menyusun tabel perbandingan, melengkapi setiap poin rangkuman dengan catatan `[MODIFIKASI]`, serta merumuskan bagian contoh penerapan dan analisis yang mengacu pada studi kasus dalam materi.
Keterangan `[MODIFIKASI]`:
Tanda `[MODIFIKASI]` digunakan untuk menunjukkan penjelasan tambahan atau elaborasi analisis yang disusun oleh AI untuk membantu pemahaman. Bagian tersebut bukan merupakan kutipan langsung dari materi dosen.
Hasil rangkuman tetap perlu diperiksa dan dipahami kembali oleh mahasiswa sebelum digunakan sebagai tugas perkuliahan.
---
F. KESIMPULAN
Berdasarkan materi Pertemuan 3, sinkronisasi dan koordinasi diperlukan agar proses, data, dan sumber daya pada berbagai node dalam sistem terdistribusi tetap konsisten, andal, dan terhindar dari konflik seperti data race, race condition, maupun deadlock. Tantangan sinkronisasi mencakup network latency dan partitioning, skalabilitas, fault-tolerant system, concurrency control, data consistency, serta sinkronisasi waktu.
Untuk menyelaraskan waktu dan mengatur akses bersama, sistem terdistribusi memanfaatkan sinkronisasi waktu fisik (berbasis standar seperti UTC/TAI, GPS/atomic clock, serta protokol NTP dan PTP), sinkronisasi waktu logis (seperti Lamport Logical Clock dan Vector Clocks), berbagai algoritma mutual exclusion (Centralized Algorithm, Ricart - Agrawala, dan Token-Based Algorithm), serta mekanisme pemilihan koordinator (Bully Algorithm, Ring Algorithm, serta konsensus Raft/Zab/Paxos).
---
G. DAFTAR REFERENSI
Bambang Purnomosidi D. P. (Tanpa tahun). 03: Sinkronisasi dan Koordinasi pada Sistem Terdistribusi. Materi perkuliahan Teori Sistem Terdistribusi dan Terdesentralisasi (Kode: FIF25002T, 3 SKS), Program Studi Informatika, Fakultas Teknologi Informasi, Universitas Teknologi Digital Indonesia. File: `03--sinkronisasi-sistem-terdistribusi.pdf`.
Sumber ilustrasi, dokumentasi, dan referensi yang dicantumkan dalam materi:
Wikipedia. Coordinated Universal Time. https://en.wikipedia.org/wiki/Coordinated_Universal_Time
NIST. How UTC and NIST Time are Related. https://www.nist.gov/pml/time-and-frequency-division/how-utcnist-related-coordinated-universal-time-utc-international#7114136
GeeksforGeeks. Distributed System - Types of Distributed Deadlock. https://www.geeksforgeeks.org/operating-systems/distributed-system-types-of-distributed-deadlock/
GitHub (bohnelang). gps ntp timeserver. https://github.com/bohnelang/gps_ntp_timeserver
gpsd Documentation. https://gpsd.gitlab.io/gpsd/
u-blox. u-center GNSS software. https://www.u-blox.com/sites/default/files/ublox-GNSS_u-center_windows_v8.21.zip
chrony Project. chrony Introduction. https://chrony-project.org/
LinuxPTP Project. https://linuxptp.nwtime.org/ dan https://linuxptp.sourceforge.net/
Time-Sensitive Networking (TSN) Documentation. Time Synchronization. https://tsn.readthedocs.io/timesync.html
---
INFORMASI DOKUMENTASI GITHUB
Repository: https://github.com/ciaxzs/disdec-teori
Direktori: `03/`
File: `README.md`
