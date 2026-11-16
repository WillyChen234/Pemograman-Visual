# Pertemuan 7: Validasi Input, Error Handling & Naming Convention

**Pemateri:** Shata Diyaul Haq  
**Mata Kuliah:** Pemrograman Visual  

---

## 1. Naming Convention Kontrol
Standar penamaan komponen antarmuka sangat penting untuk keterbacaan kode (*clean code*) dan menghindari kebingungan nama default bawaan Visual Studio (seperti `TextBox1`, `TextBox2`).

### Pola Penamaan:
$$\text{prefix (3 huruf kecil)} + \text{NamaFungsi (PascalCase)}$$
- Tanpa spasi dan tidak diawali angka.
- Diatur melalui properti **`(Name)`**, bukan properti `Text`.
- **Aturan penting:** Ubah nama kontrol **sebelum** melakukan *double-click* membuat event agar nama method tidak tertinggal default.

### Daftar Prefix Kontrol:
| Kontrol | Prefix | Contoh | Kontrol | Prefix | Contoh |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Form** | `frm` | `frmPendaftaran` | **CheckBox** | `chk` | `chkSetuju` |
| **Label** | `lbl` | `lblJudul` | **RadioButton** | `rdo` | `rdoLakiLaki` |
| **TextBox** | `txt` | `txtNama` | **GroupBox** | `grp` | `grpDataDiri` |
| **Button** | `btn` | `btnSimpan` | **DataGridView** | `dgv` | `dgvData` |
| **ComboBox** | `cbo` | `cboJurusan` | **DateTimePicker** | `dtp` | `dtpTanggalLahir` |
| **ListBox** | `lst` | `lstMahasiswa` | **ErrorProvider** | `err` | `errInput` |

---

## 2. Tiga Jenis Error dalam Pemrograman

1. **Syntax Error:** Kesalahan tata bahasa penulisan kode (ditandai garis bawah merah). Program tidak bisa di-compile sebelum diperbaiki.
2. **Runtime Error (Exception):** Terjadi saat program sedang berjalan, menyebabkan aplikasi *crash* jika tidak ditangani (contoh: konversi teks ke angka gagal, pembagian nol).
3. **Logic Error:** Program berjalan lancar tanpa pesan kesalahan, namun menghasilkan kalkulasi/output yang keliru (contoh: salah memasukkan rumus rata-rata).

> **Prinsip Utama:**  
> *"Cegah dengan validasi apa yang bisa dicegah. Tangkap dengan Try...Catch apa yang tidak bisa dicegah (operasi eksternal seperti file/database/jaringan)."*

---

## 3. Exception Handling (`Try...Catch...Finally`)

```vb
Try
    ' Blok kode yang berisiko memicu exception (misal: operasi I/O file)
Catch ex As IOException
    ' Tangkap error spesifik terlebih dahulu
Catch ex As Exception
    ' Tangkap error umum jika ada error tak terduga
Finally
    ' Selalu dijalankan dalam kondisi apapun (baik ada error maupun normal)
    ' Tempat bersih-bersih resource: menutup file, menutup koneksi database
    If penulis IsNot Nothing Then penulis.Close()
End Try
```

### Exception yang Sering Muncul:
- `FormatException`: Teks gagal dikonversi ke format angka (`Integer.Parse("abc")`).
- `InvalidCastException`: Kegagalan casting tipe data.
- `OverflowException`: Nilai angka melampaui batas tipe data.
- `DivideByZeroException`: Pembagian bilangan bulat dengan angka 0.
- `IndexOutOfRangeException`: Mengakses indeks array di luar batas.
- `NullReferenceException`: Objek bernilai `Nothing` (belum diinisialisasi `New`).
- `IOException`: Masalah pembacaan/penulisan file (file sedang terkunci, disk penuh, dsb).

---

## 4. Validasi Input: `TryParse` vs `Val` vs `CInt`

| Metode | Input `"abc"` | Input `"12abc"` | Input Desimal `"3,5"` | Keterangan |
| :--- | :--- | :--- | :--- | :--- |
| **`CInt(teks)`** | `InvalidCastException` | `InvalidCastException` | Berisiko error | Mematikan aplikasi jika tidak ditangkap `Try...Catch`. |
| **`Val(teks)`** | Menghasilkan `0` | Menghasilkan `12` | Menghasilkan `3` | **Sangat berbahaya**, menyembunyikan kesalahan input pengguna secara diam-diam. |
| **`Integer.TryParse`** | Menghasilkan `False` | Menghasilkan `False` | Menghasilkan `False` | **Paling direkomendasikan**. Mengembalikan nilai boolean tanpa memicu exception. |

### Jebakan Desimal (Koma vs Titik):
Regional Windows Indonesia memakai tanda koma `,` sebagai pemisah desimal, sedangkan sistem standar menggunakan titik `.`.
Gunakan `CultureInfo.InvariantCulture`:
```vb
Public Function CobaDesimal(teks As String, ByRef hasil As Decimal) As Boolean
    Dim teksTitik As String = teks.Trim().Replace(",", ".")
    Return Decimal.TryParse(teksTitik, NumberStyles.AllowDecimalPoint, CultureInfo.InvariantCulture, hasil)
End Function
```

---

## 5. Penggunaan ErrorProvider
- **ErrorProvider (`err`)** menampilkan ikon merah peringatan langsung di samping kontrol yang salah, lengkap dengan *tooltip* pesan kesalahan.
- Menghindari penggunaan rentetan `MessageBox` yang mengganggu alur pengguna.
- Perintah dasar:
  - `errInput.SetError(txtNama, "Nama wajib diisi.")`
  - `errInput.SetError(txtNama, "")` (menghapus tanda error)
  - `errInput.Clear()` (membersihkan semua tanda error)

---

## 6. Alur Validasi pada Tombol Simpan
1. Pengguna mengklik `btnSimpan`.
2. Panggil fungsi `ValidasiInput()`.
3. Jika gagal (`False`): Munculkan tanda error pada kontrol terkait, beri pesan status, lalu hentikan proses dengan `Return`.
4. Jika lolos (`True`): Lakukan konversi (dijamin aman tanpa perlu `Try...Catch`), simpan ke koleksi data, lalu bersihkan form.
