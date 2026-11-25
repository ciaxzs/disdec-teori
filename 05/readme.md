# RANGKUMAN MATERI TEORI SISTEM TERDISTRIBUSI DAN TERDESENTRALISASI

## PERTEMUAN 5

### A. IDENTITAS MATERI

| Keterangan | Informasi |
|---|---|
| Mata Kuliah | Teori Sistem Terdistribusi dan Terdesentralisasi |
| Pertemuan | Pertemuan ke-5 |
| Topik Materi | Fault Tolerance |
| Sumber Materi | 05--fault-tolerant-sys (1).pdf |
| AI yang Digunakan | ChatGPT GPT-6 |
| Format Dokumen | Markdown (.md) |

### B. TUJUAN PEMBELAJARAN

Berdasarkan materi perkuliahan, tujuan pembelajaran pada pertemuan ini adalah:

1. Memahami dan mampu menjelaskan mengapa *fault tolerance* diperlukan pada sistem terdistribusi dan terdesentralisasi.

2. Memahami dan mampu menjelaskan pengertian dari *fault tolerance* serta *fault tolerant systems*.

3. Memahami dan mampu menjelaskan berbagai jenis *fault* dalam suatu sistem teknologi informasi.

4. Memahami dan mampu menjelaskan klasifikasi *fault* berdasarkan sumbernya.

5. Memahami berbagai *design patterns* untuk mencapai *fault tolerance* serta bisa mengaplikasikannya menggunakan Python.

6. Memahami bagaimana berbagai bahasa pemrograman serta peranti pengembangan mengimplementasikan *fault tolerance*.

### C. RANGKUMAN MATERI

#### 1. Pengertian Fault Tolerance

**Fault tolerance** adalah kemampuan suatu sistem untuk mempertahankan operasional sistem dengan tepat meskipun terjadi kegagalan atau kesalahan pada satu atau lebih komponennya. Kemampuan ini penting untuk sistem dengan *high availability*, *mission critical*, atau *life-critical system*.

`[MODIFIKASI]` Keberadaan mekanisme toleransi kesalahan memungkinkan layanan kritis tetap berjalan sebagaimana mestinya saat sebagian komponen mengalami gangguan.

#### 2. Arti Penting Fault Tolerance pada Sistem Terdistribusi dan Terdesentralisasi

Sistem terdistribusi dan terdesentralisasi memiliki banyak komponen, di mana koneksi antarkomponen dapat menjadi masalah. Namun, semakin *critical* suatu aplikasi, semakin tinggi tuntutan untuk tetap berfungsi dengan baik sehingga memunculkan tuntutan terhadap *high availability* yang harus diantisipasi.

`[MODIFIKASI]` Banyaknya titik koneksi antar-komponen pada sistem terdistribusi maupun terdesentralisasi meningkatkan peluang gangguan sehingga *high availability* menjadi kebutuhan yang perlu dirancang sejak awal.

#### 3. Jenis Fault

Materi menguraikan empat jenis *fault* dalam suatu sistem:

* **Transient Fault:** gangguan yang bersifat sementara, misalnya karena petir.

* **Intermittent Fault:** gangguan yang muncul dan hilang secara berulang, misalnya karena *overheat* pada *hardware*.

* **Permanent Fault:** gangguan yang bersifat tetap.

* **Byzantine Fault:** kondisi ketika komponen memberikan hasil yang acak atau tidak konsisten (diilustrasikan dengan skenario *Byzantine Fault Tolerance* terkait adanya *traitor* di antara pihak-pihak yang berkomunikasi).

`[MODIFIKASI]` Perbedaan durasi kemunculan (*transient*, *intermittent*, *permanent*) dan perilaku menyimpang atau tidak konsisten (*byzantine*) memengaruhi cara sistem mendeteksi serta merespons kegagalan.

#### 4. Klasifikasi Fault Berdasarkan Sumber

Berdasarkan sumbernya, *fault* diklasifikasikan menjadi tiga kelompok:

* **Hardware Faults:** kegagalan perangkat keras, seperti *disk crash* atau *power failure*.

* **Software Faults:** kesalahan perangkat lunak, seperti *bugs*, *memory leak*, atau *race condition*.

* **Communication Faults:** gangguan komunikasi, seperti *packet loss* atau *network partition*.

`[MODIFIKASI]` Pengelompokan *fault* ke dalam ranah perangkat keras, perangkat lunak, dan komunikasi membantu mengidentifikasi lapisan sistem yang terdampak saat gangguan terjadi.

#### 5. Design Patterns untuk Mencapai Fault Tolerance

Materi mengacu pada teknik dan pola desain untuk meningkatkan *fault tolerance* pada sistem terdistribusi, antara lain:

1. **Redundansi dan Replikasi (*Redundancy and Replication*):** *resources* tidak hanya satu melainkan direplikasi ke berbagai *node* (terjadi redundansi) agar tidak muncul *single point of failure*.

2. **Load Balancing:** proses melakukan *scaling* aplikasi menjadi lebih dari satu *instance* (satu proses aplikasi penuh yang aktif) menggunakan *load balancer* seperti HAProxy atau *nginx* (sebagaimana dibahas pada file `web-app-py-blacksheep-load-balancing-nginx.pdf`).

3. **Checkpointing and Rollback Recovery:** *checkpointing* adalah proses menyimpan status sistem secara berkala ke media penyimpan, sedangkan *rollback recovery* adalah proses mengembalikan sistem ke *checkpoint* yang tercatat sebelumnya setelah terjadi kegagalan agar pemulihan dapat dimulai dari status tersimpan (bukan dari awal) untuk meminimalkan kehilangan data dan waktu pemrosesan.

4. **Heartbeat and Failure Detection:** *heartbeat* adalah sinyal periodik yang dikirim antarkomponen untuk menunjukkan bahwa komponen masih aktif, sedangkan *failure detection* adalah penggunaan *heartbeat* tersebut untuk menentukan apakah suatu komponen telah gagal (jika sinyal tidak diterima dalam jangka waktu tertentu, komponen diasumsikan gagal dan tidak responsif, seperti pada skrip `check-server.py`).

5. **Retry (dengan `tenacity`):** pustaka `tenacity` dapat digunakan untuk mengelola proses yang memerlukan keterkaitan dengan komponen di luar aplikasi karena selalu ada kemungkinan kegagalan koneksi dengan komponen eksternal (seperti pada skrip `check-retry.py`).

6. **Circuit Breaker (dengan `pybreaker`):** pola desain pada *microservices* untuk mencegah kegagalan berantai dengan memblokir sementara panggilan ke layanan yang gagal, bekerja seperti *state machine* dengan tiga status: *closed* (permintaan diizinkan dan dipantau), *open* (menolak permintaan sementara setelah ambang batas kegagalan terpenuhi agar layanan pulih), dan *half-open* (mengizinkan permintaan terbatas untuk menguji pemulihan, lalu kembali ke *closed* jika berhasil atau kembali ke status terbuka jika gagal, seperti pada contoh `pybreaker.CircuitBreaker(fail_max=4, reset_timeout=20)` di `check-circuit-breaker.py`).

7. **Consensus and Coordination:** *consensus* adalah proses di mana beberapa *node* menyepakati satu nilai, status, atau urutan operasi meskipun terjadi kegagalan dan penundaan jaringan, sedangkan *coordination* adalah praktik yang lebih luas dalam mengelola interaksi antar-*node* agar bekerja sama secara efektif dan konsisten (sering melibatkan *consensus* sebagai komponen kunci), misalnya pada *database leader election* (seperti Raft), *cloud storage file updates* (seperti komit ke mayoritas server sebelum direplikasi ke semua server seperti pada layanan Google Drive), serta *cryptocurrency and blockchain* untuk validasi dan persetujuan transaksi.

`[MODIFIKASI]` Berbagai pola tersebut bekerja saling melengkapi—mulai dari mencegah *single point of failure* dan kegagalan berantai hingga memulihkan status dan menyepakati keputusan antar-*node*.

#### 6. Actor Model untuk Supervisi Proses

Dalam **Actor System** (*Actor Model*), entitas *Actor* berinteraksi melalui pengiriman pesan ke *Mailbox* masing-masing. Pada supervisi proses dengan pendekatan *Actor Model*, terdapat struktur hierarki supervisor dan *actor* (seperti *top level supervisor* dan *supervisor* di bawahnya) yang memantau kondisi *actor* lain (`check if alive`) dan dapat melakukan *restart* terhadap *actor* yang mengalami masalah.

`[MODIFIKASI]` Struktur supervisi bertingkat pada *Actor Model* memisahkan tugas pemantauan serta pemulihan proses yang gagal dari *actor* pekerja yang menjalankan logika utama.

#### 7. Implementasi Fault Tolerance pada Berbagai Bahasa Pemrograman dan Peranti Pengembangan

Materi mencatat bahwa **Erlang/Elixir** memiliki mekanisme *builtin* untuk *actor model* dan *Supervisor-Worker*, sedangkan **Pony** merupakan bahasa pemrograman yang mengkhususkan diri pada *Actor model*. Sementara itu, bahasa pemrograman lain umumnya menggunakan *3rd party library*, antara lain:

* **Python:** Xoscar, `tenacity`, `circuit breaker` (seperti `pybreaker`), dan lainnya.

* **Java:** Apache Pekko untuk *actor model* dan *Supervisor-Worker*, serta Resilience4j untuk *fault tolerance*.

Materi juga mengarahkan eksplorasi berbagai *library* untuk *fault tolerance* pada ekosistem bahasa pemrograman lain seperti `npm` (JavaScript) dan `crates.io` (Rust).

`[MODIFIKASI]` Ketersediaan dukungan *builtin* maupun *library* pihak ketiga memungkinkan penerapan pola *fault tolerance* disesuaikan dengan ekosistem bahasa pemrograman yang digunakan.

### D. CONTOH PENERAPAN DAN ANALISIS

Berdasarkan materi perkuliahan, terdapat beberapa contoh penerapan *fault tolerance* pada pengembangan maupun sistem terdistribusi.

#### 1. Pengecekan Ketersediaan Server dan Percobaan Ulang dengan `tenacity`

**Konsep yang digunakan:**

*Failure detection* dan *retry* pada koneksi ke komponen di luar aplikasi.

**Cara kerja:**

Skrip `check-server.py` memeriksa status server pada *host* dan *port* tertentu (seperti `localhost` *port* `44777` yang aktif dan *port* `80` yang tidak aktif), sedangkan skrip `check-retry.py` memanfaatkan pustaka `tenacity` untuk mencoba kembali mengakses URL `http://localhost:44777` ketika terjadi kegagalan koneksi hingga batas percobaan terpenuhi.

`[MODIFIKASI]` Percobaan ulang otomatis membantu mengatasi kegagalan sementara pada koneksi jaringan atau layanan eksternal tanpa langsung menyerah pada satu percobaan gagal.

**Alasan penggunaan:**

Koneksi dengan komponen di luar aplikasi selalu memiliki kemungkinan gagal sehingga perlu ditangani secara terstruktur.

**Hubungan dengan materi pertemuan:**

Contoh ini menunjukkan penerapan langsung deteksi kegagalan dan mekanisme *retry* berbasis Python dalam materi.

#### 2. Pencegahan Kegagalan Berantai dengan Circuit Breaker (`pybreaker`)

**Konsep yang digunakan:**

Pola *Circuit Breaker* sebagai *state machine* (*closed*, *open*, *half-open*).

**Cara kerja:**

Skrip `check-circuit-breaker.py` membungkus fungsi permintaan HTTP menggunakan `pybreaker.CircuitBreaker(fail_max=4, reset_timeout=20)` dan memantau status respons atau kesalahan koneksi ke `http://localhost:44777`.

`[MODIFIKASI]` Dengan membatasi jumlah kegagalan dan memberi jeda waktu sebelum pengujian ulang, *circuit breaker* menghindarkan pemanggil dari penumpukan permintaan yang terus gagal ke layanan yang sedang bermasalah.

**Alasan penggunaan:**

Mencegah kegagalan berantai (*cascading failure*) pada arsitektur *microservices* saat layanan tujuan mengalami gangguan.

**Hubungan dengan materi pertemuan:**

Contoh ini merepresentasikan implementasi praktis pola *circuit breaker* menggunakan Python pada materi.

#### 3. Konsensus dan Koordinasi pada Pembaruan File Cloud Storage

**Konsep yang digunakan:**

*Consensus* dan *coordination* pada sistem terdistribusi.

**Cara kerja:**

Saat memperbarui file pada layanan seperti Google Drive, sistem menggunakan mekanisme konsensus untuk memastikan perubahan di-*commit* ke mayoritas server terlebih dahulu sebelum dianggap final dan kemudian direplikasi ke seluruh server.

`[MODIFIKASI]` Persetujuan mayoritas server memastikan pembaruan memiliki dasar kesepakatan yang kuat sebelum disebarkan secara menyeluruh ke replika lainnya.

**Alasan penggunaan:**

Menjaga kesepakatan status atau pembaruan data meskipun terjadi kegagalan atau penundaan jaringan di sebagian *node*.

**Hubungan dengan materi pertemuan:**

Contoh ini menggambarkan bagaimana konsensus menjadi komponen inti dalam koordinasi sistem terdistribusi berskala luas.

#### 4. Perbandingan Pola Pemulihan dan Pengendalian Kegagalan

Materi memaparkan beberapa mekanisme pengendalian dan pemulihan kegagalan yang memiliki fungsi berbeda dalam sistem.

| Aspek | Checkpointing & Rollback Recovery | Heartbeat & Failure Detection | Circuit Breaker | 
| ----- | ----- | ----- | ----- | 
| Fokus utama | Menyimpan status secara berkala dan mengembalikan ke *checkpoint* saat gagal | Mengirim sinyal periodik untuk mendeteksi komponen yang gagal/tidak responsif | Memblokir sementara panggilan ke layanan gagal melalui status *closed*, *open*, dan *half-open* | 
| Tujuan operasional | Meminimalkan kehilangan data dan waktu pemrosesan saat pulih | Mengetahui kondisi aktif/gagal komponen secara tepat waktu | Mencegah kegagalan berantai pada layanan yang mengalami gangguan | 
| Contoh/alat dalam materi | Penyimpanan status berkala ke media penyimpan & pemulihan ke *checkpoint* | Sinyal periodik *heartbeat* & skrip `check-server.py` | Pola *circuit breaker* pada *microservices* & `pybreaker` | 

`[MODIFIKASI]` Ketiga mekanisme tersebut menangani fase yang berbeda dari siklus kegagalan—mulai dari deteksi dini komponen mati, pembatasan dampak kegagalan panggilan, hingga pemulihan ke titik status yang tersimpan.

### E. PENGGUNAAN AI

Berikut prompt yang digunakan untuk menghasilkan rangkuman awal:

> Saya merupakan mahasiswa S1 Informatika yang sedang mengerjakan tugas rangkuman mata kuliah Teori Sistem Terdistribusi dan Terdesentralisasi pertemuan ke-5. Baca dan pelajari seluruh isi PDF yang saya lampirkan dengan teliti, kemudian buat rangkuman berdasarkan materi tersebut.
>
> Gunakan struktur berikut:
> A. Identitas Materi
> B. Tujuan Pembelajaran
> C. Rangkuman Materi
> D. Contoh Penerapan dan Analisis
> E. Penggunaan Artificial Intelligence (AI)
> F. Kesimpulan
> G. Daftar Referensi
>
> Pada bagian rangkuman materi, susun subbab berdasarkan pokok bahasan yang benar-benar terdapat dalam PDF. Jangan memaksakan jumlah subbab yang sama untuk setiap pertemuan.
>
> Jelaskan setiap konsep menggunakan bahasa Indonesia yang natural, jelas, dan mudah dipahami mahasiswa. Pertahankan istilah teknis yang digunakan dalam materi, kemudian berikan penjelasan tambahan jika diperlukan agar konsep lebih mudah dipahami.
>
> Sertakan contoh penerapan dan analisis yang relevan dengan bidang Informatika. Jangan mengarang informasi, kode program, hasil pengujian, atau detail implementasi yang tidak tersedia dalam sumber. Jika materi hanya menyebutkan nama file atau program pendukung tetapi file tersebut tidak dilampirkan, jelaskan keterbatasan tersebut.
>
> Berikan tanda **[MODIFIKASI]** pada bagian yang mendapatkan pengembangan penjelasan, tambahan contoh, atau analisis dari hasil awal AI. Pastikan isi rangkuman tetap sesuai dengan materi dosen dan tidak menggantikan pokok pembahasan aslinya.
>
> Buat hasil akhir dalam format Markdown yang siap disimpan sebagai README.md di GitHub.

### 3. Bagian yang Disesuaikan dari Keluaran AI

Bagian dari hasil AI yang dikembangkan atau disesuaikan meliputi:

1. **Pengertian dan Jenis Fault**: Penjelasan mengenai perbedaan *transient fault*, *intermittent fault*, *permanent fault*, dan *Byzantine fault* dikembangkan agar karakteristik setiap jenis kegagalan lebih mudah dipahami.
2. **Teknik Fault Tolerance**: Penjelasan mengenai redundansi, replikasi, load balancing, checkpointing, heartbeat, retry, dan circuit breaker dikembangkan dengan memberikan gambaran fungsi masing-masing teknik.
3. **Consensus dan Actor Model**: Penjelasan mengenai proses kesepakatan antar-node serta supervisi proses dikembangkan agar hubungannya dengan penanganan kegagalan lebih mudah dipahami.
4. **Contoh Penerapan dan Analisis**: Ditambahkan contoh penerapan dalam sistem perbankan, microservices, aplikasi dengan banyak server, pemrosesan data, dan kluster basis data untuk menghubungkan teori dengan penggunaan teknologi informasi.

Penyesuaian dilakukan untuk memperjelas pemahaman materi, mengembangkan penjelasan yang masih singkat pada slide, serta memberikan contoh penerapan yang relevan.


### F. KESIMPULAN

Berdasarkan materi Pertemuan 5, *fault tolerance* merupakan kemampuan sistem untuk mempertahankan operasional secara tepat ketika terjadi kegagalan pada satu atau lebih komponen, yang sangat krusial bagi sistem dengan *high availability*, *mission critical*, atau *life-critical* pada lingkungan terdistribusi dan terdesentralisasi. Pemahaman terhadap jenis *fault* (*transient*, *intermittent*, *permanent*, dan *byzantine*) serta sumbernya (*hardware*, *software*, dan *communication faults*) menjadi dasar dalam memilih strategi pencegahan dan pemulihan yang tepat.

Berbagai pola dan pendekatan—seperti redundansi dan replikasi, *load balancing*, *checkpointing and rollback recovery*, *heartbeat and failure detection*, *retry* (`tenacity`), *circuit breaker* (`pybreaker`), *consensus and coordination*, serta *Actor Model* untuk supervisi proses—dapat diterapkan baik melalui fitur bawaan bahasa (seperti Erlang/Elixir dan Pony) maupun *library* pendukung di berbagai bahasa pemrograman seperti Python dan Java.

### G. DAFTAR REFERENSI

1. Bambang Purnomosidi D. P. (Tanpa tahun). *Fault Tolerance*. Materi perkuliahan Teori Sistem Terdistribusi dan Terdesentralisasi (Kode: FIF25002T, 3 SKS), Program Studi Informatika, Fakultas Teknologi Informasi, Universitas Teknologi Digital Indonesia. File: `05--fault-tolerant-sys.pdf`.

**Sumber ilustrasi, pustaka, dan referensi yang dicantumkan dalam materi:**

* Medium (Coinmonks). *Byzantine Fault Tolerance*. https://medium.com/coinmonks/byzantine-fault-tolerance-222a8134be7

* Design Gurus. *5 Expert Techniques for Boosting Fault Tolerance in Distributed Systems*. https://www.designgurus.io/kb/design-patterns-5-expert-techniques-for-boosting-fault-tolerance-in-distributed-systems

* GitHub (jd/tenacity). *tenacity*. https://github.com/jd/tenacity

* Medium (nguyenthanhquang.cse). *Introduction to Actor Model*. https://medium.com/@nguyenthanhquang.cse/introduction-to-actor-model-2c82d25d1b83

* System Design Newsletter. *Actor Model*. https://newsletter.systemdesign.one/p/actor-model

* Pony Programming Language. https://www.ponylang.io

* Xoscar Documentation. https://xoscar.dev

* GitHub (resilience4j/resilience4j). *Resilience4j*. https://github.com/resilience4j/resilience4j

### INFORMASI DOKUMENTASI GITHUB

* **Repository:** https://github.com/ciaxzs/disdec-teori

* **Direktori:** `05/`

* **File:** `README.md`
