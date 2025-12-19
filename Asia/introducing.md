
# Panduan Lengkap Bahasa **`.in`** — IntegratedN (v1.0)

> **IntegratedN (`.in`)** adalah bahasa pemrograman *beginner‑friendly* yang berfungsi sebagai **jembatan menuju JavaScript**. Transpiler ditulis menggunakan **Rust** dan men‑transpile kode `.in` menjadi JavaScript 1:1 secara semantik.

* * *

# Daftar Isi

1. Tujuan singkat
2. Cara cepat: convert file `.in` → `.js` (CLI)
3. Syntax dasar & komentar
4. Tipe data & literal
5. Variabel (`set`, `let`, `local`)
6. Assignment & ekspresi
7. String interpolation
8. Array & object literal
9. Function — definisi & panggilan
10. Control flow: `if` / `else`, `while`, `for`
11. Operator logika & perbandingan
12. Built-in: `print`, `includes`, `undefined`
13. Error & pesan umum (error catalog)
14. Pipeline transpiler (arsitektur)
15. Perubahan implementasi (AST / Parser / Semantic / CodeGen)
16. Contoh lengkap (.in → JS)
17. Quick reference
18. VS Code extension & integrasi
19. Testing & debugging
20. Roadmap & kontribusi
21. License

* * *

## 1. Tujuan singkat

* Mudah dipelajari pemula
* Sintaks mirip bahasa manusia (Indonesia/Inggris campur)
* Perilaku 1:1 dengan JavaScript
* Error yang jelas & edukatif
* Transpilasi tanpa runtime tambahan

* * *

## 2. Cara cepat: convert file `.in` → `.js` (CLI)

Asumsi: lo udah build project Rust jadi `transpiler.exe` (Windows) atau `transpiler` (Linux/Mac).

**Perintah dasar:**

    # Windows (cmd / PowerShell)
    transpiler path/to/file.in            # output default: file.js (sama nama)
    transpiler file.in output.js           # input + output
    transpiler convert file.in output.js   # alias: convert subcommand

Contoh:

    C:/Projects/> transpiler test.in
    # hasil: test.js di folder yang sama

Jika executable nggak di PATH, taruh saja `transpiler.exe` di folder kerja.

* * *

## 3. Syntax dasar & komentar

Komentar:

    // komentar satu baris
    /* komentar
       multi baris */

Semua keyword case-sensitive (direkomendasikan lowercase untuk konsistensi).

* * *

## 4. Tipe data & literal

* `Number` — `1`, `3.14`
* `String` — double atau single quoted: `"halo"`, `'hai'`
* `Boolean` — `true`, `false`
* `Undefined` — `undefined`
* `Array` — `[1, 2, 3]`
* `Object` — `{ name: "Akang", age: 20 }`
* `StringInterpolation` — menggunakan `$identifier` di dalam string

* * *

## 5. Variabel: `set`, `let`, `local`

* `set name = value` → `const name = value;`
* `let name = value` → `let name = value;`
* `local name = value` → alias `let` (diperuntukkan untuk block‑local clarity)

Contoh:

    set appName = "IN Transpiler"
    let totalUser = 0
    local counter = 5

Aturan penting:

* Reassign ke identifier yang dideklarasikan dengan `set` → **semantic error**
* Deklarasi tanpa inisialisasi tidak didukung (untuk v1.0)

* * *

## 6. Assignment & ekspresi

Assignment mendukung target:

* identifier (`a = 1`)
* array index (`arr[0] = 5`)
* property access (`obj.name = "x"`)

Ekspresi mendukung urutan precedence:

* unary (`-x`, `not x`)
* multiplicative (`*`, `/`, `%`)
* additive (`+`, `-`)
* comparison (`==`, `!=`, `===`, `<`, `>`, `<=`, `>=`)
* logical (`and`, `or`)

Contoh:

    totalUser = totalUser + 1
    numbers[0] = numbers[0] + 10
    user.name = "Akang"

Validasi dilakukan di semantic phase: hanya `identifier`, `index`, `property` boleh jadi left-hand-side.

* * *

## 7. String interpolation

Gunakan `$identifier` di dalam string. Parser mendeteksi dan codegen akan menghasilkan template literal JS.

    set nama = "Rauf"
    print("Halo $nama, selamat datang")

→ JS: ``console.log(`Halo ${nama}, selamat datang`)``

Catatan: `$` harus diikuti identifier alfanumerik/underscore; untuk ekspresi kompleks gunakan variable sementara.

* * *

## 8. Array & Object literal

Deklarasi array:

    set roles = ["admin", "editor", "viewer"]

Object literal:

    let user = { name: "Akang", age: 20 }

Akses:

* index: `arr[0]`
* property: `obj.name`
* chaining: `users[0].profile.name`

Built-in `includes` tersedia sebagai operator/member:

    if (roles includes "admin") {
        print("Role admin tersedia")
    }

→ JS: `roles.includes("admin")`

* * *

## 9. Function — definisi & panggilan

Definisi:

    function greet(name, role) {
        print("Halo $name, role kamu adalah $role")
    }
    
    greet("Akang", "admin")

Return:

    function tambah(a, b) {
        return a + b
    }
    let hasil = tambah(2, 3)

Parameter dan variabel fungsi memiliki scope sendiri; `return` hanya valid di dalam fungsi — di luar akan error.

* * *

## 10. Control flow

### if / else

    if (x > 5) {
        print("besar")
    } else {
        print("kecil")
    }

### while

    let i = 0
    while (i < 3) {
        print(i)
        i = i + 1
    }

### for (custom `from`/`to` syntax)

    for i from 1 to 5 {
        print("Loop ke-$i")
    }

→ JS: `for (let i = 1; i <= 5; i++) { ... }`

* * *

## 11. Operator logika & perbandingan

* Arithmetic: `+ - * / %`
* Comparison: `== != === > >= < <=`
* Logical: `and` → `&&`, `or` → `||`, `not` → `!`

Contoh:

    if (isActive and hasil == 8) {
        print("OK")
    }

* * *

## 12. Built-in

* `print(expr)` → `console.log(expr)`
* `includes` → `array.includes(x)`
* `undefined` literal tersedia

* * *

## 13. Error & pesan umum (error catalog)

Format error yang dihasilkan oleh pipeline:

    SemanticError (line X:Y): message

Contoh pesan dan arti:

* `Unexpected token: ...` — parser menemui token tak terduga
* `Expected identifier` — identifier yang dibutuhkan tidak ditemukan
* `variable 'x' is not declared` — pakai variabel tanpa deklarasi
* `variable 'x' is constant and cannot be reassigned` — coba assign ke `set`
* `return statement is only allowed inside functions` — `return` di luar fungsi
* `Assignment target is not assignable` — mencoba assign ke literal/ekspresi non-target

Tips debugging:

* Lihat `line` & `col` dari error
* Buka file `.in` di lokasi itu
* Jalankan `transpiler` di mode debug (jika tersedia) untuk melihat AST

* * *

## 14. Pipeline transpiler (arsitektur)

Tahapan:

    Lexer → Parser → AST → Semantic Analyzer → Code Generator → JavaScript

Setiap modul terpisah:

* **Lexer:** tokenization
* **Parser:** membangun AST (menangani precedence, postfix chaining)
* **Semantic Analyzer:** validasi scope, tipe dasar (sebagaimana JS), assignment target
* **CodeGen:** emit JavaScript yang mudah dibaca (1:1 semantik)

* * *

## 15. Perubahan implementasi (v1.0 updates)

**Perubahan AST**

* Ditambahkan `Expression::Index`, `Expression::Property`, `Expression::ObjectLiteral`.
* Ditambahkan `Statement::AssignmentTarget` dan enum `AssignmentTarget` untuk representasi target assignment yang valid.

**Perubahan Parser**

* Mendukung parsing postfix chaining: `()` (call), `[]` (index), `.` (property)
* Assignment ke index/property menggunakan node `AssignmentTarget`
* Object literal: kunci bisa identifier atau string

**Perubahan Semantic Analyzer**

* Validasi assignment target (hanya identifier, index, property)
* Larangan assignment ke literal (contoh: `1 = x` → error)
* Cek keberadaan identifier di scope (global/function/block)
* Validasi object literal, index access, property access

**Perubahan Code Generator**

* Emit JS untuk array indexing, property access, assignment, object literal
* Output mengikuti struktur JS (indentation, semicolon optional/consistent)

Hasil: seluruh pipeline sekarang mendukung array indexing, property access, assignment ke index/property, dan object literal sesuai spesifikasi.

* * *

## 16. Contoh lengkap (.in → JS)

**Contoh `.in`:**

    let users = [
        { name: "Akang", age: 20 },
        { name: "Wahyu", age: 22 }
    ]
    
    users[0].age = users[0].age + 1
    
    print("Nama: $users[0].name, Umur: $users[0].age")

**Hasil JS:**

    let users = [
        { name: "Akang", age: 20 },
        { name: "Wahyu", age: 22 }
    ];
    
    users[0].age = users[0].age + 1;
    
    console.log(`Nama: ${users[0].name}, Umur: ${users[0].age}`);

Langkah penerjemahan:

1. Parser membangun AST untuk array literal & object literal
2. Semantic memvalidasi assignment ke `users[0].age`
3. CodeGen menghasilkan indexing & template literal JS

* * *

## 17. Quick reference

| Keyword | Deskripsi |
| --- | --- |
| `set` | deklarasi konstanta → `const` |
| `let` | deklarasi variabel |
| `local` | alias `let` untuk clarity |
| `function` | definisi fungsi |
| `return` | mengembalikan nilai |
| `if` / `else` | percabangan |
| `while` | pengulangan kondisi |
| `for ... from ... to ...` | loop numerik |
| `print()` | output ke console |
| `includes` | array.includes (member call) |

Operators: `+ - * / %`, comparators `== != === > >= < <=`, logical `and or not`

* * *

## 18. VS Code extension & integrasi

Fitur yang tersedia / direkomendasikan:

* Syntax highlighting (TextMate grammar)
* Snippets untuk `function`, `for`, `if`, `set`, `let`
* Command `Convert .in → .js` (menjalankan binary lokal)
* Diagnostics integration: jalankan transpiler untuk parse/semantic dan peta error ke Diagnostics API

Packaging:

* `vsce package` → hasil `.vsix`
* `vsce publish` → butuh publisher & Personal Access Token

* * *

## 19. Testing & debugging

* Siapkan suite unit tests untuk:
  
  * Lexer (token sequences)
  * Parser (AST shapes)
  * Semantic (diagnostics)
  * CodeGen (JS output string equality / snapshot)
* Contoh tools: `cargo test` (Rust)
  
* Buat fixtures `.in` → expected `.js` untuk snapshot testing
  

Debugging tips:

* Jaga supaya CodeGen deterministik (whitespace predictable)
* Sediakan `--emit-ast` flag di CLI untuk inspeksi AST

* * *

## 20. Roadmap & kontribusi

**Planned (v1.1+):**

* async / await
* module system (import/export)
* class & OOP primitives
* Improved linter & suggestions
* Better VS Code integration (hover, go-to-def)
