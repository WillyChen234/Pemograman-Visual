# Pertemuan 8: DataGridView, Array & Koleksi Data

**Pemateri:** Shata Diyaul Haq  
**Mata Kuliah:** Pemrograman Visual  

---

## 1. Mengenal DataGridView
- **DataGridView (prefix: `dgv`)** adalah komponen visual (grup *Data* di Toolbox) untuk menampilkan dan mengelola data dalam format baris dan kolom menyerupai lembar kerja Excel.
- Digunakan untuk menggantikan `ListBox` ketika data memiliki banyak atribut/kolom agar rapi, sejajar, mudah dibaca, serta dapat diurutkan.
- **Akses Elemen Sel:**
  ```vb
  dgvMahasiswa.Rows(1).Cells(2).Value ' Baris indeks 1, Kolom indeks 2 (dimulai dari 0)
  ```

---

## 2. Dua Pendekatan Mengisi DataGridView

### A. Cara 1: Manual (*Unbound*)
- Kolom dibuat secara manual di Designer atau kode.
- Data dimasukkan per baris menggunakan:
  ```vb
  dgvMahasiswa.Rows.Add("231712001", "Andi", "Informatika")
  ```
- **Cocok untuk:** Data sederhana, sedikit, dan bersifat statis.

### B. Cara 2: DataSource (*Bound*)
- Grid dihubungkan langsung ke objek sumber data (`List(Of T)` atau `DataTable`).
- Kolom dapat terbentuk secara otomatis berdasarkan properti objek/kolom tabel.
- **Pola Arsitektur:**
  $$\text{Sumber Data (List / DataTable)} \longrightarrow \text{BindingSource} \longrightarrow \text{DataGridView}$$

> **PERINGATAN PENTING:**  
> Jangan mencampur kedua cara! Jika grid sudah menggunakan `DataSource`, memanggil `Rows.Add()` akan memicu error `InvalidOperationException`.

---

## 3. Pola Modern: Satu Baris = Satu Objek (Class + List)
Daripada menggunakan Array 2 Dimensi yang terbatas pada tipe data String saja dan berisiko salah indeks, gunakan pendekatan Berorientasi Objek (*OOP*):

```vb
Public Class Mahasiswa
    Public Property Nim As String
    Public Property Nama As String
    Public Property Jurusan As String
    Public Property Angkatan As Integer
    Public Property Ipk As Decimal
End Class
```
- Setiap instance `New Mahasiswa(...)` merepresentasikan **1 baris data**.
- Setiap `Public Property` otomatis menjadi **1 kolom data** pada grid.

---

## 4. Peran BindingSource (Perantara Data)
- **BindingSource (prefix: `bs`)** bertindak sebagai perantara (*broker*) antara sumber data asli dengan `DataGridView`.
- **Analogi Perpustakaan:** Rak buku adalah sumber data (tetap utuh). Petugas meja layanan adalah `BindingSource` yang mengatur buku apa yang diambil, difilter, atau diurutkan untuk pengunjung (grid).
- **Sinkronisasi Data:** Menambah data dilakukan melalui `bsMahasiswa.Add(baru)` agar tampilan grid langsung otomatis terperbarui. Jika terlanjur menggunakan `daftar.Add`, panggil `bsMahasiswa.ResetBindings(False)`.

---

## 5. Perbandingan Sumber Data

| Aspek | Array 2D | List(Of T) + Class | DataTable |
| :--- | :--- | :--- | :--- |
| **Ukuran** | Tetap (*Fixed*) | Dinamis | Dinamis |
| **Tipe Data per Kolom** | Satu tipe (semua String) | Sesuai tipe `Property` | Sesuai tipe kolom |
| **Pengisian Grid** | `Rows.Add` (manual loop) | `DataSource` | `DataSource` |
| **Kolom Grid** | Dibuat sendiri | Terbentuk otomatis | Terbentuk otomatis |
| **Sorting Header** | Diurutkan sebagai teks (`"10"` sebelum `"9"`) | Tidak otomatis | Ya, otomatis sesuai tipe |
| **BindingSource.Filter** | Tidak mendukung | Tidak mendukung (diabaikan) | Didukung penuh |
| **Penggunaan Terbaik** | Data kecil dan tetap | Logika bisnis diolah di kode | Membutuhkan fitur filter & sort cepat |

---

## 6. Merapikan Format Kolom
Pengaturan kolom otomatis dilakukan via kode **setelah** `DataSource` terisi:
```vb
Private Sub AturKolom()
    dgvMahasiswa.Columns("Nim").HeaderText = "NIM"
    dgvMahasiswa.Columns("Ipk").HeaderText = "IPK"
    dgvMahasiswa.Columns("Ipk").DefaultCellStyle.Format = "N2" ' Tampil 3.80 bukan 3.8
    dgvMahasiswa.Columns("Ipk").DefaultCellStyle.Alignment = DataGridViewContentAlignment.MiddleRight
    dgvMahasiswa.Columns("Nama").FillWeight = 200
    dgvMahasiswa.AutoSizeColumnsMode = DataGridViewAutoSizeColumnsMode.Fill
End Sub
```

---

## 7. Pencarian Data

### Cara A: Menggunakan `BindingSource.Filter` (Khusus DataTable)
Memanfaatkan ekspresi pencarian langsung di memori:
```vb
bsMahasiswa.Filter = "Nama LIKE '%" & kata & "%' OR Nim LIKE '%" & kata & "%'"
```

### Cara B: Menggunakan Perulangan `For Each` (Untuk `List(Of T)`)
Menyaring data yang cocok ke dalam `List` baru, lalu mengikat ulang `DataSource`:
```vb
Dim hasil As New List(Of Mahasiswa)
For Each mhs As Mahasiswa In daftarMahasiswa
    If mhs.Nama.ToLower().Contains(kata) OrElse mhs.Nim.Contains(kata) Then
        hasil.Add(mhs)
    End If
Next
bsMahasiswa.DataSource = hasil
```

---

## 8. Kesalahan Umum yang Wajib Dihindari
1. Memanggil `Rows.Add()` pada grid yang sudah diikat ke `DataSource` $\rightarrow$ `InvalidOperationException`.
2. Mengatur properti kolom `Columns("...")` sebelum `DataSource` dihubungkan $\rightarrow$ `NullReferenceException`.
3. Membiarkan `AllowUserToAddRows = True` sehingga baris kosong paling bawah ikut terhitung ke dalam total data.
4. Memasukkan `List(Of String)` sebagai `DataSource`, yang menyebabkan grid hanya menampilkan kolom `Length`.
