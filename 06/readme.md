# RANGKUMAN MATERI TEORI SISTEM TERDISTRIBUSI DAN TERDESENTRALISASI

## PERTEMUAN 6

### A. IDENTITAS MATERI

| Keterangan | Informasi |
|---|---|
| Mata Kuliah | Teori Sistem Terdistribusi dan Terdesentralisasi |
| Pertemuan | Pertemuan ke-6 |
| Topik Materi | Distributed File System |
| Sumber Materi | 06--distributed-filesystem (1).pdf |
| AI yang Digunakan | ChatGPT GPT-6 |
| Format Dokumen | Markdown (.md) |

### B. TUJUAN PEMBELAJARAN

Berdasarkan materi perkuliahan, tujuan pembelajaran pada pertemuan ini adalah:

1. Memahami dan mampu menjelaskan pengertian dari *file system*.

2. Mampu menyebutkan berbagai jenis *file system*.

3. Mampu menjelaskan cara kerja *file system* secara umum.

4. Memahami dan mampu menjelaskan pengertian *distributed file system* (DFS).

5. Mampu menyebutkan berbagai jenis DFS.

6. Mampu menjelaskan cara kerja DFS secara umum.

7. Mampu melakukan instalasi salah satu DFS sehingga mampu memahami cara kerjanya.

8. Mampu memahami dan menjelaskan *cloud storage* serta hubungannya dengan DFS.

9. Mampu melakukan instalasi salah satu *object storage* sebagai *cloud storage*.

### C. RANGKUMAN MATERI

#### 1. Pengertian File System

**File system** (sering ditulis *file system*, *filesystem*, atau disingkat **FS** / **fs**) merupakan metode yang digunakan sistem operasi untuk mengelola dan mengatur *file* pada media penyimpan (seperti *harddisk*, USB *flashdisk*, SSD, dan lainnya). Suatu FS dapat diakses melalui *driver file system* yang dikelola oleh *kernel* dengan menyediakan *virtual file system* untuk diakses oleh aplikasi di *user space*.

Materi juga menegaskan bahwa FS berbeda dengan **hierarki FS**: hierarki pada FS merupakan pengaturan *files* dan *dirs* pada suatu OS (seperti standar *Filesystem Hierarchy Standard* / FHS pada sistem bertipe UNIX, misalnya struktur direktori `/bin`, `/boot`, `/dev`, `/etc`, `/home`, `/lib`, `/proc`, `/root`, `/run`, `/srv`, `/sys`, `/tmp`, `/usr`, `/var`), di mana pengguna hanya melihat hierarki FS tanpa mempedulikan FS yang mendasarinya.

Beberapa contoh FS berdasarkan sistem operasi yang disebutkan dalam materi meliputi:

* **Linux:** `ext4`, `XFS`, `btrfs`, `ReiserFS`, dan lainnya.

* **DOS/Windows:** `FAT 16`, `FAT 32`, `NTFS`, dan lainnya.

* **Mac:** `APFS` (*Apple File System*), dan lainnya.

`[MODIFIKASI]` Memisahkan antara implementasi sistem berkas di balik layar dan struktur direktori yang tampak bagi pengguna memungkinkan aplikasi maupun pengguna bekerja melalui antarmuka yang seragam.

#### 2. Cara Kerja File System secara Umum

Pada arsitektur sistem operasi seperti Linux, interaksi antara aplikasi dan media penyimpanan melalui alur dari **Aplikasi (*User Space / Applications*)** (seperti *system utilities*, *shell/CLI*, dan *GUI applications*) $\rightarrow$ **System Call Interface** (seperti `read()`, `write()`) $\rightarrow$ **Virtual FS / File Systems** (di *Kernel Space*, berinteraksi dengan *process management*, *memory management* / MMU, *inter-process communication* / IPC, dan *network stack* / TCP/IP) $\rightarrow$ **Device Drivers** (*storage*, *network*, *input/output*) $\rightarrow$ **Hardware** (seperti CPU, RAM, *disk storage*, dan *network interface*).

`[MODIFIKASI]` Alur berlapis dari *user space* melalui *system call* hingga *kernel* dan *device driver* menjaga isolasi sekaligus mengatur akses ke perangkat keras penyimpanan secara aman.

#### 3. Pengertian Distributed File System (DFS) dan Perbedaannya dengan Penyimpanan Lain

**Distributed File System (DFS)** bukan sekadar "FS yang tersebar di lebih dari 1 mesin", melainkan secara konseptual merupakan sistem abstraksi terkoordinasi dari sekumpulan media penyimpan yang menutupi heterogenitas, kegagalan, dan konkurensi, sehingga menghasilkan jaringan penyimpanan yang terintegrasi, andal, dan berkinerja tinggi. Komponen media penyimpan pada DFS terdiri dari lebih dari satu media penyimpan, tetapi terlihat dari sisi pengguna sebagai satu media penyimpan.

Materi membedakan beberapa pendekatan penyimpanan terkait DFS:

* **DFS:** abstraksi level *software* yang mengelola data ke dalam *file* serta direktori yang dapat didistribusikan ke banyak *node*, dan lebih mengarah pada **DAS (*Direct-Attached Storage*)** di setiap *node*.

* **DAS:** penyimpanan yang terhubung langsung ke mesin/server (seperti perangkat penyimpanan lokal yang terlihat melalui perintah `df -h`).

* **NAS (*Network-Attached Storage*):** *shared storage over shared network*, berbasis *file system*, dengan pengelolaan yang relatif lebih mudah.

* **SAN (*Storage Area Network*):** *shared storage over dedicated network*, berupa *block storage* yang cepat namun mahal, menyajikan penyimpanan sebagai sekumpulan *block level devices* yang dapat dihubungkan langsung oleh server dan diformat dengan FS sendiri (secara konseptual bisa dipakai sebagai *storage* DFS meski tidak disarankan, dan umum digunakan untuk *backend* basis data besar, *video-audio editing*, atau virtualisasi besar).

`[MODIFIKASI]` Memahami perbedaan antara DFS, DAS, NAS, dan SAN membantu menentukan arsitektur penyimpanan yang sesuai dengan kebutuhan skalabilitas, biaya, dan pola akses data.

#### 4. Berbagai DFS yang Umum dan Cara Kerjanya

Contoh berbagai DFS yang umum dalam materi meliputi:

* **Google File System (GFS)** dan **Colossus** (pengganti GFS, digunakan antara lain pada YouTube, Gmail, dan Google Docs).

* **CephFS** (`https://ceph.io/en/`).

* **Gluster** (`https://www.gluster.org/`).

* **HDFS (*Hadoop DFS*)** (`https://hadoop.apache.org/`).

* **Lustre** (`https://www.lustre.org/`).

Secara umum, DFS menyatukan berbagai *namespace* dan lokasi penyimpanan (seperti *data center* dengan NAS 1 dan NAS 2, *remote location* dengan Linux NFS dan Windows SMB, serta *public cloud*) ke dalam satu **Global Namespace** bagi pengguna dan aplikasi yang mengakses data.

`[MODIFIKASI]` Penyajian *global namespace* menyembunyikan kompleksitas distribusi data lintas lokasi dan teknologi penyimpanan di bawah satu tampilan terpadu.

#### 5. Studi Kasus: HDFS (*Hadoop Distributed File System*)

**HDFS** adalah suatu FS yang bersifat *open source*, *scalable*, terdistribusi, dan *fault-tolerant* yang dirancang untuk mengelola dan menyimpan *datasets* besar di seluruh klaster *commodity hardware* (perangkat keras komputer yang diproduksi secara massal, murah, mudah dipertukarkan, dan tersedia luas dari berbagai vendor). HDFS merupakan komponen utama Apache Hadoop yang membagi *file* menjadi blok-blok, mendistribusikannya ke beberapa server, dan mereplikasinya untuk mencapai *high-availability*.

Dalam arsitektur HDFS terdapat **NameNode** (mengelola *metadata* seperti nama dan replika, misalnya `/home/foo/data, 3, ...`, menangani *metadata ops* dari *client* serta *block ops*) dan **DataNodes** di berbagai *rack* (seperti *Rack 1* dan *Rack 2*) yang menyimpan *blocks* serta melakukan replikasi data, berdampingan dengan komponen klaster Hadoop seperti *Resource Manager* (pada *master*), *Node Manager*, dan *MapReduce* (pada *slave*).

Untuk praktik penggunaan HDFS (seperti pada dokumen `menggunakan-hadoop-hdfs--linux.pdf`), disyaratkan antara lain JDK versi 17 dan/atau 21 (JDK 17 untuk kompilasi dan server; JDK 17 atau 21 untuk *client*), Apache Hadoop versi 3.5.0, `pdsh`, `ssh`, serta layanan `sshd` yang aktif (`sudo dinitctl start sshd` pada Artix Linux + dinit atau `sudo systemctl start ssh` pada systemd).

`[MODIFIKASI]` Pemisahan pengelolaan *metadata* pada *NameNode* dan penyimpanan blok replikasi pada *DataNode* memungkinkan skala penyimpanan besar dibangun dari *commodity hardware* dengan ketahanan terhadap kegagalan *node*.

#### 6. Pengertian Cloud Storage, Relasinya dengan DFS, dan Tipe Cloud Storage

**Cloud storage** adalah layanan *online* yang memungkinkan pengguna menyimpan dan mengakses data di server jarak jauh melalui internet (bukan di *hard drive* lokal atau perangkat fisik), dikelola secara *remote* dalam suatu *pool* (*logical*) pada penyimpanan fisik multi-server/multi-lokasi yang umumnya dimiliki dan dikelola oleh penyedia *cloud computing*. Contohnya meliputi Amazon S3, Azure Blob Storage, dan GCS (*Google Cloud Storage*).

Relasi *cloud storage* dengan DFS terletak pada pembagian peran: *cloud storage* menjadi tempat penyimpanan data, sedangkan pengorganisasiannya dapat dilakukan oleh DFS. Misalnya, S3 dapat digunakan oleh HDFS sebagai penyimpanan sementara HDFS menjalankan operasi FS, yang dapat diatur melalui konfigurasi pada `core-site.xml` (`fs.s3a.access.key`, `fs.s3a.secret.key`, dan `fs.s3a.endpoint`).

Materi juga menguraikan tiga tipe penyimpanan utama (*Storage Types*) terkait *cloud storage*:

| Aspek | Block Storage | File Storage | Object Storage |
|---|---|---|---|
| **Transport** | FC atau iSCSI | TCP/IP | TCP/IP |
| **Interface** | *Direct Attached* atau SAN | NFS, SMB | HTTP, REST |
| **Use Case** | Latensi rendah, terbaik untuk data terstruktur | Performa baik, *file sharing*, *global file locking* | Skalabilitas mudah tanpa batas, dapat diakses lintas LAN & WAN |

`[MODIFIKASI]` Menggabungkan *cloud storage* dengan DFS atau memilih tipe penyimpanan yang tepat memungkinkan pemisahan antara kapasitas/antarmuka penyimpanan dan pengelolaan operasi berkas.

#### 7. Studi Kasus Cloud Storage dan Sistem Penyimpanan Terdistribusi

Materi menampilkan beberapa contoh sistem dan proyek penyimpanan terdistribusi/*cloud storage*, antara lain:

* **Ceph** (`https://ceph.com/en/`): sistem penyimpanan terdistribusi *open-source* yang andal dan *scalable*.

* **CubeFS** (`https://cubefs.io`): sistem penyimpanan *open-source* generasi baru *cloud-native* untuk data tak terstruktur yang mendukung protokol akses S3, HDFS, dan POSIX, serta memiliki arsitektur terpisah antara *Master*, *Metadata Subsystem* (*Meta Partition* in-memory pada *Meta Node*), *Data Subsystem* (*Data Partition* pada *Data Node* serta *Erasure Code Stripe* pada *Blob Node*), *Object Subsystem* (*Object Node*), *Volume*, dan antarmuka *Client* (POSIX/HDFS *interface* maupun AWS S3 SDK).

* **RustFS** (`rustfs.com`): alternatif penyimpanan objek yang diposisikan untuk menggantikan MinIO & S3 dengan fokus pada *throughput* tinggi dan *built for multi-cloud storage*.

* **PGSTY SILO** (`silo.pgsty.com`): *open-source S3/MinIO-compatible object storage* (fork MinIO yang dikelola PGSTY) dengan antarmuka S3 API (`:9000`), Console (`:9001`), dan *erasure set* pada *distributed disks*.

* **Rook** (`https://rook.io`): manajemen penyimpanan *cloud-native* *open-source* untuk Kubernetes (mengelola *File*, *Block*, dan *Object Storage*).

`[MODIFIKASI]` Ekosistem penyimpanan terdistribusi dan *object storage* modern semakin banyak menyediakan kompatibilitas S3/POSIX/HDFS serta dukungan *cloud-native* untuk kebutuhan *big data*, AI/LLM, dan *container*.

### D. CONTOH PENERAPAN DAN ANALISIS

Berdasarkan materi perkuliahan, terdapat beberapa contoh penerapan dan analisis arsitektur penyimpanan terdistribusi serta *cloud storage*.

#### 1. Arsitektur HDFS dengan NameNode dan DataNodes Lintas Rack

**Konsep yang digunakan:**

*Distributed File System*, pemisahan *metadata* dan blok data, serta replikasi blok pada klaster *commodity hardware*.

**Cara kerja:**

*Client* melakukan operasi *metadata* ke *NameNode* dan operasi blok baca/tulis langsung ke *DataNodes* di berbagai *rack* (*Rack 1* dan *Rack 2*), sementara blok-blok data direplikasi antar *DataNode* sesuai konfigurasi replika.

`[MODIFIKASI]` Dengan mengarahkan transfer blok data langsung antara *client* dan *DataNode*, *NameNode* tidak dibebani aliran isi *file* yang besar sehingga skalabilitas klaster dapat terjaga.

**Alasan penggunaan:**

Mengelola *datasets* berukuran besar secara *scalable* dan *fault-tolerant* menggunakan perangkat keras komoditas.

**Hubungan dengan materi pertemuan:**

Contoh ini menjadi studi kasus utama cara kerja DFS dalam materi.

#### 2. Integrasi HDFS dengan Amazon S3 melalui `core-site.xml`

**Konsep yang digunakan:**

Relasi *cloud storage* sebagai tempat penyimpanan data dan DFS sebagai pengelola operasi *file system*.

**Cara kerja:**

HDFS dikonfigurasi pada `core-site.xml` dengan properti `fs.s3a.access.key`, `fs.s3a.secret.key`, dan `fs.s3a.endpoint` agar dapat berinteraksi dengan *endpoint* S3.

`[MODIFIKASI]` Pendekatan ini memungkinkan alur kerja berbasis HDFS memanfaatkan layanan penyimpanan objek di *cloud* tanpa harus mengubah cara operasi FS dikelola.

**Alasan penggunaan:**

Memadukan pengelolaan operasi FS ala DFS dengan layanan penyimpanan jarak jauh berbasis *cloud*.

**Hubungan dengan materi pertemuan:**

Contoh ini memperjelas hubungan praktis antara *cloud storage* dan DFS pada materi.

#### 3. Arsitektur Multi-Subsistem pada CubeFS

**Konsep yang digunakan:**

Sistem penyimpanan *cloud-native* dengan pemisahan subsistem *metadata*, *data*, dan *object* serta dukungan multi-protokol (S3, HDFS, POSIX).

**Cara kerja:**

Komponen *Master* berkoordinasi dengan *Metadata Subsystem* (*Meta Node* / *Meta Partition* in-memory), *Data Subsystem* (*Data Node* / *Data Partition* dan *Blob Node* / *Erasure Code Stripe*), *Object Subsystem* (*Object Node*), serta *Volume* untuk melayani *client* (kontainer, VM, server, maupun aplikasi dengan AWS S3 SDK).

`[MODIFIKASI]` Pemisahan subsistem *metadata*, *data*, dan *object* serta dukungan *erasure code stripe* memberi fleksibilitas protokol akses dan efisiensi ruang penyimpanan.

**Alasan penggunaan:**

Mendukung penyimpanan data tak terstruktur untuk *big data*, AI/LLM, platform *container*, dan pemisahan *storage* serta *compute*.

**Hubungan dengan materi pertemuan:**

Contoh ini menggambarkan evolusi sistem penyimpanan terdistribusi *cloud-native* yang mendukung berbagai antarmuka akses.

#### 4. Perbandingan Tipe Penyimpanan (*Block*, *File*, dan *Object Storage*)

Materi membandingkan tiga tipe penyimpanan berdasarkan protokol transport, antarmuka, dan skenario penggunaannya.

| Aspek | Block Storage | File Storage | Object Storage |
|---|---|---|---|
| Protokol transport | FC atau iSCSI | TCP/IP | TCP/IP |
| Antarmuka akses | *Direct Attached* atau SAN | NFS, SMB | HTTP, REST |
| Karakteristik & penggunaan | Latensi rendah, cocok untuk data terstruktur | Performa baik, *file sharing*, *global file locking* | Mudah di-scale tanpa batas, dapat diakses lintas LAN & WAN |

`[MODIFIKASI]` Pemilihan antara *block*, *file*, atau *object storage* bergantung pada apakah beban kerja menuntut latensi blok rendah, struktur direktori/penguncian berkas bersama, atau skalabilitas objek lintas jaringan.

### E. PENGGUNAAN AI

### 1. AI yang Digunakan

- Nama AI: ChatGPT GPT-6.
- Tujuan penggunaan: Membantu memahami, menyusun, dan mengembangkan rangkuman materi perkuliahan.
- Sumber utama: Materi perkuliahan yang diberikan oleh dosen dalam bentuk PDF.
- Bentuk penggunaan: Membantu mengidentifikasi pokok bahasan, menyusun penjelasan, dan mengembangkan contoh penerapan berdasarkan materi.

### 2. Prompt yang Digunakan

Berikut prompt yang digunakan untuk menghasilkan rangkuman awal:

> Saya merupakan mahasiswa S1 Informatika yang sedang mengerjakan tugas rangkuman mata kuliah Teori Sistem Terdistribusi dan Terdesentralisasi pertemuan ke-6. Baca dan pelajari seluruh isi PDF yang saya lampirkan dengan teliti, kemudian buat rangkuman berdasarkan materi tersebut.
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
> Bahas file system, cara kerja file system, distributed file system, perbedaan DAS, DFS, NAS, dan SAN, berbagai contoh DFS, HDFS, cloud storage, hubungan cloud storage dengan DFS, serta tipe-tipe cloud storage.
>
> Sertakan contoh penerapan dan analisis yang relevan dengan bidang Informatika. Jangan mengarang informasi, kode program, hasil pengujian, atau detail implementasi yang tidak tersedia dalam sumber. Jika materi hanya menyebutkan nama teknologi atau mengarahkan ke dokumen praktik yang tidak dilampirkan, jelaskan keterbatasan tersebut.
>
> Buat hasil akhir dalam format Markdown yang siap disimpan sebagai README.md di GitHub. Berikan tanda **[MODIFIKASI]** pada bagian yang mendapatkan pengembangan penjelasan atau tambahan contoh dari hasil awal AI.

### 3. Bagian yang Disesuaikan dari Keluaran AI

Bagian dari hasil AI yang dikembangkan atau disesuaikan meliputi:

1. **File System dan Alur Kerjanya**: Penjelasan mengenai hubungan aplikasi, system call interface, VFS, driver kernel, dan media penyimpanan dikembangkan agar alur akses file lebih mudah dipahami.
2. **Distributed File System**: Penjelasan mengenai abstraksi penyimpanan, distribusi data pada beberapa node, serta perbedaan DFS dengan penyimpanan lainnya dikembangkan untuk memperjelas konsep.
3. **HDFS dan Cloud Storage**: Penjelasan mengenai pembagian file menjadi blok, replikasi data, serta hubungan HDFS dengan layanan cloud storage dikembangkan dengan contoh penerapan.
4. **Tipe Cloud Storage dan Analisis**: Penjelasan mengenai object storage, file storage, dan block storage dikembangkan agar perbedaan cara penyimpanan dan penggunaannya lebih mudah dipahami.

Penyesuaian dilakukan untuk memperjelas pemahaman materi, mengembangkan penjelasan yang masih singkat pada slide, serta menambahkan contoh penerapan yang relevan dengan bidang Informatika.

### F. KESIMPULAN

Berdasarkan materi Pertemuan 6, *file system* merupakan metode sistem operasi untuk mengelola berkas pada media penyimpanan melalui *system call*, *virtual file system*, dan *device driver*—yang perlu dibedakan dari hierarki FS yang dilihat pengguna. Sementara itu, *distributed file system* (DFS) menyediakan abstraksi terkoordinasi atas banyak media penyimpan menjadi satu *global namespace* yang andal, *scalable*, serta menutupi heterogenitas, kegagalan, dan konkurensi, berbeda dari karakteristik DAS, NAS, maupun SAN.

Melalui studi kasus HDFS dan integrasinya dengan *cloud storage* (seperti S3 melalui `core-site.xml`), serta pemahaman tipe *block*, *file*, dan *object storage* dan sistem seperti Ceph, CubeFS, RustFS, PGSTY SILO, dan Rook, dapat terlihat bagaimana penyimpanan terdistribusi dan *cloud storage* saling melengkapi untuk kebutuhan data skala besar dan *cloud-native*.

### G. DAFTAR REFERENSI

1. Bambang Purnomosidi D. P. (Tanpa tahun). *Distributed File System*. Materi perkuliahan Teori Sistem Terdistribusi dan Terdesentralisasi (Kode: FIF25002T, 3 SKS), Program Studi Informatika, Fakultas Teknologi Informasi, Universitas Teknologi Digital Indonesia. File: `06--distributed-filesystem (1).pdf`.

**Sumber ilustrasi, dokumentasi, dan referensi yang dicantumkan dalam materi:**

* FreeDesktop / X.Org Foundation. *Filesystem Hierarchy Standard (Version 3.0)*. https://specifications.freedesktop.org/fhs/latest/

* Thomas-Krenn. *Linux Storage Stack Diagram*. https://www.thomas-krenn.com/en/wiki/Linux_Storage_Stack_Diagram

* Tekmart / TechTarget. *NAS vs. SAN Storage*. https://tekmart.co.za/t-blog/key-differences-between-san-and-nas-storage-systems/

* Apache Hadoop. *HDFS Architecture & Releases*. https://hadoop.apache.org/ dan https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html

* VMblog. *Five Traits to Look for in a Distributed File System*. https://vmblog.com/archive/2020/11/25/five-traits-to-look-for-in-a-distributed-file-system.aspx

* GeeksforGeeks. *Hadoop HDFS*. https://www.geeksforgeeks.org/data-engineering/hadoop-hdfs-hadoop-distributed-file-system/

* Databricks. *Hadoop Distributed File System (HDFS)*. https://www.databricks.com/glossary/hadoop-distributed-file-system-hdfs

* Cloudian. *Storage Types (Block, File, Object Storage)*. https://cloudian.com/guides/object-storage/object-storage-care/

* Ceph. https://ceph.com/en/

* CubeFS. https://cubefs.io/ dan https://cubefs.io/docs/master/overview/architecture.html

* RustFS. https://rustfs.com/

* PGSTY SILO. https://silo.pgsty.com/

* Rook. https://rook.io/

---

### INFORMASI DOKUMENTASI GITHUB

* **Repository:** https://github.com/ciaxzs/disdec-teori

* **Direktori:** `06/`

* **File:** `README.md`
