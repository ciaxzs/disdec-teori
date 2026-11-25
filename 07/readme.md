# RANGKUMAN MATERI TEORI SISTEM TERDISTRIBUSI DAN TERDESENTRALISASI

## PERTEMUAN 7

### A. IDENTITAS MATERI

| Keterangan | Informasi |
|---|---|
| Mata Kuliah | Teori Sistem Terdistribusi dan Terdesentralisasi |
| Pertemuan | Pertemuan ke-7 |
| Topik Materi | Cloud Computing |
| Sumber Materi | 07--cloud-computing.pdf |
| Dosen Pengampu | Dr. Bambang Purnomosidi D. P. |
| AI yang Digunakan | ChatGPT GPT-6 |
| Format Dokumen | Markdown (.md) |

### B. TUJUAN PEMBELAJARAN

Berdasarkan materi perkuliahan, tujuan pembelajaran pada pertemuan ini adalah:

1. Mampu menjelaskan pengertian *Cloud Computing*.
2. Mampu menyebutkan dan menjelaskan berbagai karakteristik *Cloud Computing*.
3. Mampu menjelaskan berbagai model layanan *Cloud Computing*.
4. Mampu menjelaskan berbagai model *deployment* dari *Cloud Computing*.
5. Mampu menjelaskan penggunaan model layanan serta *deployment* dari suatu kasus.
6. Mampu menjelaskan arsitektur dan berbagai komponen dari *Cloud Computing*.
7. Mampu menjelaskan dan menerapkan prinsip *scalability* dan *redundancy* dari suatu kasus bidang teknologi informasi.
8. Mampu menjelaskan komponen virtualisasi dan teknologi *Container* serta memberikan solusi secara umum menggunakan komponen-komponen tersebut.
9. Mampu menjelaskan komputasi *Serverless* dan menerapkannya secara umum untuk kasus-kasus layanan yang diperlukan.
10. Mampu menjelaskan pengertian *Cloud Native App* serta berbagai komponennya.
11. Mampu membuat *containerized app* menggunakan Podman maupun Docker.

### C. RANGKUMAN MATERI

#### 1. Pengertian dan Sejarah Cloud Computing

Berdasarkan definisi **NIST**, *Cloud Computing* adalah sebuah model yang memungkinkan akses jaringan yang mudah diakses dan tersedia di mana saja, akses *on-demand* terhadap kumpulan sumber daya komputasi yang dapat dikonfigurasi (misalnya jaringan, *server*, penyimpanan, aplikasi, dan layanan) yang dapat dengan cepat disediakan dan dirilis dengan upaya manajemen atau interaksi penyedia layanan yang minimal.

Lawan dari *Cloud Computing* adalah **On Premise** (sering disingkat *on-prem*). Selain itu terdapat istilah **Off Premise** (*off-prem*), yaitu *co-location* di mana organisasi menempatkan *server* fisik di penyedia *Cloud Computing* publik.

Perkembangan sejarah *Cloud Computing* dalam materi mencakup:

* **1950-an:** era *mainframe*, John McCarthy membuat *theory of time sharing system*.
* **1961:** John McCarthy memprediksi komputer akan seperti air dan listrik (*Grid Computing*).
* **1969:** ARPANET.
* **1990:** WWW oleh Tim Berners-Lee $\rightarrow$ *Client-Server Computing*.
* **1997:** Prof. Rahmnath Chellapa (Emory University) menggunakan istilah *Cloud Computing*.
* **1999:** Salesforce.com.
* **2002:** AWS.
* **2006:** Amazon EC2.
* **2009:** Google Cloud, dan seterusnya.

Contoh penyedia *Cloud Computing* yang disebutkan dalam materi meliputi:

* **Di luar Indonesia:** AWS, Google, Alibaba, Heroku, Microsoft, Oracle, IBM.
* **Di Indonesia:** Biznet Gio, Telkom Telstra, Lintas Arta, DCI Indonesia.

`[MODIFIKASI]` Konsep *cloud computing* melanjutkan evolusi pembagian sumber daya komputasi menuju penyediaan layanan terukur dan fleksibel melalui jaringan.

#### 2. Karakteristik Cloud Computing

Enam karakteristik utama *Cloud Computing* yang dijelaskan dalam materi adalah:

1. **On-demand self service:** pengguna memperoleh sumber daya komputasi (seperti penyimpanan atau waktu *server*) secara otomatis dan instan tanpa interaksi manusia dengan penyedia layanan.
2. **Broad Network Access:** layanan *cloud* dapat diakses melalui jaringan menggunakan berbagai perangkat (*smartphone*, tablet, laptop) dari berbagai lokasi (kantor, rumah, atau saat bepergian).
3. **Resource Pooling:** penyedia *cloud* mengelompokkan dan mengelola kumpulan besar sumber daya komputasi fisik dan virtual (*server*, penyimpanan, jaringan) untuk melayani banyak pelanggan (*multi-tenancy*) secara bersamaan.
4. **Rapid Elasticity:** kemampuan sistem menyesuaikan sumber daya komputasi (daya pemrosesan, memori, penyimpanan) secara otomatis dan cepat sesuai perubahan permintaan.
5. **Measured Service:** pemantauan, pengendalian, dan pelaporan penggunaan sumber daya (*storage*, pemrosesan, *bandwidth*) secara otomatis untuk transparansi dan penagihan berbasis konsumsi atau *bayar per penggunaan*.
6. **Multitenancy:** satu *instance* perangkat lunak atau perangkat keras melayani banyak penyewa (*tenant*) dengan data dan operasi masing-masing tetap terisolasi dan aman.

`[MODIFIKASI]` Karakteristik-karakteristik ini membuat sumber daya komputasi dapat dialokasikan secara dinamis, terukur, dan terisolasi antar pengguna.

#### 3. Model Layanan dan Model Deployment

Terdapat tiga kelompok besar **Model Layanan** *Cloud Computing* (dan secara umum saat ini berkembang menjadi **XaaS** / *Everything as a Service*):

* **SaaS (*Software as a Service*):** ditujukan untuk *end users*.
* **PaaS (*Platform as a Service*):** ditujukan untuk *developers*.
* **IaaS (*Infrastructure as a Service*):** ditujukan untuk *network/infrastructure architect*.

Dalam pembagian lapisan layanan (*Applications*, *Data*, *Runtime*, *Middleware*, *O/S*, *Virtualization*, *Servers*, *Storage*, *Networking*), porsi yang dikelola pengguna vs penyedia *cloud* bergeser dari *on-premises* (semua dikelola pengguna) ke IaaS, PaaS, hingga SaaS (semakin banyak lapisan dikelola penyedia *cloud*).

Sementara itu, **Model Deployment** terdiri dari:

* **Public**
* **Private (*On-Premise*)**
* **Hybrid**
* **Community**

`[MODIFIKASI]` Pemilihan model layanan dan *deployment* bergantung pada tingkat kendali teknis yang diinginkan serta batasan operasional atau kebijakan organisasi.

#### 4. Arsitektur dan Komponen Cloud Computing

Arsitektur *Cloud Computing* memisahkan sisi **Front End** (*User Interface*) yang terhubung melalui **Internet** ke sisi **Back End**, dengan **Management** dan **Security** di kedua sisi. Komponen pada sisi *Back End* meliputi:

* **Application:** merepresentasikan SaaS.
* **Service:** merepresentasikan PaaS dan IaaS.
* **Cloud Runtime:** *execution and runtime environment for the VM*.
* **Storage** dan **Cloud**.
* **Infrastructure:** mencakup *Hypervisor* (*virtual machine monitor*), *Management software* (spesifik milik *cloud provider*), *Deployment software* (*tools* untuk DevOps), *Network*, *Server*, dan *Security-related tools*.

`[MODIFIKASI]` Pemisahan antarmuka pengguna (*front end*) dari lapisan komputasi, penyimpanan, dan manajemen di *back end* memungkinkan pengelolaan layanan terpusat dan aman.

#### 5. Scalability dan Redundancy

Materi membedakan **Skalabilitas** (*scalability*) dan **Elastisitas** (*elasticity*):

* **Skalabilitas:** kemampuan menangani penurunan atau kenaikan kebutuhan sumber daya pada *cloud* secara statis (dapat diterapkan pada 4 area umum: *Disk I/O*, *Memory*, *Network I/O*, dan *CPU*, dengan fitur kunci *sizeable difference*, *grow or shrink*, *speed*, mudah, dan *non-disruptive* tanpa *downtime*).
* **Elastisitas:** lebih mengarah pada naik turunnya kebutuhan sumber daya secara dinamis.

Tipe skalabilitas meliputi:

* **Vertical Scaling:** menambah daya dalam satu *server*.
* **Horizontal Scaling:** menambah *server*.
* **Diagonal Scaling:** gabungan vertikal dan horizontal (menambah daya terlebih dahulu sampai kapasitas penuh, lalu menambah *server*).

Pengaturan skalabilitas dapat bersifat **Manual**, **Scheduled** (berdasarkan karakteristik *user*), atau **Automatic** (seperti AWS Autoscaling, Google Load Balancing and Auto Scaling, dan Azure Autoscale).

Sementara itu, **Redundansi** di *cloud* merujuk pada duplikasi (lebih dari satu penyimpanan data / *storage systems*, *server*, *systems*, konfigurasi, dll.) agar data tetap aman saat satu *node* gagal, misalnya melalui layanan seperti AWS Backup dan Microsoft Azure Backup serta fitur pada *distributed database management systems* seperti PostgreSQL (SQL), Apache Cassandra (NoSQL), dan YugabyteDB/TiDB (NewSQL).

`[MODIFIKASI]` Skalabilitas membantu sistem menyesuaikan kapasitas terhadap beban kerja, sedangkan redundansi mengurangi *single point of failure* melalui duplikasi komponen dan data.

#### 6. Virtualisasi dan Teknologi Container

**Virtualisasi** (*virtualization*) menciptakan lingkungan virtual dari berbagai sumber daya dan/atau peranti komputasi, menjadi teknologi utama di *cloud* karena memungkinkan solusi *scalable* dengan mengurangi kebutuhan sumber daya fisik tanpa mengurangi fungsionalitas. Arsitektur hipervisor/VMM meliputi *Hosted Architecture* (dengan *Host OS* di bawah *Hypervisor Software*) dan *Bare-Metal Architecture* (seperti *Xen Project*, langsung di atas *Hardware*).

Selain mesin virtual, teknologi **Container** (sejalan dengan standar *Open Container Initiative* / OCI) membungkus aplikasi dan *library* di atas *Container Runtime* (seperti `runc` / `containerd`), engine/alat seperti **Docker** dan **Podman**, *Host OS*, serta *Physical Infrastructure*.

`[MODIFIKASI]` *Container* menawarkan paket aplikasi beserta dependensinya yang lebih ringan dibandingkan VM penuh karena berbagi *host OS* melalui *container runtime*.

#### 7. Komputasi Serverless

**Serverless** (diterjemahkan sebagai *Komputasi Nirserver*) merupakan model eksekusi pada *cloud computing* di mana penyedia layanan mengelola alokasi dan pemerolehan *server* secara dinamis. Materi mengingatkan bahwa istilah *serverless* bisa menyesatkan seolah tanpa *server*, padahal proses tetap mengikuti pola *client-server*, hanya saja pengelolaan *server* dilakukan secara dinamis oleh *provider*.

Salah satu contoh yang dicantumkan adalah *Azure SQL Database serverless compute tier*, yang menskalakan *compute* otomatis berdasarkan beban kerja, menagih penggunaan *compute* per detik, serta menjeda (*pause*) basis data saat tidak aktif (hanya menagih *storage*) dan melanjutkannya (*resume*) saat aktivitas kembali muncul.

`[MODIFIKASI]` Model *serverless* menggeser beban operasional provisi dan *scaling* *server* ke penyedia layanan sekaligus menyesuaikan biaya dengan tingkat aktivitas aktual.

#### 8. Cloud Native App (CNA)

**Cloud Native App (CNA)** pertama kali diistilahkan oleh Matt Stine (Pivotal, 2013) dan secara umum merupakan pendekatan membangun serta menjalankan aplikasi yang memanfaatkan lingkungan dan fasilitas *Cloud Computing*—terutama *elasticity* (menuju *scalability*) dan sifat *distributed*. Menurut **CNCF**, teknologi *cloud native* memberdayakan organisasi membangun dan menjalankan aplikasi *scalable* di lingkungan modern dan dinamis (*public*, *private*, dan *hybrid clouds*) menggunakan *containers*, *service meshes*, *microservices*, *immutable infrastructure*, dan *declarative APIs* yang dikombinasikan dengan otomatisasi.

Elemen dan alur pembangunan CNA dalam materi meliputi:

* **Elemen utama:** *Microservices*, *Containers* (misalnya Docker dan Kubernetes/K8s untuk *clustering-orchestration*), *DevOps* (budaya dan metode yang menyatukan *development* dan *operations* untuk *continuous delivery*), *CI/CD* (*Continuous Integration - Continuous Delivery*), serta teknologi pendukung ekosistem CNCF (seperti CoreDNS/CoreDBS dan `etcd`).
* **Tahapan membangun CNA:** *Define Architecture* $\rightarrow$ *Define Microservices* $\rightarrow$ *Containerize Services* $\rightarrow$ *Redesign Datastore* $\rightarrow$ *Build & Deploy* $\rightarrow$ *Verify*/*Validate*.
* **Contoh platform CNA:** AWS, Choreo, Google Cloud, dan Microsoft Azure.

`[MODIFIKASI]` Arsitektur *cloud native* memadukan layanan terpisah (*microservices*), *container*, dan otomatisasi *DevOps/CI-CD* agar perubahan aplikasi dapat dirilis lebih cepat dan tangguh.

### D. CONTOH PENERAPAN DAN ANALISIS

Berdasarkan materi perkuliahan, terdapat beberapa contoh penerapan dan analisis pada konsep *cloud computing* dan *cloud native*.

#### 1. Skalabilitas dan Redundansi pada Aplikasi Cloud

**Konsep yang digunakan:**

Skalabilitas (*vertical*, *horizontal*, *diagonal*) serta redundansi melalui duplikasi dan basis data terdistribusi.

**Cara kerja:**

Kapasitas sumber daya (*Disk I/O*, *Memory*, *Network I/O*, *CPU*) disesuaikan secara manual, terjadwal, atau otomatis (*autoscaling*) sesuai beban trafik, sementara salinan data/sistem/konfigurasi disiapkan pada *backup* atau klaster terdistribusi (seperti PostgreSQL, Apache Cassandra, YugabyteDB, TiDB).

`[MODIFIKASI]` Menggabungkan *auto-scaling* dengan redundansi data membantu aplikasi menghadapi lonjakan beban trafik sekaligus meminimalkan dampak kegagalan satu *node* atau pusat data.

**Alasan penggunaan:**

Menjaga kinerja aplikasi tetap responsif saat beban berubah dan mencegah kehilangan data saat terjadi kegagalan komponen.

**Hubungan dengan materi pertemuan:**

Contoh ini mengaitkan prinsip *scalability* dan *redundancy* dengan kebutuhan operasional aplikasi di *cloud*.

#### 2. Komputasi Serverless pada Basis Data (Azure SQL Database Serverless)

**Konsep yang digunakan:**

Eksekusi *serverless* dengan alokasi *compute* dinamis dan penagihan berbasis penggunaan.

**Cara kerja:**

Komputasi basis data diskalakan secara otomatis sesuai beban kerja, dijeda saat periode tidak aktif (sehingga hanya *storage* yang ditagih), dan diaktifkan kembali saat ada aktivitas.

`[MODIFIKASI]` Mekanisme jeda otomatis saat idle sangat relevan untuk beban kerja fluktuatif atau periodik agar biaya komputasi tidak terbuang saat tidak digunakan.

**Alasan penggunaan:**

Mengoptimalkan alokasi sumber daya dan biaya untuk beban kerja yang tidak berjalan konstan sepanjang waktu.

**Hubungan dengan materi pertemuan:**

Contoh ini memperjelas cara kerja model *serverless* tanpa menghilangkan pola komunikasi *client-server* di balik layar.

#### 3. Arsitektur Cloud Native App (CNA) Berbasis Microservices dan Container

**Konsep yang digunakan:**

*Cloud Native App*, *microservices*, *containers* (Docker/Kubernetes), *API gateway*, *event bus*, serta *DevOps* dan *CI/CD*.

**Cara kerja:**

Aplikasi klien (*mobile app*, *traditional web app*, *SPA web app*, IoT) mengakses layanan melalui *API gateway* ke berbagai *microservices* independen (dengan penyimpanan/cache sesuai kebutuhan dan komunikasi asinkron melalui *event bus*) yang dikemas dalam *container* dan dikelola melalui alur *DevOps* serta *CI/CD*.

`[MODIFIKASI]` Memecah fungsionalitas ke dalam *microservices* dalam *container* memungkinkan setiap layanan diskalakan dan diperbarui secara mandiri melalui *pipeline* otomatis.

**Alasan penggunaan:**

Meningkatkan *scalability*, *resiliency*, kecepatan rilis (*continuous delivery*), dan kemudahan pemeliharaan di lingkungan *cloud*.

**Hubungan dengan materi pertemuan:**

Contoh ini merangkum penerapan elemen dan tahapan pembangunan CNA yang dibahas pada bagian akhir materi.

### E. PENGGUNAAN AI

Dalam penyusunan rangkuman materi Pertemuan 7 ini, AI digunakan sebagai alat bantu untuk membaca, memahami, mengelompokkan, dan menyusun kembali materi perkuliahan ke dalam format laporan Markdown.

**AI yang digunakan:**

Gemini.

**Prompt yang digunakan:**

### 1. AI yang Digunakan

- Nama AI: ChatGPT GPT-6.
- Tujuan penggunaan: Membantu memahami, menganalisis, menyusun, dan mengembangkan rangkuman materi perkuliahan.
- Sumber utama: Materi perkuliahan yang diberikan oleh dosen dalam bentuk PDF.
- File yang dianalisis: `07--cloud-computing.pdf`.

### 2. Prompt yang Digunakan

Berikut prompt yang digunakan untuk menghasilkan rangkuman materi:

> Amatilah dan pelajari seluruh isi Modul 07 dengan topik Cloud Computing pada mata kuliah Teori Sistem Terdistribusi dan Terdesentralisasi. Baca seluruh halaman PDF, termasuk diagram, tabel, ilustrasi, dan contoh yang diberikan dosen.
>
> Buat rangkuman materi pertemuan 7 menggunakan template README.md yang telah diberikan.
>
> Kembangkan setiap pokok bahasan dengan penjelasan teori yang lengkap, mekanisme kerja, karakteristik, contoh penerapan dalam bidang Informatika, serta analisis manfaat dan keterbatasannya.
>
> Pertahankan istilah teknis dan makna materi asli. Jangan mengarang informasi yang tidak tersedia dalam materi. Gunakan bahasa Indonesia yang natural seperti laporan mahasiswa S1 Informatika, formal tetapi mudah dipahami.
>
> Berikan tanda **[MODIFIKASI]** pada bagian yang mengalami pengembangan substantif. Pertahankan seluruh struktur A sampai G sesuai template, termasuk bagian identitas, tujuan pembelajaran, rangkuman materi, contoh penerapan dan analisis, penggunaan AI, kesimpulan, serta daftar referensi.
>
> Pastikan hasil akhir lengkap, sistematis, dan siap dimasukkan ke repository GitHub dalam format Markdown.

### 3. Bagian yang Disesuaikan dari Keluaran AI

Bagian dari hasil rangkuman yang mengalami pengembangan dan penyesuaian meliputi:

1. **Karakteristik dan Model Layanan Cloud Computing:** Penjelasan SaaS, PaaS, IaaS, XaaS, dan enam karakteristik cloud dikembangkan dengan contoh penggunaan agar perbedaan setiap konsep lebih mudah dipahami.

2. **Scalability dan Redundancy:** Penjelasan vertical, horizontal, dan diagonal scaling diperluas dengan contoh penerapan pada sistem informasi akademik serta hubungan redundansi dengan distributed database.

3. **Virtualisasi dan Teknologi Container:** Pembahasan hypervisor, Virtual Machine, Hosted Architecture, Bare-Metal Architecture, dan container dikembangkan dengan penjelasan perbedaan cara kerja dan penggunaannya.

4. **Cloud Native Application:** Pembahasan microservices, DevOps, CI/CD, API Gateway, dan tahapan pembangunan CNA diperluas agar hubungan antar komponen dan proses pengembangan aplikasi lebih mudah dipahami.

Penyesuaian juga dilakukan pada bagian contoh penerapan dan analisis agar materi tidak hanya berisi definisi, tetapi menunjukkan bagaimana konsep Cloud Computing digunakan dalam pembangunan sistem informasi.

### F. KESIMPULAN

Berdasarkan materi Pertemuan 7, *Cloud Computing* menyediakan akses sumber daya komputasi terukur dan *on-demand* melalui jaringan dengan karakteristik *on-demand self service*, *broad network access*, *resource pooling*, *rapid elasticity*, *measured service*, dan *multitenancy*, yang dibedakan dari pendekatan *on-premise* maupun *off-premise* (*co-location*). Layanan dan *deployment*-nya terbagi ke dalam model IaaS, PaaS, SaaS (serta XaaS) dan *public*, *private*, *hybrid*, serta *community* yang ditopang arsitektur *front end* dan *back end*.

Ketangguhan dan fleksibilitas sistem di *cloud* didukung oleh prinsip *scalability* dan *redundancy*, teknologi virtualisasi serta *container* (seperti Docker dan Podman), model komputasi *serverless*, hingga pendekatan *Cloud Native App* yang mengintegrasikan *microservices*, *container orchestration*, *DevOps*, dan *CI/CD*.

### G. DAFTAR REFERENSI

1. Bambang Purnomosidi D. P. (Tanpa tahun). *Cloud Computing*. Materi perkuliahan Teori Sistem Terdistribusi dan Terdesentralisasi (Kode: FIF25002T, 3 SKS), Program Studi Informatika, Fakultas Teknologi Informasi, Universitas Teknologi Digital Indonesia. File: `07--cloud-computing_2.pdf`.

**Sumber ilustrasi, dokumentasi, dan referensi yang dicantumkan dalam materi:**

* AWS Autoscaling. https://aws.amazon.com/id/autoscaling/
* Google Cloud Load Balancing and Auto Scaling. https://cloud.google.com/compute/docs/load-balancing-and-autoscaling
* Microsoft Azure Autoscale. https://azure.microsoft.com/en-us/products/virtual-machines/autoscale/
* AWS Backup. https://aws.amazon.com/backup/
* Microsoft Azure Backup. https://azure.microsoft.com/en-gb/services/backup/
* Open Container Initiative (OCI). https://opencontainers.org/
* Cloud Native Computing Foundation (CNCF) Definition. https://github.com/cncf/toc/blob/master/DEFINITION.md
* Nagarro. *Cloud Native Development: Choosing Right Architecture*. https://www.nagarro.com/en/blog/cloud-native-development-choosing-right-architecture
* AWS Cloud Native. https://aws.amazon.com/what-is/cloud-native

### INFORMASI DOKUMENTASI GITHUB

* **Repository:** https://github.com/ciaxzs/disdec-teori
* **Direktori:** `07/`
* **File:** `README.md`
