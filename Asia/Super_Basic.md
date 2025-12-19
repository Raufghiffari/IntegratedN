Super Basic — Pengenalan Bahasa `.in`
=====================================

* * *

Bahasa `.in` dibuat supaya belajar logika pemrograman jadi lebih mudah dan terasa seperti berbicara sehari hari  
Syntax dibuat sederhana agar fokus ke ide program, bukan ke tanda baca atau aturan rumit

* * *

Istilah penting yang sering muncul
----------------------------------

* **Program**  
  Rangkaian instruksi yang dijalankan komputer untuk melakukan sesuatu

* **Kode**  
  Tulisan program yang dibuat oleh manusia

* **Transpiler**  
  Alat yang mengubah kode `.in` menjadi JavaScript supaya bisa dijalankan di lingkungan yang sudah umum

* * *

Apa itu variabel
----------------

Variabel itu seperti kotak penyimpanan yang diberi nama  
Kita bisa memasukkan nilai ke dalam kotak tersebut lalu memakainya lagi kapan saja

Bayangkan seperti ini

* Kotak bernama `nama` berisi nama seseorang

* Kotak bernama `umur` berisi angka umur

### Contoh di bahasa `.in`

    set nama = "Wahyu"     # nilainya tidak boleh diubah
    let umur = 20          # nilainya boleh berubah
    local hitung = 0       # mirip let, biasanya dipakai di dalam blok

Catatan penting

`set` artinya konstanta  
Jika sudah diisi lalu diubah lagi, program akan error

* * *

Tipe data dasar
---------------

* **Number**  
  Angka seperti 1 atau 3.14

* **String**  
  Teks yang diapit tanda "" atau ''

* **Boolean**  
  Nilai benar atau salah  
  Ditulis `true` atau `false`

* **Array**  
  Kumpulan nilai di dalam tanda []

* **Undefined**  
  Nilai yang belum diisi atau belum ada

### Contoh

    set pi = 3.14
    let pesan = "Halo dunia"
    let aktif = true
    let daftar = [1, 2, 3]
    let kosong = undefined

* * *

String dan interpolasi
----------------------

Interpolasi digunakan untuk memasukkan isi variabel ke dalam string  
Tidak perlu menyambung teks secara manual

Gunakan tanda `$` diikuti nama variabel
    set nama = "Rauf"
    print("Halo $nama, selamat datang")

* * *

Operator dasar dan assignment
-----------------------------

Operator yang sering dipakai

* Penjumlahan `+`

* Pengurangan `-`

* Perkalian `*`

* Pembagian `/`

Assignment atau pengisian ulang nilai
    total = total + 1

Perbandingan

* `==` sama dengan

* `!=` tidak sama dengan

* `>` lebih besar

* `<` lebih kecil

* `>=` lebih besar atau sama dengan

* `<=` lebih kecil atau sama dengan

Logika

* `and` berarti `dan`

* `or` berarti `atau`

* `not` berarti `kebalikan`

### Contoh

    let a = 2
    let b = 3
    let Orang = a + b
    
    if (Orang > 4) {
        print("Lebih dari empat")
    }

* * *

Fungsi dan pemanggilan fungsi
-----------------------------

Fungsi adalah kumpulan perintah yang diberi nama  
Tujuannya supaya kode bisa dipakai berulang ulang

### Contoh fungsi sederhana

    function sapa(nama) {
        print("Halo $nama")
    }
    
    sapa("Akang")

### Fungsi dengan nilai balik

Jika fungsi mengembalikan nilai, gunakan `return`


    function tambah(a, b) {
        return a + b
    }
    let hasil = tambah(2, 3)
    print("Hasil: $hasil")

* * *

Percabangan dengan if dan else
------------------------------

Percabangan digunakan untuk mengambil keputusan  
Program akan memilih jalur berdasarkan kondisi


    if (umur >= 18) {
        print("Sudah dewasa")
    } else {
        print("Belum dewasa")
    }

* * *

Pengulangan dengan while dan for
--------------------------------

### While

Digunakan untuk mengulang selama kondisi masih benar
    let i = 0
    while (i < 3) {
        print(i)
        i = i + 1
    }

### For

Digunakan untuk loop angka yang jelas awal dan akhirnya
    for j from 1 to 5 {
        print("Loop ke-$j")
    }

* * *

Cara melihat output
-------------------

Gunakan `print(expr)` untuk menampilkan nilai ke console
    print("Halo dari .in")

* * *

Error umum yang sering ditemui
------------------------------

* `variable 'x' is not declared`  
  Variabel dipakai tapi belum dibuat

* `variable 'x' is constant and cannot be reassigned`  
  Mencoba mengubah variabel `set`

* `Unexpected token`  
  Struktur kode salah  
  Biasanya karena kurung atau blok tidak lengkap


