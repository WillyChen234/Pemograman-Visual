# Pertemuan 6: Database (PostgreSQL, Supabase, dan Npgsql)

**Pemateri:** Shata Diyaul Haq  
**Mata Kuliah:** Pemrograman Visual  

---

## 1. Pengantar Database
- **Pengertian:** Kumpulan data terstruktur yang disimpan secara terorganisir agar dapat diakses, dikelola, dan dimanipulasi oleh aplikasi.
- **Peran dalam Aplikasi:** Menyimpan informasi penting secara persisten (permanen), memungkinkan aplikasi untuk menyajikan, mengubah, serta menjaga konsistensi dan integritas data.

---

## 2. PostgreSQL (Postgres)
- **Definisi:** Sistem manajemen basis data relasional objek (*Object-Relational Database Management System* / ORDBMS) kelas atas yang bersifat sumber terbuka (*open-source*).
- **Karakteristik:** Menggunakan dan memperluas standar bahasa SQL untuk menyimpan, mengelola, dan mengambil data secara aman, handal, dan efisien.

---

## 3. Supabase (Backend-as-a-Service / BaaS)
- **Definisi:** Platform *Backend-as-a-Service* (BaaS) modern yang membungkus database PostgreSQL menjadi solusi cloud siap pakai.
- **Analogi:**
  - Jika **PostgreSQL** adalah "mesin" utamanya,
  - Maka **Supabase** adalah "pabrik" lengkap dengan panel kendali (*Dashboard*, API, *Auth*, dan *Storage*) sehingga pengembang dapat langsung membangun aplikasi tanpa harus merancang dan memelihara infrastruktur server dari nol.

---

## 4. Npgsql (Data Provider ADO.NET untuk PostgreSQL)
- **Definisi:** *Data provider* ADO.NET sumber terbuka (*open-source*) yang berfungsi sebagai **jembatan penghubung utama** antara aplikasi berbasis .NET (seperti VB.NET, C#, atau F#) dengan database PostgreSQL.

---

## 5. Komponen Utama Npgsql dalam ADO.NET

### A. `NpgsqlConnection`
- **Fungsi:** Membuat, membuka, memelihara, dan mengelola jalur koneksi fisik (sesi koneksi) antara aplikasi .NET dengan database PostgreSQL / Supabase.
- Digunakan untuk memastikan koneksi ke server berhasil sebelum menjalankan perintah SQL.

### B. `NpgsqlCommand`
- **Fungsi:** Mendefinisikan dan mengeksekusi kueri teks SQL (seperti perintah `SELECT`, `INSERT`, `UPDATE`, `DELETE`) maupun *stored procedure* terhadap database melalui jalur koneksi yang sudah terbuka.

### C. `NpgsqlDataAdapter`
- **Fungsi:** Perantara jembatan yang bertugas:
  1. Mengambil kumpulan data dari database PostgreSQL untuk dimuat ke dalam memori aplikasi (ke dalam objek `DataTable` atau `DataSet`).
  2. Mengirimkan kembali perubahan data dari memori aplikasi kembali ke database fisik.

### D. `NpgsqlCommandBuilder`
- **Fungsi:** Utilitas yang membuat perintah SQL `INSERT`, `UPDATE`, dan `DELETE` secara otomatis untuk `NpgsqlDataAdapter` berdasarkan kueri `SELECT` yang digunakan.
- **Keunggulan:** Membebaskan pengembang dari keharusan menulis kueri modifikasi data secara manual satu per satu.

---

## 6. Manipulasi Data CRUD dengan Npgsql
Konsep dasar pengelolaan data terintegrasi:
- **Create (C):** Menyimpan data baru ke tabel database (`INSERT INTO ...`).
- **Read (R):** Mengambil data dari database dan menampilkannya ke antarmuka (misal `DataGridView`) melalui `SELECT`.
- **Update (U):** Memperbarui data yang ada di database (`UPDATE ... SET ... WHERE ...`).
- **Delete (D):** Menghapus data dari tabel database (`DELETE FROM ... WHERE ...`).
