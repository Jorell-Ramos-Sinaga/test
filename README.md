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
```c
#include <stdio.h>
#include <stdlib.h>

int main() {
system("mkdir /home/ubuntu/halo");
system("touch /home/ubuntu/halo/hai.txt");
system("cp /home/ubuntu/halo/hai.txt /home/ubuntu/");

return 0;
}

```
#### **Penjelasan Kode:**
1. Menggunakan fungsi `system` untuk menjalankan untuk melakukan pemanggilan perintah shell secara langsung dari program C.
   - `mkdir /home/ubuntu/halo` untuk membuat sebuah directory bernama `halo`
   - `touch /home/ubuntu/halo/hai.txt` untuk membuat suatu file `hai.txt` di directory `halo`
   - `cp /home/ubuntu/halo/hai.txt /home/ubuntu/` untuk mengcopy file `hai.txt` yang dibuat tadi ke directory awal `/home/ubuntu`

## Output
#### **Hasil:**

Hasil berupa suatu directory bernama `halo` yang memuat file `hai.txt`, dan salinan file `hai.txt` di directory yang memuat `process.c`

```
Direktori/
│
├── program.c
├── halo/
│   └── hai.txt
└── hai.txt  ← hasil copy dari halo/hai.txt
```

#### **Penjelasan Hasil:**

Terbuatnya direktori `halo` karena `mkdir`, `hai.txt` karena `touch`, dan salinan `hai.txt`karena `cp` yang dipanggil oleh fungsi `system` di `process.c`

#### **Screenshoot Output:**
1. `/home/ubuntu/`
<div align="center">
  <img src="https://drive.google.com/uc?export=view&id=1VlJV10nqEdmO6_UITSVdF_jU9-G_Vkbb" width="600"/>
</div>

2. `/home/ubuntu/halo/`
<div align="center">
  <img src="https://drive.google.com/uc?export=view&id=12nPZVO8LlxbskknFdafe-RLTKkwQH2Pz" width="600"/>
</div>

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

## Kode 
```c
#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>
#include <string.h>

#define MAX_THREADS 3
int urutan = 0;

void tulis_log(const char* nama_thread) {
    urutan++;
    FILE* log = fopen("log.txt", "w");
    fprintf(log, "%d. %s\n", urutan, nama_thread);
    fclose(log);
}

void* thread1(void* arg) {
    FILE* f = fopen("count.txt", "w");
    for (int i = 1; i <= 100; i++) {
        fprintf(f, "%d\n", i);
    }
    fclose(f);
    tulis_log("Thread 1");
    return NULL;
}

void* thread2(void* arg) {
    FILE* f = fopen("print.txt", "w");
    fprintf(f, "Saya pintar mengerjakan thread\n");
    fclose(f);
    tulis_log("Thread 2");
    return NULL;
}

void* thread3(void* arg) {
    FILE* f = fopen("count_2.txt", "w");
    for (int i = 2; i <= 100; i += 2) {
        fprintf(f, "%d\n", i);
    }
    fclose(f);
    tulis_log("Thread 3");
    return NULL;
}

int main() {
    pthread_t threads[MAX_THREADS];

    FILE* log = fopen("log.txt", "w");
    fclose(log);

    pthread_create(&threads[0], NULL, thread1, NULL);
    pthread_create(&threads[1], NULL, thread2, NULL);
    pthread_create(&threads[2], NULL, thread3, NULL);

    for (int i = 0; i < MAX_THREADS; i++) {
        pthread_join(threads[i], NULL);
    }

    return 0;
}

```
#### **Penjelasan Kode:**
1. Global Variable
   - `#define MAX_THREADS 3` untuk deklarasi berapa thread yang kita jalankan.
   - `int urutan = 0` sebagai variabel untuk menentukan urutan di fungsi `tulis_log` nanti.
2. Fungsi `tulis_log`
   - `tulis_log(const char* nama_thread)` memasukkan `nama_thread` untuk menentukan thread mana yang sedang dicatat sekarang.
   - `urutan++` increment untuk numbering urutan.
   - membuka file `log.txt` dengan `fopen` dengan permission `w` (write) untuk bisa mengedit file `log.txt`.
   - `fprintf(log, "%d. %s\n", urutan, nama_thread)` mencetak urutan dan thread yang sekarang dicatat ke file.
   - mentutup file kembali dengan `fclose`.
3.  Fungsi `thread1`
    - membuka dan menutup file `count.txt` dengan `fopen` dan `fclose`.
    - looping `for` untuk mencetak 1-100 ke file `print.txt`.
    - `tulis_log("Thread 1")` memanggil fungsi `thread_log` dan memasukkan string `"Thread 1"` sebagai `nama_thread`.
4.  Fungsi `thread2`
    - membuka dan menutup file `print.txt` dengan `fopen` dan `fclose`.
    - mencetak kalimat yang diminta soal ke file dengan `fprintf`.
    - `tulis_log("Thread 2")` memanggil fungsi `thread_log` dan memasukkan string `"Thread 2"` sebagai `nama_thread`.
5.  Fungsi `thread3`
    - membuka dan menutup file `count_2.txt` dengan `fopen` dan `fclose`.
    - looping `for` untuk mencetak angka genap 1-100 ke file.
    - `tulis_log("Thread 3")` memanggil fungsi `thread_log` dan memasukkan string `"Thread 3"` sebagai `nama_thread`.
6.  Fungsi `main`
    - `pthread_t threads[MAX_THREADS]` mempersiapkan 3 thread sesuai dengan `MAX_THREADS`.
    - membuka dan mengkosongkan file `log.txt` dengan `fopen` dan `fclose` agar filenya bisa kosong sebelum memasukkan urutan thread.
    - `pthread_create` untuk memulai thread yang membuat `threads[n]` menjalankan fungsi `thread_n` .
    - looping `pthread_join` untuk menunggu thread selesai sebelum melanjutkan program.


## Output
#### **Hasil:**

1. contoh hasil `count.txt`
   ```
   1
   2
   3
   ...
   99
   100
   ```
2. contoh hasil `print.txt`
   ```
   Saya pintar mengerjakan thread
   ```
3. contoh hasil `count_2.txt`
   ```
   2
   4
   ...
   98
   100
   ```
4. contoh hasil `log.txt` untuk setiap kali program dijalankan
   - ```
     1. Thread 1
     2. Thread 3
     3. Thread 2
     ```
   - ```
     1. Thread 2
     2. Thread 1
     3. Thread 3
     ```
   - ```
     1. Thread 3
     2. Thread 1
     3. Thread 2
     ```


#### **Penjelasan Hasil:**
- File `count.txt`, `print.txt`, dan `count_2.txt` menunjukkan bahwa masing-masing thread berhasil menjalankan tugasnya secara paralel.
- Hasil `log.txt` berbeda-beda disebabkan thread dijalankan tanpa mutex sehingga terjadi *race condition*.

#### **Screenshoot Output:**
1. `count.txt`
<div align="center">
  <img src="https://drive.google.com/uc?export=view&id=1chHWW5-FF1ydIynOjc2rl1EX8xrSh8ZJ" width="600"/>
</div>

2. `print.txt`
<div align="center">
  <img src="https://drive.google.com/uc?export=view&id=1chHWW5-FF1ydIynOjc2rl1EX8xrSh8ZJ" width="600"/>
</div>

3. `count_2`
<div align="center">
  <img src="https://drive.google.com/uc?export=view&id=17o7kzgGZobmk_lJ11Z-GTk6PVuzGDjKB" width="600"/>
</div>

4. `log.txt` run pertama
<div align="center">
  <img src="https://drive.google.com/uc?export=view&id=12Gq_2BlIWuMG9uczGQfAG2UKYKAk9aun" width="600"/>
</div>

5. `log.txt` run kedua
<div align="center">
  <img src="https://drive.google.com/uc?export=view&id=1hpzG64jYo0l1wiYB0EFxh1nwT5EskbxY" width="600"/>
</div>

6. `log.txt` run ketiga
<div align="center">
  <img src="https://drive.google.com/uc?export=view&id=1Hfvc7QmqwxJNG9dpxV0idYAAzl6htIn_" width="600"/>
</div>

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

## Kode 
```c
#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>
#include <unistd.h>

#define THREAD_COUNT 5

pthread_mutex_t lock;

void* count_and_log(void* arg) {
    int id = *((int*)arg);

    pthread_mutex_lock(&lock);
    FILE* file = fopen("log.txt", "a");

    for (int i = 1; i <= 3; ++i) {
        fprintf(file, "thread %d count %d\n", id, i);
        fflush(file);
        sleep(1);
    }

    fclose(file);
    pthread_mutex_unlock(&lock);
    return NULL;
}

int main() {
    pthread_t threads[THREAD_COUNT];
    int thread_ids[THREAD_COUNT];

    pthread_mutex_init(&lock, NULL);

    for (int i = 0; i < THREAD_COUNT; ++i) {
        thread_ids[i] = i + 1;
        pthread_create(&threads[i], NULL, count_and_log, &thread_ids[i]);
    }

    for (int i = 0; i < THREAD_COUNT; ++i) {
        pthread_join(threads[i], NULL);
    }

    pthread_mutex_destroy(&lock);

    return 0;
}

```
#### **Penjelasan Kode:**
1. Global Variable
   - `#define MAX_THREADS 5` untuk deklarasi berapa thread yang kita jalankan.
   - `pthread_mutex_t lock` untuk deklarasi mutex global yang akan dipakai untuk mengatur file tidak ditulis berbagai thread sekaligus.
2. Fungsi `count_and_log`
   - `arg` sebagai pointer id thread
   - `pthread_mutex_lock(&lock)` untuk mengunci mutex sebelum menulis file, agar cuman thread sekarang yang mengakses file saat ini.
   - membuka file `log.txt` dengan `fopen` dalam mode append `a` agar tidak menghapus penulisan thread sebelumnya jika ini bukan thread pertama yang menulis di file.
   - looping `for` untuk mencetak 1-3 dan menuliskan thread yang mana yang sedang menuliskan.
   - `fflush(file)` untuk memastikan data segera ditulis ke disk.
   - `sleep(1)` membuat jeda 1 detik antara setiap penulisan (untuk simulasi lambat dan agar urutan lebih jelas terlihat).
   - mentutup file kembali dengan `fclose`.
   - melepaskan thread ini agar thread lain bisa menulis dengan `pthread_mutex_unlock(&lock)`.
3.  Fungsi `main`
    - `pthread_t threads[THREAD_COUNT];` mempersiapkan 5 thread sesuai dengan `MAX_THREADS`.
    - `int thread_ids[THREAD_COUNT]` untuk menandakan thread dengan id yang akan digunakan saat print di file.
    - `pthread_mutex_init(&lock, NULL)` meng-inisialisasi mutex sebelum digunakan.
    - looping `pthread_create(&threads[i], NULL, count_and_log, &thread_ids[i])` untuk membuat 5 thread dan menandakan setiap thread dengan id, kemudian menjalankan fungsi `count_and_log`.
    - looping `pthread_join(threads[i], NULL)` untuk menunggu semua thread selesai menjalankan tugasnya.
    - Membersihkan mutex setelah selesai dengan `pthread_mutex_destroy(&lock)`.


## Output
#### **Hasil:**

1. contoh hasil `count.txt`
   ```
   thread 3 count 1
   thread 3 count 2
   thread 3 count 3
   thread 1 count 1
   ...
   thread 5 count 3
   ```

#### **Penjelasan Hasil:**
- Setiap thread melakukan counting dari 1 hingga 3 dan menuliskannya ke file log.txt.
- Karena digunakan pthread_mutex, maka:
  - Hanya satu thread yang dapat menulis ke file pada satu waktu (critical section).
  - Oleh karena itu, output dari setiap thread tidak akan tumpang tindih dengan thread lain.
- Fungsi sleep(1) digunakan untuk memberikan jeda antar penulisan agar lebih mudah melihat perbedaan antar thread.
- Urutan thread dalam file bisa berbeda setiap kali program dijalankan karena eksekusi thread ditentukan oleh penjadwalan OS, namun isi setiap blok tetap konsisten.

#### **Screenshoot Output:**
1. `log.txt`
<div align="center">
  <img src="https://drive.google.com/uc?export=view&id=1klXuR3AWketHV4G_YNkgcIamLfR3jO6A" width="600"/>
</div>

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

---

## Kode 4a
#### `sender.c`
```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sys/ipc.h>
#include <sys/shm.h>

int main() {
    key_t key = 1234;
    int shmid = shmget(key, 1024, IPC_CREAT | 0666);

    char *data = (char *) shmat(shmid, NULL, 0);

    strcpy(data, "aku lagi belajar ipc");

    shmdt(data);

    return 0;
}
```

#### `receiver.c`
```
#include <stdio.h>
#include <stdlib.h>
#include <sys/ipc.h>
#include <sys/shm.h>

int main() {
    key_t key = 1234;
    int shmid = shmget(key, 1024, 0666);

    char *data = (char *) shmat(shmid, NULL, 0);

    printf("%s\n", data);

    shmdt(data);
    shmctl(shmid, IPC_RMID, NULL);

    return 0;
}
```

#### **Penjelasan Kode:**
1. `sender.c`
   - `key_t key = 1234` : Menetapkan kunci unik untuk shared memory.
   - `shmget(...)` untuk membuat atau mendapatkan shared memory `IPC_CREAT` dengan ukuran 1024 byte dengan izin `0666`.
   - Menempelkan shared memory ke alamat proses saat ini dan mengembalikan pointer-nya dengan `char *data = (char *) shmat(shmid, NULL, 0)`.
   - Menyalin string `"aku lagi belajar ipc"` ke dalam shared memory menggunakan pointer `data` dengan `strcpy`.
   - `shmdt(data)` untuk melepaskan (detach) shared memory dari alamat proses, tidak menghapus shared memory-nya dari sistem.
2. `receiver.c`
   - Mengakses shared memory yang telah dibuat oleh `sender.c` menggunakan `key = 1234` dan ukuran yang sama (1024) dengan `shmget`.
   - `char *data = (char *) shmat(shmid, NULL, 0)` untuk menempelkan shared memory ke proses `receiver`.
   - Mencetak isi shared memory dengan `printf`
   - Melepaskan shared memory dari proses `receiver` dengan `shmdt(data)`.
   - `shmctl(..., IPC_RMID, NULL)` untuk menghapus shared memory dari sistem.
  
## Output
#### **Hasil:**

```
aku lagi belajar ipc
```

#### **Penjelasan Hasil:**
- Shared memory digunakan sebagai media komunikasi antara dua proses (`sender` dan `receiver`).
- Karena kedua program menggunakan `key_t key = 1234` dan ukuran memori yang sama (1024 byte), mereka mengakses segmen memori yang sama.
- `sender.c` menulis pesan ke dalam shared memory.
- `receiver.c` membaca pesan dari shared memory, lalu menampilkannya ke layar.
- Setelah membaca, `receiver.c` juga menghapus shared memory dari sistem dengan `shmctl(..., IPC_RMID, NULL);`, agar tidak menumpuk di memori.

#### **Screenshoot Output:**
<div align="center">
  <img src="https://drive.google.com/uc?export=view&id=1jLnBF5sKxKLhrb04f_60fj8Xnu2O0dxf" width="600"/>
</div>

---

## Kode 4b
#### `sender.c`
```
#include <stdio.h>
#include <sys/ipc.h>
#include <sys/msg.h>
#include <string.h>

#define MAX 100

struct mesg_buffer {
    long mesg_type;
    char mesg_text[MAX];
};

int main() {
    key_t key;
    int msgid;
    struct mesg_buffer message;

    key = ftok("progfile", 65);

    msgid = msgget(key, 0666 | IPC_CREAT);

    message.mesg_type = 1;
    strcpy(message.mesg_text, "yah belajar ipc mulu");

    msgsnd(msgid, &message, sizeof(message.mesg_text), 0);

    printf("Data yang dikirim: %s\n", message.mesg_text);

    return 0;
}
```

#### `receiver.c`
```
#include <stdio.h>
#include <sys/ipc.h>
#include <sys/msg.h>

#define MAX 100

struct mesg_buffer {
    long mesg_type;
    char mesg_text[MAX];
};

int main() {
    key_t key;
    int msgid;
    struct mesg_buffer message;

    key = ftok("progfile", 65);

    msgid = msgget(key, 0666 | IPC_CREAT);

    msgrcv(msgid, &message, sizeof(message.mesg_text), 1, 0);

    printf("Data yang diterima: %s\n", message.mesg_text);

    msgctl(msgid, IPC_RMID, NULL);

    return 0;
}

```

#### **Penjelasan Kode:**
1. `sender.c`
   - Membuat struct `struct mesg_buffer`. `long mesg_type` untuk mengelompokkan atau membedakan pesan di dalam satu message queue. `char mesg_text[100]` untuk menyimpan isi pesan.
   - `key = ftok("progfile", 65)` : Membuat key unik menggunakan `ftok`.
   - `msgid = msgget(key, 0666 | IPC_CREAT)` : Membuat atau mengakses message queue berdasarkan key.
   - `message.mesg_type = 1; strcpy(message.mesg_text, "yah belajar ipc mulu");` : Menentukan jenis pesan (`mesg_type`) dan mengisi isi pesan (`mesg_text`). Jika belum ada, maka queue akan dibuat dengan permission `0666`.
   - `msgsnd(msgid, &message, sizeof(message.mesg_text), 0)` : Mengirimkan pesan ke message queue.
   - `printf("Data yang dikirim: %s\n", message.mesg_text)` : Menampilkan pesan yang dikirim.
2. `receiver.c`
   - struct yang sama dengan di `sender.c`.
   - `key = ftok("progfile", 65)` : Membuat key unik menggunakan `ftok` yang sama dengan `sender`.
   - `msgid = msgget(key, 0666 | IPC_CREAT)` : Membuat atau mengakses message queue berdasarkan key.
   - `msgrcv(msgid, &message, sizeof(message.mesg_text), 1, 0)` : Menerima pesan dengan `mesg_type = 1`. Pesan disimpan ke dalam struktur `message`.
   - `printf("Data yang dikirim: %s\n", message.mesg_text)` : Menampilkan isi pesan.
   - `msgctl(msgid, IPC_RMID, NULL)` : Menghapus message queue dari sistem setelah pesan diterima, agar tidak menumpuk di memori.
  
## Output
#### **Hasil:**

```
Data yang dikirim: yah belajar ipc mulu
Data yang diterima: yah belajar ipc mulu
```

#### **Penjelasan Hasil:**

Output menunjukkan bahwa pesan berhasil dikirim dari satu proses (sender) ke proses lainnya (receiver) menggunakan message queue. Proses receiver menerima pesan yang persis sama seperti yang dikirim oleh sender, menunjukkan bahwa IPC berhasil dilakukan dengan benar.

Jika program berjalan seperti yang diharapkan, maka message queue bekerja sebagai media komunikasi antar proses secara efektif di sistem operasi.

#### **Screenshoot Output:**
<div align="center">
  <img src="https://drive.google.com/uc?export=view&id=16ZCOSL5r2G6po4q3Y3DCYX1tlOXajfAl" width="600"/>
</div>
