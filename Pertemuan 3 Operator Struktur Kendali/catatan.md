# Pertemuan 3: Operator dan Struktur Pengendalian

**Pemateri:** Shata Diyaul Haq  
**Mata Kuliah:** Pemrograman Visual  

---

## 1. Operator
**Operator** adalah simbol khusus yang digunakan untuk melakukan operasi tertentu pada satu atau lebih nilai (yang disebut sebagai *operand*).

### A. Operator Aritmatika
Digunakan untuk melakukan kalkulasi matematika dasar pada nilai numerik atau variabel:
| Operator | Simbol | Nama Operator | Deskripsi | Contoh |
| :---: | :---: | :--- | :--- | :--- |
| **$+$** | `+` | Penjumlahan | Menjumlahkan dua nilai | `5 + 3 = 8` |
| **$-$** | `-` | Pengurangan | Mengurangi nilai satu dengan nilai lain | `7 - 4 = 3` |
| **$\times$** | `*` | Perkalian | Mengalikan dua nilai | `6 * 2 = 12` |
| **$\div$** | `/` | Pembagian | Membagi nilai satu dengan nilai lain | `10 / 2 = 5` |
| **$\%$** | `Mod` / `%` | Modulus | Menghasilkan sisa bagi pembagian | `10 Mod 3 = 1` |

---

### B. Operator Penugasan (*Assignment*)
Digunakan untuk memasukkan atau memberikan nilai ke dalam suatu variabel:
| Simbol | Nama Operator | Deskripsi | Ekuivalen | Contoh |
| :---: | :--- | :--- | :--- | :--- |
| `=` | Penugasan Sederhana | Mengisi nilai ke variabel | `a = b` | `x = 10` |
| `+=` | Tambah dan Simpan | Menambahkan nilai ke variabel | `a = a + b` | `x += 5` |
| `-=` | Kurang dan Simpan | Mengurangi nilai dari variabel | `a = a - b` | `x -= 3` |
| `*=` | Kali dan Simpan | Mengalikan nilai dengan variabel | `a = a * b` | `x *= 2` |
| `/=` | Bagi dan Simpan | Membagi nilai dengan variabel | `a = a / b` | `x /= 4` |
| `%=` | Modulus dan Simpan | Mengambil sisa bagi ke variabel | `a = a Mod b` | `x %= 3` |

---

### C. Operator Perbandingan (*Relational*)
Membandingkan dua nilai dan menghasilkan nilai boolean (**`True`** atau **`False`**):
| Simbol | Nama Operator | Deskripsi | Contoh |
| :---: | :--- | :--- | :--- |
| `=` | Sama dengan | Memeriksa apakah kedua nilai bernilai sama | `5 = 5` $\rightarrow$ `True` |
| `<>` | Tidak sama dengan | Memeriksa apakah kedua nilai tidak sama | `5 <> 3` $\rightarrow$ `True` |
| `>` | Lebih besar dari | Nilai kiri lebih besar dari nilai kanan | `7 > 3` $\rightarrow$ `True` |
| `<` | Lebih kecil dari | Nilai kiri lebih kecil dari nilai kanan | `2 < 4` $\rightarrow$ `True` |
| `>=` | Lebih besar atau sama | Nilai kiri lebih besar atau sama dengan kanan | `5 >= 5` $\rightarrow$ `True` |
| `<=` | Lebih kecil atau sama | Nilai kiri lebih kecil atau sama dengan kanan | `3 <= 7` $\rightarrow$ `True` |

---

### D. Operator Logika
Menghubungkan beberapa ekspresi boolean untuk menghasilkan satu nilai kebenaran:
- **`And`**: Menghasilkan `True` hanya jika **kedua** kondisi bernilai `True`.
- **`Or`**: Menghasilkan `True` jika **salah satu atau kedua** kondisi bernilai `True`.
- **`Not`**: Membalikkan nilai logika (`Not True` $\rightarrow$ `False`).
- **`Xor`**: Menghasilkan `True` jika salah satu kondisi bernilai `True`, namun bukan keduanya.
- **`Not (A Or B)` (NOR)**: Kebalikan dari `Or`. Menghasilkan `True` hanya jika kedua kondisi `False`.
- **`Not (A And B)` (NAND)**: Kebalikan dari `And`. Menghasilkan `True` kecuali jika kedua kondisi `True`.

---

### E. Operator Increment & Decrement
- **Increment (`+1`):** Menambahkan nilai variabel sebesar satu (`x += 1` atau bentuk `++x` / `x++`).
- **Decrement (`-1`):** Mengurangi nilai variabel sebesar satu (`x -= 1` atau bentuk `--x` / `x--`).

---

## 2. Ekspresi
**Ekspresi** adalah kombinasi nilai, variabel, operator, dan pemanggilan method yang dievaluasi menjadi satu nilai tunggal. Ekspresi dapat diletakkan di mana pun nilai dibutuhkan (misal di parameter fungsi, penugasan variabel, atau syarat percabangan).

---

## 3. Percabangan (*Conditional Statements*)
Struktur kontrol alur program untuk menentukan jalannya eksekusi berdasarkan kondisi tertentu (`True`/`False`).

### 1. `If` Statement (Tunggal)
Hanya memiliki satu blok pilihan yang dieksekusi saat kondisi bernilai benar.
```vb
If nilai >= 75 Then
    lblHasil.Text = "Selamat, Anda Lulus!"
End If
```

### 2. `If - Else` Statement (Dua Cabang)
Menjalankan satu blok kode jika benar, dan blok alternatif jika salah.
```vb
If nilai >= 75 Then
    lblHasil.Text = "Lulus"
Else
    lblHasil.Text = "Tidak Lulus"
End If
```

### 3. `If - ElseIf` Statement (Banyak Kondisi)
Digunakan saat terdapat beberapa tingkatan kondisi yang harus diperiksa secara berurutan.
```vb
If nilai >= 85 Then
    grade = "A"
ElseIf nilai >= 75 Then
    grade = "B"
ElseIf nilai >= 60 Then
    grade = "C"
Else
    grade = "D"
End If
```

### 4. `Select Case` (Switch Statement)
Alternatif yang jauh lebih rapi dibanding banyak `If...ElseIf`, cocok untuk memeriksa satu variabel dengan banyak kemungkinan nilai:
```vb
Select Case nilai
    Case 1
        hasil = "Sangat Baik"
    Case 2
        hasil = "Baik"
    Case 3
        hasil = "Cukup"
    Case Else
        hasil = "Kurang"
End Select
```

### 5. Operator Ternary (Percabangan Singkat Satu Baris)
Bentuk ringkas percabangan `If...Else` dalam satu baris ekspresi:
```vb
Dim status As String = If(nilai >= 75, "Lulus", "Tidak Lulus")
```
