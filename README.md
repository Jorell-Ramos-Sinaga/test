# Latihan Soal Modul 2 Praktikum Sistem Operasi

## 📝 Aturan Pengerjaan

- Yang dikumpulkan hanyalah file dengan format nama `NRP_Nama_Latihan_2.md`.
- File tersebut merupakan **laporan** yang berisi penjelasan tentang program yang dibuat untuk setiap soal.
- Semua soal **wajib dikerjakan menggunakan bahasa pemrograman C**.
- Laporan ditulis dalam **format Markdown** dengan memperhatikan kaidah penulisan Markdown yang baik.
- **Gunakan format penamaan file yang sesuai dengan ketentuan.**

## 📋 Isi Laporan

Laporan harus memuat informasi berikut:

1. Identitas diri:

   - NRP
   - Nama
   - Kelas
   - Kelompok

2. Program yang telah dibuat
3. Penjelasan tentang program yang dibuat
4. Hasil output dari program yang telah dibuat
5. Penjelasan tentang hasil output yang diperoleh
6. Screenshot hasil output yang diperoleh
   (clue: upload terlebih dahulu gambarnya ke cloud storage/image hosting/apapun yang bisa diakses publik, lalu masukkan linknya ke dalam laporan)

> Catatan: Silahkan explorasi lebih lanjut tentang Markdown untuk mempercantik laporan. (Hitung-hitung sebagai latihan dalam menulis laporan resmi praktikum)

## 📅 Deadline Pengumpulan

- Laporan dikumpulkan melalui **Google Form** berikut: [Link](https://docs.google.com/forms/d/e/1FAIpQLSfFN8E-J2207l1uGYY9PzOCL6VOHs_aL-Us41juNDXWxEUzeg/viewform?usp=dialog)
- Batas akhir pengumpulan: **16 April 2025 pukul 23.59 WIB**

## 1. Process

**Deskripsi:**

Buat satu program C yang melakukan tiga proses secara berurutan:

a. Membuat folder baru bernama `halo`.

b. Membuat file kosong bernama `hai.txt` di dalam folder `halo`.

c. Mengcopy file `hai.txt` tersebut ke luar folder, sehingga hasilnya:

- Ada `hai.txt` di dalam folder `halo/`
- Ada juga salinan `hai.txt` di luar folder `halo` (di direktori yang sama dengan program ini dijalankan)

**Hasil akhir struktur direktori:**

```
Direktori/
│
├── program.c
├── halo/
│   └── hai.txt
└── hai.txt  ← hasil copy dari halo/hai.txt
```

**Catatan:**

- Semua proses ditulis dalam **satu file C**.
- Program dijalankan **sekali saja**.

## Kode 
```Shell
#include <stdio.h>
#include <stdlib.h>

int main() {
system("mkdir /home/ubuntu/halo");
system("touch /home/ubuntu/halo/hai.txt");
system("cp /home/ubuntu/halo/hai.txt /home/ubuntu/");

return 0;
}

```
**Penjelasan Kode:**
1. Menggunakan fungsi `system` untuk menjalankan untuk melakukan pemanggilan perintah shell secara langsung dari program C.
   - `mkdir /home/ubuntu/halo` untuk membuat sebuah directory bernama `halo`
   - `touch /home/ubuntu/halo/hai.txt` untuk membuat suatu file `hai.txt` di directory `halo`
   - `cp /home/ubuntu/halo/hai.txt /home/ubuntu/` untuk mengcopy file `hai.txt` yang dibuat tadi ke directory awal `/home/ubuntu`

## Output
**Hasil:**
Hasil berupa suatu directory bernama `halo` yang memuat file `hai.txt`, dan salinan file `hai.txt` di directory yang memuat `process.c`

**Penjelasan Hasil:**
Terbuatnya direktori `halo` karena `mkdir`, `hai.txt` karena `touch`, dan salinan `hai.txt`karena `cp` yang dipanggil oleh fungsi `system` di `process.c`

**Screenshoot Output**
https://drive.google.com/file/d/1VlJV10nqEdmO6_UITSVdF_jU9-G_Vkbb/view?usp=sharing
![Screenshot Output](https://drive.google.com/uc?export=view&id=1VlJV10nqEdmO6_UITSVdF_jU9-G_Vkbb)
![Screenshot Output](https://drive.google.com/uc?export=view&id=12nPZVO8LlxbskknFdafe-RLTKkwQH2Pz)

---

## 2. Thread

**Deskripsi:**

Buat satu program dengan **3 thread**, masing-masing bertugas:

a. **Thread 1:** Menulis angka 1–100 secara berurutan ke file `count.txt`.

b. **Thread 2:** Menulis `"Saya pintar mengerjakan thread"` ke file `print.txt`.

c. **Thread 3:** Menulis semua angka **genap** dari 1–100 ke file `count_2.txt`.

**Catatan:**

- Jalankan program **sebanyak 3 kali**.
- Catat **urutan thread** yang selesai duluan ke file `log.txt`.

**Contoh isi `log.txt`:**

```
1. Thread 1
2. Thread 1
3. Thread 1
```

> Setiap kali program dijalankan, bisa saja urutan thread yang selesai berbeda-beda.

---

## 3. Thread dengan Mutex

Buatlah satu program yang:

a. Membuat **5 thread**, masing-masing menghitung dari 1 sampai 3.

b. Setiap thread menulis hasil hitungannya ke file `log.txt` dengan format:

```
thread {id} count {angka}
```

c. Gunakan `pthread_mutex` untuk mencegah **race condition** saat menulis ke file.

> **Catatan:** Saat satu thread sedang counting dan menulis ke file, thread lain **harus menunggu**.

**Contoh isi `log.txt`:**

```
thread 3 count 1
thread 3 count 2
thread 3 count 3
thread 1 count 1
...
thread 5 count 3
```

---

## 4. IPC

### a. Shared Memory

**Buat dua file C:**

- `sender.c`: Membuat shared memory dan mengirim pesan:
  ```
  aku lagi belajar ipc
  ```
- `receiver.c`: Membaca pesan dari shared memory dan menampilkannya ke layar.

### b. Message Queue

- Buat program yang menggunakan **message queue**.
- Kirimkan pesan:
  ```
  yah belajar ipc mulu
  ```
- Setelah itu, program membaca pesan dari queue dan menampilkannya ke layar.

### c. Pipe dengan `fork()`

- Gunakan **pipe** dan **`fork()`** untuk membuat _child process_.
- _Parent process_ mengirim string:
  ```
  hai, anak sisop 24
  ```
- _Child process_ menerima pesan dan menampilkannya ke layar.
