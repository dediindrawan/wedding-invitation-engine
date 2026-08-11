# Business Entities

Business entity merupakan representasi dari data atau objek utama yang dibutuhkan oleh Wedding Invitation Engine.

Setiap entity memiliki tanggung jawab dan informasi tertentu yang digunakan untuk membangun fitur serta tampilan pada wedding invitation.

Business entities pada Wedding Invitation Engine meliputi:

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

## 4.1 Couple

### Description

Entity Couple merepresentasikan pasangan pengantin yang menjadi tokoh utama dalam wedding invitation.

Entity ini menyimpan informasi mengenai mempelai wanita (Bride) dan mempelai pria (Groom) yang akan digunakan pada berbagai section di dalam website, seperti Cover, Hero, Couple, dan Footer.

### Purpose

Entity Couple digunakan untuk:

- Menampilkan identitas kedua mempelai.
- Menampilkan foto kedua mempelai.
- Menampilkan informasi orang tua masing-masing mempelai.
- Menampilkan informasi tambahan seperti Instagram dan urutan anak.
- Menjadi sumber data utama untuk section yang berkaitan dengan pasangan pengantin.

### Structure

```
Couple
├── Bride
└── Groom
```

**Bride**

Bride menyimpan seluruh informasi mengenai mempelai wanita.

| Attribute   | Type   | Required | Description                                          |
| ----------- | ------ | :------: | ---------------------------------------------------- |
| Full Name   | String |   Yes    | Nama lengkap mempelai wanita.                        |
| Nickname    | String |    No    | Nama panggilan mempelai wanita.                      |
| Photo       | Image  |   Yes    | Foto utama mempelai wanita.                          |
| Parents     | Object |   Yes    | Informasi orang tua mempelai wanita.                 |
| Instagram   | String |    No    | Username atau URL Instagram.                         |
| Child Order | String |    No    | Urutan anak dalam keluarga, misalnya "Anak Pertama". |

**Parents**

Parents menyimpan informasi mengenai orang tua mempelai wanita.

| Attribute | Type   | Required | Description                |
| --------- | ------ | :------: | -------------------------- |
| Father    | String |   Yes    | Nama ayah mempelai wanita. |
| Mother    | String |   Yes    | Nama ibu mempelai wanita.  |

**Notes:**

- Minimal harus memiliki Full Name dan Photo.
- Instagram bersifat opsional dan hanya ditampilkan apabila tersedia.
- Child Order digunakan apabila informasi urutan anak ingin ditampilkan.
- Parents dikelompokkan sebagai object karena terdiri dari Father dan Mother.

**Groom**

Groom menyimpan seluruh informasi mengenai mempelai pria.

| Attribute   | Type   | Required | Description                                          |
| ----------- | ------ | :------: | ---------------------------------------------------- |
| Full Name   | String |   Yes    | Nama lengkap mempelai pria.                          |
| Nickname    | String |    No    | Nama panggilan mempelai pria.                        |
| Photo       | Image  |   Yes    | Foto utama mempelai pria.                            |
| Parents     | Object |   Yes    | Informasi orang tua mempelai pria.                   |
| Instagram   | String |    No    | Username atau URL Instagram.                         |
| Child Order | String |    No    | Urutan anak dalam keluarga, misalnya "Anak Pertama". |

**Parents**

Parents menyimpan informasi mengenai orang tua mempelai pria.

| Attribute | Type   | Required | Description              |
| --------- | ------ | :------: | ------------------------ |
| Father    | String |   Yes    | Nama ayah mempelai pria. |
| Mother    | String |   Yes    | Nama ibu mempelai pria.  |

**Notes:**

- Minimal harus memiliki Full Name dan Photo.
- Instagram bersifat opsional dan hanya ditampilkan apabila tersedia.
- Child Order digunakan apabila informasi urutan anak ingin ditampilkan.
- Struktur data Groom dibuat sama dengan Bride agar memudahkan pengembangan dan pemeliharaan aplikasi.

### Relationship

```
Couple
├── Bride
│ └── Parents
└── Groom
└── Parents
```

**Struktur Lengkap Relationship**

```
Couple
├── Bride
│ ├── Full Name
│ ├── Nickname
│ ├── Photo
│ ├── Parents
│ │ ├── Father
│ │ └── Mother
│ ├── Instagram
│ └── Child Order
│
└── Groom
├── Full Name
├── Nickname
├── Photo
├── Parents
│ ├── Father
│ └── Mother
├── Instagram
└── Child Order
```

### Data Usage

Entity Couple akan digunakan oleh beberapa section berikut:

- Cover — Menampilkan nama kedua mempelai.
- Hero — Menampilkan nama dan foto kedua mempelai.
- Couple — Menampilkan informasi lengkap kedua mempelai.
- Footer — Menampilkan nama kedua mempelai.

## 4.2 Event

### Description

Entity Event merepresentasikan setiap acara yang terdapat dalam sebuah wedding.

Satu wedding dapat memiliki satu atau lebih event, seperti Akad Nikah, Resepsi, Pemberkatan, Sangjit, Ngunduh Mantu, atau acara lainnya.

Penggunaan collection pada Event membuat Wedding Invitation Engine lebih fleksibel karena setiap wedding dapat memiliki jumlah dan jenis acara yang berbeda tanpa mengubah struktur utama aplikasi.

### Purpose

Entity Event digunakan untuk:

- Menampilkan informasi acara.
- Menampilkan tanggal dan waktu pelaksanaan acara.
- Menampilkan lokasi acara.
- Menampilkan alamat acara.
- Memberikan akses menuju lokasi melalui Google Maps.
- Menampilkan informasi tambahan seperti dress code atau keterangan acara.

### Structure

```
Events
├── Event
├── Event
└── Event
```

**Contoh:**

```
Events
├── Akad Nikah
├── Resepsi
└── Ngunduh Mantu
```

**Event**

Satu Event merepresentasikan satu acara dalam rangkaian wedding.

| Attribute       | Type   | Required | Description                                       |
| --------------- | ------ | :------: | ------------------------------------------------- |
| Title           | String |   Yes    | Nama acara, misalnya "Akad Nikah" atau "Resepsi". |
| Date            | Date   |   Yes    | Tanggal pelaksanaan acara.                        |
| Start Time      | Time   |   Yes    | Waktu mulai acara.                                |
| End Time        | Time   |    No    | Waktu selesai acara.                              |
| Time Zone       | String |    No    | Zona waktu acara, misalnya WIB, WITA, atau WIT.   |
| Venue Name      | String |   Yes    | Nama gedung atau tempat pelaksanaan acara.        |
| Address         | Text   |   Yes    | Alamat lengkap lokasi acara.                      |
| Google Maps URL | URL    |    No    | URL menuju lokasi acara di Google Maps.           |
| Description     | Text   |    No    | Informasi tambahan mengenai acara.                |
| Dress Code      | String |    No    | Dress code yang berlaku untuk acara.              |

**Notes:**

- Minimal sebuah Event harus memiliki Title, Date, Start Time, Venue Name, dan Address.
- End Time bersifat opsional karena tidak semua client memiliki informasi waktu selesai acara.
- Google Maps URL bersifat opsional, tetapi disarankan untuk memudahkan tamu menemukan lokasi.
- Description digunakan untuk informasi tambahan mengenai acara.
- Dress Code hanya ditampilkan apabila informasi tersedia.
- Satu wedding dapat memiliki satu atau lebih Event.
- Struktur Event tidak membatasi jenis acara sehingga dapat digunakan untuk berbagai adat dan konsep pernikahan.

### Relationship

```
Wedding
└── Events
├── Event
├── Event
└── Event
```

**Contoh:**

```
Wedding
└── Events
├── Akad Nikah
└── Resepsi
```

### Data Usage

Entity Event dapat digunakan oleh beberapa section berikut:

- Hero — Menampilkan informasi tanggal acara atau tanggal pernikahan.
- Countdown — Menggunakan tanggal dan waktu event sebagai target countdown.
- Event — Menampilkan detail seluruh acara.
- Maps — Menggunakan Google Maps URL untuk mengarahkan tamu ke lokasi acara.

## 4.3 Gallery

### Description

Entity Gallery merepresentasikan kumpulan media berupa gambar dan video yang digunakan untuk menampilkan dokumentasi serta berbagai momen pernikahan pada website wedding invitation.

Gallery dapat berisi satu atau lebih media yang ditampilkan pada berbagai section di dalam website. Setiap media dalam Gallery direpresentasikan sebagai Media Item.

Dengan menggunakan collection, jumlah dan jenis media dapat disesuaikan dengan kebutuhan masing-masing client tanpa mengubah struktur utama Wedding Invitation Engine.

### Purpose

Entity Gallery digunakan untuk:

- Menampilkan kumpulan foto dan video pernikahan.
- Mendukung visual storytelling untuk meningkatkan pengalaman pengguna.
- Menyimpan informasi setiap media yang ditampilkan.
- Mengatur urutan tampilan media.
- Mendukung penggunaan berbagai jenis media dalam satu wedding invitation.
- Menjadi sumber data untuk section Gallery dan section lain yang membutuhkan media.

### Structure

```
Gallery
├── Media Item
├── Media Item
└── Media Item
```

Setiap Media Item dapat berupa gambar atau video.

**Contoh:**

```
Gallery
├── Image
├── Image
├── Video
├── Image
└── Video
```

**Media Item**

Media Item merepresentasikan satu aset media yang menjadi bagian dari sebuah Gallery.

Media Item dapat berupa gambar maupun video. Jenis media ditentukan oleh attribute Type, sedangkan lokasi asset ditentukan oleh attribute Source.

| Attribute   | Type   | Required | Description                                         |
| ----------- | ------ | :------: | --------------------------------------------------- |
| Type        | Enum   |   Yes    | Jenis media yang digunakan, yaitu Image atau Video. |
| Source      | URL    |   Yes    | Lokasi atau URL asset media yang akan ditampilkan.  |
| Title       | String |    No    | Judul atau nama media.                              |
| Description | Text   |    No    | Deskripsi atau keterangan tambahan mengenai media.  |
| Order       | Number |   Yes    | Menentukan urutan media saat ditampilkan.           |

**Notes:**

- Gallery dapat memiliki satu atau lebih Media Item.
- Setiap Media Item wajib memiliki Type dan Source.
- Type untuk V1 dibatasi menjadi Image atau Video.
- Title dan Description bersifat opsional dan hanya digunakan apabila diperlukan oleh desain atau client.
- Order digunakan untuk menentukan urutan media saat ditampilkan.
- Media dapat ditampilkan dalam berbagai layout tanpa mengubah struktur data utama.
- Asset media dapat menggunakan URL atau sistem storage yang digunakan oleh aplikasi.
- Ukuran dan format file media perlu diperhatikan untuk menjaga performa website.
- Video perlu mempertimbangkan ukuran file dan metode penyimpanan atau
  penyajian agar tidak memberikan beban berlebihan terhadap website.
- Gallery V1 difokuskan pada kebutuhan utama wedding invitation dan belum
  mencakup fitur album, kategori media, atau pengelolaan media yang kompleks.

### Relationship

```
Wedding
└── Gallery
├── Media Item
├── Media Item
└── Media Item
```

**Struktur Lengkap Relationship**

```
Gallery
│
├── Media Item
│ ├── Type: Image
│ ├── Source: photo-01.jpg
│ └── Order: 1
│
├── Media Item
│ ├── Type: Image
│ ├── Source: photo-02.jpg
│ └── Order: 2
│
└── Media Item
├── Type: Video
├── Source: prewedding.mp4
└── Order: 3
```

### Data Usage

Entity Gallery akan digunakan pada beberapa section berikut:

- Gallery — Menampilkan kumpulan foto dan video pernikahan.
- Hero — Dapat menggunakan media tertentu sebagai visual utama apabila diperlukan oleh desain.
- Story — Dapat menggunakan media sebagai bagian dari dokumentasi perjalanan pasangan.

## 4.4 Story

### Description

Entity Story merepresentasikan rangkaian cerita atau perjalanan hubungan pasangan yang ditampilkan pada website wedding invitation.

Story digunakan untuk menyampaikan momen-momen penting dalam perjalanan pasangan, mulai dari pertama kali bertemu, menjalin hubungan, lamaran, hingga pernikahan.

Setiap cerita dalam Story direpresentasikan sebagai Story Item.

### Purpose

Entity Story digunakan untuk:

- Menampilkan perjalanan hubungan pasangan.
- Menampilkan berbagai momen penting dalam hubungan.
- Menyampaikan cerita pernikahan secara kronologis.
- Memberikan pengalaman yang lebih personal dan emosional kepada tamu.
- Menjadi sumber data untuk section Story atau Timeline pada website.

### Structure

```
Story
├── Story Item
├── Story Item
└── Story Item
```

**Story Item**

Story Item merepresentasikan satu momen atau peristiwa penting dalam perjalanan hubungan pasangan.

| Attribute   | Type   | Required | Description                                    |
| ----------- | ------ | :------: | ---------------------------------------------- |
| Title       | String |   Yes    | Judul atau nama momen.                         |
| Date        | Date   |    No    | Tanggal terjadinya momen.                      |
| Description | Text   |   Yes    | Cerita atau informasi mengenai momen tersebut. |
| Image       | Image  |    No    | Foto yang digunakan untuk mendukung cerita.    |
| Order       | Number |   Yes    | Menentukan urutan cerita saat ditampilkan.     |

**Notes**

- Story dapat memiliki satu atau lebih Story Item.
- Title digunakan sebagai identitas utama setiap momen.
- Date bersifat opsional karena tidak semua cerita memiliki tanggal yang pasti.
- Description digunakan untuk menjelaskan cerita atau momen secara lebih detail.
- Image bersifat opsional dan hanya digunakan apabila client memiliki foto yang relevan.
- Order digunakan untuk menentukan urutan cerita pada timeline atau layout Story.
- Story Item dapat ditampilkan dalam bentuk timeline, carousel, atau layout lainnya tanpa mengubah struktur data utama.
- Story pada V1 difokuskan pada perjalanan hubungan pasangan dan belum mencakup fitur storytelling yang kompleks.

### Relationship

```
Wedding
└── Story
├── Story Item
├── Story Item
└── Story Item
```

**Struktur Lengkap Relationship**

```
Story
└── Story Item
├── Title
├── Date
├── Description
├── Image
└── Order
```

### Data Usage

Entity Story akan digunakan pada beberapa section berikut:

- Story / Timeline — Menampilkan perjalanan hubungan pasangan.
- Couple — Dapat digunakan sebagai informasi pendukung mengenai perjalanan pasangan.
- Gallery — Image pada Story Item dapat menggunakan media yang berkaitan dengan momen tertentu.

## 4.5 Gift

### Description

Entity Gift merepresentasikan informasi yang digunakan oleh pasangan untuk menerima hadiah atau tanda kasih dari tamu undangan secara digital.

Gift dapat digunakan untuk menampilkan informasi rekening bank, e-wallet, maupun informasi lain yang berkaitan dengan pengiriman hadiah kepada pasangan.

Setiap informasi hadiah direpresentasikan sebagai Gift Item.

### Purpose

Entity Gift digunakan untuk:

- Menampilkan informasi rekening atau metode penerimaan hadiah.
- Memudahkan tamu dalam memberikan hadiah secara digital.
- Menampilkan informasi tambahan mengenai pengiriman hadiah apabila diperlukan.
- Menjadi sumber data untuk section Gift atau Wedding Gift pada website.

### Structure

```
Gift
├── Gift Item
├── Gift Item
└── Gift Item
```

**Gift Item**

Gift Item merepresentasikan satu metode atau informasi penerimaan hadiah
yang dapat digunakan oleh tamu.

| Attribute      | Type   | Required | Description                                               |
| -------------- | ------ | :------: | --------------------------------------------------------- |
| Type           | Enum   |   Yes    | Jenis metode hadiah, misalnya Bank Account atau E-Wallet. |
| Provider       | String |   Yes    | Nama bank, e-wallet, atau penyedia layanan.               |
| Account Name   | String |   Yes    | Nama pemilik rekening atau akun.                          |
| Account Number | String |   Yes    | Nomor rekening, nomor akun, atau identifier penerima.     |
| Logo           | Image  |    No    | Logo bank atau provider yang digunakan.                   |
| Description    | Text   |    No    | Informasi tambahan mengenai metode hadiah.                |
| Order          | Number |   Yes    | Menentukan urutan Gift Item saat ditampilkan.             |

**Notes**

- Gift dapat memiliki satu atau lebih Gift Item.
- Type digunakan untuk menentukan jenis metode penerimaan hadiah.
- Provider digunakan untuk mengidentifikasi bank atau penyedia layanan.
- Account Name dan Account Number merupakan informasi utama yang digunakan untuk transfer hadiah digital.
- Logo bersifat opsional dan hanya digunakan apabila diperlukan oleh desain.
- Description dapat digunakan untuk memberikan instruksi tambahan kepada tamu.
- Order digunakan untuk menentukan urutan Gift Item saat ditampilkan.
- Informasi Gift bersifat opsional karena tidak semua pasangan ingin menerima hadiah secara digital.
- Informasi sensitif seperti nomor rekening harus ditampilkan sesuai dengan konfigurasi dan kebutuhan client.
- Gift pada V1 difokuskan pada penyajian informasi penerimaan hadiah dan belum mencakup proses pembayaran atau transaksi secara langsung.

### Relationship

```
Wedding
└── Gift
├── Gift Item
├── Gift Item
└── Gift Item
```

**Struktur Lengkap Relationship**

```
Gift
└── Gift Item
├── Type
├── Provider
├── Account Name
├── Account Number
├── Logo
├── Description
└── Order
```

### Data Usage

Entity Gift akan digunakan pada section berikut:

- Gift / Wedding Gift — Menampilkan metode dan informasi penerimaan hadiah.
- Footer — Dapat menampilkan informasi singkat mengenai gift apabila diperlukan.

## 4.6 Guest

### Description

Entity Guest merepresentasikan data penerima undangan yang digunakan untuk mengidentifikasi dan mempersonalisasi undangan pernikahan.

Setiap Guest mewakili satu penerima atau satu kelompok penerima undangan yang dapat diberikan akses ke wedding invitation secara personal.

Data Guest dapat digunakan untuk menampilkan nama penerima pada halaman undangan, seperti "Kepada Dedi", serta mendukung fitur tambahan seperti RSVP dan pencatatan kehadiran tamu.

### Purpose

Entity Guest digunakan untuk:

- Menyimpan daftar penerima undangan.
- Menampilkan nama penerima secara personal pada undangan.
- Mengidentifikasi setiap penerima undangan.
- Mendukung personalisasi URL atau akses undangan.
- Menyimpan status RSVP apabila fitur tersebut digunakan.
- Menyimpan informasi jumlah tamu yang akan hadir.
- Menjadi sumber data untuk fitur guest management pada Wedding Invitation Engine.

### Structure

```
Guests
├── Guest
├── Guest
└── Guest
```

**Guest**

Guest merepresentasikan satu penerima atau satu kelompok penerima undangan.

| Attribute   | Type   | Required | Description                                                                     |
| ----------- | ------ | :------: | ------------------------------------------------------------------------------- |
| Name        | String |   Yes    | Nama penerima undangan yang akan ditampilkan pada invitation.                   |
| Slug        | String |   Yes    | Identifier yang digunakan untuk membentuk URL atau akses personal.              |
| Phone       | String |    No    | Nomor telepon penerima, apabila diperlukan untuk kebutuhan pengiriman undangan. |
| Group       | String |    No    | Kelompok atau kategori tamu, misalnya Family, Friend, atau Colleague.           |
| Guest Count | Number |    No    | Jumlah tamu yang diwakili oleh satu Guest.                                      |
| RSVP Status | Enum   |    No    | Status konfirmasi kehadiran tamu.                                               |
| Message     | String |    No    | Catatan internal mengenai Guest.                                                |

**Notes**

- Setiap Guest minimal harus memiliki Name dan Slug.
- Name digunakan untuk menampilkan personalisasi nama penerima pada invitation.
- Slug digunakan sebagai identifier untuk membedakan satu Guest dengan Guest lainnya.
- Phone bersifat opsional dan hanya digunakan apabila sistem membutuhkan informasi kontak untuk proses pengiriman undangan.
- Group dapat digunakan untuk mengelompokkan tamu berdasarkan hubungan dengan pasangan.
- Guest Count digunakan apabila satu undangan ditujukan kepada lebih dari satu orang.
- RSVP Status digunakan apabila fitur RSVP diaktifkan.
- Message merupakan catatan internal dan tidak ditampilkan kepada tamu.
- Satu Guest dapat mewakili satu orang maupun satu kelompok penerima undangan.
- Data Guest harus memiliki identifier yang unik agar setiap undangan personal dapat dibedakan.
- Guest pada V1 difokuskan pada personalisasi undangan dan kebutuhan dasar pengelolaan tamu. Fitur guest management yang lebih kompleks dapat dikembangkan pada versi berikutnya.

### Relationship

```
Wedding
└── Guests
└── Guest
├── Name
├── Slug
├── Phone
├── Group
├── Guest Count
├── RSVP Status
└── Message
```

**Struktur Lengkap Relationship**

```
Guests
├── Guest
│ ├── Name: Dedi
│ └── Slug: dedi
│
├── Guest
│ ├── Name: Budi
│ └── Slug: budi
│
└── Guest
├── Name: Keluarga Pak Andi
└── Slug: keluarga-pak-andi
```

### Data Usage

Entity Guest akan digunakan pada beberapa bagian berikut:

- Cover — Menampilkan nama penerima, misalnya "Kepada Dedi".
- Invitation Access — Mengidentifikasi undangan berdasarkan identifier atau slug.
- RSVP — Menyimpan status konfirmasi kehadiran tamu.
- Guest Management — Mengelola daftar penerima undangan.
- Wishes — Dapat menghubungkan ucapan dengan Guest yang mengirimkannya.

## 4.7 Wishes

### Description

Entity Wishes merepresentasikan kumpulan ucapan, doa, dan pesan yang dikirimkan oleh tamu kepada pasangan melalui website wedding invitation.

Setiap ucapan yang dikirim oleh tamu direpresentasikan sebagai Wish Item.

Wishes dapat terhubung dengan Entity Guest sehingga setiap ucapan dapat dikaitkan dengan penerima undangan yang mengirimkannya.

### Purpose

Entity Wishes digunakan untuk:

- Menyediakan media bagi tamu untuk mengirimkan ucapan dan doa.
- Menampilkan kumpulan ucapan dari tamu.
- Menghubungkan ucapan dengan Guest yang mengirimkannya.
- Menyimpan waktu ketika ucapan dikirim.
- Mendukung moderasi ucapan apabila diperlukan.
- Menjadi sumber data untuk section Wishes pada website.

### Structure

```
Wishes
├── Wish Item
├── Wish Item
└── Wish Item
```

**Wish Item**

Wish Item merepresentasikan satu ucapan atau pesan yang dikirimkan oleh seorang tamu kepada pasangan.

| Attribute  | Type     | Required | Description                                                |
| ---------- | -------- | :------: | ---------------------------------------------------------- |
| Guest      | Relation |   Yes    | Guest yang mengirimkan ucapan.                             |
| Message    | Text     |   Yes    | Isi ucapan atau doa yang dikirimkan oleh tamu.             |
| Created At | DateTime |   Yes    | Waktu ketika ucapan dibuat atau dikirim.                   |
| Status     | Enum     |   Yes    | Status ucapan, misalnya Pending, Published, atau Rejected. |

**Notes**

- Setiap Wish Item harus memiliki Message.
- Wish Item dapat terhubung dengan satu Guest.
- Created At digunakan untuk mengetahui waktu ucapan dikirim.
- Status digunakan untuk mengatur apakah ucapan dapat ditampilkan pada website.
- Ucapan dengan status Published dapat ditampilkan pada section Wishes.
- Ucapan dengan status Pending dapat menunggu proses moderasi sebelum ditampilkan.
- Ucapan dengan status Rejected tidak ditampilkan kepada pengunjung.
- Moderasi dapat digunakan untuk mencegah spam atau konten yang tidak sesuai.
- Wishes pada V1 difokuskan pada pengiriman dan penampilan ucapan sederhana.
- Fitur seperti reaction, reply, notification, atau threaded discussion belum menjadi bagian dari V1.

### Relationship

```
Wedding
└── Wishes
└── Wish Item
├── Guest
├── Message
├── Created At
└── Status

Guest
└── Wishes
└── Wish Item
```

**Struktur Lengkap Relationship**

```
├── Wishes
│ └── Wish Item
│ ├── Guest
│ ├── Message
│ ├── Created At
│ └── Status
```

### Data Usage

Entity Wishes akan digunakan pada beberapa bagian berikut:

- Wishes — Menampilkan kumpulan ucapan dan doa dari tamu.
- Guest — Mengidentifikasi tamu yang mengirimkan ucapan.
- RSVP — Dapat digunakan bersama informasi Guest apabila diperlukan.

## 4.8 Theme

### Description

Entity Theme merepresentasikan konfigurasi visual yang digunakan untuk menentukan tampilan dan identitas visual sebuah wedding invitation.

Theme memungkinkan setiap wedding memiliki tampilan yang berbeda tanpa perlu mengubah source code utama aplikasi.

Theme dapat menentukan elemen visual seperti warna, typography, style, dan konfigurasi tampilan lainnya yang digunakan oleh berbagai section di dalam website.

### Purpose

Entity Theme digunakan untuk:

- Menentukan identitas visual sebuah wedding invitation.
- Mengatur warna utama dan warna pendukung website.
- Menentukan typography yang digunakan.
- Menentukan gaya visual dari berbagai komponen.
- Memungkinkan penggunaan beberapa tema pada Wedding Invitation Engine.
- Memisahkan konfigurasi visual dari source code utama.
- Memungkinkan client memiliki tampilan yang berbeda tanpa mengubah logic aplikasi.

### Structure

```
Theme
└── Theme Configuration
```

**Theme Configuration**

Theme Configuration merepresentasikan konfigurasi visual yang digunakan untuk menentukan tampilan sebuah wedding invitation.

| Attribute        | Type   | Required | Description                                                          |
| ---------------- | ------ | :------: | -------------------------------------------------------------------- |
| Name             | String |   Yes    | Nama atau identifier dari theme.                                     |
| Primary Color    | String |   Yes    | Warna utama yang digunakan pada website.                             |
| Secondary Color  | String |    No    | Warna pendukung yang digunakan pada elemen tertentu.                 |
| Background Color | String |    No    | Warna dasar background website atau section.                         |
| Text Color       | String |    No    | Warna utama teks.                                                    |
| Heading Font     | String |    No    | Font yang digunakan untuk heading.                                   |
| Body Font        | String |    No    | Font yang digunakan untuk body text.                                 |
| Style            | Enum   |    No    | Gaya visual utama, misalnya Elegant, Romantic, Minimal, atau Modern. |

**Notes**

- Setiap Wedding menggunakan satu Theme Configuration sebagai konfigurasi visual utama.
- Name digunakan untuk mengidentifikasi theme.
- Warna dan typography dapat digunakan oleh berbagai section pada website.
- Secondary Color, Background Color, dan Text Color bersifat opsional dan dapat menggunakan nilai default apabila tidak tersedia.
- Heading Font dan Body Font digunakan untuk membedakan typography berdasarkan kebutuhan desain.
- Style digunakan sebagai identifier konsep visual dan bukan sebagai penentu langsung seluruh tampilan UI.
- Theme tidak menyimpan struktur layout atau business logic.
- Theme hanya bertanggung jawab terhadap konfigurasi visual.
- Theme pada V1 difokuskan pada konfigurasi visual dasar dan belum mencakup sistem theme builder atau visual editor.
- Struktur Theme harus memungkinkan penambahan konfigurasi visual baru tanpa mengubah struktur utama Wedding.

### Relationship

```
Wedding
└── Theme
└── Theme Configuration
```

**Struktur Lengkap Relationship**

```
Wedding
└── Theme
└── Theme Configuration
├── Name: Romantic Rose
├── Primary Color: ...
├── Heading Font: ...
└── Body Font: ...
```

### Data Usage

Entity Theme akan digunakan pada berbagai bagian website:

- Global Layout — Menentukan konfigurasi visual utama website.
- Typography — Menentukan font heading dan body.
- Color System — Menentukan warna utama, pendukung, background, dan teks.
- Component Styling — Menjadi sumber konfigurasi visual untuk berbagai komponen dan section.
- UI Sections — Setiap section dapat menggunakan konfigurasi Theme sesuai kebutuhan desain.

## 4.9 Music

### Description

Entity Music merepresentasikan konfigurasi musik yang digunakan sebagai background audio pada website wedding invitation.

Music digunakan untuk memberikan pengalaman yang lebih emosional dan personal kepada pengunjung selama membuka undangan.

Setiap Wedding dapat memiliki satu konfigurasi Music yang menentukan audio yang digunakan serta bagaimana audio tersebut dijalankan pada website.

### Purpose

Entity Music digunakan untuk:

- Menentukan musik background yang digunakan pada wedding invitation.
- Menyimpan informasi mengenai audio yang digunakan.
- Mengatur apakah musik aktif atau tidak.
- Mengatur perilaku pemutaran musik.
- Memberikan pengalaman yang lebih immersive dan emosional kepada tamu.
- Memisahkan konfigurasi musik dari source code utama.

### Structure

```
Music
└── Music Configuration
```

**Music Configuration**

Music Configuration merepresentasikan konfigurasi audio yang digunakan oleh sebuah wedding invitation.

| Attribute | Type    | Required | Description                                                                       |
| --------- | ------- | :------: | --------------------------------------------------------------------------------- |
| Title     | String  |    No    | Judul atau nama musik yang digunakan.                                             |
| Source    | URL     |   Yes    | Lokasi atau URL file audio yang digunakan.                                        |
| Enabled   | Boolean |   Yes    | Menentukan apakah musik diaktifkan pada invitation.                               |
| Autoplay  | Boolean |    No    | Menentukan apakah musik mencoba diputar secara otomatis ketika invitation dibuka. |
| Loop      | Boolean |    No    | Menentukan apakah musik diputar berulang setelah selesai.                         |
| Volume    | Number  |    No    | Menentukan tingkat volume default musik.                                          |

**Notes**

- Setiap Wedding dapat memiliki satu Music Configuration.
- Source merupakan field wajib apabila Music diaktifkan.
- Enabled digunakan untuk mengaktifkan atau menonaktifkan musik tanpa menghapus konfigurasi yang sudah dibuat.
- Autoplay digunakan sebagai konfigurasi perilaku pemutaran musik.
- Loop dapat digunakan agar musik terus diputar selama pengunjung berada di dalam invitation.
- Volume bersifat opsional dan dapat menggunakan nilai default apabila tidak tersedia.
- Implementasi autoplay perlu mempertimbangkan kebijakan browser karena browser dapat membatasi pemutaran audio otomatis sebelum adanya interaksi pengguna.
- Music pada V1 difokuskan pada background music sederhana dan belum mencakup playlist atau multiple audio tracks.

### Relationship

```
Wedding
└── Music
└── Music Configuration
```

**Struktur Lengkap Relationship**

```
Theme
└── Theme Configuration

Music
└── Music Configuration
```

### Data Usage

Entity Music akan digunakan pada beberapa bagian berikut:

- Invitation Opening — Menentukan perilaku musik ketika invitation dibuka.
- Global Layout — Menjalankan background music selama pengunjung berada di dalam invitation.
- Music Control — Menyediakan kontrol play, pause, atau mute apabila diperlukan oleh UI.

## 4.10 Config

### Description

Entity Config merepresentasikan konfigurasi umum yang menentukan perilaku dan fitur sebuah wedding invitation.

Config digunakan untuk mengatur bagaimana invitation berfungsi tanpa perlu mengubah source code utama aplikasi.

Berbeda dengan Theme yang bertanggung jawab terhadap tampilan visual dan Music yang bertanggung jawab terhadap audio, Config digunakan untuk mengatur pengaturan umum dan fitur yang tersedia pada sebuah wedding invitation.

### Purpose

Entity Config digunakan untuk:

- Mengatur konfigurasi umum wedding invitation.
- Mengaktifkan atau menonaktifkan fitur tertentu.
- Mengatur section yang ditampilkan pada invitation.
- Menentukan perilaku umum website.
- Memungkinkan setiap wedding memiliki konfigurasi yang berbeda tanpa mengubah source code utama.
- Menjadi pusat konfigurasi untuk fitur yang tidak termasuk ke dalam entity lain.

### Structure

```
Config
└── Configuration
```

**Configuration**

Configuration merepresentasikan kumpulan pengaturan umum yang digunakan oleh sebuah wedding invitation.

| Attribute        | Type    | Required | Description                                           |
| ---------------- | ------- | :------: | ----------------------------------------------------- |
| Invitation Title | String  |    No    | Judul atau title utama invitation.                    |
| Is Published     | Boolean |   Yes    | Menentukan apakah invitation dapat diakses oleh tamu. |
| Show Gallery     | Boolean |   Yes    | Menentukan apakah section Gallery ditampilkan.        |
| Show Story       | Boolean |   Yes    | Menentukan apakah section Story ditampilkan.          |
| Show Gift        | Boolean |   Yes    | Menentukan apakah section Gift ditampilkan.           |
| Show Wishes      | Boolean |   Yes    | Menentukan apakah section Wishes ditampilkan.         |
| Show RSVP        | Boolean |   Yes    | Menentukan apakah fitur RSVP diaktifkan.              |
| Show Music       | Boolean |   Yes    | Menentukan apakah fitur Music digunakan.              |

**Notes**

- Setiap Wedding memiliki satu Configuration.
- Configuration digunakan untuk mengatur perilaku dan fitur invitation.
- Is Published digunakan untuk menentukan apakah invitation sudah dapat diakses oleh tamu.
- Pengaturan Show digunakan untuk mengaktifkan atau menonaktifkan section tertentu tanpa mengubah source code.
- Section yang dinonaktifkan tidak perlu ditampilkan pada UI.
- Nilai default dapat digunakan apabila konfigurasi tertentu tidak tersedia.
- Config tidak digunakan untuk menyimpan konfigurasi visual seperti warna dan typography karena hal tersebut menjadi tanggung jawab Theme.
- Config tidak digunakan untuk menyimpan konfigurasi audio karena hal tersebut menjadi tanggung jawab Music.
- Config pada V1 difokuskan pada pengaturan umum dan feature visibility. Pengaturan yang lebih kompleks dapat ditambahkan pada versi berikutnya.

### Relationship

```
Wedding
└── Config
└── Configuration
```

**Struktur Lengkap Relationship**

```
Wedding
│
├── CONTENT
│ ├── Couple
│ ├── Event
│ ├── Gallery
│ ├── Story
│ └── Gift
│
├── INTERACTION
│ ├── Guest
│ └── Wishes
│
└── CONFIGURATION
├── Theme
├── Music
└── Config
```

### Data Usage

Entity Config akan digunakan pada beberapa bagian berikut:

- Application — Menentukan konfigurasi umum invitation.
- Section Rendering — Menentukan section yang ditampilkan atau disembunyikan.
- Invitation Access — Menentukan apakah invitation sudah dipublikasikan.
- Feature Control — Mengaktifkan atau menonaktifkan fitur tertentu.

## Folder Structure

```
Wedding
│
├── Couple ✅
│ ├── Bride
│ │ └── Parents
│ │ ├── Father
│ │ └── Mother
│ └── Groom
│ └── Parents
│ ├── Father
│ └── Mother
│
├── Event ✅
│ └── Event
│ ├── Title
│ ├── Date
│ ├── Start Time
│ ├── End Time
│ ├── Time Zone
│ ├── Venue Name
│ ├── Address
│ ├── Google Maps URL
│ ├── Description
│ └── Dress Code
│
├── Gallery ✅
│ └── Media Item
│ ├── Type
│ ├── Source
│ ├── Title
│ ├── Description
│ └── Order
│
├── Story ✅
│ └── Story Item
│ ├── Title
│ ├── Date
│ ├── Description
│ ├── Image
│ └── Order
│
├── Gift ✅
│ └── Gift Item
│ ├── Type
│ ├── Provider
│ ├── Account Name
│ ├── Account Number
│ ├── Logo
│ ├── Description
│ └── Order
│
├── Guest ✅
│ └── Guest Item
│ ├── Name
│ ├── Slug
│ ├── Phone
│ ├── Group
│ ├── Guest Count
│ ├── RSVP Status
│ └── Message
│
├── Wishes ✅
│ └── Wish Item
│ ├── Guest
│ ├── Message
│ ├── Created At
│ └── Status
│
├── Theme ✅
│ └── Theme Configuration
│ ├── Name
│ ├── Primary Color
│ ├── Secondary Color
│ ├── Background Color
│ ├── Text Color
│ ├── Heading Font
│ ├── Body Font
│ └── Style
│
├── Music ✅
│ └── Music Configuration
│ ├── Title
│ ├── Source
│ ├── Enabled
│ ├── Autoplay
│ ├── Loop
│ └── Volume
│
└── Config ✅
│ └── Configuration
│ ├── Invitation Title
│ ├── Is Published
│ ├── Show Gallery
│ ├── Show Story
│ ├── Show Gift
│ ├── Show Wishes
│ ├── Show RSVP
└ └── Show Music
```
