# RANGKUMAN MATERI TEORI SISTEM TERDISTRIBUSI DAN TERDESENTRALISASI

## PERTEMUAN 1

### A. IDENTITAS MATERI

- **Mata Kuliah:** Teori Sistem Terdistribusi dan Terdesentralisasi
- **Program Studi:** S1 Informatika
- **Universitas:** Universitas Teknologi Digital Indonesia (UTDI)
- **Pertemuan:** 1
- **Topik Materi:** Pengenalan Sistem Terdistribusi dan Terdesentralisasi
- **Dosen Pengampu:** Dr. Bambang Purnomosidi D. P.
- **Sumber Materi:** 01--pengenalan.pdf
- **AI yang Digunakan:** ChatGPT (GPT-6)
- **Format Dokumen:** Markdown (README.md)

---

### B. TUJUAN PEMBELAJARAN

Berdasarkan materi perkuliahan, tujuan pembelajaran pada pertemuan ini adalah:

1. Mampu menjelaskan konsep sistem terdistribusi.
2. Mampu menjelaskan konsep sistem terdesentralisasi.
3. Mampu menjelaskan perbedaan sistem terdistribusi dengan sistem terdesentralisasi.
4. Mampu menyebutkan berbagai contoh penerapan nyata dari sistem terdistribusi dan terdesentralisasi.
5. Mampu menyebutkan berbagai tantangan dan tren terbaru di dunia sistem terdistribusi dan terdesentralisasi.

---

### C. RANGKUMAN MATERI

#### 1. Arti Penting Sistem Terdistribusi dan Terdesentralisasi

Sistem terdistribusi dan terdesentralisasi menjadi bagian penting dalam perkembangan teknologi informasi modern. Hal ini disebabkan oleh pertumbuhan jumlah data dan pengguna yang semakin besar, sehingga layanan digital membutuhkan sistem yang mampu menangani peningkatan beban kerja.

Layanan modern tidak hanya membutuhkan kapasitas yang besar, tetapi juga harus memiliki skalabilitas, toleransi terhadap kegagalan (*fault tolerance*), performa yang baik, serta ketersediaan layanan selama 24 jam sehari dan 7 hari seminggu.

Tanpa adanya sistem terdistribusi dan terdesentralisasi, berbagai layanan teknologi modern seperti Google, Netflix, dan Blockchain akan sulit diwujudkan.

Beberapa konsep penting yang mendukung kebutuhan tersebut adalah:

- **Skalabilitas:** Kemampuan suatu sistem, jaringan, proses, atau organisasi untuk berkembang dan menangani peningkatan beban kerja, pengguna, atau permintaan tanpa mengorbankan kinerja maupun kualitas.
- **Fault-Tolerant:** Kemampuan sistem untuk tetap beroperasi secara normal meskipun terjadi kegagalan atau malfungsi pada sebagian komponennya, baik perangkat keras (*hardware*) maupun perangkat lunak (*software*).

Dengan demikian, sistem terdistribusi dan terdesentralisasi diperlukan untuk mendukung layanan digital yang mampu berkembang, tetap tersedia, dan dapat diandalkan.

#### 2. Pengertian Sistem Terdistribusi

Menurut Andrew S. Tanenbaum dan Maarten van Steen (2007), sistem terdistribusi merupakan kumpulan komputer independen yang bagi penggunanya terlihat sebagai satu kesatuan sistem yang utuh (*a collection of independent computers that appears to its users as a single coherent system*).

Berdasarkan pengertian tersebut, sistem terdistribusi terdiri dari beberapa komputer atau komponen yang bekerja secara independen, tetapi saling berkomunikasi melalui jaringan untuk menjalankan suatu layanan.

Beberapa karakteristik dasar sistem terdistribusi meliputi:

- **Komponen independen:** Setiap komputer atau komponen dapat bekerja secara mandiri.
- **Komunikasi melalui jaringan:** Komponen-komponen sistem saling berkomunikasi untuk bertukar informasi dan menjalankan proses.
- **Transparansi:** Pengguna tidak harus mengetahui bagaimana komponen internal sistem bekerja.

Dalam materi dijelaskan beberapa bentuk transparansi, yaitu:

1. **Transparansi lokasi:** Pengguna tidak perlu mengetahui lokasi fisik sumber daya yang digunakan.
2. **Transparansi akses:** Penggunaan sumber daya dapat dilakukan tanpa harus mengetahui mekanisme internal aksesnya.
3. **Transparansi replikasi:** Pengguna tidak perlu mengetahui bahwa suatu data atau sumber daya memiliki beberapa salinan.
4. **Transparansi kegagalan:** Sistem berusaha menyembunyikan atau menangani kegagalan komponen agar tidak selalu terlihat oleh pengguna.

Transparansi tersebut membuat sistem terdistribusi dapat memberikan pengalaman penggunaan yang terlihat seperti menggunakan satu sistem, meskipun sebenarnya proses berlangsung pada beberapa komputer yang saling terhubung.

#### 3. Arsitektur Sistem Dasar

Dalam sistem terdistribusi, terdapat beberapa bentuk arsitektur dasar yang menggambarkan bagaimana komputer atau komponen saling berhubungan.

**a. Client-Server**

Client-Server merupakan arsitektur yang melibatkan dua peran utama, yaitu client dan server.

Client bertugas mengirimkan permintaan layanan, sedangkan server bertugas menerima permintaan, memprosesnya, dan memberikan respons kepada client.

Contohnya, ketika pengguna membuka sebuah aplikasi atau website, perangkat pengguna bertindak sebagai client yang mengirimkan permintaan kepada server melalui jaringan internet.

**b. Peer-to-Peer (P2P)**

Peer-to-Peer merupakan arsitektur jaringan yang memungkinkan setiap komputer atau perangkat (*peer*) berkomunikasi dan berbagi sumber daya secara langsung dengan perangkat lainnya.

Dalam arsitektur ini, setiap peer dapat berperan sebagai penyedia maupun pengguna sumber daya. Dengan demikian, hubungan antarperangkat tidak sepenuhnya bergantung pada satu server pusat.

Salah satu contoh penerapannya adalah BitTorrent, yang memungkinkan pengguna saling berbagi bagian file melalui jaringan P2P.

**c. Hybrid**

Arsitektur Hybrid merupakan kombinasi dari beberapa pendekatan arsitektur, khususnya Client-Server dan Peer-to-Peer.

Dalam pendekatan ini, sebagian fungsi dapat dikelola oleh komponen yang memiliki peran seperti server, sedangkan komunikasi atau pertukaran sumber daya tertentu dapat berlangsung secara langsung antarkomponen.

Materi menampilkan ilustrasi arsitektur Hybrid yang menggabungkan hubungan client-server dan peer-to-peer.

Secara umum, ketiga arsitektur tersebut memiliki pola hubungan yang berbeda dalam mengatur komunikasi dan pertukaran informasi antarkomponen.

#### 4. Karakteristik Sistem Terdistribusi

Berdasarkan materi perkuliahan, terdapat lima karakteristik utama sistem terdistribusi:

1. **Transparansi Lokasi**

   Sistem memungkinkan pengguna mengakses sumber daya tanpa harus mengetahui lokasi fisik tempat sumber daya tersebut berada.

2. **Skalabilitas**

   Sistem mampu berkembang untuk menangani peningkatan jumlah pengguna, data, maupun permintaan layanan.

3. **Fault Tolerance**

   Sistem memiliki kemampuan untuk tetap berjalan meskipun terdapat komponen yang mengalami kegagalan.

4. **Kinerja Tinggi**

   Pembagian proses dan sumber daya ke beberapa komponen dapat mendukung peningkatan kinerja sistem.

5. **Heterogenitas**

   Sistem dapat melibatkan berbagai jenis perangkat keras, perangkat lunak, sistem operasi, maupun teknologi jaringan yang berbeda.

Kelima karakteristik tersebut mendukung kemampuan sistem terdistribusi dalam menyediakan layanan yang dapat diakses oleh banyak pengguna dengan kebutuhan yang beragam.

#### 5. Pengertian Sistem Terdesentralisasi

Sistem terdesentralisasi merupakan sistem yang mendistribusikan kontrol atau kendali kepada beberapa pihak atau komponen, sehingga tidak bergantung pada satu titik pengendalian utama.

Untuk memahami konsep ini, perlu dibedakan terlebih dahulu antara sentralisasi dan desentralisasi.

- **Sentralisasi:** Sistem memiliki satu titik kontrol utama yang mengatur keseluruhan proses.
- **Desentralisasi:** Kontrol didistribusikan ke beberapa pihak atau komponen sehingga tidak bergantung pada satu titik pengendalian.

Salah satu karakteristik penting sistem terdesentralisasi adalah tidak adanya *single point of failure*, yaitu satu titik kegagalan yang dapat menyebabkan keseluruhan sistem terganggu.

Selain itu, keputusan dalam sistem terdesentralisasi dapat dilakukan secara kolektif melalui mekanisme konsensus. Mekanisme ini memungkinkan beberapa pihak mencapai kesepakatan mengenai keputusan atau kondisi sistem.

Contoh sistem terdesentralisasi yang disebutkan dalam materi antara lain:

- Blockchain.
- DNS (Domain Name System).
- BitTorrent.

Materi juga menampilkan ilustrasi dari Paul Baran (1964) yang membandingkan tiga bentuk jaringan, yaitu:

1. **Centralized:** Jaringan memiliki satu pusat pengendalian yang terhubung dengan berbagai titik lainnya.
2. **Decentralized:** Jaringan memiliki beberapa pusat atau kelompok pengendalian.
3. **Distributed:** Jaringan terdiri dari banyak titik yang saling terhubung dan tidak bergantung pada satu pusat saja.

Ilustrasi tersebut membantu menjelaskan perbedaan pola hubungan dan pengendalian dalam sebuah jaringan.

#### 6. Perbedaan Sistem Terdistribusi dan Sistem Terdesentralisasi

Sistem terdistribusi dan sistem terdesentralisasi memiliki hubungan yang erat, tetapi keduanya mempunyai fokus yang berbeda.

Sistem terdistribusi lebih menekankan pada pembagian beban kerja dan sumber daya ke beberapa komputer atau komponen. Sementara itu, sistem terdesentralisasi lebih menekankan pada pembagian kontrol atau kewenangan pengambilan keputusan.

Perbedaan keduanya dapat dilihat pada tabel berikut.

| Aspek | Sistem Terdistribusi | Sistem Terdesentralisasi |
|---|---|---|
| Fokus utama | Pembagian beban kerja | Pembagian kontrol |
| Tujuan | Mendukung pemrosesan dan pengelolaan sumber daya pada beberapa komputer | Menghindari ketergantungan pada satu titik pengendalian |
| Pengelolaan | Komponen bekerja bersama melalui jaringan | Kontrol didistribusikan ke beberapa pihak atau komponen |
| Contoh | Google File System dan MinIO Object Storage | Blockchain |

Berdasarkan materi, contoh sistem terdistribusi adalah Google File System dan MinIO Object Storage (yang disebutkan dalam materi telah di-*fork* menjadi Silo). Sementara itu, Blockchain menjadi salah satu contoh sistem terdesentralisasi.

Dengan demikian, perbedaan paling mendasar terletak pada hal yang didistribusikan. Sistem terdistribusi membagi beban kerja, sedangkan sistem terdesentralisasi membagi kendali.

#### 7. Studi Kasus Sistem Terdistribusi

Materi memberikan beberapa contoh penerapan sistem terdistribusi dalam teknologi modern.

**a. Google File System (GFS) dan HDFS**

Google File System dan HDFS digunakan sebagai contoh teknologi penyimpanan data berukuran besar. Keduanya berkaitan dengan kebutuhan untuk mengelola data melalui sistem penyimpanan yang terdistribusi.

**b. Apache Kafka dan Apache Pulsar**

Kedua teknologi ini merupakan contoh sistem yang digunakan untuk kebutuhan *messaging* dan *streaming*. Teknologi tersebut berkaitan dengan pertukaran serta pengelolaan aliran pesan atau data.

**c. Netflix dan Twitch**

Kedua layanan ini disebutkan sebagai contoh penerapan sistem terdistribusi dalam penyediaan layanan digital.

**d. YouTube**

YouTube merupakan salah satu contoh layanan digital yang membutuhkan dukungan infrastruktur untuk melayani pengguna dan distribusi konten dalam jumlah besar.

**e. Instagram, Threads, Facebook, dan TikTok**

Platform media sosial tersebut menjadi contoh layanan modern yang membutuhkan sistem untuk menangani banyak pengguna, data, serta aktivitas secara bersamaan.

Contoh-contoh tersebut memperlihatkan bahwa sistem terdistribusi banyak digunakan dalam layanan digital yang membutuhkan kemampuan pemrosesan, penyimpanan, dan penyediaan layanan dalam skala besar.

#### 8. Studi Kasus Sistem Terdesentralisasi

Selain sistem terdistribusi, materi juga memberikan beberapa contoh penerapan sistem terdesentralisasi.

**a. Blockchain**

Blockchain merupakan salah satu contoh sistem terdesentralisasi. Beberapa platform Blockchain yang disebutkan dalam materi adalah:

- Bitcoin.
- Ethereum.
- Algorand.
- Sui.
- Near.
- Aptos.

Blockchain berkaitan dengan pengelolaan data dan mekanisme kesepakatan antarpartisipan dalam jaringan.

**b. DNS (Domain Name System)**

DNS merupakan sistem yang digunakan untuk membantu proses penerjemahan nama domain menjadi alamat IP. Dalam materi, DNS dicantumkan sebagai salah satu contoh sistem terdesentralisasi.

**c. BitTorrent**

BitTorrent merupakan teknologi berbagi file yang menggunakan pendekatan Peer-to-Peer. Pengguna dapat saling bertukar bagian file melalui jaringan tanpa sepenuhnya bergantung pada satu server pusat.

Ketiga contoh tersebut menunjukkan penerapan konsep pembagian kontrol maupun sumber daya dalam lingkungan jaringan.

#### 9. CAP Theorem (Brewer's Theorem)

CAP Theorem merupakan konsep penting dalam perancangan sistem terdistribusi, khususnya sistem penyimpanan data (*distributed data store*).

Konsep ini dikaitkan dengan Eric Brewer pada tahun 2000 dan menjelaskan tiga aspek utama, yaitu Consistency, Availability, dan Partition Tolerance.

**a. Consistency**

Consistency atau konsistensi berarti setiap operasi pembacaan data akan mengembalikan hasil penulisan terbaru atau menghasilkan error.

Dengan kata lain, sistem berusaha memastikan bahwa data yang dibaca sesuai dengan data terbaru yang telah ditulis.

**b. Availability**

Availability atau ketersediaan berarti setiap permintaan yang diterima oleh node yang tidak mengalami kegagalan akan mendapatkan respons yang tidak berupa error, meskipun data yang diberikan belum tentu merupakan data terbaru.

**c. Partition Tolerance**

Partition Tolerance merupakan kemampuan sistem untuk tetap beroperasi dan berfungsi ketika komunikasi antar-node terputus atau mengalami fragmentasi jaringan.

Dalam sistem terdistribusi, ketiga aspek tersebut memiliki hubungan yang menghasilkan suatu trade-off.

Materi menjelaskan bahwa pada distributed data store, Consistency dan Availability tidak dapat diperoleh secara bersamaan ketika terjadi network partition. Oleh karena itu, sistem harus menentukan prioritas antara konsistensi dan ketersediaan selama kondisi tersebut berlangsung.

Dua pendekatan yang dijelaskan adalah:

**1. AP (Availability + Partition Tolerance)**

Pendekatan AP mengutamakan ketersediaan layanan dan toleransi terhadap gangguan jaringan.

Permintaan terhadap data tetap dilayani meskipun terdapat risiko data yang diberikan belum sinkron atau belum konsisten.

Karakteristik:
- Permintaan tetap dilayani.
- Sistem tetap tersedia ketika terjadi partition.
- Konsistensi data dapat dikorbankan sementara.

Contoh yang disebutkan dalam materi: MongoDB.

**2. CP (Consistency + Partition Tolerance)**

Pendekatan CP mengutamakan konsistensi data dan toleransi terhadap gangguan jaringan.

Ketika terjadi partition, permintaan pembacaan maupun penulisan data dapat ditolak untuk menjaga agar data tetap konsisten.

Karakteristik:
- Konsistensi data diprioritaskan.
- Sistem tetap mempertahankan toleransi terhadap partition.
- Ketersediaan layanan dapat dikorbankan sementara.

Contoh yang disebutkan dalam materi: Apache Casandra.

Perbandingan kedua pendekatan tersebut dapat dilihat pada tabel berikut.

| Aspek | AP | CP |
|---|---|---|
| Prioritas | Availability | Consistency |
| Partition Tolerance | Dipertahankan | Dipertahankan |
| Respons permintaan | Tetap dilayani | Dapat ditolak |
| Kondisi data | Berisiko belum sinkron | Konsistensi dipertahankan |
| Contoh dalam materi | MongoDB | Apache Casandra |

Materi juga menjelaskan bahwa setelah gangguan jaringan berakhir, sistem dapat melakukan *auto healing* untuk memulihkan kondisi sistem.

#### 10. Konsistensi Data

Konsistensi data merupakan aspek penting dalam sistem terdistribusi karena data dapat disimpan atau diproses pada beberapa komponen yang saling berkomunikasi.

Materi menjelaskan dua jenis konsistensi data.

**a. Strong Consistency**

Strong Consistency merupakan kondisi ketika hasil pembacaan data selalu sama dengan kondisi data terbaru yang seharusnya terlihat oleh pengguna.

Pendekatan ini penting untuk sistem yang membutuhkan ketepatan dan keseragaman informasi.

Contoh dalam materi adalah sistem perbankan. Informasi saldo dan transaksi harus memiliki konsistensi yang kuat agar tidak menimbulkan perbedaan informasi.

**b. Eventual Consistency**

Eventual Consistency merupakan kondisi ketika data tidak harus langsung konsisten pada seluruh komponen, tetapi akan mencapai keadaan konsisten setelah beberapa waktu.

Pendekatan ini dapat digunakan pada sistem yang masih dapat menerima keterlambatan sinkronisasi data.

Contoh dalam materi adalah media sosial. Perubahan informasi atau aktivitas pengguna tidak selalu harus langsung terlihat secara bersamaan pada seluruh pengguna.

Perbandingan kedua jenis konsistensi tersebut adalah:

| Aspek | Strong Consistency | Eventual Consistency |
|---|---|---|
| Kondisi data | Hasil pembacaan mengikuti data terbaru | Data dapat berbeda sementara |
| Sinkronisasi | Konsistensi harus terjaga | Konsistensi tercapai setelah beberapa waktu |
| Contoh | Sistem perbankan | Media sosial |

Pemilihan jenis konsistensi perlu disesuaikan dengan kebutuhan sistem dan karakteristik layanan yang dikembangkan.

#### 11. Tantangan dalam Sistem Terdistribusi dan Terdesentralisasi

Dalam penerapannya, sistem terdistribusi dan terdesentralisasi memiliki beberapa tantangan yang perlu diperhatikan.

**a. Latency dan Throughput**

Kedua istilah ini berkaitan dengan performa sistem.

- **Latency:** Waktu yang dibutuhkan untuk memproses suatu permintaan atau aktivitas.
- **Throughput:** Jumlah permintaan atau pekerjaan yang dapat diproses dalam periode waktu tertentu.

Sistem perlu memperhatikan kedua aspek tersebut agar mampu memberikan layanan dengan respons yang baik dan kapasitas pemrosesan yang memadai.

**b. Keamanan**

Keamanan menjadi tantangan penting karena sistem melibatkan banyak komponen dan komunikasi melalui jaringan.

Materi menyebutkan dua contoh ancaman keamanan, yaitu:

- DDoS (*Distributed Denial of Service*).
- Sybil Attack.

Sybil Attack merupakan jenis serangan siber yang dilakukan dengan membuat banyak identitas palsu, seperti akun, node, atau pseudonim, secara bersamaan untuk mendominasi pengaruh, suara, maupun reputasi dalam suatu jaringan.

Serangan ini biasanya berkaitan dengan sistem terdesentralisasi, seperti jaringan Peer-to-Peer dan Blockchain.

Dengan menyamar sebagai banyak pengguna yang sah, penyerang dapat memanipulasi sistem, merusak integritasnya, melakukan tindakan tidak sah, serta berpotensi memperoleh akses ke informasi sensitif.

**c. Kompleksitas Manajemen Node**

Sistem yang memiliki banyak node membutuhkan pengelolaan yang lebih kompleks. Setiap node perlu dikelola agar dapat berkomunikasi dan bekerja sesuai dengan kebutuhan sistem.

**d. Governance (Tata Kelola)**

Tata kelola menjadi tantangan khusus pada sistem terdesentralisasi karena kontrol tidak hanya berada pada satu pihak.

Diperlukan mekanisme yang jelas untuk mengatur pengambilan keputusan, kesepakatan, serta pengelolaan sistem secara kolektif.

#### 12. Tren Masa Depan

Materi memperkenalkan beberapa tren teknologi yang berkaitan dengan perkembangan sistem terdistribusi dan terdesentralisasi.

**a. Cloud-Native**

Cloud-Native merupakan pendekatan pengembangan dan pengelolaan aplikasi yang memanfaatkan lingkungan komputasi berbasis cloud.

Materi menyebutkan Kubernetes dan Docker sebagai teknologi yang berkaitan dengan pendekatan ini.

**b. Edge dan Fog Computing**

Edge Computing dan Fog Computing merupakan pendekatan komputasi yang berkaitan dengan pemrosesan data pada lokasi yang lebih dekat dengan sumber data atau perangkat pengguna.

Keduanya menjadi salah satu tren dalam perkembangan sistem komputasi terdistribusi.

**c. Web3 dan DeFi**

Web3 dan Decentralized Finance (DeFi) merupakan tren yang berkaitan dengan perkembangan teknologi berbasis desentralisasi.

Konsep ini menjadi bagian dari perkembangan layanan digital yang memanfaatkan teknologi terdesentralisasi.

**d. Federated Data-Learning (AI Terdistribusi)**

Federated Data-Learning atau AI terdistribusi merupakan salah satu tren yang disebutkan dalam materi.

Konsep ini berkaitan dengan perkembangan kecerdasan buatan yang memanfaatkan pendekatan terdistribusi dalam pengelolaan atau proses pembelajaran data.

Keempat tren tersebut menunjukkan bahwa konsep distribusi dan desentralisasi masih memiliki peran penting dalam perkembangan teknologi masa depan.

---

### D. CONTOH PENERAPAN DAN ANALISIS

Berdasarkan materi perkuliahan, terdapat beberapa penerapan sistem terdistribusi dan terdesentralisasi dalam kehidupan sehari-hari maupun layanan teknologi modern.

#### 1. Netflix sebagai Contoh Sistem Terdistribusi

**Konsep yang digunakan:**

Sistem terdistribusi.

**Cara kerja:**

Netflix merupakan layanan streaming yang disebutkan dalam materi sebagai salah satu contoh penerapan sistem terdistribusi.

[MODIFIKASI] Dalam gambaran penerapannya, layanan streaming membutuhkan infrastruktur yang mampu menangani permintaan dari banyak pengguna secara bersamaan serta mendukung penyediaan konten melalui jaringan.

**Alasan penggunaan:**

Sistem terdistribusi mendukung kebutuhan layanan yang memiliki banyak pengguna, data, dan permintaan akses.

**Hubungan dengan sistem terdistribusi:**

Netflix menggambarkan bagaimana sistem terdistribusi dapat digunakan untuk mendukung layanan digital berskala besar.

#### 2. BitTorrent sebagai Contoh Sistem Peer-to-Peer

**Konsep yang digunakan:**

Peer-to-Peer (P2P) dan desentralisasi.

**Cara kerja:**

BitTorrent memungkinkan pengguna saling berbagi file melalui jaringan. Setiap peer dapat menerima sekaligus menyediakan bagian file kepada peer lainnya.

[MODIFIKASI] Dengan pola tersebut, proses berbagi file tidak harus sepenuhnya bergantung pada satu server yang menyediakan seluruh file kepada semua pengguna.

**Alasan penggunaan:**

Pendekatan P2P memungkinkan sumber daya jaringan dimanfaatkan bersama oleh para pengguna.

**Hubungan dengan sistem terdistribusi dan terdesentralisasi:**

BitTorrent memperlihatkan pembagian sumber daya dan komunikasi langsung antarkomponen jaringan.

#### 3. Blockchain sebagai Contoh Sistem Terdesentralisasi

**Konsep yang digunakan:**

Sistem terdesentralisasi dan mekanisme konsensus.

**Cara kerja:**

Blockchain merupakan contoh sistem yang melibatkan beberapa pihak atau node dalam jaringan. Pengambilan keputusan atau kesepakatan dilakukan melalui mekanisme konsensus.

[MODIFIKASI] Mekanisme ini membantu jaringan mencapai kesepakatan mengenai informasi atau kondisi yang diterima bersama tanpa harus bergantung pada satu pusat pengendalian.

**Alasan penggunaan:**

Pendekatan desentralisasi memungkinkan kontrol tidak sepenuhnya berada pada satu pihak.

**Hubungan dengan sistem terdesentralisasi:**

Blockchain menunjukkan penerapan pembagian kontrol dan pengambilan keputusan secara kolektif dalam jaringan.

#### 4. Sistem Perbankan dan Media Sosial dalam Konsistensi Data

Materi memberikan dua contoh penggunaan konsistensi data yang berbeda.

| Aspek | Sistem Perbankan | Media Sosial |
|---|---|---|
| Jenis konsistensi | Strong Consistency | Eventual Consistency |
| Kebutuhan | Ketepatan informasi transaksi dan saldo | Sinkronisasi informasi secara bertahap |
| Prioritas | Konsistensi data | Ketersediaan dan sinkronisasi bertahap |

[MODIFIKASI] Perbedaan tersebut menunjukkan bahwa kebutuhan konsistensi setiap sistem tidak selalu sama. Sistem perbankan membutuhkan ketepatan informasi yang tinggi, sedangkan media sosial masih dapat menerima keterlambatan penyebaran perubahan informasi selama data pada akhirnya mencapai kondisi konsisten.

Secara keseluruhan, berbagai contoh tersebut memperlihatkan bahwa sistem terdistribusi dan terdesentralisasi memiliki penerapan yang berbeda sesuai dengan kebutuhan layanan, pengelolaan data, pembagian beban kerja, serta mekanisme pengendalian sistem.

---

### E. PENGGUNAAN AI

Dalam penyusunan rangkuman materi Pertemuan 1 ini, AI digunakan sebagai alat bantu untuk membaca, memahami, mengelompokkan, dan menyusun kembali materi perkuliahan ke dalam format laporan Markdown.

**AI yang digunakan:**

ChatGPT (GPT-6).

**Prompt yang digunakan:**

AI diberikan instruksi untuk berperan sebagai asisten akademik mahasiswa S1 Informatika yang memahami mata kuliah Teori Sistem Terdistribusi dan Terdesentralisasi.

Instruksi yang diberikan mencakup:

1. Membaca dan memeriksa seluruh halaman PDF materi perkuliahan.
2. Mengidentifikasi tujuan pembelajaran, pokok bahasan, konsep, istilah teknis, contoh, diagram, dan referensi.
3. Menyusun rangkuman berdasarkan urutan dan isi materi dosen.
4. Menjelaskan setiap konsep menggunakan bahasa Indonesia yang natural dan mudah dipahami.
5. Membedakan informasi dari materi sumber dengan tambahan penjelasan menggunakan tanda [MODIFIKASI].
6. Menyusun laporan dengan struktur A sampai G sesuai ketentuan.
7. Menghasilkan dokumen Markdown yang siap digunakan sebagai README.md di repository GitHub.

**Bagian yang disesuaikan:**

AI membantu menyusun penjelasan materi, mengelompokkan pembahasan berdasarkan subtopik, membuat tabel perbandingan, serta menyusun analisis contoh penerapan berdasarkan konsep yang terdapat dalam materi.

Penyesuaian juga dilakukan pada struktur kalimat agar lebih runtut, mudah dipahami, dan tidak sekadar menyalin isi slide. Istilah teknis, contoh, serta pokok pembahasan tetap mengacu pada materi dosen.

**Keterangan [MODIFIKASI]:**

Tanda [MODIFIKASI] digunakan untuk menunjukkan penjelasan tambahan, pengembangan analisis, atau contoh yang disusun oleh AI untuk membantu pemahaman. Bagian tersebut bukan merupakan kutipan langsung dari materi dosen.

Hasil rangkuman tetap perlu diperiksa dan dipahami kembali oleh mahasiswa sebelum digunakan sebagai tugas perkuliahan.

---

### F. KESIMPULAN

Berdasarkan materi Pertemuan 1, dapat dipahami bahwa sistem terdistribusi dan sistem terdesentralisasi merupakan dua konsep penting dalam perkembangan teknologi informasi modern. Keduanya memiliki hubungan yang erat, tetapi mempunyai fokus penerapan yang berbeda.

Sistem terdistribusi berfokus pada pembagian beban kerja dan sumber daya ke beberapa komputer atau komponen yang saling berkomunikasi melalui jaringan. Sistem ini memiliki karakteristik seperti transparansi lokasi, skalabilitas, fault tolerance, kinerja tinggi, dan heterogenitas. Sementara itu, sistem terdesentralisasi lebih menekankan pada pembagian kontrol serta pengambilan keputusan secara kolektif melalui mekanisme konsensus.

Materi juga memperkenalkan berbagai arsitektur dasar, yaitu Client-Server, Peer-to-Peer, dan Hybrid. Ketiga arsitektur tersebut menunjukkan bagaimana komponen dalam sebuah sistem dapat saling berhubungan dan bertukar informasi.

Selain itu, pemahaman mengenai CAP Theorem dan konsistensi data menjadi bagian penting dalam merancang sistem terdistribusi. Pengembang perlu mempertimbangkan keseimbangan antara konsistensi, ketersediaan, serta kemampuan sistem menghadapi gangguan jaringan.

Melalui berbagai contoh seperti Google File System, Netflix, BitTorrent, Blockchain, dan media sosial, dapat diketahui bahwa penerapan sistem terdistribusi maupun terdesentralisasi telah menjadi bagian penting dari berbagai layanan digital.

Dengan demikian, pemahaman terhadap kedua konsep ini menjadi dasar untuk mempelajari bagaimana teknologi modern dibangun agar mampu menangani pertumbuhan data, jumlah pengguna, kebutuhan ketersediaan layanan, serta tantangan keamanan dan pengelolaan sistem.

---

### G. DAFTAR REFERENSI

1. Bambang Purnomosidi D. P. (Tanpa tahun). *Pengenalan Sistem Terdistribusi dan Terdesentralisasi*. Materi perkuliahan Teori Sistem Terdistribusi dan Terdesentralisasi, Program Studi Informatika, Universitas Teknologi Digital Indonesia. File: `01--pengenalan.pdf`.

2. Tanenbaum, A. S., & van Steen, M. (2007). Referensi definisi sistem terdistribusi sebagaimana dicantumkan dalam materi perkuliahan. Detail judul dan penerbit tidak dicantumkan dalam slide.

3. Baran, P. (1964). *On Distributed Communications*. Memorandum RM-3420-PR.

**Sumber ilustrasi yang dicantumkan dalam materi:**

- SolarWinds. *What Is a Distributed System?* https://www.solarwinds.com/blog/what-is-a-distributed-system
- Wikimedia Commons. *Peer-to-Peer (P2P) Illustration*. https://commons.wikimedia.org/w/index.php?curid=116056511
- ResearchGate. *Hybrid P2P System Overview*. https://www.researchgate.net/figure/Hybrid-P2P-system-overview_fig5_321745039

---

### INFORMASI DOKUMENTASI GITHUB

- **Repository:** https://github.com/hendfirmsh/disdec-teori
- **Direktori:** `01/`
- **File:** `README.md`
