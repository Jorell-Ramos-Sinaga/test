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

  ![](https://drive.google.com/uc?export=view&id=1fJAeexuvVmRvA6sbMDnmASakZ-A5JgnG)
  
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

  ![](https://drive.google.com/uc?export=view&id=1WkLsWqCfv9NehE1La21QL_ZwclfTPHzu)
  ![](https://drive.google.com/uc?export=view&id=1GF7C-dkA8KM19u4tWQHLjuKUAJ8CpjlP)
  
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

  ![](https://drive.google.com/uc?export=view&id=1dHS7_NQVC79p6R_5aV7Q_SRR75dgirpv)
  
  <br>
  <br>

> d. Ada berapa banyak packet dengan protokol TCP murni yang terekam pada traffic (tanpa data)?

> _d. How many packets with pure TCP protocol are recorded in the traffic (without data)?_

**Answer:** `3223`

- Filter expression

  `tcp.len == 0`

- Explanation

  Mencari `tcp` yang `length`-nya 0, karena itu menandakan bahwa paket itu tidak ada data. Melihat hasil display di status bar bawah Wireshark dan **tambahkan 1.**

- Output result
  
  ![](https://drive.google.com/uc?export=view&id=1pJJoMypvImdnYXObwmJTSYQTje08aTp6)

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

  ![](https://drive.google.com/uc?export=view&id=1qepXuCVqZoUHgetlhzdnmZomfOdMGYXC)

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

  ![](https://drive.google.com/uc?export=view&id=1sjbnkU5tGEgo5FF7KCti0GkhWdeFrl11)
  ![](https://drive.google.com/uc?export=view&id=1PMHFem59Z81_IchU-lRsKgpd7kA3tblN)

  <br>
  <br>

> c. Berapa banyak packet berhasil yang berbasis murni TCP dan memiliki flag selain hanya [ACK]?

> _c. How many packets succeed that are pure TCP based and contain flags other than just [ACK] flag?_

**Answer:** `49`

- Filter expression

  `tcp.len == 0 && !(tcp.flags == 0x10)`

- Explanation

  Menggunakan `tcp.len == 0` sebelumnya untuk TCP murni **AND** (`&&`) `!(tcp.flags == 0x10)` yang berarti ini kebalikan dari pertanyaan sebelumnya dengan mencari tcp yang **bukan hanya** memiliki flag [ACK]. Hasil _displayed_ **ditambah 1**.

- Output result

  ![](https://drive.google.com/uc?export=view&id=1aulqB_8mkSi1VWnz0yj9ad0kuEAIFWzw)

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

  `put your output result here`

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

  `put your output result here`

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

  `put your output result here`

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

  `put your output result here`

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

  `put your output result here`

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

  `put your output result here`

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

  `put your output result here`

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

  `http.request` untuk menunjukkan packet request dan `http.response` untuk menunjukkan packet respons. Menggunakkan operator OR agar gabungan dari dua-duanya bisa muncul.

- Output result

  `put your output result here`

  <br>
  <br>

> b. Ada berapa HTTP packet yang berupa response?

> _b. How many response HTTP packets are recorded in the traffic?_

**Answer:** `149`

- Filter expression

  `http.response`

- Explanation

  Hanya mengeluarkan `http.request` dari pertanyaan sebelumnya agar yang diperlihatkan hanya packet respons.

- Output result

  `put your output result here`

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

  `put your output result here`

  <br>
  <br>

> d. Apa alamat IP dari client HTTP yang tersambung lokal dengan mesin lain?

> _d. What is the client HTTP IP Address in connection with other local machine?_

**Answer:** `172.16.16.101`

- Filter expression

  `http.request or http.response`

- Explanation

  Select salah satu packet di `http.request or http.response` dan melihat `Src : ...` di bagian Details.

- Output result

  `put your output result here`

  <br>
  <br>

## Task 6

- Flag

  `put your flag here`

> a. Apakah kamu menemukan fake flag? Tuliskan seluruhnya!

> _a. Did you find the fake flag? Write it whole!_

**Answer:** `put your answer here`

- Filter expression

  `put your filter here (if any)`

- Explanation

  `put your explanation here`

- Output result

  `put your output result here`

  <br>
  <br>

> b. Tuliskan username dan password yang tertulis! (format username:password)

> _b. Write the written username and password! (format username:password)_

**Answer:** `put your answer here`

- Filter expression

  `put your filter here (if any)`

- Explanation

  `put your explanation here`

- Output result

  `put your output result here`

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

  `put your output result here`

  <br>
  <br>

## Task 8

- Flag

  `JARKOM25{y0u_4r3_s0_G00d_1n_F0r3nsic_HH5G9QLYM54V6H6755MTIA2DAUUMW7x45y4n6obsze6i71kwivilnykvoaa7_de009d3c1d04818a4a089b721667311b}`

> a. Berapa banyak packet berbasis FTP yang terekam pada file pcapng? (with the data)

> _a. How many FTP packets are recorded in the pcapng file? (with the data)_

**Answer:** `put your answer here`

- Filter expression

  `put your filter here (if any)`

- Explanation

  `put your explanation here`

- Output result

  `put your output result here`

  <br>
  <br>

> b. Apa username dan password client di koneksi FTP? (tulis dalam format username:password)

> _b. What is the client's username and password in FTP connection? (write in following format username:password)_

**Answer:** `put your answer here`

- Filter expression

  `put your filter here (if any)`

- Explanation

  `put your explanation here`

- Output result

  `put your output result here`

  <br>
  <br>

> c. What is the client's command for showing server directory that was sent on request packet?

> _c. Apa command client untuk melihat direktori server yang dikirimkan dalam request packet?_

**Answer:** `put your answer here`

- Filter expression

  `put your filter here (if any)`

- Explanation

  `put your explanation here`

- Output result

  `put your output result here`

  <br>
  <br>

## Task 9

- Flag

  `put your flag here`

> a. Apa alamat IP dari FTP server?

> _a. What is the FTP server IP Address?_

**Answer:** `put your answer here`

- Filter expression

  `put your filter here (if any)`

- Explanation

  `put your explanation here`

- Output result

  `put your output result here`

  <br>
  <br>

> b. Berapa banyak file yang ada dalam direktori FTP server?

> _b. How many files are there inside the FTP server directory?_

**Answer:** `put your answer here`

- Filter expression

  `put your filter here (if any)`

- Explanation

  `put your explanation here`

- Output result

  `put your output result here`

  <br>
  <br>

> c. Apa nama dari file yang digunakan dalam page.html? (tulis lengkap namanya beserta ekstensinya dan dipisahkan dengan koma ',')

> _c. What are the filenames used in the page.html? (write the filebames with their extensions and separate them with comma ',')_

**Answer:** `put your answer here`

- Filter expression

  `put your filter here (if any)`

- Explanation

  `put your explanation here`

- Output result

  `put your output result here`

  <br>
  <br>

## Task 10

- Flag

  `put your flag here`

> a. Apa nama file yang mengandung string terencode?

> _a. What is the filename that contains encoded string?_

**Answer:** `put your answer here`

- Filter expression

  `put your filter here (if any)`

- Explanation

  `put your explanation here`

- Output result

  `put your output result here`

  <br>
  <br>

> b. Apa nama file hasil copy file sebelumnya?

> _b. What is the filename of the previous file copy?_

**Answer:** `put your answer here`

- Filter expression

  `put your filter here (if any)`

- Explanation

  `put your explanation here`

- Output result

  `put your output result here`

  <br>
  <br>

> c. What is the decoded string from the previous file?

> _c. Apa decoded string dari file tersebut?_

**Answer:** `put your answer here`

- Filter expression

  `put your filter here (if any)`

- Explanation

  `put your explanation here`

- Output result

  `put your output result here`

  <br>
  <br>

## Summary

## Problems
