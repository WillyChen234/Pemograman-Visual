# Pertemuan 2: Komponen Visual

**Pemateri:** Shata Diyaul Haq  
**Mata Kuliah:** Pemrograman Visual  

---

## 1. Mengenal Control dalam Visual Studio
**Control** adalah elemen antarmuka pengguna (*User Interface* / UI) yang digunakan untuk membangun aplikasi di Visual Studio. Control memungkinkan pengguna berinteraksi dengan aplikasi melalui berbagai bentuk input (masukan) dan output (keluaran).

Seluruh komponen ini dapat ditemukan pada jendela **Toolbox** (misal kelompok *Common Controls*, *Containers*, *Menus & Toolbars*, dsb).

---

## 2. Komponen Dasar Form & Fungsinya

### A. Form
- **Fungsi:** Jendela atau wadah utama (*container*) tempat meletakkan seluruh komponen visual.
- **Peran:** Sebagai area kerja utama bagi pengguna untuk berinteraksi dengan aplikasi.

### B. Button (Command Button)
- **Fungsi:** Tombol perintah untuk menjalankan suatu aksi atau instruksi tertentu saat diklik oleh pengguna.
- **Contoh Penggunaan:** Tombol `Simpan`, `Batal`, `Keluar`, `Hitung`, dsb.

### C. Label
- **Fungsi:** Menampilkan teks statis sebagai keterangan atau informasi di atas form.
- **Peran:** Menjelaskan fungsi dari kontrol lain di sampingnya (misalnya label "Nama Mahasiswa" di samping sebuah TextBox).

### D. TextBox
- **Fungsi:** Kotak input teks yang memungkinkan pengguna memasukkan, mengedit, atau melihat data.

---

## 3. Properti Penting dalam Form & Komponen

| Properti | Fungsi |
| :--- | :--- |
| **Name** | Identitas unik kontrol yang digunakan dalam kode program untuk pemanggilan objek. |
| **Text** | Teks yang ditampilkan dan terlihat secara visual oleh pengguna pada komponen. |
| **StartPosition** | Menentukan posisi awal form saat program pertama kali dijalankan (khusus Form, misal: `CenterScreen`). |
| **BackColor** | Mengatur warna latar belakang komponen atau form. |
| **ForeColor** | Mengatur warna tulisan/teks pada komponen. |
| **Font** | Mengatur jenis font, ukuran, ketebalan, dan gaya tulisan. |
| **Enabled** | Menentukan apakah kontrol aktif dan dapat menerima interaksi pengguna (`True`/`False`). |
| **Visible** | Menentukan apakah kontrol ditampilkan atau disembunyikan dari layar (`True`/`False`). |

---

## 4. Konsep Event
- **Event** adalah peristiwa atau kejadian yang terjadi pada suatu komponen yang dapat memicu jalannya baris kode tertentu.
- Event dipicu oleh interaksi pengguna (seperti klik mouse, penekanan tombol keyboard) atau perubahan status internal aplikasi.
- **Contoh Event:** `btnSimpan_Click` (berjalan saat tombol simpan diklik pengguna).
