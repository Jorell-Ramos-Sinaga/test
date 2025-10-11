
[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/1niUih_B)
| Name           | NRP        | Kelas     |
| ---            | ---        | ----------|
| Jorell Ramos Sinaga | 5025241202 | A |



## Put your topology config image here!

![](https://drive.google.com/uc?export=view&id=1VAl_rY4aFUvBTWhZbjbaL9eb078Dej6c)

## Put your GNS3 Project file here!



<br>

## Soal 1

> Dokumentasikan hasil pengelompokan subnet yang telah dibuat.

> _Document the results of the subnet grouping that has been created._

**Answer:**

- Screenshot

  ![](https://drive.google.com/uc?export=view&id=1piiDz7G9Zypeu78LKe14eHnNYcxmSLPH)
  
- Explanation

  Setiap subnet dipisah oleh router. Node-node yang dalam lingkaran adalah suatu subnet sendiri.

  Ini pembagian IP setiap subnet sementara :
  ```
  #Kompleks Jalanan Kiri : 10.64.1.X
  eth0 BlackPanther : 10.64.1.1
  eth1 IronMan : 10.64.1.2
  
  #Kompleks Jalanan Kanan : 10.64.2.X
  eth2 IronMan : 10.64.2.1
  eth0 BlackWidow : 10.64.2.2
  
  # Kompleks Switch 1 : 10.64.3.X
  eth1 BlackPanther : 10.64.3.1
  CaptainAmerica : 10.64.3.2
  Falcon : 10.64.3.3
  
  #Kompleks Switch 2: 10.64.4.X
  eth2 BlackPanther : 10.64.4.1
  WinterSoldier : 10.64.4.2
  Hawkeye : 10.64.4.3
  
  #Kompleks Switch 3 : 10.64.5.X
  eth2 BlackWidow : 10.64.5.1
  ScarletWitch : 10.64.5.2
  Thor : 10.64.5.3
  
  #Kompleks Switch 4 : 10.64.6.X
  eth1 BlackWidow : 10.64.6.1
  eth0 Vision : 10.64.6.2
  Hulk : 10.64.6.3
  
  #Kompleks Switch 5 : 10.64.7.X
  eth1 Vision : 10.64.7.1
  SpiderMan : 10.64.7.2
  DoctorStrange : 10.64.7.3
  ```

<br>

## Soal 2

> Lakukan konfigurasi routing agar setiap node dapat saling berkomunikasi. Pastikan setiap router dapat mengirimkan paket ke jaringan lain melalui tabel routing yang sesuai. Sertakan bukti bahwa Falcon bisa melakukan ping ke SpiderMan, DoctorStrange, dan ScarletWitch.

> _Configure routing so that each node can communicate with each other. Ensure each router can forward packets to other networks through the appropriate routing table. Include proof that Falcon can ping SpiderMan, Doctor Strange, and ScarletWitch._

**Answer:**

- Screenshot

  ![](https://drive.google.com/uc?export=view&id=1UNMuWyoIzHN0cTGDhB8h56FHl0hawzkM)
  
- Explanation

  Mengkonfigurasi static routing di setiap router, tambahkan di file config masing-masing router :

  ```
  #BlackPanther
  ip route add 10.64.2.0/24 via 10.64.1.2
  ip route add 10.64.5.0/24 via 10.64.1.2
  ip route add 10.64.6.0/24 via 10.64.1.2
  ip route add 10.64.7.0/24 via 10.64.1.2
  
  #IronMan
  ip route add 10.64.3.0/24 via 10.64.1.1
  ip route add 10.64.4.0/24 via 10.64.1.1
  ip route add 10.64.5.0/24 via 10.64.2.2
  ip route add 10.64.6.0/24 via 10.64.2.2
  ip route add 10.64.7.0/24 via 10.64.2.2
  
  #BlackWidow
  ip route add 10.64.1.0/24 via 10.64.2.1
  ip route add 10.64.3.0/24 via 10.64.2.1
  ip route add 10.64.4.0/24 via 10.64.2.1
  ip route add 10.64.7.0/24 via 10.64.6.2
  
  #Vision
  ip route add 10.64.1.0/24 via 10.64.6.1
  ip route add 10.64.2.0/24 via 10.64.6.1
  ip route add 10.64.3.0/24 via 10.64.6.1
  ip route add 10.64.4.0/24 via 10.64.6.1
  ip route add 10.64.5.0/24 via 10.64.6.1
  ```

  _Assign_ IP ke client dan server masing-masing. Juga memberikan _default route_ dalam kasus IP yang ditangani tidak termasuk dalam setting routing sebelumnya :
  ```
  ip addr add [IP client/server]/24 dev eth0 
  ip route add default via [IP router terdekat] dev eth0 
  ```

  Kemudian, melakukan ping dari **_Falcon_** ke **_Spiderman_**, **_DoctorStrange_** dan **_ScarletWitch_**.

<br>

## Soal 3

> Lakukan konfigurasi agar semua node dapat terhubung ke internet. Sertakan hasil uji coba dengan melakukan ping ke google.com dari node Falcon, CaptainAmerica, SpiderMan, dan Thor.

> _Configure all nodes to connect to the internet. Include test results by pinging google.com from the Falcon, CaptainAmerica, SpiderMan, and Thor nodes._

**Answer:**

- Screenshot

  ![](https://drive.google.com/uc?export=view&id=1Ejb-b5I8_27s1hY_RKEVE9-W22ZbJNxh)
  
- Explanation

  Menambahkan default gateway ke internet/NAT di router Ironman agar semua yang diarahkan lewat IronMan yang prefix IP nya tidak ada di routing, diarahkan ke NAT1 (Internet).

  ```
  ip route add default via 192.168.122.1 dev eth0
  ```

  Konfigurasi di router yang terhubung ke NAT (IronMan). Ini untuk mengizinkan node di dalam jaringan lokal (LAN) agar bisa mengakses internet lewat router ini, walaupun mereka punya IP privat.

  ```
  iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
  ```
  
  Konfigurasi _IP Forwarding_ di setiap router pada `/etc/sysctl.conf`.

  ```
  net.ipv4.ip_forward=1
  ```

  Menambahkan DNS di Semua Node. Ini agar bisa `ping google.com` bukan `ping 8.8.8.8`.

  ```
  echo "nameserver 8.8.8.8" > /etc/resolv.conf
  ```

<br>

## Soal 4

> Berikan Falcon alamat IP dalam rentang [Prefix IP].3.20 - [Prefix IP].3.25
> <br> </br>
> Berikan Hawkeye alamat IP dalam rentang [Prefix IP].4.30 - [Prefix IP].4.35
> <br> </br>
> Berikan Hulk alamat IP dalam rentang [Prefix IP].6.50 - [Prefix IP].6.55

<br>

> _Give Falcon an IP address in the range [IP Prefix].3.20 - [IP Prefix].4.35_
> <br> </br>
> _Give Hawkeye an IP address in the range [IP Prefix].4.30 - [IP Prefix].4.35_
> <br> </br>
> _Give Hulk an IP address in the range [IP Prefix].6.50 - [IP Prefix].6.55_

**Answer:**

- Screenshot

  `Put your screenshot in here`

- Explanation

  `Put your explanation in here`

<br>

## Soal 5

> Berikan ScarletWitch dan Thor alamat IP dalam rentang [Prefix IP].5.40 - [Prefix IP].5.45 dan [Prefix IP].5.100 - [Prefix IP].5.105

> _Give ScarletWitch and Thor IP addresses in the range [IP Prefix].5.40 - [IP Prefix].5.45 and [IP Prefix].5.100 - [IP Prefix].5.105_

**Answer:**

- Screenshot

  `Put your screenshot in here`

- Explanation

  `Put your explanation in here`

<br>

## Soal 6

> Berikan SpiderMan dan DoctorStrange alamat IP dalam rentang [Prefix IP].7.60 - [Prefix IP].7.65  dan [Prefix IP].7.110 - [Prefix IP].7.115

> _Give SpiderMan and DoctorStrange IP addresses in the ranges [IP Prefix].7.60 - [IP Prefix].7.65 and [IP Prefix].7.110 - [IP Prefix].7.115_

**Answer:**

- Screenshot

  `Put your screenshot in here`

- Explanation

  `Put your explanation in here`

<br>

## Soal 7

> Tetapkan waktu peminjaman alamat IP pada DHCP server untuk client yang terhubung melalui Switch 2 selama 5 menit (Default), dan untuk client melalui Switch 5 selama 10 menit (Default). Tetapkan juga batas waktu peminjaman maksimal selama 2 jam.
> <br> </br>
> Tetapkan waktu peminjaman alamat IP pada DHCP server untuk client yang terhubung melalui Switch 1 dan Switch 3 selama 2 menit (Default). Tetapkan juga batas waktu peminjaman maksimal selama 100 menit.

<br>

> _Set the IP address lease period on the DHCP server for clients connected through Switch 2 to 5 minutes (default), and for clients connected through Switch 5 to 10 minutes (default). Also, set the maximum lease period to 2 hours._
> <br> </br>
> _Set the IP address lease time on the DHCP server for clients connected via Switch 1 and Switch 3 to 2 minutes (default). Also set the maximum lease time limit to 100 minutes._

**Answer:**

- Screenshot

  `Put your screenshot in here`

- Explanation

  `Put your explanation in here`

<br>

## Soal 8

> Ubah konfigurasi DHCP Server agar Hawkeye, Thor, dan SpiderMan mendapatkan IP statis dengan [Prefix IP].x.5, namun masih menggunakan DHCP.

> _Change the DHCP Server configuration so that Hawkeye, Thor, and SpiderMan get static IPs with [Prefix IP].x.5, but still use DHCP._

**Answer:**

- Screenshot

  `Put your screenshot in here`

- Explanation

  `Put your explanation in here`

<br>

## Soal 9

> Buatlah konfigurasi DHCP Failover dengan WinterSoldier sebagai DHCP server backup untuk CaptainAmerica.

> _Create a DHCP Failover configuration with WinterSoldier as the backup DHCP server for CaptainAmerica._

**Answer:**

- Screenshot

  `Put your screenshot in here`

- Explanation

  `Put your explanation in here`

<br>

## Soal 10

> Buatlah konfigurasi agar CaptainAmerica dan WinterSoldier berjalan dengan mode Load Balancing.

> _Create a configuration so that CaptainAmerica and WinterSoldier run in Load Balancing mode._

**Answer:**

- Screenshot

  `Put your screenshot in here`

- Explanation

  `Put your explanation in here`

<br>
  
## Problems

## Revisions (if any)
