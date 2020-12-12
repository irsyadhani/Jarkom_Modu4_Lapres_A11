# Jarkom_Modul4_Lapres_A11
Kelompok A11:
* _Irsyadhani Dwi Shubhi (0511184000022)_
* _Anggun Wahyuni (05111840000154)_

----------------------------------------------------------------
## Soal
* [VLSM](#vlsm)
* [CIDR](#cidr)
----------------------------------------------------------------
# VLSM

## Tabel Subnetting
![alt text](/img/tabel.png)

## Cisco Packet Tracer dengan metode VLSM

### Perhitungan Subnet

#### 1. Menentukan jumlah subnet pada topologi
![alt text](/img/vlsm_1.png)

#### 2. Menentukan jumlah alamat IP yang dibutuhkan oleh tiap subnet dan lakukan labelling netmask berdasarkan jumlah IP yang dibutuhkan
![alt text](/img/vlsm_2.png)

#### 3. Menghitung pembagian IP berdasarkan NID dan netmask menggunakan pohon serta melakukan subnetting
![alt text](/img/vlsm_3.png)

#### 4. Dari pohon tersebut, subnet akan mendapat pembagian IP sebagai berikut
![alt text](/img/vlsm_4.png)

#### 5. Pembagian IP server menggunakan IP DMZ adalah sebagai berikut
![alt text](/img/vlsm_5.png)

### Praktik

#### 1. Membuat topologi pada CPT
![alt text](/img/vlsm_6.png)

#
#### 2. Subnetting
Mengatur IP untuk masing-masing interface yang ada di setiap device sesuai dengan pembagian subnet pada pohon VLSM dengan menu Config > Interface > "nama interface". Contoh untuk mengatur IP pada interface KEDIRI yang terhubung dengan subnet A2, A3 dan Server.

Pada subnet A2, ROUTER KEDIRI terhubung dengan ROUTER BLITAR dan CLIENT LUMAJANG.
Karena subnet A2 memiliki Network ID 192.168.1.0, atur IP pada interface KEDIRI yang mengarah ke subnet A2 dengan 192.168.1.1
![alt text](/img/vlsm_7.png)

Atur IP pada interface BLITAR yang mengarah ke subnet A2 dengan 192.168.1.2
![alt text](/img/vlsm_8.png)

Atur IP pada CLIENT LUMAJANG yang mengarah ke KEDIRI dengan 192.168.1.3. Pengaturan IP dapat dibuat dengan cara masuk ke client > pilih tab desktop > pilih IP Configuration
![alt text](/img/vlsm_9.png)

Kemudian, ROUTER KEDIRI terhubung dengan SERVER MALANG. Karena SERVER MALANG mempunyai Network ID 10.151.73.100, atur IP pada interface KEDIRI yang mengarah ke SERVER MALANG dengan 10.151.73.101
![alt text](/img/vlsm_10.PNG)

Atur IP pada SERVER MALANG yang mengarah ke KEDIRI dengan 10.151.73.102
![alt text](/img/vlsm_11.png)

Lakukan hal yang sama untuk mengatur alamat IP setiap interface pada device yang ada dalam topologi.

#
#### 3. Routing
Atur routing seperti tabel berikut

![alt text](/img/vlsm_12.png)

Routing dapat dilakukan pada menu Config > Routing > Static pada device Router dengan menambahkan NID (network), netmask (mask) dan gateway (next hop) lalu menekan tombol Add. Pada static routing juga dibutuhkan default routing agar router dapat mengirimkan paket sesuai tujuan. Default routing dibutuhkan untuk router yang berada di bawah router utama (SURABAYA). Sebagai contoh router KEDIRI hanya mengenal A2, A3 dan server MALANG sehingga harus dikenalkan dengan subnet A1 dan juga dilakukan default routing
![alt text](/img/vlsm_13.png)

#
#### 4. Testing
Hasil testing

![alt text](/img/vlsm_14.png)

###
# CIDR

## Topologi Subnet
![alt text](/img/A11_CIDR_fix.jpg)

* B1: Gabungan subnet A1 dan A2
* B2: Gabungan subnet A6 dan A5
* B3: Gabungan subnet A12 dan A13
* C1: Gabungan subnet B1 dan A3
* C2: Gabungan subnet B2 dan A4
* C3: Gabungan subnet B3 dan A11
* D1: Gabungan subnet C1 dan C2
* D2: Gabungan subnet C3 dan A10
* E1: Gabungan subnet D1 dan A7
* E2: Gabungan subnet D1 dan A9
* F1: Gabungan subnet E1 dan A8
* G1: Gabungan subnet F1 dan E2

#
## Tree Subnet
![alt text](/img/A11_Tree.jpg)

#
## Pembagian IP

### Tabel Pembagian IP
![alt text](/img/A11_Tabel_Pembagian_IP.jpg)

### Tree Pembagian IP
![alt text](/img/Pembagian_IP_CIDR.jpg)

#
## UML dengan metode CIDR
