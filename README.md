# Jarkom-Modul-4-C13-2021

## Anggota Kelompok :

| Anggota              | NRP            |
| -------------------- | -------------- |
| M. Auliya Mirzaq R.  | 05111940000065 |
| M. Akmal Joedhiawan  | 05111940000125 |
| M. Arsyad Ardiansyah | 05111940000228 |

## Soal

![img](./img/topologi1.png)

Dengan menggunakan topologi jaringan di atas akan dilakukan perhitungan subnet dengan menggunakan 2 buah metode, yaitu VLSM (Variable Length Subnet Masking) dan CIDR (Classless Inter Domain Routing)

## CPT - VLSM

### Pembagian IP

Untuk pembagian subnet nya akan dibagi seperti gambar berikut :

![img](./img/vlsm.png)

Kemudian dengan pembagian subnet sesuai gambar tersebut, akan dilakukan penghitungan kebutuhan IP untuk tiap subnet nya. Hasilnya dapat dilihat pada tabel di bawah :

| Subnet    | Jumlah IP | Netmask |
| --------- | --------- | ------- |
| A1        | 101       | /25     |
| A2        | 2021      | /21     |
| A3        | 2         | /30     |
| A4        | 701       | /22     |
| A5        | 2         | /30     |
| A6        | 1001      | /22     |
| A7        | 2         | /30     |
| A8        | 521       | /22     |
| A9        | 502       | /23     |
| A10       | 13        | /28     |
| A11       | 2         | /30     |
| A12       | 252       | /24     |
| A13       | 721       | /22     |
| A14       | 2         | /30     |
| A15       | 2         | /30     |
| **TOTAL** | **5845**  | **/19** |

Berdasarkan total IP dan netmask yang dibutuhkan, maka kita dapat menggunakan netmask **/19** untuk memberikan pengalamatan pada subnet.

Setelah menghitung total IP yang dibutuhkan, subnet paling besar yang dibentuk memiliki NID **192.190.0.0** dan netmask **/19**. Dengan menggunakan NID dan netmask tersebut kita dapat menghitung pembagian alamat IP untuk tiap subnet pada gambar pohon pengalamatan dibawah.

![img](./img/vlsmtree.png)

Untuk dapat melihat lebih jelas pohon pengalamatannya, dapat juga diakses menggunakan link berikut: https://gitmind.com/app/doc/4ee6169070

Dari pohonn tersebut akan mendapat pembagian alamt IP untuk setiap subnet sebagai berikut:

![img](./img/vlsmip.png)

### Routing

Setelah melakukan penghitungan untuk pembagian alamat IP untuk tiap subnet. Selanjutnya kita akan melakukan routing pada topologi tersebut. Routing ini bertujuan agar tiap subnet dapat terhubung ke subnet lain dan juga agar bisa bertukar _packet_ antar subnetnya.

#### Mengatur IP setiap subnet

Pertama, masukkan alamat IP yang sudah dihitung sebelumnya ke setiap subnet dalam topologi.

Misalnya untuk mengatur alamt IP untuk subnet `A1`, pada subnet ini terdapat 2 _device_ yang perlu diatur yaitu `Router Pucci` dan `Client Jipangu`. Untuk subnet A1 memiliki NID `192.190.0.128`, maka dari itu kita dapat membagikan alamat IP pada subnet ini mulai dari `192.190.0.129`.

Untuk Router Pucci terhubung ke subnet A1 melalui interface `Fa0/1`. Jadi kita akan atur pada interface tersebut. Kita akan memberi IP pada `192.190.0.129` pada `Router Pucci` untuk interdace `Fa0/1`.

![img](./img/a1pucci.png)

Sedangkan untuk client `jipangu`, kita akan memberi IP `192.190.0.130`. Jangan lupa untuk mengisi Default Gateway nya dengan alamat milik router, yaitu `192.190.0.129`

![img](./img/a1jipangu.png)

Itu contoh mengatur IP untuk subnet `A1`. Untuk subnet yang lain menggunakan cara yang sama, hanya tinggal menyesuaikan range ip dan netmask nya.

Jika pembagian IP nya diringkas maka akan menjadi seperi ini :

```
//====A1===//
PUCCI Fa0/1
IP      : 192.190.0.129
Netmask : 255.255.255.128

JIPANGU Fa0
IP      : 192.190.0.130
Netmask : 255.255.255.128
Default Gateway : 192.190.0.129

//====A2===//
PUCCI Fa1/0
IP      : 192.190.24.1
Netmask : 255.255.248.0

COURTYARD Fa0
IP      : 192.190.24.3
Netmask : 255.255.248.0
Default Gateway : 192.190.24.1

CALMBELT Fa0
IP      : 192.190.24.2
Netmask : 255.255.248.0
Default Gateway : 192.190.24.1

//====A3===//
PUCCI Fa0/1
IP      : 192.190.0.2
Netmask : 255.255.255.252

WATER7 Fa0/1
IP      : 192.190.0.1
Netmask : 255.255.255.252

//====A4===//
WATER7 Fa1/0
IP      : 192.190.12.1
Netmask : 255.255.252.0

CHIPER Fa0
IP      : 192.190.12.2
Netmask : 255.255.252.0
Default Gateway : 192.190.12.1

//====A5===//
WATER7 Fa0/0
IP      : 192.190.0.6
Netmask : 255.255.255.252

FOOSHA Fa1/0
IP      : 192.190.0.5
Netmask : 255.255.255.252

//====A6===//
FOOSHA Fa0/0
IP      : 192.190.16.1
Netmask : 255.255.252.0

BLUENO Fa0
IP      : 192.190.16.2
Netmask : 255.255.252.0
Default Gateway : 192.190.16.1

//====A7===//
FOOSHA Fa1/1
IP      : 192.190.0.9
Netmask : 255.255.255.252

GUANHAO Fa0/0
IP      : 192.190.0.10
Netmask : 255.255.255.252

//====A8===//
GUANHAO Fa1/0
IP      : 192.190.4.1
Netmask : 255.255.252.0

JABRA Fa0
IP      : 192.190.4.2
Netmask : 255.255.252.0
Default Gateway : 192.190.4.1

//====A9===//
GUANHAO Fa1/1
IP      : 192.190.2.1
Netmask : 255.255.254.0

MAINGATE Fa0
IP      : 192.190.2.2
Netmask : 255.255.254.0
Default Gateway : 192.190.2.1

ALABASTA Fa0/0
IP      : 192.190.2.3
Netmask : 255.255.254.0

//====A10===//
ALABASTA Fa0/1
IP      : 192.190.0.33
Netmask : 255.255.255.240

JORGE Fa0
IP      : 192.190.0.34
Netmask : 255.255.255.240
Default Gateway : 192.190.0.33

//====A11===//
GUANHAO Fa0/1
IP      : 192.190.0.13
Netmask : 255.255.255.252

OIMO Fa0/0
IP      : 192.190.0.14
Netmask : 255.255.255.252

//====A12===//
OIMO Fa0/1
IP      : 192.190.1.1
Netmask : 255.255.255.0

ENIESLOBBY Fa0
IP      : 192.190.1.2
Netmask : 255.255.255.0
Default Gateway : 192.190.1.1

SEASTONE Fa0/0
IP      : 192.190.1.3
Netmask : 255.255.255.0

//====A13===//
SEASTONE Fa0/1
IP      : 192.190.8.1
Netmask : 255.255.252.0

ELENA Fa0
IP      : 192.190.8.2
Netmask : 255.255.252.0
Default Gateway : 192.190.8.1

//====A14===//
OIMO Fa1/0
IP      : 192.190.0.17
Netmask : 255.255.255.252

FUKUROU Fa0
IP      : 192.190.0.18
Netmask : 255.255.255.252
Default Gateway : 192.190.0.17

//====A15===//
FOOSHA Eth0/3/0
IP      : 192.190.0.21
Netmask : 255.255.255.252

DORIKI Fa0
IP      : 192.190.0.22
Netmask : 255.255.255.252
Default Gateway : 192.190.0.21
```

#### Pengaturan Router

Jika sudah sekarang untuk mengatur jalur atau rute nya untuk dapat mengirimkan paket ke semua subnet dalam topologi. Perangkat yang diatur adalah Routernya. Metode routing yang dipakai adalah static routing.

Pengaturan routing ada pada menu `config->Routing->static`

Untuk router utama yaitu `Foosha` cara mengaturnya adalah dengan menambahkan routing untuk semua subnet selain yang berhubungan langsung dengan router tersebut. Maka akan menambahkan route untuk semua subnet kecuali untuk A5, A6, A7, dan A15.

Untuk router yang lain (di bawah router utama) hanya meneruskan sambungan agar mencapai router utama.

Berikut ringkasan untuk pengaturan routingnya

- **Foosha**
  ```
    192.190.12.0/22 via 192.190.0.6
    192.190.0.0/30 via 192.190.0.6
    192.190.24.0/21 via 192.190.0.6
    192.190.0.128/25 via 192.190.0.6
    192.190.4.0/22 via 192.190.0.10
    192.190.2.0/23 via 192.190.0.10
    192.190.0.12/30 via 192.190.0.10
    192.190.0.32/28 via 192.190.0.10
    192.190.0.16/30 via 192.190.0.10
    192.190.1.0/24 via 192.190.0.10
    192.190.8.0/22 via 192.190.0.10
  ```
- **Water 7**
  ```
    0.0.0.0/0 via 192.190.0.5
    192.190.0.128/25 via 192.190.0.2
    192.190.24.0/21 via 192.190.0.2
  ```
- **Pucci**
  ```
    0.0.0.0/0 via 192.190.0.1
  ```
- **Guanhao**
  ```
    0.0.0.0/0 via 192.190.0.9
    192.190.0.32/28 via 192.190.2.3
    192.190.0.16/30 via 192.190.0.14
    192.190.1.0/24 via 192.190.0.14
    192.190.8.0/22 via 192.190.0.14
  ```
- **Alabasta**
  ```
    0.0.0.0/0 via 192.190.2.1
  ```
- **Oimo**
  ```
    0.0.0.0/0 via 192.190.0.13
    192.190.8.0/22 via 192.190.1.3
  ```
- **Seastone**
  ```
    0.0.0.0/0 via 192.190.1.1
  ```

Jika sudah menambahkan pengaturan untuk setiap router, kita bisa mencoba untuk mengirim paket untuk mengetesnya. Untuk testing kita akan mencoba untuk mengirim paket dari `Client Chiper` ke `Client Courtyard`. Percobaanya dapat dilihat dibawah ini.

![img](./img/testing.gif)

## GNS3 - CIDR

### Penggabungan Subnet

Penggabungan subnet dilakukan dengan menggabungkan subnet yang letaknya paling jauh dari cloud terlebih dahulu seperti gambar dibawah ini:

![image](https://user-images.githubusercontent.com/73766214/143665836-c88e7bab-8652-4ac4-b887-40144f39bf3f.png)

![image](https://user-images.githubusercontent.com/73766214/143665852-2ae2bde7-4799-47b3-acc8-658bb1671e5d.png)

![image](https://user-images.githubusercontent.com/73766214/143665864-e326586e-07de-49d6-8802-5569ee63013b.png)

![image](https://user-images.githubusercontent.com/73766214/143665868-901de30c-001d-4cb2-a555-c02cf79bfff0.png)

![image](https://user-images.githubusercontent.com/73766214/143665876-79588c3c-b56b-4356-ad08-41c53a81f244.png)

Setelah itu membuat Tree CIDR yang dapat dilihat pada gambar dibawah atau di link berikut : https://gitmind.com/app/doc/2fc6169364

![CIDR Revisi](https://user-images.githubusercontent.com/73766214/143665952-99786186-1c02-4b1f-87d5-6733205af3fc.png)

Dilakukan perhitungan Network ID dan Broadcast Address, didapatkan :

![img](./img/NID-CIDR.png)
