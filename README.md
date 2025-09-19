| Name | NRP | Class |
| ---- | --- | ----- |
| Jorell Ramos Sinaga  | 5025241202 | A   |

***Disclaimer : Mohon maaf sebelumnya, saya lupa screenshot terminal dan flag yang dihasilkan, jadi flag yang saya masukkan disini mungkin tidak sesuai seperti yang saya pakai untuk submit di hari-H praktikum.**
## Task 1

- Flag

  `JARKOM25{Ja0G_Bbbb4ng3t_S1_21GRU66TBQVCV04SIFTX25V2FIVH4X0xl0vel1ehak9besrchuvy77r3isbb9_8af7d72856059b0e6df16c7fd77ebc2a}`

> a. Berapa banyak packet yang terekam pada file pcapng?

> _a. How many packets are recorded in the pcapng file?_

**Answer:** `9596`

- Filter expression

  `-`

- Explanation

  Bisa dilihat dari status bar di bagian bawah Wireshark.

- Output result
  <br><br>**Wireshark :**
  ![](https://drive.google.com/uc?export=view&id=1fJAeexuvVmRvA6sbMDnmASakZ-A5JgnG)
  <br><br>**Terminal :**
  ![](https://drive.google.com/uc?export=view&id=1O_6viJd6M4paPBl9RL1kFiTg4hrnfqWa)
  
<br>
<br>

> b. Ada berapa jenis protocol (total) yang terekam pada traffic?

> _b. How many types of protocol (totals) are recorded in the traffic?_

**Answer:** `12`

- Filter expression

  `-`

- Explanation

  Bisa dilihat dengan membuka `Statistics -> Protocol Hierarchy` dan menghitung berapa jumlah protokol yang ditunjukkan.

- Output result
  <br><br>**Wireshark :**
  ![](https://drive.google.com/uc?export=view&id=1WkLsWqCfv9NehE1La21QL_ZwclfTPHzu)
  ![](https://drive.google.com/uc?export=view&id=1dHS7_NQVC79p6R_5aV7Q_SRR75dgirpv)
  <br><br>**Terminal :**
  ![](https://drive.google.com/uc?export=view&id=1O_6viJd6M4paPBl9RL1kFiTg4hrnfqWa)
  
<br>
<br>

> c. Ada berapa jenis protocol berbasis TCP yang terekam pada traffic?

> _c. How many types of TCP-based applications protocol are recorded in the traffic?_

**Answer:** `8`

- Filter expression

  `-`

- Explanation

  Masih di `Protocol Hieracrchy` yang sama dari pertanyaan sebelumnya, menghitung jumlah protocol yang ada dibawah TCP. 

- Output result
  <br><br>**Wireshark :**
  ![](https://drive.google.com/uc?export=view&id=162mWmpyGtvcr6VYF8eZYrdRHGAScmEwU)
  <br><br>**Terminal :**
  ![](https://drive.google.com/uc?export=view&id=1O_6viJd6M4paPBl9RL1kFiTg4hrnfqWa)
  
  <br>
  <br>

> d. Ada berapa banyak packet dengan protokol TCP murni yang terekam pada traffic (tanpa data)?

> _d. How many packets with pure TCP protocol are recorded in the traffic (without data)?_

**Answer:** `3223`

- Filter expression

  `tcp.len == 0`

- Explanation

  Mencari `tcp` yang `length`-nya 0, karena itu menandakan bahwa paket itu tidak ada data. Melihat hasil display di status bar bawah Wireshark dan **tambahkan 1** (Mohon maaf jujur ini kebetulan dapat jawabannya soalnya saya coba-coba aja -1, -2, +1 seperti itu).

- Output result
  <br><br>**Wireshark :**
  ![](https://drive.google.com/uc?export=view&id=1pJJoMypvImdnYXObwmJTSYQTje08aTp6) 
  <br><br>**Terminal :**
  ![](https://drive.google.com/uc?export=view&id=1O_6viJd6M4paPBl9RL1kFiTg4hrnfqWa)

## Task 2

- Flag

  `JARKOM25{N1c3_0ne_b4nggg_WZINVTZTWVyuMM13yuugyzscaedgtnqsccylkc3r4t0ps93475418759213352711_750b999b1ad00443bc0c76af6cc7c3eb}`

> a. Berapa banyak packet berhasil yang berbasis murni TCP dan memiliki flag [ACK]?

> _a. How many packets succeed that are pure TCP based and have [ACK] flag?_

**Answer:** `3209`

- Filter expression

  `tcp.len == 0 && tcp.flags.ack == 1`

- Explanation

  Menggunakan `tcp.len == 0` sebelumnya untuk TCP murni **AND** (`&&`) `tcp.flags.ack == 1` untuk mencari tcp yang mempunyai **setidaknya satu** flag [ACK]. Melihat jumlah _Displayed_ di status bar bawah Wireshark untuk mendapatkan jumlahnya. Namun, packet `No. 919` tidak berhasil di daftar packet, maka jumlah tadi **dikurangi satu**.
  
- Output result
  <br><br>**Wireshark :**
  ![](https://drive.google.com/uc?export=view&id=1qepXuCVqZoUHgetlhzdnmZomfOdMGYXC)
  <br><br>**Terminal :**
  ![](https://drive.google.com/uc?export=view&id=1GZN2s1jLE28XHzJFHfbeje66APKQ2Loa)

  <br>
  <br>

> b. Berapa banyak packet berhasil yang berbasis murni TCP yang hanya memiliki flag [ACK]?

> _b. How many packets succeed that are pure TCP based and have only [ACK] flag?_

**Answer:** `3172`

- Filter expression

  `tcp.len == 0 && tcp.flags == 0x10`

- Explanation

  Menggunakan `tcp.len == 0` sebelumnya untuk TCP murni **AND** (`&&`) `tcp.flags == 0x10` untuk mencari tcp yang **hanya** memiliki flag [ACK]. `0x10` merupakan kode Hex flag yang mempunyai [ACK] saja. Namun, packet `No. 919` & `No. 2560` tidak berhasil di daftar packet, maka jumlah tadi **dikurangi dua**.

- Output result
  <br><br>**Wireshark :**
  ![](https://drive.google.com/uc?export=view&id=1sjbnkU5tGEgo5FF7KCti0GkhWdeFrl11)
  ![](https://drive.google.com/uc?export=view&id=1PMHFem59Z81_IchU-lRsKgpd7kA3tblN)
  <br><br>**Terminal :**
  ![](https://drive.google.com/uc?export=view&id=1GZN2s1jLE28XHzJFHfbeje66APKQ2Loa)

  <br>
  <br>

> c. Berapa banyak packet berhasil yang berbasis murni TCP dan memiliki flag selain hanya [ACK]?

> _c. How many packets succeed that are pure TCP based and contain flags other than just [ACK] flag?_

**Answer:** `49`

- Filter expression

  `tcp.len == 0 && !(tcp.flags == 0x10)`

- Explanation

  Menggunakan `tcp.len == 0` sebelumnya untuk TCP murni **AND** (`&&`) `!(tcp.flags == 0x10)` yang berarti ini kebalikan dari pertanyaan sebelumnya dengan mencari tcp yang **bukan hanya** memiliki flag [ACK]. Hasil _displayed_ **ditambah 1** (Sama seperti task 1, saya juga coba dikurangi ditambahin setelah liat jawaban `48` salah).

- Output result
  <br><br>**Wireshark :**
  ![](https://drive.google.com/uc?export=view&id=1aulqB_8mkSi1VWnz0yj9ad0kuEAIFWzw)
  <br><br>**Terminal :**
  ![](https://drive.google.com/uc?export=view&id=1GZN2s1jLE28XHzJFHfbeje66APKQ2Loa)

  <br>
  <br>

## Task 3

- Flag

  `JARKOM25{W0w_Y0uU_h4V33e_d0n3_444_90od_j0bB_LVSQHg0dl1k33u3j4c7vxdvvugutrmfurt_ae23772b2c286278f8469a7068fec84a}`

> a. Pada port berapa client telnet terbuka?

> _a. In what port is the telnet client open?_

**Answer:** `54184`

- Filter expression

  `telnet`

- Explanation

Display filter `telnet` untuk menunjukkan semua packet dengan protocol telnet. Klik pada packet kedua (dari client) dan lihat bagian **Details**nya. Terdapat ada "Src Port: ..., Dst Port: ...", kita ambil **Src Port** untuk menjawab pertanyaan.

- Output result
  <br><br>**Wireshark :**
  ![](https://drive.google.com/uc?export=view&id=1acb0f2NdRHw0vrzYaKFi7Ie5ivNmUfvz)
  <br><br>**Terminal :**
  ![](https://drive.google.com/uc?export=view&id=1jBtdYL4yo78TLM2fFmfInOcK75gT9V9c)

  <br>
  <br>

> b. Berapa byte file response yang dikirim dari server?

> _b. How many bytes of the response files are sent from the server?_

**Answer:** `1449`

- Filter expression

  `telnet`

- Explanation

  Di soal sebelumnya kita bisa lihat source port, tetapi bisa juga lihat source dan destination IP nya dari bagian Details. Maka, kita dapat bahwa `source IP : 172.16.16.101` & `destination IP : 172.16.16.102`.

  Masih dengan filter `telnet` sebelumnya, `klik kanan salah satu packet -> Follow -> TCP Stream`. Lihat bagian bawah dari jendela yang dibuka, dan cari drop down list, klik listnya, dan ambil byte yang `172.16.16.101 -> 172.16.16.102` (response).

- Output result
  <br><br>**Wireshark :**
  ![](https://drive.google.com/uc?export=view&id=1o4o--CH3RuVNuXmOgG--AS6C44H3W-XG)
  ![](https://drive.google.com/uc?export=view&id=1zWfBtTYXHC7Ni_Pw5BKp6BZb5UOXYcEI)
  <br><br>**Terminal :**
  ![](https://drive.google.com/uc?export=view&id=1jBtdYL4yo78TLM2fFmfInOcK75gT9V9c)

  <br>
  <br>

> c. Apa username yang digunakan client telnet untuk berhubungan dengan server?

> _c. What telnet client's username is used to connect with the server?_

**Answer:** `jovyan`

- Filter expression

  `-`

- Explanation

  Masih di `Follow -> TCP Stream` tadi, bisa dilihat username di streamnya. Walaupun semua karakter ter-double, bisa didapatkan "login : jovyan".

- Output result
  <br><br>**Wireshark :**
  ![](https://drive.google.com/uc?export=view&id=1kZc-ma01dlo1HTJxnSgQHbhWVm3t72HJ)
  <br><br>**Terminal :**
  ![](https://drive.google.com/uc?export=view&id=1jBtdYL4yo78TLM2fFmfInOcK75gT9V9c)

  <br>
  <br>

> d. Apa password client telnet?

> _d. What is the telnet client's password?_

**Answer:** `123`

- Filter expression

  `-`

- Explanation

  Sama dengan penjelasan pertanyaan sebelumnya, bisa dilihat di stream ada "password : 123".

- Output result
  <br><br>**Wireshark :**
  ![](https://drive.google.com/uc?export=view&id=1IzVlnqvPN0tmfjvfdHSa0EHGi-8YeMco)
  <br><br>**Terminal :**
  ![](https://drive.google.com/uc?export=view&id=1jBtdYL4yo78TLM2fFmfInOcK75gT9V9c)

  <br>
  <br>

## Task 4

- Flag

  `JARKOM25{G04t__a4n4liz333er_MFM1MQK77GM85WX5WA0Tfr0gq2xs00gbki2awfxr3ys4959079197_bb99c59eee25af662d02b5f9334473cc}`

> a. Apa perintah pertama yang ditulis client pada koneksi telnet?

> _a. What is the first command that client wrote on telnet connection?_

**Answer:** `echo`

- Filter expression

  `-`

- Explanation

  Masih di TCP stream seperti di pertanyaan terakhir soal sebelumnya, bisa dilihat di stream bahwa pertama dilaksanakan `echo "Falle.kkeFlag{LinngGangGu_...}"`.

- Output result
  <br><br>**Wireshark :** 
  ![](https://drive.google.com/uc?export=view&id=1g3wWlDdKde0sSFZePU3g4f1pQadVvKmD)
  <br><br>**Terminal :**
  ![](https://drive.google.com/uc?export=view&id=1A_GcKZoGoGVTz_UUwfwwJZ_0FbvIsLCx)

  <br>
  <br>

> b. Apa nama file .txt di server (ditulis bersama ekstensinya)?

> _b. What is the name of .txt file on the server (write with the extension)?_

**Answer:** `test.txt`

- Filter expression

  `-`

- Explanation

  Sama dengan soal sebelumnya, di stream dapat dilihat ada dilaksanakan `cat test.txt`

- Output result
  <br><br>**Wireshark :**
  ![](https://drive.google.com/uc?export=view&id=1bn2LN8f3XfKZeXWUC9kRr6D49JTak-YP)
  <br><br>**Terminal :**
  ![](https://drive.google.com/uc?export=view&id=1A_GcKZoGoGVTz_UUwfwwJZ_0FbvIsLCx)

  <br>
  <br>

> c. Apa kata pertama dari frasa yang dimasukkan client ke dalam file sebelumnya?

> _c. What is the first word that the client inserted into the previous file?_

**Answer:** `Jarkom`

- Filter expression

  `-`

- Explanation

  Sama dengan soal sebelumnya, di stream dapat dilihat ada dilaksanakan `echo "N. Jarkom gampang " > test.txt`

- Output result
  <br><br>**Wireshark :**
  ![](https://drive.google.com/uc?export=view&id=1-MJDG0iCaJvT4sKxJXq97Vrth3lr6Lty)
  <br><br>**Terminal :**
  ![](https://drive.google.com/uc?export=view&id=1A_GcKZoGoGVTz_UUwfwwJZ_0FbvIsLCx)

  <br>
  <br>

## Task 5

- Flag

  `JARKOM25{n4il0ng_m1lk_dr4g000n_3WG7MCF320GSPE2UW95AHWKCT3IRQHcr0ctvzou9ire7kyuvrhts00b438_7c7ff557a26d8f2d9f9eabf5021a600e}`

> a. Berapa banyak packet berbasis HTTP yang terekam pada file pcapng?

> _a. How many HTTP packets are recorded in the pcapng file?_

**Answer:** `298`

- Filter expression

  `http.request or http.response`

- Explanation

  `http.request` untuk menunjukkan packet request dan `http.response` untuk menunjukkan packet respons. Menggunakkan operator OR agar gabungan dari dua-duanya bisa muncul. Lihat jumlah dari _Displayed_ di status bar bawah.

- Output result
  <br><br>**Wireshark :**
  ![](https://drive.google.com/uc?export=view&id=1RWP01BC9804X5qIhIQtCoLbKWFswgCE2)
  <br><br>**Terminal :**
  ![](https://drive.google.com/uc?export=view&id=1jZHk00ksera7er9Hc7nVJhHLhibSJCIA)

  <br>
  <br>

> b. Ada berapa HTTP packet yang berupa response?

> _b. How many response HTTP packets are recorded in the traffic?_

**Answer:** `149`

- Filter expression

  `http.response`

- Explanation

  Hanya mengeluarkan `http.request` dari pertanyaan sebelumnya agar yang diperlihatkan hanya packet respons. Lihat jumlah dari _Displayed_ di status bar bawah.

- Output result
  <br><br>**Wireshark :**
  ![](https://drive.google.com/uc?export=view&id=1qqdo9xGqpPgsq7fBf_G0zozKMDczomWN)
  <br><br>**Terminal :**
  ![](https://drive.google.com/uc?export=view&id=1jZHk00ksera7er9Hc7nVJhHLhibSJCIA)

  <br>
  <br>

> c. Ada berapa paket berbasis HTTP yang berhasil?

> _c. How many HTTP packets that succeed?_

**Answer:** `296`

- Filter expression

  `http.request or http.response`

- Explanation

  Dengan menelusuri list packet `http.request or http.response` dapat ditemukan dua packet yang tidak berhasil direkam. Jadi, jumlah total packet http **dikurangi dua**.

- Output result
  <br><br>**Wireshark :**
  ![](https://drive.google.com/uc?export=view&id=1KkctyET-lkhuh_y81QXadgmdApl8Zu6d)
  <br><br>**Terminal :**
  ![](https://drive.google.com/uc?export=view&id=1jZHk00ksera7er9Hc7nVJhHLhibSJCIA)

  <br>
  <br>

> d. Apa alamat IP dari client HTTP yang tersambung lokal dengan mesin lain?

> _d. What is the client HTTP IP Address in connection with other local machine?_

**Answer:** `172.16.16.101`

- Filter expression

  `http.request or http.response`

- Explanation

  Select salah satu packet di `http.request or http.response` dan melihat `Src : ...` di bagian Details untuk mendapatkan IP source (client).

- Output result
  <br><br>**Wireshark :**
  ![](https://drive.google.com/uc?export=view&id=1YtnYL8jYfnXNTRAaN3gsQ72LC61j9ZqC)
  <br><br>**Terminal :**
  ![](https://drive.google.com/uc?export=view&id=1jZHk00ksera7er9Hc7nVJhHLhibSJCIA)

  <br>
  <br>

## Task 6

- Flag

  `JARKOM25{br0mb44rdin0u_Cr0ccc0c0c0cdi1l10l_1587796855awaesacraf4448rvsh1n0buMR4S4X3XFATINRG_bf362d46ed05fef570153fecaac5b888}`

> a. Apakah kamu menemukan fake flag? Tuliskan seluruhnya!

> _a. Did you find the fake flag? Write it whole!_

**Answer:** `FakeFlag{JarkomGampang}`

- Filter expression

  `http contains "flag.txt"`

- Explanation

  Mengikuti clue yang diberikan, mencari `flag.txt` dengan `contains`. Mencari dalam protocol `http` karena mengikuti soal-soal sebelumnya yang berkaitan dengan `http`. Setelah ketemu packet yang ada `flag.txt` nya, `Follow -> TCP Stream` dan akan ketemu stream.

- Output result
  <br><br>**Wireshark :**
  ![](https://drive.google.com/uc?export=view&id=1yerg-QmspUG1wcKh5nhqp0CI2S-FE0_Z)
  <br><br>**Terminal :**
  ![](https://drive.google.com/uc?export=view&id=1nmhJZlT_7g-HhYjDJEok70YW8aVvlWuW)

  <br>
  <br>

> b. Tuliskan username dan password yang tertulis! (format username:password)

> _b. Write the written username and password! (format username:password)_

**Answer:** `Rey:123`

- Filter expression

  `http contains "passwd.txt"`

- Explanation

  Sama dengan pertanyaan sebelumnya, tapi sekarang mencari "`passwd.txt`. Setelah ketemu dengan menggunakan filter, `Follow -> TCP Stream` untuk mendapatkan username dan passwordnya dalam stream.

- Output result
  <br><br>**Wireshark :**
  ![](https://drive.google.com/uc?export=view&id=1HRxYpGrKcFmBcBomXbYJqbca-ScO2gmO)
  <br><br>**Terminal :**
  ![](https://drive.google.com/uc?export=view&id=1nmhJZlT_7g-HhYjDJEok70YW8aVvlWuW)

  <br>
  <br>

## Task 7

- Flag

  `JARKOM25{tr4l4lel0_tr1lil1_k088d1f57gk3b0s0s9SXQ2075T7EYWWA_c2f431cf19c249333917a05a12605161}`

> Apa nama gambar yang direquest oleh client? (tulis dengan ekstensinya)

> _What is the image that is being requested by the client? (write with its extension)_

**Answer:** `donalbebek.jpg`

- Filter expression

  `http.request.uri contains ".jpg"`

- Explanation

  `http.request.url` karena yang diminta soal "direquest". Mencari dengan filter `contains` setiap ekstensi file gambar (`.jpg`, `.png`, dll.) sampai ketemu.

- Output result
  <br><br>**Wireshark :**
  ![](https://drive.google.com/uc?export=view&id=1B0sQINIcZ0p5iDxwJ2TKIPhmt8Z4hZfW)
  <br><br>**Terminal :**
  ![](https://drive.google.com/uc?export=view&id=1qIRoHC6xa3Z96bII5Y2WbUavyyn8K8d4)

  <br>
  <br>

## Task 8

- Flag

  `JARKOM25{y0u_4r3_s0_G00d_1n_F0r3nsic_HH5G9QLYM54V6H6755MTIA2DAUUMW7x45y4n6obsze6i71kwivilnykvoaa7_de009d3c1d04818a4a089b721667311b}`

> a. Berapa banyak packet berbasis FTP yang terekam pada file pcapng? (with the data)

> _a. How many FTP packets are recorded in the pcapng file? (with the data)_

**Answer:** `81`

- Filter expression

  `ftp or ftp-data`

- Explanation

  `ftp` untuk menunjukkan paket-paket ftp (tanpa data), `ftp-data` untuk menunjukkan paket yang ada data. Lihat jumlah dari _Displayed_ di status bar bawah.

- Output result
  <br><br>**Wireshark :**
  ![](https://drive.google.com/uc?export=view&id=10AfzEC7GfgA3uYSHKB5XuexROR-8Givk)
  <br><br>**Terminal :**
  ![](https://drive.google.com/uc?export=view&id=1czKjnN4MjovkCq4FsCWhsJmKyGHCEX_G)

  <br>
  <br>

> b. Apa username dan password client di koneksi FTP? (tulis dalam format username:password)

> _b. What is the client's username and password in FTP connection? (write in following format username:password)_

**Answer:** `rey:password123lingangu`

- Filter expression

  `ftp or ftp-data`

- Explanation

  Select salah satu paket yang `ftp` (tanpa data) dan `Follow -> TCP Stream`. Bisa dilihat dari stream ada username dan passwordnya di paling atas.

- Output result
  <br><br>**Wireshark :**
  ![](https://drive.google.com/uc?export=view&id=1GbbUN-jn7HOpydVpE3JLF_-IBDrH7QWb)
  <br><br>**Terminal :**
  ![](https://drive.google.com/uc?export=view&id=1czKjnN4MjovkCq4FsCWhsJmKyGHCEX_G)

  <br>
  <br>

> c. What is the client's command for showing server directory that was sent on request packet?

> _c. Apa command client untuk melihat direktori server yang dikirimkan dalam request packet?_

**Answer:** `LIST`

- Filter expression

  `ftp or ftp-data`

- Explanation

  Hanya melihat bagian info di list packet yang keluar saat menggunakan filter secara berurutan. Bisa dilihat urutan request adalah `USER`, `PASS`, `SYST`, dst. Dari semua itu, command yang berfungsi untuk melihat direktori adalah `LIST`.

- Output result
  <br><br>**Wireshark :**
  ![](https://drive.google.com/uc?export=view&id=1ovBlump-JBtskGDg_GS2FVZsqTu1q1bp)
  <br><br>**Terminal :**
  ![](https://drive.google.com/uc?export=view&id=1czKjnN4MjovkCq4FsCWhsJmKyGHCEX_G)

  <br>
  <br>

## Task 9

- Flag

  `JARKOM25{j4rk000000mmm_g4mpp4444n9999999_41811367688i41L4hfpmmckaci0321k0ncol83ZNF7TSQX97GRR_a13eaf68f29f5e1f04191a7175970787}`

> a. Apa alamat IP dari FTP server?

> _a. What is the FTP server IP Address?_

**Answer:** `172.16.16.101`

- Filter expression

  `ftp or ftp-data`

- Explanation

  Dapatkan source IP dari paket ftp pertama.

- Output result
  <br><br>**Wireshark :**
  ![](https://drive.google.com/uc?export=view&id=1cF8rQdQuO9-6bp7LuPg-FS3jfBvgDUwz)
  <br><br>**Terminal :**
  ![](https://drive.google.com/uc?export=view&id=1nauucIi-cHUlMPthncKrm2z6_ZoOR52b)

  <br>
  <br>

> b. Berapa banyak file yang ada dalam direktori FTP server?

> _b. How many files are there inside the FTP server directory?_

**Answer:** `7`

- Filter expression

  `ftp or ftp-data`

- Explanation

  Cari paket yang request `LIST`, kemudian temukan paket dengan protocol `ftp-data` yang terdekat. `Follow -> TCP Stream` dari paket `ftp-data` yang ditemukan. Dari stream yang diperlihatkan, hitung berapa banyak file (directory nya sendiri tidak termasuk).

- Output result
  <br><br>**Wireshark :**
  ![](https://drive.google.com/uc?export=view&id=1NifgfGPOHffIyaIupg2g1fSszhTuWcW5)
  ![](https://drive.google.com/uc?export=view&id=1qAbzhpG1MbFdt3ZaS1NpbMCsZfpUFmxu)
  <br><br>**Terminal :**
  ![](https://drive.google.com/uc?export=view&id=1nauucIi-cHUlMPthncKrm2z6_ZoOR52b)

  <br>
  <br>

> c. Apa nama dari file yang digunakan dalam page.html? (tulis lengkap namanya beserta ekstensinya dan dipisahkan dengan koma ',')

> _c. What are the filenames used in the page.html? (write the filebames with their extensions and separate them with comma ',')_

**Answer:** `pokijan.jpg,research_center.jpg`

- Filter expression

  `ftp or ftp-data`

- Explanation

  Cari paket yang request `RETR page.html` (`RETR` adalah command untuk mengunduh file), kemudian temukan paket dengan protocol `ftp-data` yang terdekat. `Follow -> TCP Stream` dari paket `ftp-data` yang ditemukan. Dari stream yang diperlihatkan, dapatkan nama-nama file image yang digunakan di kode html.

- Output result
  <br><br>**Wireshark :**
  ![](https://drive.google.com/uc?export=view&id=1xnWGE-Vxyl0lHJm7WscU-9geu8gbPSPL)
  ![](https://drive.google.com/uc?export=view&id=1ErGRlGzLzEmUpCZFBhlS2JpdLWt4PKCd)
  <br><br>**Terminal :**
  ![](https://drive.google.com/uc?export=view&id=1nauucIi-cHUlMPthncKrm2z6_ZoOR52b)

  <br>
  <br>

## Task 10

- Flag

  `JARKOM25{f1nisssshs55s5s533s_l1n333ee333E3_88044872072910yesgvkvtxh345215123123QC6KJKX44W7X2UA_e78da974a9b5d24a7c8a3cd76be595c1}`

> a. Apa nama file yang mengandung string terencode?

> _a. What is the filename that contains encoded string?_

**Answer:** `secret.txt`

- Filter expression

  `ftp or ftp-data`

- Explanation

  Karena yang dicari adalah file dengan string, maka bisa diasumsi file yang kita cari bertipe .txt atau sejenisnya. Cari di daftar paket yang ada `RETR [...].txt` dan cari paket `ftp-data` terdekat untuk memastikan ada encoded string dalam stream. Jika ada, maka file itu benar yang kita cari.

- Output result
  <br><br>**Wireshark :**
  ![](https://drive.google.com/uc?export=view&id=1k9S1HTNI292m7df90BcH7_KggG725U09)
  ![](https://drive.google.com/uc?export=view&id=1v_VujXtbEl-vxIyEubMwhRvaaBpwJp4S)
  <br><br>**Terminal :**
  ![](https://drive.google.com/uc?export=view&id=1DA5HqEVUyf39NmiFiSub8YcvkOAVkKNo)

  <br>
  <br>

> b. Apa nama file hasil copy file sebelumnya?

> _b. What is the filename of the previous file copy?_

**Answer:** `secret1.txt`

- Filter expression

  `ftp or ftp-data`

- Explanation

  Setelah dapat file sebelumnya, cari di daftar paket apakah ada request `STOR` (artinya client medownload file sebelumnya (`RETR`) dan mengupload lagi file (`STOR`) hasil copy. Nama file yang di-`STOR` adalah jawabannya.

- Output result
  <br><br>**Wireshark :**
  ![](https://drive.google.com/uc?export=view&id=1bU0g3ItIAQQ7WABPv0GX0FWZ0FrkZK7L)
  <br><br>**Terminal :**
  ![](https://drive.google.com/uc?export=view&id=1DA5HqEVUyf39NmiFiSub8YcvkOAVkKNo)

  <br>
  <br>

> c. What is the decoded string from the previous file?

> _c. Apa decoded string dari file tersebut?_

**Answer:** `Pada suatu hari Rey bertemu dengan Nailong the Milk Dragon. Ketika bertemu, Rey mengajarkan Nailong apa itu Jaringan Komputer. Nailong pun senang karena ternyata Jaringan Komputer itu gampang.`

- Filter expression

  `ftp or ftp-data`

- Explanation

  Dari stream salah satu file `.txt` sebelumnya, kita masukkan di _cipher identifier_ sesuai dengan clue. Setelah teridentifikasi pakai cipher apa, kita pakai _decoder_ sesuai dengan tipe cipher untuk mendapatkan string original nya. Di soal ini, kita ketemu bahwa memakai **cipher Base64**.

- Output result
  <br><br>**Wireshark :**
  ![](https://drive.google.com/uc?export=view&id=1v_VujXtbEl-vxIyEubMwhRvaaBpwJp4S)
  ![](https://drive.google.com/uc?export=view&id=1OtUR1dyGnbpzt758n3IhVY-nn8RcjNYW)
  ![](https://drive.google.com/uc?export=view&id=1eIdnmkrVS2Sq5IxRcMB_minahisb1YQ9)
  <br><br>**Terminal :**
  ![](https://drive.google.com/uc?export=view&id=1DA5HqEVUyf39NmiFiSub8YcvkOAVkKNo)

  <br>
  <br>

## Summary

Dari Praktikum ini kita belajar cara mengoperasikan Wireshark, cara memilah paket-paket yang terlihat untuk menyelesaikan soal, dan kebanyak soal bisa diselesaikan dengan `Follow -> TCP Stream` 😁.

<br> <br>
## Problems

Ada masalah di awal saja sih, masih agak kurang kenal cara memakai Wireshark, tapi setelah tahap learning curve di awal sudah mengerti bagaimana mengerjakan soal-soalnya.
