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

#### Pembagian IP

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
