# Pertemuan 4: Struktur Perulangan (Looping)

**Pemateri:** Shata Diyaul Haq  
**Mata Kuliah:** Pemrograman Visual  

---

## 1. Pengertian Perulangan (*Looping*)
**Perulangan** adalah struktur kontrol yang menjalankan sebuah blok instruksi berulang kali selama kondisi tertentu terpenuhi (*boolean True*) atau sebanyak jumlah pengulangan yang telah ditentukan.

### Fungsi dan Manfaat:
- **Mengautomasi Pekerjaan Berulang:** Mempermudah dan mempercepat eksekusi tugas repetitif.
- **Menghindari Duplikasi Kode (*DRY - Don't Repeat Yourself*):** Tidak perlu menulis instruksi manual berulang-ulang.
- **Pengolahan Data Skala Besar:** Memproses koleksi data (Array / List) dengan cepat.
- **Meningkatkan Struktur Kode:** Kode menjadi lebih rapi, terstruktur, fleksibel, dan mudah dirawat.

---

## 2. Dua Tipe Perulangan Utama

| Tipe Perulangan | Karakteristik | Contoh di VB.NET |
| :--- | :--- | :--- |
| **Counted Loop** | Jumlah iterasi/pengulangan **sudah diketahui secara pasti** di awal berdasarkan batas tertentu. | `For...Next` |
| **Uncounted Loop** | Jumlah pengulangan **tidak diketahui sebelumnya**; terus berjalan selama kondisi masih terpenuhi (`True`). | `While...End While`, `Do...Loop` |

---

## 3. Jenis-Jenis Perulangan

### A. Perulangan `For...Next` (Counted Loop)
Mengulang perintah sebanyak jumlah iterasi yang ditentukan dengan bantuan **variabel pengontrol**.
- **Menaikkan Nilai (*Step Positif*):**
  ```vb
  For i As Integer = 1 To 10 Step 1
      ListBox1.Items.Add(i)
  Next
  ```
- **Menurunkan Nilai (*Step Negatif*):**
  ```vb
  For i As Integer = 10 To 1 Step -1
      ListBox1.Items.Add(i)
  Next
  ```

---

### B. Perulangan `While...End While` (Kondisi Dicek di Awal)
Kondisi diuji **sebelum** blok perintah dijalankan. Jika kondisi awal sudah bernilai `False`, perulangan **tidak akan dijalankan sama sekali**.
```vb
Dim i As Integer = 1
While i <= 10
    ListBox1.Items.Add(i)
    i = i + 1
End While
```

---

### C. Perulangan `Do...Loop While` (Kondisi Dicek di Akhir)
Blok perintah dijalankan terlebih dahulu, baru kemudian kondisi dievaluasi di akhir. Oleh karena itu, blok kode **dijamin berjalan minimal satu kali**.
```vb
Dim i As Integer = 1
Do
    ListBox1.Items.Add(i)
    i += 1
Loop While i <= 10
```

---

### D. Perulangan `Do While...Loop` (Kondisi Dicek di Awal)
Perulangan terus berjalan selama kondisi bernilai `True`. Pengujian dilakukan sebelum masuk ke dalam blok perulangan:
```vb
Dim i As Integer = 1
Do While i <= 10
    ListBox1.Items.Add(i)
    i += 1
Loop
```

---

## 4. Perulangan Bersarang (*Nested Loop*)
**Nested Loop** adalah perulangan yang berada di dalam perulangan lainnya.
- Perulangan luar (*outer loop*) akan memicu perulangan dalam (*inner loop*) untuk dijalankan secara penuh pada setiap iterasinya.
- Sering digunakan untuk mengolah matriks / Array 2 Dimensi (baris dan kolom).

### Contoh Kode:
```vb
For i As Integer = 1 To 3      ' Perulangan Luar (Baris)
    For j As Integer = 1 To 3  ' Perulangan Dalam (Kolom)
        ListBox1.Items.Add(i & " - " & j)
    Next
Next
```

### Hasil Output:
```text
1 - 1
1 - 2
1 - 3
2 - 1
2 - 2
2 - 3
3 - 1
3 - 2
3 - 3
```
