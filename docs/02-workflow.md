# 1. Business

Tahap pertama adalah memahami kebutuhan bisnis dari produk yang akan dibuat. Pada tahap ini fokusnya bukan pada teknologi atau coding, melainkan menjawab pertanyaan seperti:

- Apa tujuan website ini?
- Siapa target penggunanya?
- Fitur apa saja yang benar-benar dibutuhkan?
- Bagaimana website ini dapat digunakan kembali untuk client berikutnya?

Untuk Wedding Invitation Engine V1, tujuan utamanya adalah membangun satu aplikasi yang dapat digunakan berulang kali hanya dengan mengganti data, assets, dan konfigurasi tanpa mengubah source code utama.

# 2. Data

Setelah tujuan bisnis jelas, langkah berikutnya adalah menentukan data apa saja yang dibutuhkan oleh aplikasi. Pada tahap ini akan dibuat struktur data (data model) yang menjadi fondasi seluruh sistem. Contohnya:

- Couple
- Event
- Gallery
- Story
- Gift
- Guest
- Wishes
- Theme
- Music
- Config

Semua tampilan dan fitur nantinya akan mengambil informasi dari data tersebut.

# 3. Flow

Tahap ini mendesain bagaimana data mengalir di dalam aplikasi. Flow menjelaskan hubungan antar data, proses yang dilakukan pengguna, dan bagaimana aplikasi merespon setiap aksi pengguna. Contohnya:

- Pengunjung membuka undangan
- Pengunjung melihat informasi acara
- Pengunjung mengirim ucapan
- Data ucapan disimpan
- Daftar ucapan diperbarui

**User Flow**

Buka Undangan
↓
Buka Invitation
↓
Scroll
↓
Lihat Event
↓
Kirim Wishes

**Data Flow**

User
↓
Form
↓
Validation
↓
Supabase
↓
Database
↓
Fetch
↓
UI

Dengan flow yang jelas, proses implementasi akan lebih mudah dilakukan.

# 4. UI

Setelah data dan jalur aplikasi selesai dirancang, barulah dibuat tampilan antar muka pengguna. Pada tahap ini ditentukan:

- Struktur halaman
- Layout setiap section
- Komponen yang digunakan
- Warna
- Tipografi
- Animasi
- Responsif untuk berbagai layar

UI dirancang berdasarkan data yang sudah dibuat sebelumnya, sehingga setiap informasi memiliki tempat yang jelas untuk ditampilkan.

# 5. Code

Tahap terakhir adalah mengimplementasikan seluruh perencanaan ke dalam source code menggunakan teknologi yang telah dipilih. Proses coding bertugas menerjemahkan hasil analisis dan perancangan sebelumnya menjadi aplikasi yang dapat dijalankan. Karena kebutuhan utama dan struktur aplikasi telah dirancang sejak awal, proses development menjadi lebih terarah, mudah dipelihara, dan siap dikembangkan menjadi produk yang lebih besar di masa mendatang.

**Catatan:**

Prinsip utama Wedding Invitation Engine V1 adalah:

**Data First, UI Second, Code Last.**

Seluruh tampilan website dibangun berdasarkan data yang telah dirancang, sehingga aplikasi dapat digunakan kembali untuk banyak client tanpa perlu mengubah logika utama.
