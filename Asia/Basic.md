# Basic — Dasar Dasar Bahasa `.in`

---

## Struktur dasar file `.in`

Sebuah file `.in` biasanya berisi

1. Deklarasi variabel
2. Definisi fungsi
3. Logika program utama

### Contoh struktur sederhana

```
set appName = "Demo App"
let counter = 0

function tambahSatu(x) {
    return x + 1
}

counter = tambahSatu(counter)
print(counter)
```

---

## Komentar

Komentar adalah catatan untuk manusia
Komentar tidak dijalankan oleh program

### Komentar satu baris

```
// ini komentar satu baris
let x = 10
```

### Komentar banyak baris

```
/*
Ini komentar
bisa lebih dari satu baris
*/
```

---

## Variabel lebih dalam

### set

Digunakan untuk nilai yang tidak boleh berubah

```
set maxUser = 100
```

Jika dicoba diubah

```
maxUser = 200
```

Akan muncul error saat compile

---

### let

Digunakan untuk nilai yang bisa berubah

```
let score = 0
score = score + 10
```

---

### local

Secara fungsi sama dengan `let`
Biasanya dipakai di dalam blok seperti `if`, `while`, atau `function`
Tujuannya supaya kode lebih mudah dibaca

```
if (true) {
    local temp = 5
    print(temp)
}
```

---

## Assignment dan ekspresi

Assignment adalah proses mengisi atau mengubah nilai variabel

```
let total = 1
total = total + 2
total = total * 3
```

Ekspresi mengikuti urutan operasi matematika

---

## String dan teks

String adalah data berbentuk teks

```
let pesan1 = "Halo"
let pesan2 = 'Dunia'
```

### Interpolasi string

Gunakan `$namaVariabel` di dalam string

```
set nama = "Ayu"
let umur = 21

print("Nama $nama, umur $umur tahun")
```

---

## Array dasar

Array digunakan untuk menyimpan banyak nilai dalam satu variabel

```
let angka = [1, 2, 3, 4]
let nama = ["Ani", "Budi", "Cici"]
```

### Mengambil nilai array

```
let pertama = angka[0]
print(pertama)
```

### Mengecek isi array dengan includes

```
if (nama includes "Ani") {
    print("Ani ada di daftar")
}
```

---

## Percabangan if dan else

Digunakan untuk membuat keputusan

```
let nilai = 80

if (nilai >= 75) {
    print("Lulus")
} else {
    print("Tidak lulus")
}
```

### Kondisi gabungan

```
if (nilai >= 75 and nilai <= 100) {
    print("Nilai valid")
}
```

---

## Pengulangan while

While akan mengulang selama kondisi benar

```
let i = 0

while (i < 5) {
    print(i)
    i = i + 1
}
```

Pastikan kondisi bisa berhenti

---

## Pengulangan for

For digunakan untuk perulangan angka yang jelas

```
for i from 1 to 5 {
    print("Iterasi ke-$i")
}
```

Artinya
Mulai dari 1
Berhenti di 5
Naik satu setiap loop

---

## Function lebih detail

Function membantu memecah program menjadi bagian kecil

### Function tanpa return

```
function tampilPesan() {
    print("Halo dari fungsi")
}

tampilPesan()
```

---

### Function dengan parameter

```
function sapa(nama) {
    print("Halo $nama")
}

sapa("Rina")
```

---

### Function dengan return

```
function kali(a, b) {
    return a * b
}

let hasil = kali(4, 5)
print(hasil)
```

Catatan
`return` cuma boleh dipakai di dalam function sebelum akhiran kurung kurawal pada sebuah function {}

---

## Built in function

### print

Digunakan untuk menampilin data ke console

```
print("Hello World")
```

---

## Error yang sering muncul

- `Expected identifier`
  Biasanya lupa nulis nama variabel atau fungsi

- `variable is not declared`
  Variabel belum dibuat tapi udah dipakai

- `return statement is only allowed inside functions`
  Return ditulis di luar function

---

## Contoh program kecil

```
set appName = "Counter App"
let count = 0

function naik() {
    count = count + 1
}

for i from 1 to 3 {
    naik()
}

print("App $appName")
print("Count akhir: $count")
```

---

## Tips menulis kode `.in`

- Gunakan nama variabel yang jelas
- Pisahkan kode dengan baris kosong
- Jangan menulis semua di satu baris
- Biasakan membaca error dengan teliti

---
