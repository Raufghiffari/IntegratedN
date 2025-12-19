# Intermediate — Pendalaman Bahasa `.in`

---

Fokus utama

- Aturan aturan yang sering bikin error
- Cara berpikir yang benar saat menulis kode `.in`
- Kebiasaan yang baik supaya kode aman dan mudah dirawat

---

## Scope dan blok kode

Scope adalah wilayah di mana variabel bisa dipakai
Biasanya ditandai dengan tanda `{` dan `}`

### Contoh scope sederhana

```
let x = 10

if (x > 5) {
    let y = 20
    print(y)
}

print(x)
```

Penjelasan

- `x` bisa dipakai di mana saja setelah dibuat
- `y` hanya bisa dipakai di dalam blok `if`

Jika `y` dipakai di luar blok, akan muncul error

---

## Shadowing variabel

Shadowing terjadi ketika variabel dengan nama yang sama dibuat di scope berbeda

```
let value = 10

function demo() {
    let value = 5
    print(value)
}

demo()
print(value)
```

Hasil

- Di dalam fungsi: 5
- Di luar fungsi: 10

Catatan
harus dipakai dengan hati hati supaya tidak membingungkan

---

## Aturan `set`, `let`, dan `local`

### set

- Hanya boleh diisi satu kali
- Tidak boleh diubah
- Cocok untuk konfigurasi atau nilai tetap

```
set VERSION = 1
```

---

### let

- Bisa diubah
- Berlaku di scope tempat dibuat

```
let total = 0
total = total + 1
```

---

### local

- Sama seperti `let`
- Digunakan khusus di dalam blok
- Membantu membaca kode

```
while (true) {
    local temp = 1
    break
}
```

---

## Return dan alur fungsi

`return` menghentikan fungsi dan mengembalikan nilai

```
function cekAngka(x) {
    if (x > 0) {
        return "positif"
    }

    return "nol atau negatif"
}
```

Catatan penting

- Kode setelah `return` tidak akan dijalankan
- `return` hanya boleh ada di dalam function

---

## Function tanpa return eksplisit

Jika function tidak memiliki `return`
Maka hasilnya adalah `undefined`

```
function tampil() {
    print("Halo")
}

let hasil = tampil()
print(hasil)
```

---

## Parameter dan validasi sederhana

Parameter adalah nilai yang dikirim ke function

```
function bagi(a, b) {
    if (b == 0) {
        return "Tidak bisa dibagi nol"
    }

    return a / b
}
```

Biasakan mengecek kondisi tidak aman

---

## Boolean dan logika kompleks

Logika bisa digabung lebih dari satu kondisi

```
let umur = 20
let punyaKTP = true

if (umur >= 17 and punyaKTP) {
    print("Boleh mendaftar")
}
```

Gunakan tanda kurung jika kondisi mulai panjang

---

## While dan kondisi berbahaya

Contoh while yang aman

```
let i = 0

while (i < 3) {
    print(i)
    i = i + 1
}
```

Contoh while berbahaya

```
while (true) {
    print("jalan terus")
}
```

Loop ini tidak akan berhenti
Gunakan dengan sangat hati hati

---

## For dan variable loop

Variabel pada `for` hanya berlaku di dalam loop

```
for i from 1 to 3 {
    print(i)
}
```

Menggunakan `i` di luar loop akan error

---

## Array dan logika sederhana

### Loop array manual

```
let data = [10, 20, 30]

for i from 0 to 2 {
    print(data[i])
}
```

### Pengecekan isi array

```
if (data includes 20) {
    print("Ada angka 20")
}
```

---

## Error semantik yang sering muncul

### Variabel belum dideklarasikan

```
x = 10
```

Error

```
variable 'x' is not declared
```

---

### Mengubah konstanta

```
set a = 1
a = 2
```

Error

```
variable 'a' is constant and cannot be reassigned
```

---

### Return di luar function

```
return 10
```

Error

```
return statement is only allowed inside functions
```

---

## Contoh program intermediate

```
set APP_NAME = "Checker"

function cekNilai(nilai) {
    if (nilai >= 75) {
        return "Lulus"
    }

    return "Tidak lulus"
}

let daftar = [60, 80, 90]

for i from 0 to 2 {
    let hasil = cekNilai(daftar[i])
    print("Nilai $daftar[i] : $hasil")
}
```

---

## Kebiasaan baik menulis kode `.in`

- Selalu deklarasikan variabel sebelum dipakai
- Jangan mengubah `set`
- Gunakan `local` di dalam blok
- Buat function pendek dan jelas
- Baca error dari atas ke bawah

---

## Setelah ini belajar apa

Jika sudah sampai sini
Kamu sudah cukup nyaman dengan bahasa `.in`

Langkah selanjutnya

- Advanced.md
- Optimasi transpiler
- Struktur project besar
- Kontribusi ke compiler

---
