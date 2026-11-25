# RANGKUMAN MATERI TEORI SISTEM TERDISTRIBUSI DAN TERDESENTRALISASI

## PERTEMUAN 4

### A. IDENTITAS MATERI

| Keterangan | Informasi |
|---|---|
| Mata Kuliah | Teori Sistem Terdistribusi dan Terdesentralisasi |
| Pertemuan | Pertemuan ke-4 |
| Topik Materi | Konsistensi dan Replikasi pada Sistem Terdistribusi |
| Sumber Materi | 04--konsistensi-dan-replikasi (1).pdf |
| AI yang Digunakan | ChatGPT GPT-6 |
| Format Dokumen | Markdown (.md) |
---

### B. TUJUAN PEMBELAJARAN

Berdasarkan materi perkuliahan, tujuan pembelajaran pada pertemuan ini adalah:

1. Memahami dan mampu menjelaskan konsep konsistensi dalam sistem terdistribusi.
2. Mampu menjelaskan berbagai model konsistensi.
3. Mampu menjelaskan konsep replikasi data.
4. Mengetahui dan mampu menjelaskan berbagai protokol dan strategi replikasi.
5. Mampu melakukan analisis studi kasus replikasi pada sistem nyata yang banyak digunakan di industri.

---

### C. RANGKUMAN MATERI

#### 1. Pengertian Konsistensi pada Sistem Terdistribusi

**Konsistensi** pada sistem terdistribusi adalah jaminan bahwa semua *node* (komputer/server) dalam sistem memiliki data yang sama atau tampak sama pada waktu tertentu, meskipun data tersebut berada di banyak tempat dan bisa diubah secara bersamaan oleh pengguna atau proses yang berbeda. Jika suatu aplikasi mengubah data di satu server, sistem harus memastikan bahwa server lain akhirnya memiliki data yang sama.

`[MODIFIKASI]` Keberadaan salinan data di berbagai lokasi fisik menuntut adanya mekanisme penyelarasan agar perubahan data di satu titik tidak menyebabkan perbedaan persepsi data antar-server.

#### 2. Mengapa Konsistensi Penting pada Sistem Terdistribusi?

Jika konsistensi tidak diperhatikan, pengguna dapat melihat versi data yang berbeda tergantung pada server tempat data dibaca. Dalam materi diberikan ilustrasi transfer uang nasabah dari rekening A ke rekening B: jika Server 1 sudah mengurangi saldo A tetapi Server 2 belum menambah saldo B, nasabah dapat gagal melakukan transaksi dari rekening B karena saldo belum bertambah. Karena data disimpan di banyak *node*, muncul potensi ketidaksamaan data antar-*node*, sehingga tujuan utamanya adalah memastikan pengguna melihat data yang benar dan *up-to-date* serta memahami *trade-off* antara *Consistency*, *Availability*, dan *Partition Tolerance* (CAP Theorem).

`[MODIFIKASI]` Ketidaksinkronan pembaruan antar-server secara langsung berdampak pada validitas alur transaksi maupun keakuratan informasi yang diterima pengguna.

#### 3. Teorema CAP

Partisi (koneksi terputus) pada jaringan merupakan kondisi yang wajar dan tetap dapat terjadi pada jaringan mana pun, sehingga dalam praktiknya kondisi ideal CAP secara penuh tidak mungkin dicapai. Tiga komponen pada **CAP Theorem** meliputi:

- **Consistency:** data konsisten, semua *node* mempunyai data yang sama.
- **Availability:** ketersediaan data saat pengguna memerlukan data.
- **Partition Tolerance:** sistem tetap bisa berjalan meskipun ada satu atau beberapa komponen jaringan yang gagal atau terputus.

Pada contoh aplikasi *e-commerce* dengan Server A (wilayah barat Indonesia) dan Server B (wilayah timur Indonesia) saat koneksi antarwilayah terputus (*partition*):
- Jika memilih **Availability (AP)**, pengguna tetap bisa berbelanja di kedua wilayah, tetapi stok berisiko sementara tidak sinkron.
- Jika memilih **Consistency (CP)**, sistem menolak transaksi sampai jaringan pulih agar data stok tetap konsisten, sehingga mengorbankan *Availability*.

`[MODIFIKASI]` Saat partisi jaringan terjadi, sistem harus memilih prioritas antara tetap melayani permintaan dengan potensi perbedaan data sementara (AP) atau menahan operasi demi menjaga keseragaman data (CP).

#### 4. Model Konsistensi

**Model konsistensi** merupakan aturan atau jaminan tentang bagaimana dan kapan perubahan data pada sistem terdistribusi terlihat oleh *node* atau klien lain, serta menentukan seberapa cepat seluruh salinan data menjadi sama setelah terjadi *update*. Materi menguraikan beberapa model konsistensi dari tingkat kuat (*Strong*) hingga lemah (*Weak*):

1. **Strong Consistency:** setelah data diperbarui, semua *node* langsung melihat versi terbaru, dan setiap pembacaan (*read*) setelah penulisan (*write*) pasti mendapatkan nilai yang sama (umumnya menggunakan protokol seperti *Two-Phase Commit* atau *Paxos*, misalnya pada sistem perbankan).
2. **Eventual Consistency:** tidak menjamin data langsung sama di semua *node*, tetapi akhirnya akan sama jika tidak ada *update* baru dalam jangka waktu tertentu; cocok untuk sistem yang mengutamakan *availability* dan kecepatan serta dikaitkan dengan **BASE** (*Basically Available*, *Soft State*, *Eventual Consistency*), misalnya pada Amazon DynamoDB dan Apache Cassandra.
3. **Causal Consistency:** jika satu operasi bergantung pada operasi lain, urutan ketergantungan tersebut harus dijaga, sedangkan operasi yang tidak saling berhubungan dapat terlihat dengan urutan berbeda oleh *node* lain (misalnya komentar/reaksi pada media sosial tidak muncul sebelum postingan asalnya).
4. **Read-Your-Writes Consistency:** setelah pengguna menulis data, pembacaan berikutnya oleh pengguna yang sama akan melihat hasil tulisannya sendiri, meskipun belum tentu langsung terlihat oleh orang lain pada saat yang sama (misalnya pesan yang baru dikirim langsung tampil di layar pengirim).
5. **Monotonic Read Consistency:** jika pengguna membaca data beberapa kali, pengguna tersebut tidak akan melihat versi yang lebih lama dari versi yang sudah pernah dibacanya sebelumnya (misalnya *timeline* media sosial tidak "mundur" ke versi lama setelah di-*refresh*).
6. **Sequential Consistency:** semua operasi di sistem tampak dieksekusi dalam urutan yang sama untuk semua *node*, meskipun tidak harus *real-time* (urutan penulisan dijaga meski ada sedikit *delay*, misalnya urutan postingan di media sosial).
7. **Linearizability:** varian paling kuat dari *strong consistency* di mana operasi tampak dilakukan secara atomik dan langsung dengan urutan yang sama bagi semua *node* seolah-olah menjadi satu *node* atomik tunggal secara *real-time* (digunakan pada sistem seperti etcd, ZooKeeper, dan Spanner, misalnya mencegah dua pengguna mendaftarkan *username* atau ID yang sama secara bersamaan).

`[MODIFIKASI]` Setiap model konsistensi menawarkan jaminan urutan dan kesegeraan data yang berbeda sehingga pemilihannya disesuaikan dengan sifat operasi seperti keunikan ID, ketergantungan kausal, atau toleransi keterlambatan.

#### 5. Trade-Off Latensi dengan Konsistensi

Terdapat kompromi antara tingkat konsistensi dan latensi (waktu respons): semakin tinggi tingkat konsistensi yang dijamin, biasanya semakin besar latensi yang ditanggung pengguna ($\text{Konsistensi} \uparrow \rightarrow \text{Latensi} \uparrow$), sedangkan tingkat konsistensi yang lebih lemah cenderung memberikan latensi lebih rendah ($\text{Konsistensi} \downarrow \rightarrow \text{Latensi} \downarrow$). Pada **konsistensi tinggi (*Strong Consistency*)**, sistem menunggu sinkronisasi antar-server selesai sebelum memberi respons sehingga latensi lebih tinggi akibat komunikasi lintas jaringan; sebaliknya pada **konsistensi lemah (*Eventual Consistency*)**, sistem langsung memberi respons tanpa menunggu semua *node* sinkron sehingga latensi rendah namun ada risiko data belum terbaru.

Pada contoh dua pusat data di **Jakarta** dan **Yogyakarta** ketika data diubah di Jakarta lalu dibaca: memilih *Strong Consistency* menunggu hingga data di Jakarta dan Yogyakarta sama persis sebelum menjawab (konsisten tetapi respons lambat), sedangkan memilih *Eventual Consistency* menjawab langsung dan menyebarkan *update* ke Yogyakarta menyusul (respons cepat tetapi data bisa berbeda sementara).

`[MODIFIKASI]` Perbedaan jarak geografis dan kebutuhan waktu respons membuat perancang sistem perlu menyeimbangkan waktu tunggu sinkronisasi jaringan dengan kecepatan balasan ke pengguna.

#### 6. Pengertian Replikasi Data

**Replikasi data** adalah proses membuat dan memelihara salinan data yang sama di beberapa *node* atau server dalam sistem terdistribusi agar sistem tetap tersedia, andal, dan cepat meskipun terjadi kegagalan pada salah satu *node*. Sebagai contoh, basis data utama di Jakarta dapat memiliki salinan di Yogyakarta dan Denpasar untuk mendukung *high-availability*, di mana *write* diarahkan ke *Source* dan *read* dapat dilayani oleh *Replica #1* hingga *Replica #N* melalui proses *Replication*.

Tujuan replikasi data meliputi:
- **Ketersediaan (*Availability*):** jika satu server gagal, server lain masih memiliki salinan data.
- **Kinerja (*Performance*):** pengguna dapat membaca dari server terdekat sehingga lebih cepat.
- **Reliabilitas (*Reliability*):** risiko kehilangan data menurun karena tersedia cadangan di banyak tempat.
- **Skalabilitas:** beban baca (*read load*) dapat dibagi ke beberapa server.

`[MODIFIKASI]` Penyebaran replika di berbagai lokasi membantu mengurangi risiko kehilangan data akibat kegagalan satu server sekaligus membagi beban pembacaan.

#### 7. Jenis Replikasi

Materi menguraikan jenis-jenis replikasi berdasarkan peran *node* dan alur penulisan:
- **Master-Slave (*Primary-Secondary*):** satu *master* menulis data dan *slave* membaca data; memiliki konsistensi kuat namun berpotensi menimbulkan *bottleneck* di *master* (contoh: PostgreSQL *streaming replication*).
- **Multi-Master (*Peer-to-Peer*):** semua *node* dapat menulis dan membaca; lebih fleksibel tetapi rawan konflik data (contoh: PostgreSQL *logical replication*, Apache Cassandra, MongoDB, Apache Ignite).
- **Synchronous Replication:** *update* ditulis ke semua *node* sekaligus sebelum dianggap selesai; konsisten tetapi lebih lambat (contoh: Google Spanner).
- **Asynchronous Replication:** *update* dikirim ke *node* lain setelah transaksi selesai di *master*; cepat tetapi berpotensi terjadi *data delay* (contoh: MySQL *async mode*, DynamoDB).

`[MODIFIKASI]` Perbedaan antara pendekatan *master-slave* dan *multi-master* serta replikasi sinkron dan asinkron mencerminkan pertukaran antara kemudahan penulisan/kecepatan dan potensi konflik atau keterlambatan data.

#### 8. Strategi Sinkronisasi Replika

Strategi sinkronisasi replika dikelompokkan berdasarkan beberapa aspek:

1. **Berdasarkan waktu sinkronisasi:**
   - *Asynchronous:* *source* melakukan *commit* tanpa menunggu replika; performa tercepat tetapi risiko kehilangan data tertinggi.
   - *Semi-synchronous:* *source* menunggu satu replika menerima data; memberikan keseimbangan antara konsistensi dan performa (digunakan pada MySQL).
   - *Synchronous:* *source* menunggu semua replika melakukan *commit* data; konsistensi tertinggi tetapi performa terendah.

2. **Berdasarkan arah replikasi:**
   - *Master-slave* (*read write - read*).
   - *Master-master* (*read write* dengan peran, sumber daya, dan kapabilitas setara).
   - *Master-master asymmetric* (*read write* dengan peran, sumber daya, dan kapabilitas berbeda).

3. **Berdasarkan cara sinkronisasi:**
   - *Pull-based:* replika memeriksa *update* secara periodik ke *source* dan memperbarui jika ada perubahan.
   - *Push-based:* *source* secara aktif mengirimkan *update* ke replika saat terjadi perubahan, misalnya menggunakan *CDC (Change Data Capture)* di *source* dan pengiriman melalui *WebSockets* atau *SSE (Server-Side Events)*.
   - *Hybrid:* gabungan pendekatan *pull* dan *push*.

4. **Berdasarkan penanganan konflik (jika terjadi *multiple updates*):**
   - **LWW (*Last Write Wins*):** *timestamp* terbaru yang dikerjakan dan lainnya diabaikan.
   - **Vector Clock:** pengurutan menggunakan *vector clock*.
   - **CRDT (*Conflict-free Replicated Data Type*):** menggunakan struktur data di tiap *node* alih-alih server pusat (contoh: Yjs untuk *collaborative editor* seperti Google Docs).
   - **OT (*Operational Transformation*):** transformasi operasi berdasarkan informasi lokal.

`[MODIFIKASI]` Mekanisme seperti CRDT dan OT membantu menyelaraskan perubahan konkuren tanpa memerlukan satu server pusat pengatur konflik yang sama pada setiap kasus.

#### 9. Protokol Replikasi

Materi menyebutkan lima protokol replikasi pada sistem terdistribusi:
1. **Primary-based (*Master-Slave*):** satu *node* menangani *write-read* dan *node* lainnya menangani *read*.
2. **Quorum-based:** operasi *write* dan *read* dianggap berhasil jika mendapat konfirmasi dari sejumlah *node* tertentu dengan syarat $W + R > N$ (di mana $W$ = jumlah *node* minimal untuk *Write*, $R$ = jumlah *node* minimal untuk *Read*, dan $N$ = total jumlah *node*). Pada contoh $N = 3$, $W = 2$, dan $R = 2$ ($2 + 2 > 3$), operasi *write* $x = 100$ berhasil setelah mendapat 2 ACK meskipun satu *node* lambat/*timeout*, dan pembacaan dari minimal 2 *node* memastikan irisan memuat data terbaru.
3. **State Machine Replication:** beberapa server (replika) mengeksekusi perintah yang sama dalam urutan yang sama untuk *high-availability*; *leader* menerima permintaan klien, memberi nomor urutan dan mencatat ke *log*, meneruskan ke replika lain, menganggap perintah ter-*commit* setelah mendapat konfirmasi *log*, mengeksekusi perintah secara lokal (misalnya `SET x=20` dari `x=10`), lalu mengembalikan hasil akhir ke klien.
4. **Gossip Protocol:** digunakan pada *distributed database* seperti Apache Cassandra untuk memeriksa eksistensi *node* dan replikasi data; *node* yang mendeteksi perubahan memilih 1--3 *peer* secara acak setiap detik untuk berbagi status, lalu *peer* tersebut menyebarkannya ke *node* lain hingga seluruh klaster mengetahui keadaan terbaru.
5. **Chain Replication:** replika disusun berantai dari *head* hingga *tail*; operasi *write* masuk ke *head* dan diteruskan berurutan melalui *node* perantara hingga *tail* lalu mengirimkan *ack*, sedangkan operasi *read* dilakukan pada *tail*.

`[MODIFIKASI]` Setiap protokol replikasi mengatur alur *write*, *read*, dan penyebaran status dengan cara berbeda untuk menyeimbangkan konsistensi, ketersediaan, serta ketahanan terhadap kegagalan *node*.

#### 10. Studi Kasus pada Industri

Materi mencantumkan dua studi kasus replikasi pada sistem nyata di industri:
1. **PostgreSQL 18 Streaming Replication**
2. **Apache Ignite 3 Master-Master**

Materi juga mengarahkan pembaca untuk menelaah dokumen *lecture notes* serta *source code* yang menyertai materi, dan menyediakan pertanyaan diskusi mengenai kelebihan/kekurangan *strong vs eventual consistency* serta penanganan jika replikasi gagal pada satu *node*.

`[MODIFIKASI]` Studi kasus PostgreSQL 18 *streaming replication* dan Apache Ignite 3 *master-master* menjadi rujukan konkret untuk membandingkan penerapan replikasi dalam praktik basis data industri.

---

### D. CONTOH PENERAPAN DAN ANALISIS

Berdasarkan materi perkuliahan, terdapat beberapa contoh penerapan konsistensi dan replikasi pada sistem terdistribusi.

#### 1. Transfer Saldo Antar Rekening dan CAP pada Sistem E-Commerce

**Konsep yang digunakan:**

Konsistensi data, *CAP Theorem* (*Consistency*, *Availability*, *Partition Tolerance*), dan pemilihan CP vs AP.

**Cara kerja:**

Pada transfer antar-rekening atau transaksi *e-commerce* lintas wilayah (barat dan timur Indonesia), sistem harus menangani potensi perbedaan salinan data antar-server serta gangguan koneksi (*partition*) antarwilayah.

`[MODIFIKASI]` Jika partisi jaringan terjadi dan sistem mengutamakan AP, transaksi tetap berjalan dengan potensi selisih stok sementara, sedangkan pilihan CP menahan transaksi agar konsistensi tetap terjaga sampai koneksi pulih.

**Alasan penggunaan:**

Menunjukkan perlunya konsistensi data serta keputusan *trade-off* yang jelas saat data tersebar di banyak *node* dan jaringan mengalami gangguan.

**Hubungan dengan materi pertemuan:**

Contoh ini mengaitkan urgensi konsistensi dengan *CAP Theorem* dan skenario nyata transaksi maupun *e-commerce* dalam materi.

#### 2. Perhitungan Akses Website dengan CRDT dan Penyuntingan Dokumen dengan OT

**Konsep yang digunakan:**

Strategi penanganan konflik (*conflict resolution*) melalui *CRDT (Conflict-free Replicated Data Type)* dan *OT (Operational Transformation)*.

**Cara kerja:**

Pada contoh CRDT, pencatatan jumlah akses di tiap perangkat digabung menggunakan operasi `max` per entri lalu dijumlahkan (`5 + 3 = 8`), sedangkan pada contoh OT, pengeditan teks konkuren ("abc" yang disisipi `'x'` di indeks 0 dan dihapus `'c'` di indeks 2) ditransformasikan agar hasil akhir kedua pihak sama.

`[MODIFIKASI]` Kedua pendekatan tersebut menangani pembaruan paralel tanpa harus bergantung pada satu antrean terpusat yang kaku untuk setiap perubahan lokal.

**Alasan penggunaan:**

Menyelesaikan konflik ketika beberapa pihak melakukan perubahan data secara bersamaan pada salinan masing-masing.

**Hubungan dengan materi pertemuan:**

Contoh ini menggambarkan secara langsung mekanisme penanganan konflik pada strategi sinkronisasi replika yang dibahas pada materi.

#### 3. Replikasi Kuorum ($N=3, W=2, R=2$) dan Protokol Gossip

**Konsep yang digunakan:**

*Quorum-based replication* ($W + R > N$) dan *Gossip Protocol*.

**Cara kerja:**

Pada konfigurasi kuorum $N=3, W=2, R=2$, penulisan data `x=100` dinyatakan berhasil setelah memperoleh 2 *ACK* meski satu *node* lambat, dan pembacaan dari minimal 2 *node* memastikan data terbaru terambil dari irisan; sementara pada *Gossip Protocol*, pembaruan atau status *node* disebarkan secara acak antar-*peer* setiap detik ke seluruh klaster.

`[MODIFIKASI]` Kombinasi aturan kuorum dan penyebaran gosip membantu replika tetap mencapai kesepakatan data atau status klaster tanpa mengharuskan seluruh *node* merespons secara serentak dalam satu langkah tunggal.

**Alasan penggunaan:**

Menjaga keandalan baca-tulis serta penyebaran informasi status di tengah keterlambatan atau kegagalan sebagian *node*.

**Hubungan dengan materi pertemuan:**

Contoh ini memperjelas cara kerja protokol replikasi modern yang dipaparkan dalam slide perkuliahan.

#### 4. Perbandingan Strong Consistency dan Eventual Consistency

Materi membandingkan konsistensi kuat dan konsistensi *eventual* pada beberapa aspek dalam perkuliahan.

| Aspek | Strong Consistency | Eventual Consistency |
|---|---|---|
| Sinkronisasi pembacaan/penulisan | Semua *node* langsung melihat versi terbaru setelah *update* | Data tidak langsung sama di semua *node*, tetapi akhirnya sama jika tidak ada *update* baru |
| Latensi & *trade-off* | Konsistensi tinggi, latensi cenderung lebih tinggi karena menunggu sinkronisasi | Berbasis BASE; respons lebih cepat/latensi rendah, tetapi data bisa berbeda sementara |
| Contoh dalam materi | Sistem perbankan | Amazon DynamoDB, Apache Cassandra |

`[MODIFIKASI]` Pemilihan antara *strong consistency* dan *eventual consistency* bergantung pada apakah sistem lebih menuntut keseragaman data instan atau ketersediaan serta respons yang cepat.

---

### E. PENGGUNAAN AI

Dalam penyusunan rangkuman materi Pertemuan 4 ini, AI digunakan sebagai alat bantu untuk membaca, memahami, mengelompokkan, dan menyusun kembali materi perkuliahan ke dalam format laporan Markdown.

**AI yang digunakan:**

### 1. AI yang Digunakan

- Nama AI: ChatGPT GPT-6
- Tujuan penggunaan: Membantu memahami, menganalisis, menyusun, dan mengembangkan rangkuman materi perkuliahan.
- Sumber utama: Materi perkuliahan yang diberikan oleh dosen, yaitu file `04--konsistensi-dan-replikasi (1).pdf`.

### 2. Prompt yang Digunakan

Berikut prompt yang digunakan untuk menghasilkan rangkuman:

> Analisis seluruh isi file PDF materi Teori Sistem Terdistribusi dan Terdesentralisasi pertemuan 4 yang saya lampirkan. Susun rangkuman lengkap dalam format Markdown dengan mengikuti template README bagian A sampai G yang telah saya berikan.
>
> Gunakan materi dosen sebagai sumber utama dan pertahankan istilah serta konsep sesuai materi. Kembangkan penjelasan agar mudah dipahami, tambahkan contoh penerapan yang relevan dengan bidang Informatika, serta berikan analisis terhadap konsep yang dibahas.
>
> Pastikan pembahasan mencakup pengertian konsistensi, pentingnya konsistensi, Teorema CAP, model konsistensi, trade-off latensi dan konsistensi, pengertian replikasi data, jenis replikasi, strategi sinkronisasi replika, penanganan konflik menggunakan LWW, Vector Clocks, CRDT dan OT, serta protokol replikasi seperti Primary-Based, Quorum-Based, State Machine Replication, Gossip Protocol, dan Chain Replication.
>
> Sertakan contoh perhitungan quorum dan contoh penggabungan data menggunakan CRDT sesuai materi. Jelaskan studi kasus PostgreSQL 18 Streaming Replication dan Apache Ignite 3 Master-Master hanya berdasarkan informasi yang tersedia. Jika lecture notes atau source code pendukung tidak tersedia, jangan mengarang hasil implementasinya.
>
> Gunakan bahasa Indonesia yang natural seperti laporan mahasiswa S1 Informatika, bukan bahasa yang terlalu kaku. Jangan mengarang fakta atau referensi. Berikan hasil akhir berupa README lengkap yang siap dimasukkan ke repository GitHub.

### 3. Bagian yang Disesuaikan dari Keluaran AI

Bagian dari hasil rangkuman yang dikembangkan atau disesuaikan meliputi:

1. **Pengertian dan Model Konsistensi:** Penjelasan diperluas dengan membandingkan Strong Consistency, Eventual Consistency, Causal Consistency, Read-Your-Writes, Monotonic Read, Sequential Consistency, dan Linearizability beserta contoh penerapannya.
2. **Teorema CAP dan Trade-off Latensi:** Pembahasan dikembangkan dengan menggunakan contoh aplikasi e-commerce dan dua pusat data agar hubungan antara konsistensi, ketersediaan, toleransi partisi, serta waktu respons lebih mudah dipahami.
3. **Jenis dan Strategi Replikasi:** Penjelasan mengenai Master-Slave, Multi-Master, Synchronous, Asynchronous, Semi-Synchronous, Pull-Based, Push-Based, dan Hybrid disusun dengan membandingkan cara kerja serta kelebihan dan keterbatasannya.
4. **Penanganan Konflik dan Protokol Replikasi:** Contoh CRDT, Operational Transformation, Quorum-Based, State Machine Replication, Gossip Protocol, dan Chain Replication dikembangkan dengan penjelasan tahapan kerja dan contoh yang sesuai dengan materi.

Penyesuaian dilakukan untuk memperjelas pemahaman materi, memperbaiki penjelasan yang kurang lengkap, serta menambahkan contoh dan analisis yang relevan dengan bidang Informatika.
---

### F. KESIMPULAN

Berdasarkan materi Pertemuan 4, konsistensi dalam sistem terdistribusi memastikan salinan data di berbagai *node* tampak sama atau selaras pada waktu tertentu, sekaligus menghadapi *trade-off* pada *CAP Theorem* (*Consistency*, *Availability*, *Partition Tolerance*) serta kompromi antara konsistensi dan latensi. Berbagai model konsistensi—mulai dari *Linearizability* dan *Strong Consistency* hingga *Sequential*, *Causal*, *Read-Your-Writes*, *Monotonic Read*, dan *Eventual Consistency* (BASE)—digunakan sesuai kebutuhan aplikasi.

Untuk menjaga ketersediaan, kinerja, reliabilitas, dan skalabilitas, sistem terdistribusi menerapkan replikasi data dengan berbagai jenis (*master-slave*, *multi-master*, *synchronous*, *asynchronous*), strategi sinkronisasi dan penanganan konflik (seperti LWW, *Vector Clock*, CRDT, dan OT), serta protokol replikasi (*primary-based*, *quorum-based* dengan $W + R > N$, *state machine replication*, *gossip protocol*, dan *chain replication*), sebagaimana tercermin pada studi kasus PostgreSQL 18 dan Apache Ignite 3.

---

### G. DAFTAR REFERENSI

1. Bambang Purnomosidi D. P. (Tanpa tahun). *04: Konsistensi dan Replikasi pada Sistem Terdistribusi*. Materi perkuliahan Teori Sistem Terdistribusi dan Terdesentralisasi (Kode: FIF25002T, 3 SKS), Program Studi Informatika, Fakultas Teknologi Informasi, Universitas Teknologi Digital Indonesia. File: `04--konsistensi-dan-replikasi.pdf`.

**Sumber ilustrasi dan dokumentasi yang dicantumkan dalam materi:**

- Medium (Codex). *An Overview of MySQL Replication*. https://medium.com/codex/an-overview-of-mysql-replication-9e5635cc3a8a
- Yjs Documentation. https://yjs.dev/
- Medium (m.hassan.def). *Chain Replication: How Does Azure Storage Handle Replication Under the Hood*. https://medium.com/@m.hassan.def/chain-replication-how-does-azure-storage-handle-replication-under-the-hood-79acbd3ac441

---

### INFORMASI DOKUMENTASI GITHUB

- **Repository:** https://github.com/ciaxzs/disdec-teori
- **Direktori:** `04/`
- **File:** `README.md`
