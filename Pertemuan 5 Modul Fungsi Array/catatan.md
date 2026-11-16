# Pertemuan 5: Modul, Fungsi, Array, dan Koleksi Data

**Pemateri:** Shata Diyaul Haq  
**Mata Kuliah:** Pemrograman Visual  

---

## 1. Modul (Module)
- **Pengertian:** Bagian dari program yang digunakan untuk mengelompokkan kode berdasarkan fungsi atau kebutuhan tertentu.
- **Tujuan:** Memisahkan kode logika dan pemrosesan dari kode tampilan (*Form*), sehingga struktur kode lebih rapi, terorganisir, dan mudah dikelola (*maintainable*).

---

## 2. Access Modifier (Hak Akses)
Pengaturan yang menentukan tingkat aksesibilitas suatu anggota program (variabel, fungsi, atau prosedur):

1. **`Public`**: Dapat diakses oleh form atau modul lain di dalam satu proyek.
   ```vb
   Public nilai As Integer = 80
   ```
2. **`Private`**: Hanya dapat diakses dari dalam modul atau form tempat anggota tersebut dideklarasikan.
   ```vb
   Private hasil As Integer = 100
   ```

---

## 3. Procedure (Sub) vs Function

### A. Procedure (`Sub`)
- Sekumpulan instruksi yang dibuat untuk menjalankan tugas tertentu ketika dipanggil.
- **Tidak mengembalikan nilai** ke pemanggilnya.
```vb
Public Sub TampilkanPesan()
    MessageBox.Show("Halo dari Procedure!")
End Sub
```

### B. Function (`Function`)
- Blok kode yang memproses data dan **mengembalikan suatu nilai hasil** (`Return`).
- Cocok digunakan jika hasil perhitungan/pemrosesan perlu diolah lebih lanjut oleh bagian program lain.
```vb
Public Function HitungLuas(panjang As Integer, lebar As Integer) As Integer
    Return panjang * lebar
End Function
```

---

## 4. Array (Larik)
Struktur data untuk menyimpan sekumpulan nilai dengan tipe data yang sama dalam satu variabel. Pada VB.NET, indeks array selalu dimulai dari **0**.

### A. Array Satu Dimensi
- Menyimpan data secara linier dalam satu baris. Pengaksesan elemen cukup membutuhkan satu indeks.
```vb
Dim nilai() As Integer = {10, 20, 30, 40, 50}
Console.WriteLine(nilai(2)) ' Menghasilkan 30
```

### B. Array Multi-Dimensi (2 Dimensi atau Lebih)
- Membentuk struktur seperti matriks (baris dan kolom) atau ruang 3D.
- Seluruh baris wajib memiliki jumlah kolom yang sama.
```vb
Dim data(,) As Integer = {
    {10, 20, 30},
    {40, 50, 60},
    {70, 80, 90}
}
Console.WriteLine(data(1, 2)) ' Baris indeks 1, kolom indeks 2 -> 60
```

---

## 5. Koleksi Data (Collection)
Struktur data dinamis untuk menyimpan dan memanipulasi sekumpulan objek atau nilai (menambah, menghapus, mencari, dan mengiterasi).

### Perbandingan Jenis-Jenis Koleksi Data:

| Jenis Koleksi | Sifat Ukuran | Tipe Data | Cara Akses | Karakteristik Utama | Contoh Deklarasi |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Array** | Tetap (*Fixed*) | Seragam | Melalui indeks numerik (mulai dari 0) | Ukuran tidak bisa berubah dinamis. Menambah ukuran memerlukan `ReDim Preserve`. | `Dim nilai() As Integer = {10, 20}` |
| **List(Of T)** | Dinamis | Seragam | Melalui indeks numerik | Mendukung operasi `Add()`, `Remove()`, dan `Count`. Sangat fleksibel. | `Dim angka As New List(Of Integer)` |
| **Dictionary(Of K, V)** | Dinamis | Pasangan Key & Value | Melalui *Key* | Setiap *Key* wajib unik. Sangat cepat untuk pencarian data berdasarkan label/identitas. | `Dim mhs As New Dictionary(Of String, String)` |
| **HashSet(Of T) / Set** | Dinamis | Seragam | Iterasi (tidak ada indeks) | Menjamin semua nilai unik, otomatis menolak data duplikat. | `Dim angka As New HashSet(Of Integer)` |
