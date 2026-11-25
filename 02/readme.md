# RANGKUMAN MATERI TEORI SISTEM TERDISTRIBUSI DAN TERDESENTRALISASI

# PERTEMUAN 2

---

## A. IDENTITAS MATERI

| Keterangan | Informasi |
|---|---|
| Mata Kuliah | Teori Sistem Terdistribusi dan Terdesentralisasi |
| Program Studi | S1 Informatika |
| Kode Mata Kuliah | FIF25002T |
| Pertemuan | 2 |
| Topik Materi | Pengenalan Sistem Terdistribusi dan Terdesentralisasi |
| Dosen Pengampu | Dr. Bambang Purnomosidi D. P. |
| Institusi | Universitas Teknologi Digital Indonesia (UTDI) |
| Sumber Materi | 01 - Pengenalan.pdf |
| AI yang Digunakan | ChatGPT GPT-6 |
| Format Dokumen | Markdown (.md) |

---

## B. TUJUAN PEMBELAJARAN

Berdasarkan materi perkuliahan, tujuan pembelajaran pada pertemuan ini adalah:

1. Mampu menjelaskan konsep proses pada sistem terdistribusi.
2. Mampu menjelaskan berbagai jenis komunikasi antar proses (IPC).
3. Mampu menganalisis isu sinkronisasi, reliabilitas, dan keamanan pada sistem terdistribusi.
4. Mampu mengaitkan konsep ke contoh nyata seperti microservices, cloud, maupun distributed messaging.

---

## C. RANGKUMAN MATERI

### 1. Konsep Proses dan Manajemen Proses
   
Dalam sistem operasi, program yang tersimpan di dalam disk (berisi sekumpulan instruksi) diinstansiasi ke dalam RAM sebagai proses. Proses terdiri atas beberapa thread dengan tingkat prioritas berbeda yang dikelola oleh scheduler (bagian dari OS) melalui mekanisme context switch dan preemption untuk dieksekusi oleh CPU.
Sistem operasi mengelola proses melalui tiga aktivitas utama:

- **Process Creation:**
OS membuat proses baru berdasarkan permintaan (request) pengguna/aplikasi, mengalokasikan sumber daya (seperti memori dan file), serta menginisialisasi lingkungan eksekusinya (PCB, registers, dan stack) hingga siap dijalankan.

- **Process Migration:** 
OS memindahkan proses yang sedang berjalan atau siap dijalankan dari satu CPU (atau node) ke CPU/node lain untuk menyeimbangkan beban (load balancing), meningkatkan performa, atau menangani kegagalan.

- **Process Monitoring:** 
OS melacak dan mengamati status proses (seperti Running atau Sleeping), penggunaan CPU, penggunaan memori, serta performa sistem untuk memastikan eksekusi berjalan dengan baik dan mengambil tindakan korektif jika diperlukan.

**[MODIFIKASI]**
Pemisahan antara program statis di disk dan proses aktif di RAM serta pengelolaan thread oleh scheduler menjadi fondasi sebelum memahami bagaimana proses-proses tersebut saling berinteraksi ketika berada pada node yang berbeda.

### 2. Sistem Terdistribusi dan Komunikasi Antar Node

Sistem terdistribusi merupakan sekumpulan komputer atau node yang independen dan bekerja bersama dalam satu koordinasi sebagai satu kesatuan logis. Setiap node menjalankan prosesnya masing-masing, sehingga agar dapat beroperasi sebagai satu sistem logis yang utuh, antar-node harus saling berkomunikasi melalui jaringan.

Komunikasi antar-node pada sistem terdistribusi mencakup empat fungsi utama:

- **Pertukaran Data:** 
Node saling mengirim dan menerima data untuk menjalankan layanan terdistribusi.

- **Koordinasi:** 
Node berkoordinasi untuk sinkronisasi, konsistensi data, dan manajemen transaksi.

- **Keandalan:** 
Komunikasi antar-node memastikan sistem tetap berjalan meskipun terjadi kegagalan pada salah satu node.

- **Skalabilitas:** 
Node dapat ditambah atau dikurangi secara dinamis sesuai kebutuhan beban kerja.

- **Dalam komunikasi antar-node, terdapat empat jenis interaksi utama, yaitu**
Request (permintaan layanan/data), 
Response (hasil/balasan), 
Publish (mengirim event atau pembaruan), dan 
Subscribe (menerima notifikasi). 

- **Protokol yang umum digunakan meliputi** 
HTTP/HTTPS, 
gRPC, 
Message Queue (seperti Kafka dan RabbitMQ), serta 
DNS / Service Discovery.

- **Beberapa contoh penerapan komunikasi antar-node di dunia nyata antara lain:**
1. Multiplayer games.
2. Aplikasi transportasi daring seperti Gojek/Grab (interaksi antara antarmuka pengguna dengan berbagai layanan seperti pengemudi, pelacakan lokasi, dan penghitungan biaya).
3. Fitur chat atau video call pada WhatsApp yang menggunakan komunikasi point-to-point pada infrastruktur terdistribusi.

**[MODIFIKASI]**
Tanpa lapisan komunikasi antar-node (seperti HTTP, gRPC, atau message queue), setiap node hanya akan berjalan sebagai entitas terpisah dan tidak mampu menghadirkan layanan terpadu seperti pelacakan lokasi maupun pembaruan event secara terkoordinasi.

### 3. Model Komunikasi Pesan

Dalam pengiriman pesan antar proses, terdapat beberapa model komunikasi yang digunakan:

- **Komunikasi Langsung:** 
Menggunakan socket jaringan (seperti contoh implementasi socket TCP di Python dengan `AF_INET` dan `SOCK_STREAM` yang menghubungkan alamat host dan port secara langsung antara server dan klien).

- **Komunikasi Tidak Langsung** 
Menggunakan perantara seperti mailboxes dan message queues (misalnya perintah `write` di Linux).

- **Publish/Subscribe (Pub/Sub):** 
Publisher mengirimkan pesan (`msg`) ke sebuah Topic, kemudian pesan tersebut didistribusikan kepada para Subscriber yang berlangganan pada topik tersebut.

- **[MODIFIKASI]**
Perbedaan antara komunikasi langsung berbasis socket dan pola perantara seperti message queue atau Pub/Sub menunjukkan variasi tingkat keterikatan (coupling) dan distribusi pesan antara pengirim dan penerima.

### 4. Proses pada Sistem Terdistribusi dan Jenis-Jenis IPC

Proses pada sistem terdistribusi dapat berada pada node fisik yang berbeda, sehingga tidak memiliki shared memory bersama. Oleh karena itu, diperlukan mekanisme IPC (Inter-Process Communication) khusus untuk lingkungan terdistribusi.

**Pada dasarnya terdapat 4 jenis IPC:**

- **Shared Memory:** 
Proses A menulis ke area memori bersama yang dibaca oleh Proses B melalui dukungan kernel. Namun, mekanisme ini tidak cocok untuk sistem terdistribusi karena tidak ada akses terhadap memori fisik antar-node yang terpisah.

- **Message Passing:** 
Proses berkomunikasi dengan saling mengirim dan menerima pesan (`send` dan `receive`) melalui jaringan berkecepatan tinggi. Standar yang digunakan adalah MPI (Message Passing Interface), dengan versi terakhir hingga Oktober 2026 adalah MPI 5.0 (seperti implementasi OpenMPI dan pustaka `mpi4py` pada Python).

- **Remote Procedure Call (RPC):** 
Mekanisme yang memungkinkan klien memanggil prosedur pada server jarak jauh seolah-olah pemanggilan tersebut dilakukan secara lokal, dengan bantuan komponen Stub di sisi klien maupun server untuk menangani pengemasan permintaan dan hasil. Contoh penerapannya adalah gRPC (misalnya komunikasi antara Ruby Client atau Android-Java Client dengan C++ Service menggunakan Proto Request dan Proto Response).

- **Message-Oriented Middleware (MOM):**
Infrastruktur perangkat lunak perantara yang memfasilitasi komunikasi dan pertukaran data antar aplikasi melalui saluran komunikasi berisi unit informasi mandiri (message). Dalam lingkungan MOM, pesan dikirim dan diterima secara asinkron melalui Messaging Provider.

Standar dan protokol MOM yang tercantum dalam materi meliputi:
- XATMI Specification dari X/Open group (Distributed Transaction Processing).
- AMQP (Advanced Message Queuing Protocol) — umumnya digunakan untuk aplikasi berskala enterprise.
- HLA (The High Level Architecture IEEE 1516) dari IEEE dan SISO.
- MQTT (MQ Telemetry Transport) — umumnya digunakan untuk perangkat dengan sumber daya terbatas (resource-constrained devices).
- DDS (Data Distribution Service) dari OMG (Object Management Group).
- XMPP (eXtensible Messaging and Presence Protocol).

**[MODIFIKASI]**
Karena shared memory tidak tersedia lintas node dalam sistem terdistribusi, pemilihan antara Message Passing, RPC, atau MOM sangat bergantung pada kebutuhan komunikasi langsung antar proses, pemanggilan prosedur terstruktur, atau pengiriman pesan asinkron melalui perantara.

### 5. Studi Kasus Arsitektur Microservices serta Komunikasi Sinkron dan Asinkron

Pada arsitektur Microservices, sebuah aplikasi dipecah menjadi beberapa layanan (microservice) independen yang terhubung dengan antarmuka pengguna (user interface), di mana masing-masing microservice memiliki database-nya sendiri dan saling berkomunikasi melalui jaringan.

Dalam interaksi antar layanan atau antara klien dan server, terdapat dua pola komunikasi utama:
- Aspek	Komunikasi Sinkron (Synchronous)	Komunikasi Asinkron (Asynchronous)
- Alur kerja klien	Klien mengirim request lalu menunggu (waiting for response) hingga server  membalas	Klien mengirim request lalu dapat langsung melanjutkan pekerjaan lain (continue working)
- Pemrosesan respons	Eksekusi klien tertahan sampai respons diterima	Respons diterima kemudian hari dan ditindaklanjuti saat sudah tersedia

**[MODIFIKASI]**
Pada arsitektur microservices dengan database yang terpisah per layanan, pola sinkron dan asinkron menentukan apakah suatu layanan harus menunggu balasan segera atau dapat memproses tugas secara independen tanpa menghambat alur kerja pemanggil.

### 6. Masalah dan Protokol Komunikasi Antar Proses

Dalam membangun komunikasi antar proses pada sistem terdistribusi, terdapat empat masalah utama yang harus ditangani:

- **Reliability (Keandalan):** 
Memastikan pesan terkirim secara lengkap dan dalam urutan yang benar meskipun terjadi kehilangan paket atau system crash. Solusinya meliputi penggunaan acknowledgement, mekanisme transmisi ulang (retransmission), serta penggunaan protokol transport yang andal seperti TCP.

- **Ordering (Pengurutan):** 
Memastikan pesan diproses dalam urutan yang logis dan dapat diprediksi. Solusinya meliputi penggunaan Pipes (FIFO), Message queues, Shared memory, Sockets dan message passing, serta RPC.

- **Security (Keamanan):** 
Menjaga keamanan pertukaran pesan melalui mekanisme enkripsi dan autentikasi.

- **Performance (Performa):** 
Mengelola faktor latensi (latency) dan lebar pita (bandwidth) jaringan.

Adapun protokol komunikasi yang digunakan terbagi menjadi dua lapisan utama:

- **Protokol yang mendasari:**
TCP, UDP, dan HTTP.

- **Protokol utama (berjalan di atas HTTP sebagai protokol transport):**
gRPC, GraphQL, dan REST.

- **Dalam arsitektur protokol web modern, terdapat perbedaan struktur antara HTTP/2 dan HTTP/3:**
- Lapisan	HTTP/2	HTTP/3
- Application Layer	HTTPS	HTTPS
- Security Layer	TLS	QUIC (User space)
- Transport Layer	TCP	QUIC (User space) + UDP (Kernel & network space)
- Network Layer	IP (Internet Protocol)	IP (Internet Protocol)

**[MODIFIKASI]**
Peralihan dari TCP + TLS pada HTTP/2 menuju QUIC di atas UDP pada HTTP/3 memperlihatkan upaya optimasi pada lapisan keamanan dan transport dalam komunikasi jaringan modern.

### 7. Konsep Sinkronisasi dan Logical Clock

Karena setiap node dalam sistem terdistribusi memiliki jam lokal (local clock) masing-masing, pergeseran jam perangkat keras (clock drift) dan latensi jaringan dapat menyebabkan perbedaan waktu antar-node. 

Sinkronisasi clock diperlukan untuk menyelaraskan waktu antar komputer guna menjaga akurasi urutan kejadian, konsistensi data, dan koordinasi operasi.

Metode sinkronisasi waktu eksternal memanfaatkan atomic clock yang menghasilkan TAI (International Atomic Time), dipadukan dengan GPS dan UTC (Universal Coordinated Time), lalu disinkronkan ke jaringan menggunakan protokol NTP (Network Time Protocol) atau PTP (Precision Time Protocol), di mana PTP memiliki tingkat presisi lebih tinggi dibandingkan NTP.

Selain jam fisik, sistem terdistribusi menggunakan Logical Clock untuk menentukan urutan kejadian tanpa bergantung langsung pada jam fisik (real clock), karena real clock rentan mengalami pergeseran pencatatan akibat latensi atau gangguan jaringan.

- **Pada Lamport Logical Clock, aturan kerjanya adalah sebagai berikut:**
- Setiap terjadi kejadian internal pada suatu proses, nilai logical clock bertambah 1.
- Saat mengirim pesan, pengirim menyertakan nilai logical clock-nya.
- Saat menerima pesan, penerima membandingkan nilai logical clock pada pesan dengan nilai logical clock lokalnya, mengambil nilai terbesar, lalu menambahkannya dengan 1.

- **Sebagai ilustrasi pada sistem logging dengan tiga layanan (Sales Service, Product Service, dan Invoice Service) yang masing-masing bermula dari nilai `0`:**

- Sales Service mencatat transaksi penjualan, menaikkan logical clock menjadi `1`, dan mengirim request ke Product Service dengan stempel waktu `1`.
- Product Service menerima request (`1`), membandingkannya dengan jam lokal (`0`), mengambil nilai terbesar (`1`), memperbaruinya menjadi `2` ($1 + 1$), lalu mengirim request ke Invoice Service dengan nilai `2`.
- Invoice Service menerima request (`2`), membandingkannya dengan jam lokal (`0`), mengambil nilai terbesar (`2`), memperbaruinya menjadi `3` ($2 + 1$), lalu menerbitkan faktur.
- Dengan mekanisme ini, urutan kejadian tercatat secara konsisten: `1` (Sales Service), `2` (Product Service), dan `3` (Invoice Service).

- **Karena Lamport Logical Clock masih bersifat scalar clock, konsep ini kemudian dikembangkan lebih lanjut menjadi:**

- Vector Clocks — Colin Fidge dan Friedemann Mattern (1988).
- Plausible Clocks — Torres-Rojas dan Ahamad (1999).
- Chain Clocks — Agarwal dan Garg (2005).
- Interval Tree Clocks — Almeida et al. (2008).
- Blum Clocks — Lum Ramabaja (2019).

**[MODIFIKASI]**
Pendekatan logical clock memberikan cara penentuan urutan kejadian yang lebih tahan terhadap deviasi jam fisik dan latensi jaringan dibandingkan mengandalkan real clock semata.

### 8. Koordinasi Proses, Tantangan, dan Isu Terkini

Koordinasi proses merupakan mekanisme yang memungkinkan beberapa proses independen di berbagai komputer bekerja sama secara harmonis untuk mencapai tujuan bersama, dengan mengelola komunikasi, sinkronisasi, dan akses terhadap sumber daya bersama agar terhindar dari konflik seperti deadlock maupun race condition. Contoh perangkat lunak koordinasi proses antara lain Apache ZooKeeper, etcd, Consul, ClickHouse Keeper, Oxia, dan KRaft.

- **Berbagai tantangan terkait proses pada sistem terdistribusi beserta solusinya dirangkum dalam tabel berikut:**

- **Tantangan	Solusi yang Digunakan :**

- Message loss (kehilangan pesan)	Retransmission (transmisi ulang) dan acknowledgement
- Deadlock	Timeout dan algoritma deteksi (detection algorithm)
- Data inconsistency (ketidakkonsistenan data)	Protokol konsensus seperti Raft dan Paxos
- Security (keamanan)	SSL/TLS dan OAuth2

- **Sementara itu, isu terkini (current issues) yang berkembang dalam ranah proses dan komunikasi sistem terdistribusi meliputi:**

- Edge and Fog Computing.
- Observability and Tracing: pemanfaatan telemetry.

- **Container Orchestration :**
penggunaan Kubernetes dan Docker Swarm.

- **Sebagai bahan diskusi perkuliahan pada pertemuan ini, diajukan tiga pertanyaan utama:**
1. Apakah GraphQL merupakan contoh dari RPC?
2. Apakah REST merupakan contoh dari RPC?
3. Apakah Telemetry merupakan solusi etis?

**[MODIFIKASI]**
Keberadaan perangkat koordinasi seperti ZooKeeper, etcd, dan KRaft serta protokol konsensus seperti Raft dan Paxos menjadi bagian penting untuk menjaga keteraturan eksekusi dan konsistensi data di tengah potensi kegagalan maupun konflik antar proses.

---

### D. CONTOH PENERAPAN DAN ANALISIS
Berdasarkan materi perkuliahan, terdapat beberapa contoh penerapan proses dan komunikasi antar proses dalam layanan teknologi modern.

### 1. Aplikasi Transportasi Daring (Gojek / Grab) sebagai Contoh Komunikasi Antar Node
   
- **Konsep yang digunakan:**
Komunikasi antar proses pada sistem terdistribusi (distributed inter-process communication) dan koordinasi antar-node.

- **Cara kerja:**
Antarmuka pengguna (user interface) berkomunikasi melalui jaringan dengan berbagai layanan terdistribusi di sisi backend, seperti layanan pengelolaan pengemudi (driver), pelacakan lokasi (location tracing), dan layanan penghitungan biaya perjalanan.

**[MODIFIKASI]**
Setiap layanan tersebut berjalan sebagai proses terpisah pada node yang berbeda dan saling bertukar data (seperti koordinat lokasi dan tarif) untuk membentuk satu pengalaman pemesanan yang utuh bagi pengguna.

- **Alasan penggunaan:**
Pemisahan proses ke berbagai layanan memungkinkan pengelolaan beban kerja yang lebih terstruktur dan skalabilitas sesuai kebutuhan masing-masing fungsi aplikasi.
Hubungan dengan materi pertemuan:
Contoh ini menunjukkan bagaimana node independen saling berkomunikasi dan berkoordinasi agar berfungsi sebagai satu kesatuan sistem logis.

### 2. gRPC sebagai Contoh Implementasi Remote Procedure Call (RPC)

- **Konsep yang digunakan:**
Remote Procedure Call (RPC) dan penggunaan Stub.

- **Cara kerja:**
Klien yang dibangun dengan bahasa pemrograman berbeda (misalnya Ruby Client atau Android-Java Client) memanggil layanan pada gRPC Server (misalnya berbasis C++) menggunakan gRPC Stub dengan mengirimkan Proto Request dan menerima Proto Response.

**[MODIFIKASI]**
Penggunaan stub menyembunyikan kerumitan komunikasi jaringan sehingga klien dapat berinteraksi dengan layanan jarak jauh secara terstruktur lintas platform.

**Alasan penggunaan:**
Mendukung komunikasi antar proses pada sistem heterogen yang menggunakan bahasa pemrograman dan platform berbeda.
Hubungan dengan materi pertemuan:
gRPC merupakan contoh konkret penerapan mekanisme RPC yang berjalan di atas protokol HTTP sebagai protokol transport.

### 3. Sistem Logging Layanan Penjualan dengan Lamport Logical Clock

- **Konsep yang digunakan:**
Logical Clock (Lamport Logical Clock) untuk pengurutan kejadian (event ordering).

- **Cara kerja:**
Tiga layanan terdistribusi (Sales Service, Product Service, dan Invoice Service) mencatat setiap transaksi dengan menaikkan nilai logical clock lokal dan menyertakannya saat mengirim pesan ke layanan berikutnya sebelum dicatat ke Central Logging Service.

**[MODIFIKASI]** 
Dengan membandingkan nilai clock kiriman dan lokal lalu menambahkan angka 1, sistem tetap dapat merekonstruksi urutan kejadian (`1` $\rightarrow$ `2` $\rightarrow$ `3`) meskipun terjadi pergeseran waktu akibat latensi atau gangguan jaringan antar-node.

- **Alasan penggunaan:**
Menghindari kesalahan urutan pencatatan akibat latensi, masalah jaringan, atau masalah perangkat keras jika hanya mengandalkan real clock timestamp.

- **Hubungan dengan materi pertemuan:**
Penerapan ini menjawab permasalahan sinkronisasi waktu dan pengurutan kejadian (ordering) pada sistem terdistribusi.

### 4. Perbandingan Komunikasi Sinkron dan Asinkron pada Layanan Terdistribusi

Materi membedakan dua mekanisme komunikasi utama antara klien dan server.
Aspek	Komunikasi Sinkron (Synchronous)	Komunikasi Asinkron (Asynchronous)
Perilaku pengirim	Menunggu respons (waiting for response) setelah mengirim permintaan	Tetap melanjutkan pekerjaan lain (continue working) setelah mengirim permintaan
Pemrosesan lanjutan	Menunggu balasan dari server sebelum melanjutkan	Menerima respons dan melakukan sesuatu (get response and do something)
Kebutuhan	Respons langsung dari server	Pemrosesan terpisah tanpa menahan alur kerja pengirim

**[MODIFIKASI]**
Pemilihan antara komunikasi sinkron dan asinkron bergantung pada apakah proses pengirim perlu menunggu respons langsung dari server atau dapat langsung melanjutkan aktivitas lain sambil menunggu balasan.

---

## E. PENGGUNAAN ARTIFICIAL INTELLIGENCE (AI)

### 1. AI yang Digunakan

- Nama AI: Gemini AI
- Pengembang: OpenAI.
- Tujuan penggunaan: Membantu membaca, memahami, merangkum, mengembangkan, dan mengevaluasi materi perkuliahan.
- Sumber utama: File PDF pertemuan kedua yang diberikan oleh dosen.
- Format hasil: Markdown (.md).

### 2. Prompt yang Digunakan

Berikut prompt yang digunakan dalam proses penyusunan rangkuman:

**Prompt 1 — Analisis dan Rangkuman Materi**

> Kamu adalah mahasiswa S1 Informatika yang sedang mempelajari mata kuliah Teori Sistem Terdistribusi dan Terdesentralisasi. Saya akan memberikan materi PDF dari dosen untuk pertemuan pertama.
>
> Baca dan analisis seluruh isi PDF secara menyeluruh. Identifikasi tujuan pembelajaran, agenda pembahasan, konsep utama, istilah teknis, contoh penerapan, dan kesimpulan dari materi.
>
> Buat rangkuman yang lengkap, sistematis, dan menggunakan bahasa Indonesia yang natural seperti mahasiswa Informatika.
>
> Ketentuan:
> 1. Gunakan materi PDF dosen sebagai sumber utama.
> 2. Jangan menghilangkan konsep penting dari materi.
> 3. Jangan mengarang informasi yang tidak didukung sumber.
> 4. Jelaskan setiap konsep dengan bahasa yang mudah dipahami.
> 5. Kembangkan penjelasan dari poin-poin slide menjadi paragraf yang informatif.
> 6. Sertakan contoh penerapan teknologi informasi jika relevan.
> 7. Jelaskan perbedaan sistem terdistribusi dan terdesentralisasi.
> 8. Berikan pembahasan mendalam tentang CAP Theorem, Strong Consistency, dan Eventual Consistency.
> 9. Susun hasil dalam format Markdown menggunakan heading dan subheading.
> Setelah rangkuman selesai, lakukan pemeriksaan ulang terhadap kesesuaiannya dengan materi PDF dosen. Jangan mengklaim seluruh hasil sebagai pekerjaan manual.

### 3. Bagian yang Disesuaikan dari Keluaran AI

Setelah proses analisis dan pengembangan terhadap rangkuman awal, beberapa bagian mendapatkan penyesuaian sebagai berikut:

1. **Pengertian Sistem Terdistribusi:** Penjelasan dikembangkan dengan menambahkan ilustrasi komunikasi antar-komputer, konsep transparansi, dan contoh penerapan pada layanan penyimpanan cloud.

2. **Arsitektur Sistem Dasar:** Pembahasan Client-Server, Peer-to-Peer, dan Hybrid dikembangkan dengan menambahkan mekanisme kerja, kelebihan, serta contoh penerapan masing-masing arsitektur.

3. **Karakteristik Sistem Terdistribusi:** Setiap karakteristik seperti skalabilitas, fault tolerance, transparansi, kinerja tinggi, dan heterogenitas dijelaskan lebih lanjut dengan contoh yang relevan.

4. **Sistem Terdistribusi dan Terdesentralisasi:** Ditambahkan tabel perbandingan berdasarkan fokus, tujuan, pengelolaan, dan contoh penerapan. Penjelasan juga dikembangkan untuk menunjukkan bahwa sistem terdistribusi tidak selalu bersifat terdesentralisasi.

5. **Studi Kasus:** Contoh GFS, HDFS, Kafka, Pulsar, Netflix, Twitch, YouTube, Blockchain, DNS, dan BitTorrent dikembangkan dengan penjelasan fungsi serta penerapan teknologinya.

6. **CAP Theorem:** Ditambahkan ilustrasi dua server yang mengalami gangguan komunikasi untuk mempermudah pemahaman hubungan Consistency, Availability, dan Partition Tolerance.

7. **Konsistensi Data:** Strong Consistency dan Eventual Consistency dikembangkan dengan penjelasan mekanisme serta perbandingan penerapannya pada sistem perbankan dan media sosial.

8. **Tantangan Sistem:** Pembahasan latency, throughput, keamanan, DDoS, Sybil Attack, kompleksitas manajemen node, dan governance dikembangkan menggunakan contoh situasi nyata.

9. **Tren Masa Depan:** Cloud-Native, Edge Computing, Fog Computing, Web3, DeFi, Federated Data, dan Federated Learning diberikan penjelasan tambahan mengenai fungsi dan penerapannya.

10. **Contoh Penerapan dan Analisis:** Ditambahkan pembahasan yang menghubungkan konsep perkuliahan dengan layanan teknologi yang digunakan dalam kehidupan sehari-hari.

---

## F. KESIMPULAN
Berdasarkan materi Pertemuan 2, proses pada sistem terdistribusi berjalan pada berbagai node yang terpisah secara fisik dan tidak memiliki shared memory bersama. Agar sekumpulan node independen tersebut dapat beroperasi sebagai satu kesatuan logis, diperlukan mekanisme komunikasi antar proses (Inter-Process Communication) seperti Message Passing (MPI), Remote Procedure Call (RPC/gRPC), dan Message-Oriented Middleware (MOM) dengan pola komunikasi sinkron maupun asinkron.
Keberhasilan komunikasi antar proses berkaitan dengan penanganan isu reliability, ordering, security, dan performance. Selain penggunaan protokol seperti TCP, UDP, HTTP, gRPC, GraphQL, dan REST (serta perkembangan HTTP/2 dan HTTP/3), sistem terdistribusi juga menggunakan sinkronisasi clock (melalui TAI, GPS, UTC, NTP, PTP, maupun Logical Clock seperti Lamport Logical Clock dan Vector Clocks) serta perangkat koordinasi proses seperti Apache ZooKeeper, etcd, Consul, ClickHouse Keeper, Oxia, dan KRaft untuk menghadapi tantangan seperti message loss, deadlock, data inconsistency, dan security.

---

## G. DAFTAR REFERENSI
- Bambang Purnomosidi D. P. (Tanpa tahun). Proses dan Komunikasi Antar Proses pada Sistem Terdistribusi. Materi perkuliahan Teori Sistem Terdistribusi dan Terdesentralisasi (Kode: FIF25002T, 3 SKS), Program Studi Informatika, Fakultas Teknologi Informasi, Universitas Teknologi Digital Indonesia. File: `02--proses-dan-komunikasi-antar-proses.pdf`.
- Fidge, C., & Mattern, F. (1988). Referensi konsep Vector Clocks sebagaimana dicantumkan dalam materi perkuliahan.
- Torres-Rojas, F. J., & Ahamad, M. (1999). Referensi konsep Plausible Clocks sebagaimana dicantumkan dalam materi perkuliahan.
- Agarwal, A., & Garg, V. K. (2005). Referensi konsep Chain Clocks sebagaimana dicantumkan dalam materi perkuliahan.
- Almeida, P. S., Baquero, C., & Fonte, V. (2008). Referensi konsep Interval Tree Clocks sebagaimana dicantumkan dalam materi perkuliahan.
- Ramabaja, L. (2019). Referensi konsep Blum Clocks sebagaimana dicantumkan dalam materi perkuliahan.

**Sumber ilustrasi dan dokumentasi yang dicantumkan dalam materi:**
- Wikipedia. Process (computing). https://en.wikipedia.org/wiki/Process_(computing)
- Dashbird. Pub/Sub Messaging. https://dashbird.io/knowledge-base/well-architected/pub-sub-messaging/
- Medium (Haasita Pinnepu). The Art of Conversation in Distributed Systems: Interprocess Communication. https://medium.com/@haasitapinnepu/the-art-of-conversation-in-distributed-systems-interprocess-communication-a651d97e12e1
- University of Hull HPC MediaWiki. OpenMPI. https://hpc.mediawiki.hull.ac.uk/Programming/OpenMPI
- MPI Forum. Message Passing Interface & Implementation Status. https://www.mpi-forum.org/ dan https://www.mpi-forum.org/implementation-status/
- mpi4py Documentation. https://mpi4py.readthedocs.io/en/stable/
- gRPC Documentation. What is gRPC? Introduction. https://grpc.io/docs/what-is-grpc/introduction/
- Akamai. What Are Microservices? https://www.akamai.com/glossary/what-are-microservices
- Stackscale. HTTP/3. https://www.stackscale.com/blog/http3/
- Medium (Outreach Prague). Lamport Clocks: Determining the Order of Events in Distributed Systems. https://medium.com/outreach-prague/lamport-clocks-determining-the-order-of-events-in-distributed-systems-41a9a8489177

---
INFORMASI DOKUMENTASI GITHUB
Repository: https://github.com/ciaxzs/disdec-teori
Direktori: `02/`
File: `README.md`
